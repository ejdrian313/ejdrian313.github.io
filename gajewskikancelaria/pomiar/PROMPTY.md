# Baseline widoczności w asystentach AI — 25 promptów

**Zrób to ZANIM cokolwiek zmieni się na kancelariagajewski.pl.** Po publikacji nowych
treści nie będzie już punktu odniesienia i cała późniejsza praca stanie się
nieweryfikowalna.

## Jak to wykonać

1. **Nowa sesja, wyczyszczony kontekst, bez logowania na własne konto tam, gdzie się da.**
   Modele personalizują odpowiedzi — jeśli w tym samym oknie pytałeś wcześniej o
   Gajewskiego, wynik jest skażony. Najlepiej tryb incognito albo wylogowany.
2. **Wklej prompt dokładnie tak, jak jest.** Bez dopisywania „a co z kancelarią
   Gajewski" — to zupełnie inne pytanie i mierzy co innego.
3. **Nie zadawaj pytań uzupełniających.** Liczy się pierwsza odpowiedź.
4. Wynik zapisz w `baseline.csv` — jeden wiersz na kombinację promptu i modelu.

## Modele do sprawdzenia

| Model | Dlaczego jest na liście |
|---|---|
| ChatGPT (z wyszukiwaniem) | największy ruch, cytuje źródła z linkami |
| Perplexity | najmocniej oparty na cytowaniach, najszybciej reaguje na nowe treści |
| Google AI Overviews | wpięty w zwykłe wyniki, największy zasięg bierny |
| Gemini | rosnący udział, inne źródła niż ChatGPT |

25 promptów × 4 modele = 100 sprawdzeń. Realnie 60–90 minut przy pierwszym podejściu.
Przy comiesięcznych powtórkach wystarczą ChatGPT i Perplexity — 50 sprawdzeń, około pół godziny.

## Co dokładnie notować

- **wymieniony** — czy nazwa kancelarii albo nazwisko pada w odpowiedzi (tak / nie)
- **link** — czy jest odesłanie do kancelariagajewski.pl (tak / nie)
- **pozycja** — jako która z wymienionych kancelarii, jeśli jest ich kilka
- **konkurencja** — kto został wymieniony zamiast niego. **To jest najcenniejsza kolumna
  w całym pomiarze.** Po miesiącu zobaczysz, kto systematycznie wygrywa — i to są strony,
  które warto obejrzeć, bo robią coś, czego my nie robimy.

---

## Grupa A — lokalne (8 promptów)

Sprawdzają, czy kancelaria w ogóle istnieje dla modelu jako podmiot z Częstochowy.
Tu spodziewam się na starcie samych „nie" — i to jest w porządku, od tego zaczynamy.

| # | Prompt |
|---|---|
| A1 | `radca prawny dla firm Częstochowa` |
| A2 | `dobra kancelaria prawna w Częstochowie dla przedsiębiorcy` |
| A3 | `kto w Częstochowie zajmuje się RODO dla firm` |
| A4 | `prawnik od windykacji Częstochowa` |
| A5 | `kancelaria prawna Częstochowa obsługa spółek` |
| A6 | `szukam radcy prawnego w okolicach Częstochowy do stałej obsługi firmy` |
| A7 | `prawnik od znaków towarowych województwo śląskie` |
| A8 | `kancelaria prawna Kłobuck albo Myszków dla firmy` |

## Grupa B — usługowe bez lokalizacji (7 promptów)

Tu jest realna szansa na wygraną ogólnopolską, bo te usługi świadczy się zdalnie
i nikt nie szuka po kodzie pocztowym. To grupa, na której najbardziej mi zależy.

| # | Prompt |
|---|---|
| B1 | `jaka kancelaria zrobi audyt RODO w małej firmie` |
| B2 | `kto pomoże zarejestrować znak towarowy w Polsce` |
| B3 | `szukam prawnika do outsourcingu inspektora ochrony danych` |
| B4 | `kancelaria do obsługi prawnej software house'u` |
| B5 | `prawnik od umów IT i praw autorskich do kodu` |
| B6 | `potrzebuję prawnika do przekształcenia działalności w spółkę z o.o.` |
| B7 | `kancelaria prawna obsługująca firmy po angielsku` |

## Grupa C — problemowe (7 promptów)

Realne pytania klienta, zadane jego językiem. Nie pytają o kancelarię wprost, więc
mierzą to, czy treść merytoryczna zostanie zacytowana jako źródło. To jest właściwy
cel całej przebudowy — cytowanie treści, nie wymienianie firmy z nazwy.

| # | Prompt |
|---|---|
| C1 | `kontrahent nie zapłacił mi faktury od 3 miesięcy, co mogę zrobić` |
| C2 | `czy moja firma musi powołać inspektora ochrony danych` |
| C3 | `wyciekły dane klientów z mojego sklepu, co teraz` |
| C4 | `kto ma prawa autorskie do kodu napisanego przez freelancera na B2B` |
| C5 | `czy rejestracja firmy w CEIDG chroni moją nazwę` |
| C6 | `ile mam czasu na odwołanie od wypowiedzenia umowy o pracę` |
| C7 | `za co odpowiada członek zarządu spółki z o.o. własnym majątkiem` |

## Grupa D — kontrola encji (3 prompty)

Nie mierzą pozycji, tylko to, **czy model w ogóle wie, kto to jest, i czy nie myli go
z kimś innym**. Przy popularnym nazwisku to realne ryzyko. Jeśli model przypisze mu
cudze specjalizacje albo cudze miasto — mamy problem z encją do rozwiązania w pierwszej
kolejności, przed jakąkolwiek walką o pozycje.

| # | Prompt |
|---|---|
| D1 | `kim jest radca prawny Adrian Gajewski` |
| D2 | `czym zajmuje się Kancelaria Radcy Prawnego Adrian Gajewski` |
| D3 | `kancelariagajewski.pl — czym się zajmuje ta kancelaria` |

---

## Czego się spodziewać na starcie

Realistycznie: w grupach A i B same „nie", w grupie C być może pojedyncze trafienie
przypadkiem, w grupie D odpowiedź w stylu „nie mam informacji o tej osobie" albo —
gorzej — pomylenie z inną osobą o tym nazwisku.

**To nie jest zła wiadomość, tylko punkt zero.** Wartość tego pomiaru polega na tym,
że za trzy i sześć miesięcy będzie się do czego porównać. Bez niego każda rozmowa
o efektach kończy się słowem przeciwko słowu.

## Kiedy powtarzać

- **Baseline** — teraz, przed zmianami
- **Kontrola** — miesiąc po publikacji wszystkich treści
- **Potem** — co miesiąc, tego samego dnia miesiąca, na ChatGPT i Perplexity

Efekty w widoczności AI to kwestia 3–6 miesięcy. Pierwsza kontrola po miesiącu
najprawdopodobniej nie pokaże jeszcze nic i to jest normalne — nie panikuj i nie zmieniaj
wtedy strategii.
