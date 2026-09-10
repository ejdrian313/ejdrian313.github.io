# Kancelaria Radcy Prawnego Adrian Gajewski — plan treści pod GEO/SEO

Status: **DO ZATWIERDZENIA**. Po akceptacji powstają teksty w `gajewskikancelaria/specjalizacje/`.
Zakres: 9 specjalizacji obecnych na stronie + FAQ globalne + strona "O mnie" + rozpiska schema.
Poza zakresem: prawo rodzinne (rozwody, alimenty, podział majątku) — kancelaria tego nie prowadzi, nie pojawia się nigdzie.

---

## 0. Założenia i rzeczy do uzupełnienia przez klienta

Zanim cokolwiek pójdzie na produkcję, potrzebne od Adriana:

| # | Dana | Po co | Blokuje |
|---|------|-------|---------|
| 1 | **Miasto i adres biura** + kod pocztowy | cała warstwa lokalna, GBP, schema `address` | wszystko |
| 2 | NIP / REGON | schema `taxID`, wiarygodność encji | schema |
| 3 | **Numer wpisu na listę radców prawnych** + rok wpisu | E-E-A-T, `Person` schema, weryfikowalność | O mnie |
| 4 | Profil LinkedIn (URL) | `sameAs`, sygnał encji | schema |
| 5 | Lata doświadczenia liczbowo (od którego roku praktykuje) | konkret zamiast "przez lata" | O mnie |
| 6 | Branże klientów in-house (bez nazw, np. "energetyka, produkcja") | dowód specjalizacji | O mnie |
| 7 | Decyzja: wpuszczamy boty AI (GPTBot, PerplexityBot, ClaudeBot, Google-Extended)? | bez tego GEO nie ma sensu | robots.txt |
| 8 | Decyzja: **"ja" czy "my"** w całej komunikacji | spójność encji | wszystkie teksty |
| 9 | Czy podajemy widełki cenowe gdziekolwiek | struktura sekcji "Koszty" | wszystkie teksty |

W tekstach poniżej miasto oznaczam jako `[MIASTO]` — do podmiany globalnej.

**Rekomendacja do pkt 8: "ja".** Kancelaria jednoosobowa. Osobista encja (imię + nazwisko + izba + nr wpisu) jest w modelach mocniejsza niż anonimowe "Zapewniamy", a "my" przy jednym radcy wprowadza w błąd co do wielkości zespołu. Wyjątek: tam gdzie realnie działa sieć współpracowników (adwokaci z innych regionów, notariusze, doradcy podatkowi) — wtedy "współpracuję z".

**Weryfikacja merytoryczna.** Każda liczba, termin, opłata i podstawa prawna w tekstach idzie do akceptacji Adriana przed publikacją. Ja piszę szkielet i research, on potwierdza stan prawny na dzień publikacji. W każdym tekście stopka: "Stan prawny na dzień: RRRR-MM-DD".

---

## 1. Architektura informacji

Dziś: jedna strona, 9 akapitów po 2–3 zdania. Zero do zacytowania przez model.

Docelowo:

```
/                                  strona główna (przebudowa sekcji, bez zmiany layoutu)
/o-mnie/                           profil encji — najważniejsza strona pod GEO
/specjalizacje/                    hub, krótkie zajawki + linki do 9 podstron
  /obsluga-prawna-firm/
  /prawo-spolek/
  /ochrona-danych-osobowych/
  /prawo-wlasnosci-intelektualnej/
  /windykacja-naleznosci/
  /prawo-pracy/
  /podatki/
  /spory-sadowe/
  /odszkodowania/
/faq/                              FAQ globalne — o współpracy, nie o prawie
/kontakt/                          pełny NAP
/blog/                             faza 2, po podstronach
```

Linkowanie wewnętrzne — sztywne reguły:
- każda podstrona linkuje do 2–3 pokrewnych (mapa w sekcji 3),
- każda linkuje do `/o-mnie/` frazą "radca prawny Adrian Gajewski",
- hub `/specjalizacje/` linkuje do wszystkich 9, każda z 9 wraca do huba przez breadcrumb,
- `/faq/` linkuje do wszystkich 9.

