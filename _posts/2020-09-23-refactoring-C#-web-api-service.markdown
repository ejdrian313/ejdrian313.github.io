---
layout: post
title:  "Refactoring C# web API service method"
date:   2020-09-23 11:35:49 +0200
---

Last day when I got new requirements on backend api. So I try to refactor this peace of code to more readable. Start with this ugly code:  

{% highlight csharp %}
public async Task<GlobalServiceModel<dynamic>> GetFlowById(string id, User user)
        {
            try
            {
                //get clicked id of item
                MatchCollection match = Regex.Matches(id);
                string itemId = null;
                for (int k = 0; k < match.Count; k++)
                {
                    var toReplace = match.ElementAt(k).Value;
                    id = id.Replace(toReplace, "");
                    itemId = JumpOutFromDoubleBracets(toReplace);
                }

                _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} GetFlowById user: {user?.Id} flowId: {id}");
                var flow = await _context.Flows.Find(f => f.FlowId.Equals(id)).FirstOrDefaultAsync();

                _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} GetFlowById : {flow?.ToString()} flowId: {id}");

                if (flow == null)
                    return new GlobalServiceModel<dynamic>(StatusCodes.Status404NotFound, "Nie znaleziono");

                if (flow.WidgetName == "dashboard")
                {
                    _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} GetNeastedCollections : {flow.FlowId}");
                    GetNeastedCollections(flow, user);
                    _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} Collection : {flow.FlowId}");
                }

                if (flow.AdditionalInfo != null)
                {
                    _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} AdditionalInfoToJson : {flow.FlowId}");
                    flow.AdditionalInfoToJson();
                    _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} AdditionalInfoToJson : {flow.FlowId}");
                }

                if (flow.WidgetName == "groupchat" || flow.WidgetName == "groupchat_dynamic")
                {
                    var liveFlowVm = _mapper.Map<LiveFlow, LiveFlowVm>(flow.Live);
                    if (liveFlowVm.StreamChannel == "{{random}}")
                    {
                        flow.Live.StreamChannel = _liveService.GetRoomName(user.Id, flow.Live.RoomSize).Message;
                    }
                }

                if (user != null)
                    DecoreTexts(flow, user);

                if (flow.WidgetName == "restrequest")
                {
                    var result = await GetResponseFromRestRequestFlow(flow, user, itemId);
                    return new GlobalServiceModel<dynamic>(StatusCodes.Status200OK, result);
                }

                var mapped = _mapper.Map<FlowCast>(flow);

                if (flow.WidgetName == "live" || flow.WidgetName == "groupchat" || flow.WidgetName == "groupchat_dynamic")
                {
                    var flowVm = _mapper.Map<LiveFlow, LiveFlowVm>(flow.Live);
                    var bsonResult = GetFieldFromUserCustomFields(user, "first_name_custom");
                    if (bsonResult.Value != null)
                        flowVm.UserName = bsonResult.Value.ToString();
                    mapped.Live = flowVm;
                }

                if (flow.Interaction != null)
                {
                    flow.Interaction.FlowId = flow.FlowId; //saveDiary fix
                }

                if (flow.IsAuthorized != null && flow.IsAuthorized.Contains("true") == false)
                {
                    var flowRedirect = new FlowCast
                    {
                        FlowId = "redirectFlow",
                        WidgetName = "interaction",
                        Interaction = new Interaction
                        {
                            FlowId = "redirectFlow",
                            Questions = new List<Question>() {
                                new Question {
                                    Answers = new List<Answer>() {
                                        new Answer {
                                            FlowId = flow.IsAuthorizedFallback
                                        }
                                    }
                                }
                            }
                        }
                    };
                    return new GlobalServiceModel<dynamic>(StatusCodes.Status200OK, flowRedirect);
                }

                _logger.Info($"END Time: {DateTime.Now:hh.mm.ss.ffffff}  FLow: {mapped?.FlowId} UserId: {user?.Id}");
                return new GlobalServiceModel<dynamic>(StatusCodes.Status200OK, mapped);
            }
            catch (Exception exception)
            {
                _logger.Error(exception);
                return new GlobalServiceModel<dynamic>(StatusCodes.Status500InternalServerError);
            }
        }
{% endhighlight %}

Then after refactoring got this:

{% highlight csharp %}
public async Task<GlobalServiceModel<dynamic>> GetFlowById(string id, User user)
        {
            try
            {
                var itemClicked = new ItemClickedIds(id);
                id = itemClicked.FlowId;

                var flow = await _context.Flows.Find(f => f.FlowId.Equals(id)).FirstOrDefaultAsync();

                _logger.Info($"Time: {DateTime.Now:hh.mm.ss.ffffff} GetFlowById : {flow?.ToString()} flowId: {id}");

                if (flow == null)
                    return new GlobalServiceModel<dynamic>(StatusCodes.Status404NotFound, "Nie znaleziono");

                flow.Update(user, _roomService, _mapper);

                if (flow.IsRestReqest())
                    return await _client.Response(flow, user, itemClicked.ItemId);

                if (flow.IsUnauthorized())
                    return FlowRedirectUnauthorized.Generate(flow.IsAuthorizedFallback);

                var mapped = _mapper.Map<FlowCastVm>(flow);

                mapped.Update(user, flow, _mapper);
              
                _logger.Info($"END Time: {DateTime.Now:hh.mm.ss.ffffff}  FLow: {mapped?.FlowId} UserId: {user?.Id}");
                return new GlobalServiceModel<dynamic>(StatusCodes.Status200OK, mapped);
            }
            catch (Exception exception)
            {
                _logger.Error(exception);
                return new GlobalServiceModel<dynamic>(StatusCodes.Status500InternalServerError, "Wystąpił błąd");
            }
{% endhighlight %}
