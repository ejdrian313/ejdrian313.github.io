---
layout: post
title:  "Refactoring huge if-else in flutter widget."
date:   2020-09-20 11:35:49 +0200
---
### Backgrounds:
We got a widget it is actually a page called dashboard. We build this dashboard based of JSON data we got from web API. 
It starts normal with two types of specyfic section so I got easy to read if statement. Then daily we adding more and more section. App grows.
Some time later i got requriment to add new type of secion. So go to dashboard and saw this:

{% highlight dart %}
ListView.builder(
  shrinkWrap: true,
  itemCount: flow.additionalInfoJson.length,
  itemBuilder: (BuildContext ctxt, int index) {
    final item = flow.additionalInfoJson[index];
    if (item['sectionType'] == 'List') {
      return _buildList(item);
    } else if (item['sectionType'] == 'Grid') {
      return _buildGrid(item);
    } else if (item['sectionType'] == 'Scroll') {
      return _horizontalList(item);
    } else if (item['sectionType'] == 'Image') {
      return _image(item);
    } else if (item['sectionType'] == 'Text') {
      return _text(item);
    } else if (item['sectionType'] == 'List_extra') {
      return _listView(item);
    } else {
      return SizedBox.shrink();
    }
  },
);
{% endhighlight %}

I saw that each sectionType is an object. I realize that huge if else statetmant like this can be replaced with strategy pattern.
I dont start writing every if-else statement as a strategy becouse it will be a huge premature optimization. 
Now is the best time to do that. Refactoring area of interests when working about feature or bug.

So we start of creating Strategy context class: 

{% highlight dart %}
abstract class ISectionStrategy {
  bool shouldBuild(item);
  Widget buildSection(item);
}

class SectionStrategy {
  final List<ISectionStrategy> _strategies;

  SectionStrategy(this._strategies);

  Widget buildConcreteSection(tile) {
    final builder = _strategies.firstWhere(
      (s) => s.shouldBuild(tile),
      orElse: () => null,
    );
    if (builder == null) return SizedBox.shrink();
    return builder.buildSection(tile);
  }
}
{% endhighlight %}

concrete section of strategy looks like: 

{% highlight dart %}
class ButtonsSection extends ISectionStrategy {
  @override
  Widget buildSection(item) {
    return Column(
      children: <Widget>[
        new ListView.builder(
          physics: NeverScrollableScrollPhysics(),
          shrinkWrap: true,
          itemCount: list.length,
          itemBuilder: (BuildContext ctxt, int i) {
            var tile = list[i];
            return ButtonTile(
              tile: tile,
            );
          },
        ),
      ],
    );
  }

  @override
  bool shouldBuild(item) => item['sectionType'] == 'Buttons';
}
{% endhighlight %}

finally dashboard ListView.Builder look tiny and pretty:  
{% highlight dart %}
ListView.builder(
  shrinkWrap: true,
  itemCount: flow.additionalInfoJson.length,
  itemBuilder: (BuildContext ctxt, int index) {
    final item = flow.additionalInfoJson[index];
    return _sectionContext.buildConcreteSection(item);
  },
);
{% endhighlight %}