---

## 2. Kolejność wdrożenia

**Fala 1 — 4 podstrony (to jest zakres barteru).** Wybrane wg: wysoka marża × niska konkurencja treściowa × realne pytania zadawane AI.

1. Ochrona danych osobowych (RODO)
2. Prawo własności intelektualnej
3. Windykacja należności
4. Prawo spółek

**Fala 2 — pozostałe 5.** Obsługa prawna firm, prawo pracy, podatki, spory sądowe, odszkodowania.

**Fala 0 — równolegle, bo tanie i krytyczne.** `/o-mnie/`, `/kontakt/` z NAP, `/faq/`, schema, robots.txt, GBP.

---

## 3. Szablon każdej podstrony specjalizacji

Ta sama struktura wszędzie — modele lubią przewidywalność, a użytkownik po drugiej stronie od razu wie, gdzie szukać.

```
H1: {Usługa} — {miasto/region}
  Lead (2–3 zdania): dla kogo, co realnie dostajesz. Bez "profesjonalnie i rzetelnie".
  [Box: kluczowe fakty — 4–5 punktów, wyciągalne przez model jako całość]

H2: Dla kogo jest ta usługa
  Lista typów klienta (spółka z o.o., JDG, fundacja...), po jednym zdaniu.

H2: Typowe sytuacje, w których pomagam
  5–8 scenariuszy pisanych językiem klienta, nie ustawy.
  ("kontrahent nie zapłacił faktury od 90 dni", a nie "dochodzenie roszczeń pieniężnych")

H2: Jak wygląda współpraca — krok po kroku
  Numerowane 4–6 kroków, przy każdym orientacyjny czas.
  To jest sekcja, którą modele cytują najczęściej. Musi być samodzielna.

H2: Terminy i koszty urzędowe
  Konkretne liczby: opłaty sądowe/skarbowe, terminy ustawowe, czasy trwania.
  NIE cennik kancelarii. Tabelka.

H2: Najczęstsze pytania
  5–7 pytań. Każda odpowiedź: pierwsze zdanie = pełna odpowiedź, potem rozwinięcie.

H2: Powiązane specjalizacje
  2–3 linki wewnętrzne.

[Blok autora: zdjęcie, imię i nazwisko, tytuł, nr wpisu, link do /o-mnie/]
[Stan prawny na dzień: RRRR-MM-DD]
[CTA: kontakt]
```

Objętość: **1200–1600 słów**. Poniżej 900 nie ma czego cytować, powyżej 2000 przy usłudze rozmywa się intencja.

Zasada nadrzędna dla GEO: **pierwsze 1–2 zdania pod każdym H2 muszą się bronić wyrwane z kontekstu.** Model wycina dokładnie taki fragment. Żadnych "Jak wspomniano wyżej".

---

## 4. Rozpiska 9 podstron

Dla każdej: URL, title, meta description, H2-ki, frazy, prompty AI, FAQ, linki.
"Prompty AI" = realne pytania, które ktoś wpisuje do ChatGPT/Perplexity. To one są celem, nie same frazy z Google.

---

### 4.1 Ochrona danych osobowych (RODO) — **PRIORYTET 1**

- **URL:** `/specjalizacje/ochrona-danych-osobowych/`
- **Title:** `Ochrona danych osobowych i RODO dla firm — [MIASTO] | radca prawny Adrian Gajewski` (58 zn.)
- **Meta:** `Audyty RODO, dokumentacja, wdrożenia i outsourcing IOD dla firm ze Śląska. Wsparcie przy kontroli UODO i naruszeniach ochrony danych.`
- **H1:** `Ochrona danych osobowych (RODO) dla firm — [MIASTO] i Śląsk`

