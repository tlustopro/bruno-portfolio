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
cd collections
bru run rest -r --env prod
bru run graphql -r --env prod
```

## CI/CD

Every push and pull request against `main` triggers the [`API Tests (Bruno)`](.github/workflows/api-tests.yml) GitHub Actions workflow, which:

1. Installs `@usebruno/cli` on an Ubuntu runner.
2. Runs the REST and GraphQL collections with `--env prod`.
3. Emits JUnit + HTML reports and uploads them as the `bruno-reports` workflow artifact.
4. On `main`, publishes the HTML reports to **GitHub Pages** — a landing page links to the REST and GraphQL reports and shows the commit SHA.

One-time setup: in the repo go to **Settings → Pages → Build and deployment → Source: GitHub Actions**. After the next successful run on `main`, the reports are live at `https://<user>.github.io/<repo>/`.

## Testing Logic Examples

- **Status codes** — 200 OK, 201 Created
- **Response structure** — required fields, data types
- **Business rules** — email validation with regex, arrays are not empty
- **GraphQL specifics** — absence of `errors`, navigation via `data.*`
- **Pre/post-request scripts** — sharing data between requests via `bru.setVar()`
