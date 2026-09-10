# Schema — instrukcja wdrożenia

## Pliki
- `organizacja-i-osoba.json` — do `<head>` **strony głównej**. Definiuje encję kancelarii
  i encję Adriana, do których pozostałe strony się odwołują przez `@id`.

## Zasady

**1. Jedna definicja, wiele odwołań.** Kancelaria i osoba są zdefiniowane raz, na stronie
głównej. Podstrony nie powtarzają tych danych — odwołują się przez `@id`. Powielanie
pełnych definicji na każdej podstronie produkuje sprzeczne sygnały o encji.

**2. Każda podstrona specjalizacji** dostaje:
```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Service",
      "name": "[nazwa usługi]",
      "serviceType": "[nazwa usługi]",
      "url": "[URL podstrony]",
      "provider": { "@id": "https://www.kancelariagajewski.pl/#kancelaria" },
      "areaServed": { "@type": "Country", "name": "Polska" }
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        { "@type": "Question", "name": "[pytanie]",
          "acceptedAnswer": { "@type": "Answer", "text": "[odpowiedź]" } }
      ]
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Strona główna", "item": "https://www.kancelariagajewski.pl/" },
        { "@type": "ListItem", "position": 2, "name": "Specjalizacje", "item": "https://www.kancelariagajewski.pl/specjalizacje/" },
        { "@type": "ListItem", "position": 3, "name": "[nazwa]" }
      ]
    }
  ]
}
```

**3. FAQPage tylko z pytaniami widocznymi na stronie.** Treść w schema musi odpowiadać
treści widocznej dla użytkownika. Rozjazd to naruszenie wytycznych dotyczących danych
strukturalnych.

**4. `/o-mnie/`** — pełna definicja `Person` + `Attorney` (ta z pliku), bo to strona
kanoniczna dla tej encji.

**5. `/kontakt/`** — `LocalBusiness` z pełnym NAP i `openingHours`.

## Wdrożenie w WordPressie
Jeśli działa Yoast albo RankMath, oba generują własne schema — trzeba je skonfigurować,
a nie dokładać drugi, konkurencyjny blok JSON-LD. Kolejność działań:
1. sprawdzić, co wtyczka już generuje (Rich Results Test),
2. uzupełnić w ustawieniach wtyczki typ organizacji, dane i profile `sameAs`,
3. dodać ręcznie tylko to, czego wtyczka nie umie — zwykle `Service` i `hasOfferCatalog`.

## Weryfikacja
- Rich Results Test (Google)
- Schema Markup Validator (schema.org)
- Po wdrożeniu: raport „Ulepszenia" w Search Console