**Dlaczego priorytet:** wysoka marża, powtarzalna usługa abonamentowa (IOD), klienci B2B szukają aktywnie, a konkurencja na Śląsku pisze wyłącznie ogólniki. Do tego Adrian ma to w swoich specjalizacjach z "O mnie" — jest pokrycie kompetencyjne.

**H2:**
1. Dla kogo — kto realnie musi wdrożyć RODO (każdy administrator, ale różna skala)
2. Zakres usług: audyt / dokumentacja / wdrożenie / outsourcing IOD / szkolenia / wsparcie przy naruszeniu
3. Audyt RODO krok po kroku (inwentaryzacja procesów → rejestr czynności → analiza ryzyka → raport z rekomendacjami → wdrożenie)
4. Kiedy trzeba powołać Inspektora Ochrony Danych
5. Naruszenie ochrony danych — 72 godziny i co dalej
6. Kontrola UODO — jak się przygotować, jak przebiega
7. Terminy i sankcje (tabela)
8. FAQ
9. Powiązane

**Frazy:** ochrona danych osobowych [MIASTO], audyt RODO firma, wdrożenie RODO, outsourcing IOD, inspektor ochrony danych dla firmy, dokumentacja RODO, kontrola UODO pomoc prawna, naruszenie ochrony danych zgłoszenie

**Prompty AI:**
- „czy moja firma musi powołać inspektora ochrony danych"
- „ile kosztuje audyt RODO w małej firmie"
- „co zrobić po wycieku danych w firmie"
- „jak przygotować się do kontroli UODO"
- „kancelaria od RODO na Śląsku"
- „jakie dokumenty RODO musi mieć firma zatrudniająca pracowników"

**FAQ (7):**
1. Czy każda firma musi mieć Inspektora Ochrony Danych?
2. Jakie dokumenty RODO musi posiadać firma?
3. Ile trwa audyt RODO?
4. Co zrobić w ciągu 72 godzin od naruszenia ochrony danych?
5. Czy jednoosobowa działalność też podlega RODO?
6. Jakie kary grożą za naruszenie RODO w Polsce?
7. Czy można powierzyć funkcję IOD kancelarii zewnętrznej?

**Linki wewnętrzne:** → obsługa prawna firm, prawo pracy (dane pracowników), prawo własności intelektualnej (umowy IT)

---

### 4.2 Prawo własności intelektualnej — **PRIORYTET 2**

- **URL:** `/specjalizacje/prawo-wlasnosci-intelektualnej/`
- **Title:** `Prawo własności intelektualnej — znaki towarowe, prawa autorskie | [MIASTO]`
- **Meta:** `Rejestracja znaków towarowych, umowy przenoszące prawa autorskie, ochrona marki i dochodzenie roszczeń przy naruszeniach IP.`
- **H1:** `Prawo własności intelektualnej — ochrona marki i praw autorskich`

**Dlaczego:** bardzo wąska nisza, mało kto w regionie ma porządną treść, a pytania są konkretne i dobrze się na nie odpowiada liczbami (opłaty UPRP/EUIPO, terminy).

**H2:**
1. Dla kogo — firmy budujące markę, software house'y, agencje, twórcy, e-commerce
2. Znak towarowy: badanie zdolności rejestrowej → zgłoszenie → sprzeciwy → rejestracja
3. Gdzie rejestrować: UPRP (Polska) vs EUIPO (UE) vs WIPO (międzynarodowo) — tabela porównawcza
4. Prawa autorskie w umowach — przeniesienie vs licencja, pola eksploatacji, prawa zależne
5. Umowy IT i przekazanie kodu — najczęstsze błędy
6. Naruszenie praw — od wezwania do pozwu
7. Opłaty i terminy (tabela: UPRP, EUIPO, czas trwania procedury)
8. FAQ
9. Powiązane

**Frazy:** rejestracja znaku towarowego [MIASTO], prawnik znaki towarowe, ochrona nazwy firmy, umowa przeniesienia praw autorskich, prawa autorskie do kodu, naruszenie znaku towarowego, kancelaria IP Śląsk

