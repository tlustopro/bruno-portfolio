# Bruno API Testing Portfolio

A sample collection of API tests written in [Bruno](https://www.usebruno.com/) — an open-source alternative to Postman/Insomnia.

## What is Bruno?

Bruno is an offline-first API client with its own DSL for defining requests and tests. Collections are plain-text files that can be version-controlled in git.

## Project Structure

```
collections/
├── environments/       # Environment variables
├── rest/
│   ├── users/          # CRUD operations on the users endpoint
│   └── posts/          # Posts + comments with pre/post scripts
└── graphql/
    └── countries/      # GraphQL queries with variables
```

## Public APIs Used

| Collection | API | Documentation |
|------------|-----|---------------|
| REST | JSONPlaceholder | https://jsonplaceholder.typicode.com |
| GraphQL | Countries API | https://countries.trevorblades.com |

## How to Run Tests

1. Install Bruno: https://www.usebruno.com/downloads
2. Open the `collections/` folder as a collection
3. Select the `prod` environment
4. Run any request or the entire collection

### CLI (headless)

```bash
npm install -g @usebruno/cli
bru run --env prod collections/rest/users/
bru run --env prod collections/graphql/
```

## Testing Logic Examples

- **Status codes** — 200 OK, 201 Created
- **Response structure** — required fields, data types
- **Business rules** — email validation with regex, arrays are not empty
- **GraphQL specifics** — absence of `errors`, navigation via `data.*`
- **Pre/post-request scripts** — sharing data between requests via `bru.setVar()`
