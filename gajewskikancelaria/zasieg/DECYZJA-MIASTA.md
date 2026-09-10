# Pokrycie największych polskich miast — co robimy i czego nie

## Problem z klasycznym podejściem

Standardowa recepta na „pokryjmy duże miasta" to zestaw podstron w rodzaju
`/rodo-warszawa/`, `/rodo-krakow/`, `/rodo-wroclaw/` — ten sam tekst z podmienioną
nazwą miasta, razy 10 miast, razy 9 specjalizacji = 90 podstron.

Nie robię tego w tej wersji, z trzech powodów:

**1. Google nazywa to doorway pages i wprost to zwalcza.** To nie jest szara strefa
ani ryzyko teoretyczne — to jedna z niewielu praktyk opisanych w wytycznych jako
naruszenie, z filtrem algorytmicznym i ręcznymi działaniami włącznie. Ryzykujemy
widocznością całej domeny, nie tylko tych podstron.

**2. W GEO to nie działa nawet gdyby było bezpieczne.** Modele nie premiują liczby
adresów URL. Budują obraz podmiotu z sygnałów spójnych i weryfikowalnych: adres,
wizytówka, rejestr, wzmianki zewnętrzne. Dziesięć sprzecznych sygnałów lokalizacji
przy jednym biurze **osłabia** encję zamiast ją wzmacniać. Model, który widzi
kancelarię deklarującą obecność w dziesięciu miastach bez adresu w żadnym z nich,
ma powód, żeby jej nie cytować.

**3. Ryzyko zawodowe po stronie klienta.** Sugerowanie obecności w mieście, w którym
kancelaria nie ma biura, to informacja wprowadzająca w błąd. Adrian jest radcą
prawnym i obowiązują go zasady etyki dotyczące informowania o wykonywaniu zawodu.
To jego licencja, nie nasza kampania.

## Co robimy zamiast tego

Wersja, która daje ten sam zasięg i jest w pełni obronialna — bo opisuje model,
który kancelaria **realnie stosuje** (na obecnej stronie: *„dzięki współpracy
z adwokatami i radcami prawnymi z innych części Polski zapewniamy reprezentację
przed sądami na terenie całego kraju"*).

### Warstwa 1 — lokalna, prawdziwa
`[MIASTO]` i Śląsk. Pełny NAP, wizytówka Google, schema `LocalBusiness`.
Tu walczymy o pozycje lokalne naprawdę i tu jesteśmy nie do podważenia.

### Warstwa 2 — jedna strona zasięgu: `/zasieg/`
Uczciwy opis, jak wygląda obsługa klienta spoza regionu: co robimy zdalnie
(doradztwo, umowy, RODO, IP, korespondencja — czyli większość pracy), jak
wygląda reprezentacja przed sądem w innym mieście, kto wtedy staje na rozprawie
i kto odpowiada za sprawę. Z listą miast w treści, ale **jako opis faktycznego
modelu pracy, nie jako dziesięć landing page'y**.

To jedna strona, która ma szansę być cytowana przy pytaniach typu
„czy kancelaria z innego miasta może prowadzić moją sprawę".

### Warstwa 3 — usługi, przy których lokalizacja nie ma znaczenia
Tu jest realna przewaga i to jest właściwa odpowiedź na „pokryjmy Polskę".

RODO, własność intelektualna, umowy, prawo spółek, doradztwo bieżące — te usługi
świadczy się zdalnie w 100% i nikt nie oczekuje, że prawnik będzie z sąsiedniej
ulicy. Klient szukający kancelarii do audytu RODO wybiera po kompetencji, nie po
kodzie pocztowym. Dlatego te podstrony pisane są **bez zawężania do miasta** i to
one przynoszą ruch z całej Polski — bez jednej sztucznej strony.

Sygnał dla modeli daje się tam wprost, w treści: *„doradztwo prowadzę zdalnie dla
klientów z całej Polski"* — zdanie prawdziwe, weryfikowalne i wystarczające.

### Warstwa 4 — jeśli klient chce iść dalej (opcja, nie rekomendacja teraz)
Realne strony miejskie mają sens **tylko wtedy**, gdy stoi za nimi coś prawdziwego:
- faktyczne biuro lub adres do korespondencji w danym mieście, albo
- unikalna treść dla tego rynku (np. specyfika sądu gospodarczego w danym mieście,
  lokalna praktyka orzecznicza) napisana od zera, 1000+ słów, bez powielania.

Wtedy to nie jest doorway page, tylko normalna podstrona lokalna. Ale to koszt
1000+ słów oryginalnej treści na miasto i wymaga wkładu merytorycznego Adriana.
**Do rozważenia w fazie 3, po pierwszych wynikach — nie teraz.**

## Rekomendacja

Warstwy 1–3 teraz. Warstwa 4 dopiero, gdy będą dane z baseline'u promptów
i gdy Adrian zdecyduje, czy chce realnej obecności w konkretnym mieście.

Efekt jest ten sam, którego chcesz — widoczność w całej Polsce — tylko osiągnięty
przez treść, której model ma powód zaufać, a nie przez liczbę adresów URL.