**Prompty AI:**
- „jak zastrzec nazwę firmy jako znak towarowy"
- „ile kosztuje rejestracja znaku towarowego w Polsce"
- „czy muszę rejestrować znak w EUIPO czy w UPRP"
- „kto ma prawa autorskie do kodu napisanego przez freelancera"
- „co zrobić gdy ktoś używa mojej nazwy firmy"
- „czym różni się licencja od przeniesienia praw autorskich"

**FAQ (7):**
1. Ile kosztuje rejestracja znaku towarowego?
2. Jak długo trwa rejestracja znaku towarowego?
3. Czy nazwa w KRS/CEIDG chroni moją markę?
4. Czym różni się przeniesienie praw autorskich od licencji?
5. Kto ma prawa do kodu stworzonego przez zleceniobiorcę?
6. Czy da się zastrzec logo i nazwę jednym zgłoszeniem?
7. Co zrobić, gdy konkurencja używa podobnego znaku?

**Linki:** → obsługa prawna firm, spory sądowe, ochrona danych osobowych

---

### 4.3 Windykacja należności — **PRIORYTET 3**

- **URL:** `/specjalizacje/windykacja-naleznosci/`
- **Title:** `Windykacja należności dla firm — [MIASTO] | radca prawny`
- **Meta:** `Windykacja przedsądowa, pozew w EPU, postępowanie egzekucyjne. Odzyskiwanie należności B2B na Śląsku i w całej Polsce.`
- **H1:** `Windykacja należności — od wezwania do egzekucji komorniczej`

**Dlaczego:** największy wolumen zapytań z całej dziewiątki, prosty i zrozumiały problem, świetnie się opisuje krokami i liczbami.

**H2:**
1. Dla kogo — firmy z niezapłaconymi fakturami B2B
2. Etap przedsądowy: wezwanie do zapłaty, negocjacje, ugoda, uznanie długu
3. Etap sądowy: nakaz zapłaty, EPU, postępowanie upominawcze i nakazowe
4. Egzekucja komornicza — wniosek, zajęcia, koszty
5. Rekompensata 40/70/100 EUR i odsetki za opóźnienie w transakcjach handlowych
6. Kiedy windykacja się nie opłaca — uczciwa sekcja o przedawnieniu i niewypłacalności dłużnika
7. Terminy i koszty (tabela: opłata od pozwu, EPU, koszty komornicze, terminy przedawnienia)
8. FAQ
9. Powiązane

**Frazy:** windykacja należności [MIASTO], odzyskiwanie długów firma, wezwanie do zapłaty wzór prawnik, nakaz zapłaty EPU, kancelaria windykacyjna Śląsk, niezapłacona faktura co zrobić

**Prompty AI:**
- „co zrobić gdy kontrahent nie płaci faktury"
- „ile kosztuje pozew o zapłatę"
- „jak długo trwa uzyskanie nakazu zapłaty"
- „kiedy przedawnia się faktura między firmami"
- „czy warto iść do sądu o 10 tys. zł"
- „rekompensata 40 euro za opóźnienie w płatności"

**FAQ (7):**
1. Po jakim czasie faktura się przedawnia?
2. Ile kosztuje złożenie pozwu o zapłatę?
3. Czy mogę doliczyć odsetki i rekompensatę 40 euro?
4. Ile trwa uzyskanie nakazu zapłaty?
5. Co jeśli dłużnik nie ma majątku?
6. Czy wezwanie do zapłaty jest obowiązkowe przed pozwem?
7. Kto ponosi koszty postępowania?

**Linki:** → spory sądowe, obsługa prawna firm, prawo spółek

---

### 4.4 Prawo spółek — **PRIORYTET 4**

- **URL:** `/specjalizacje/prawo-spolek/`
- **Title:** `Prawo spółek — zakładanie i obsługa spółek | [MIASTO]`
- **Meta:** `Zakładanie spółek, wybór formy prawnej, umowy wspólników, przekształcenia i zmiany w KRS. Doradztwo dla przedsiębiorców.`
- **H1:** `Prawo spółek — zakładanie, przekształcanie i obsługa korporacyjna`

