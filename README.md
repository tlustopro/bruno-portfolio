# Bruno API Testing Portfolio

Ukázková kolekce API testů napsaných v nástroji [Bruno](https://www.usebruno.com/) — open-source alternativa k Postman/Insomnia.

## Co je Bruno?

Bruno je offline-first API klient s vlastním DSL pro definici requestů a testů. Kolekce jsou plain-text soubory verzovatelné v gitu.

## Struktura projektu

```
collections/
├── environments/       # Environment proměnné
├── rest/
│   ├── users/          # CRUD operace nad users endpointem
│   └── posts/          # Posts + comments s pre/post skripty
└── graphql/
    └── countries/      # GraphQL dotazy s proměnnými
```

## Použitá veřejná API

| Kolekce | API | Dokumentace |
|---------|-----|-------------|
| REST | JSONPlaceholder | https://jsonplaceholder.typicode.com |
| GraphQL | Countries API | https://countries.trevorblades.com |

## Jak spustit testy

1. Nainstaluj Bruno: https://www.usebruno.com/downloads
2. Otevři složku `collections/` jako kolekci
3. Vyber environment `prod`
4. Spusť libovolný request nebo celou kolekci

### CLI (headless)

```bash
npm install -g @usebruno/cli
bru run --env prod collections/rest/users/
bru run --env prod collections/graphql/
```

## Ukázky testovací logiky

- **Stavové kódy** — 200 OK, 201 Created
- **Struktura odpovědi** — povinná pole, datové typy
- **Obchodní pravidla** — email validace regexem, pole nejsou prázdná
- **GraphQL specifika** — absence `errors`, navigace přes `data.*`
- **Pre/post-request skripty** — sdílení dat mezi requesty přes `bru.setVar()`