**H2:**
1. Dla kogo — zakładający, wspólnicy, zarządy
2. Wybór formy prawnej — tabela porównawcza (JDG / sp. z o.o. / sp. k. / P.S.A. / S.A.): odpowiedzialność, opodatkowanie, koszt startu, ZUS
3. Zakładanie spółki: S24 vs notariusz — co wybrać i kiedy
4. Umowa spółki i umowa wspólników — co musi się w nich znaleźć
5. Zmiany w KRS, podwyższenie kapitału, zbycie udziałów
6. Przekształcenia (JDG → sp. z o.o.) i likwidacja
7. Odpowiedzialność członków zarządu (art. 299 KSH) — sekcja, która sprzedaje
8. Terminy i koszty (tabela: opłaty S24/notarialne/KRS, czas rejestracji)
9. FAQ
10. Powiązane

**Frazy:** zakładanie spółki [MIASTO], przekształcenie JDG w spółkę z o.o., umowa wspólników, zmiana w KRS prawnik, odpowiedzialność zarządu sp. z o.o., prawnik prawo spółek Śląsk

**Prompty AI:**
- „jaka forma prawnej działalności jest najlepsza dla mojej firmy"
- „ile kosztuje założenie spółki z o.o."
- „czy przekształcić działalność w spółkę z o.o."
- „za co odpowiada członek zarządu spółki z o.o."
- „S24 czy u notariusza — jak założyć spółkę"
- „co powinna zawierać umowa wspólników"

**FAQ (7):**
1. Ile kosztuje założenie spółki z o.o.?
2. Ile trwa rejestracja spółki w KRS?
3. Czy warto przekształcić JDG w spółkę z o.o.?
4. Za co odpowiada zarząd spółki z o.o.?
5. Czym różni się umowa spółki od umowy wspólników?
6. Czy mogę założyć spółkę bez notariusza?
7. Jak zbyć udziały w spółce z o.o.?

**Linki:** → obsługa prawna firm, podatki, windykacja

---

### 4.5 Obsługa prawna przedsiębiorców — *fala 2*

- **URL:** `/specjalizacje/obsluga-prawna-firm/`
- **Title:** `Stała obsługa prawna firm — [MIASTO] | radca prawny Adrian Gajewski`
- **H1:** `Stała obsługa prawna przedsiębiorców — [MIASTO] i Śląsk`
- Rola: strona-parasol, główny magnes na abonament. Linkuje do wszystkich pozostałych.

**H2:** Dla kogo / Co obejmuje stała obsługa / Modele współpracy (abonament godzinowy, ryczałt, ad hoc) / Jak zaczynamy — pierwsze 30 dni / Obsługa w języku angielskim / Współpraca z notariuszami, doradcami podatkowymi, komornikami / FAQ / Powiązane (linki do 8 pozostałych)

**Prompty AI:** „ile kosztuje stała obsługa prawna firmy", „czy mała firma potrzebuje prawnika na stałe", „radca prawny dla firmy [MIASTO]", „obsługa prawna spółki w języku angielskim"

---

### 4.6 Prawo pracy — *fala 2*

- **URL:** `/specjalizacje/prawo-pracy/`
- **Title:** `Prawo pracy dla firm i pracowników — [MIASTO]`
- **H2:** Dla kogo (dwie ścieżki: pracodawca / pracownik) / Dokumentacja pracownicza i regulaminy / Rozwiązanie umowy — tryby i terminy odwołania / Spory przed sądem pracy / Restrukturyzacja zatrudnienia i zwolnienia grupowe / B2B vs umowa o pracę — ryzyko przekwalifikowania / Mobbing i dyskryminacja / Terminy (tabela: 21 dni na odwołanie itd.) / FAQ / Powiązane
- **Prompty AI:** „ile mam czasu na odwołanie od wypowiedzenia", „czy umowa B2B może zostać uznana za umowę o pracę", „jak przeprowadzić zwolnienia grupowe", „jakie dokumenty pracownicze musi mieć pracodawca"
- **Uwaga:** dwie grupy docelowe na jednej stronie to kompromis. Jeśli w fali 3 będzie ruch — rozbić na `/prawo-pracy-dla-pracodawcow/` i `/prawo-pracy-dla-pracownikow/`.

---

### 4.7 Podatki — *fala 2*

- **URL:** `/specjalizacje/podatki/`
- **Title:** `Doradztwo prawno-podatkowe dla firm — [MIASTO]`
- **H2:** Dla kogo / Zakres (opinie, struktura transakcji, spory) / Kontrola i postępowanie podatkowe — jak przebiega / Odwołanie i skarga do WSA / Interpretacja indywidualna — kiedy się opłaca / Terminy (tabela) / FAQ / Powiązane
- **Prompty AI:** „co zrobić gdy urząd skarbowy wszczyna kontrolę", „jak uzyskać interpretację indywidualną", „ile mam czasu na odwołanie od decyzji podatkowej", „skarga do WSA na decyzję podatkową"
- **Uwaga do klienta:** radca prawny może reprezentować przed organami i sądami administracyjnymi; opisujemy zakres ostrożnie, bez wchodzenia w to, co zastrzeżone dla doradców podatkowych. Sekcja o współpracy z doradcą podatkowym — do potwierdzenia przez Adriana.

---

### 4.8 Spory sądowe — *fala 2*

- **URL:** `/specjalizacje/spory-sadowe/`
- **Title:** `Spory sądowe — reprezentacja w procesach cywilnych i gospodarczych | [MIASTO]`
- **H2:** Dla kogo / Rodzaje spraw (cywilne, gospodarcze, umowne, o zapłatę) / Przebieg procesu krok po kroku z czasami / Zabezpieczenie roszczenia / Mediacja i ugoda — kiedy się opłaca bardziej niż wyrok / Ile trwa i ile kosztuje proces (tabela opłat) / Reprezentacja w całej Polsce dzięki sieci współpracowników / FAQ / Powiązane
- **Prompty AI:** „ile trwa sprawa cywilna w sądzie", „ile kosztuje pozew", „kto płaci koszty przegranej sprawy", „czy warto iść na mediację zamiast do sądu"

---

### 4.9 Odszkodowania — *fala 2*

- **URL:** `/specjalizacje/odszkodowania/`
- **Title:** `Odszkodowania i zadośćuczynienie — pomoc prawna | [MIASTO]`
- **H2:** Dla kogo / Rodzaje spraw (komunikacyjne, z ubezpieczeń majątkowych, z tytułu niewykonania umowy) / Zaniżone odszkodowanie z OC — co zrobić / Odwołanie od decyzji ubezpieczyciela / Droga sądowa / Terminy przedawnienia (tabela) / FAQ / Powiązane
- **Prompty AI:** „ubezpieczyciel zaniżył odszkodowanie co zrobić", „ile mam czasu na odwołanie od decyzji ubezpieczyciela", „jak odwołać się od decyzji o odszkodowaniu", „kiedy przedawnia się roszczenie o odszkodowanie"
- **Uwaga:** jedyna wyraźnie B2C pozycja w portfolio. Zostaje, bo jest na stronie, ale nie ciągniemy jej w fazie 1 — profil kancelarii to B2B i tam jest przewaga.

---

## 5. FAQ globalne — `/faq/`

To **nie jest** FAQ prawne (te siedzą w podstronach). To FAQ o współpracy — sekcja, którą modele cytują przy pytaniach typu "jak wygląda praca z kancelarią". Wzorowane na tym, co robią dobrze duże kancelarie: konkret, brak marketingu, odpowiedź w pierwszym zdaniu.

1. Jak rozpocząć współpracę z kancelarią?
2. Czy pierwsza konsultacja jest płatna?
3. W jaki sposób rozliczana jest praca kancelarii? (godzinowo / ryczałt / abonament / success fee tam, gdzie dopuszczalne)
4. Czy kancelaria działa tylko na Śląsku?
5. Czy możliwa jest współpraca zdalna? (wideokonferencja, podpis elektroniczny, wymiana dokumentów)
6. Czy kancelaria obsługuje klientów w języku angielskim?
7. Czym różni się radca prawny od adwokata?
8. Czy radca prawny może reprezentować mnie w sądzie?
9. Jak długo trwa odpowiedź na zapytanie?
10. Czy informacje przekazane kancelarii są objęte tajemnicą?
11. Czy kancelaria prowadzi sprawy rodzinne, spadkowe lub karne? — **odpowiedź: nie**, i tu kierujemy do tego, co robimy. Ta pozycja świadomie odcina złe leady i uczy modele, czym kancelaria NIE jest. To jest dokładnie tak samo ważne jak to, czym jest.
12. Czy mogę zlecić jednorazową sprawę bez stałej umowy?

Każda odpowiedź: 40–90 słów. Schema `FAQPage` na tej stronie.

---

## 6. `/o-mnie/` — najważniejsza strona pod GEO

Obecny tekst jest dobry, ale to akapit. Ma być stroną z sekcjami:

- **H1:** Adrian Gajewski — radca prawny
- Zdjęcie z sensownym `alt`
- Blok faktów (wyciągany przez modele w całości): tytuł zawodowy, izba (OIRP Opole), **numer wpisu**, rok wpisu, wykształcenie (WPiA UŁ), języki (PL/EN), obszar działania
- **Specjalizacje** — 5 głównych z linkami do podstron
- **Doświadczenie** — chronologicznie: kancelarie (typ, nie nazwy jeśli NDA), in-house (branże), własna praktyka od roku X
- **Podejście do pracy** — 3 akapity, konkretnie: co znaczy "praktyczne rozwiązania" na przykładach
- **Sieć współpracowników** — adwokaci w innych regionach, notariusze, komornicy, doradcy podatkowi, rzeczoznawcy, tłumacze przysięgli
- `sameAs`: LinkedIn, GBP, wyszukiwarka radców KIRP
- Schema `Person` + `Attorney`, `worksFor` → `LegalService`

---

## 7. Warstwa techniczna (poza tekstami)

### 7.1 Schema — plan
| Strona | Typy |
|---|---|
| Główna | `LegalService` + `Organization`, `areaServed`, `address`, `telephone`, `email`, `founder` → Person |
| `/o-mnie/` | `Person` / `Attorney`, `sameAs`, `alumniOf`, `memberOf` (OIRP), `knowsLanguage` |
| Każda specjalizacja | `Service` (`serviceType`, `provider`, `areaServed`) + `FAQPage` + `BreadcrumbList` |
| `/faq/` | `FAQPage` |
| `/kontakt/` | `LocalBusiness` z pełnym NAP + `openingHours` |

### 7.2 Pozostałe
- `robots.txt`: `GPTBot`, `OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`, `Google-Extended`, `CCBot` — allow (po decyzji klienta)
- Sitemap XML z nowymi URL-ami, zgłoszenie w GSC
- Ujednolicenie "ja/my" na całej stronie
- Pełny NAP w stopce na każdej podstronie
- Google Business Profile: kategoria "Radca prawny", obszar działania, godziny, opis, zdjęcia
- Core Web Vitals — sprawdzić po wdrożeniu, WordPress + page builder potrafi zabić LCP

### 7.3 Pomiar — **baseline PRZED zmianami**
- GA4: segmenty ruchu z `chatgpt.com`, `perplexity.ai`, `gemini.google.com`, `copilot.microsoft.com`
- GSC: podpięty, sitemap zgłoszony
- **Lista 25 promptów** (ze wszystkich sekcji "Prompty AI" powyżej) odpytywana raz w miesiącu w 4 modelach; log: czy pada nazwa kancelarii, czy jest link, na której pozycji. To jest raport dla klienta i dowód, że barter miał sens.

---

## 8. Czego świadomie NIE robimy

- **Prawo rodzinne** — rozwody, alimenty, podział majątku, władza rodzicielska. Zero wzmianek, także w tekstach pobocznych i FAQ (poza pkt 11 FAQ, który to wprost wyklucza).
- **Prawo karne i spadkowe** — nie ma w portfolio, nie dopisujemy.
- Cennika usług kancelarii — chyba że Adrian zdecyduje inaczej (pkt 9 sekcji 0).
- Sterowanego zbierania opinii — zasady etyki radcowskiej, do ustalenia z klientem.
- Obietnic wyniku ("wygramy Twoją sprawę") — niedopuszczalne i wywalane z każdego draftu.
- Sztucznego pompowania długości tekstów. 1200 słów konkretu > 2500 słów waty.

---

## 9. Co powstanie po zatwierdzeniu tego planu

W `gajewskikancelaria/`:

```
PLAN.md                          ← ten plik
specjalizacje/
  ochrona-danych-osobowych.md
  prawo-wlasnosci-intelektualnej.md
  windykacja-naleznosci.md
  prawo-spolek.md
  (fala 2: pozostałe 5)
faq.md
o-mnie.md
schema/                          gotowe bloki JSON-LD do wklejenia
podglad/                         wersja HTML do pokazania klientowi
```

Teksty w Markdownie — łatwo wkleić do WordPressa, łatwo dać do czytania Adrianowi, łatwo wersjonować w gicie.

---

## 10. Status decyzji

- [x] Boty AI wpuszczone — `robots.txt` gotowy
- [x] FAQ i "O mnie" — napisane
- [x] Fala 1: RODO, IP, windykacja, prawo spółek — napisane
- [x] Pokrycie największych miast — zrealizowane przez `/zasieg/`, patrz `zasieg/DECYZJA-MIASTA.md`
- [x] "ja" zamiast "my" — zastosowane we wszystkich tekstach
- [x] Widełki cenowe — nie podajemy (domyślnie, do zmiany na życzenie klienta)
- [ ] **Miasto i adres** — wciąż brak, `[MIASTO]` do podmiany globalnej
- [ ] Numer wpisu OIRP, rok wpisu, LinkedIn — do uzupełnienia
- [ ] Weryfikacja merytoryczna przez Adriana — lista w `DO-WERYFIKACJI.md`

## 11. Stan realizacji

| Plik | Status |
|---|---|
| `o-mnie.md` | gotowe |
| `faq.md` | gotowe (13 pytań) |
| `specjalizacje/ochrona-danych-osobowych.md` | gotowe |
| `specjalizacje/prawo-wlasnosci-intelektualnej.md` | gotowe |
| `specjalizacje/windykacja-naleznosci.md` | gotowe |
| `specjalizacje/prawo-spolek.md` | gotowe |
| `zasieg/zasieg.md` | gotowe |
| `zasieg/DECYZJA-MIASTA.md` | uzasadnienie podejścia do miast |
| `robots.txt` | gotowe |
| `schema/organizacja-i-osoba.json` + `README.md` | gotowe |
| `DO-WERYFIKACJI.md` | lista kontrolna dla klienta |
| `specjalizacje/index.md` (hub) | gotowe |
| `specjalizacje/obsluga-prawna-firm.md` | gotowe |
| `specjalizacje/prawo-pracy.md` | gotowe |
| `specjalizacje/spory-sadowe.md` | gotowe |
| `specjalizacje/podatki.md` | gotowe |
| `specjalizacje/odszkodowania.md` | gotowe |

**Komplet 9 specjalizacji + hub + FAQ + O mnie + zasięg napisany.**
Pozostaje: podmiana `[MIASTO]` i danych kancelarii, weryfikacja merytoryczna
(`DO-WERYFIKACJI.md`), wdrożenie w WordPressie, GBP, analityka i baseline promptów.
