# Purchasing management frontend

An Angular/TypeScript academic frontend for products, stock, invoices, settlements, operators and activity sectors. Includes a multi-stage Docker build and an Nginx configuration serving the single-page app.

This is an earlier learning project, separate from Ameni’s current professional work. [Current software engineering portfolio](https://amenibensaadaportfolio.netlify.app/?utm_source=github&utm_medium=profile&utm_campaign=personal_brand).

## Features and structure

- CRUD screens for the purchasing domain.
- Angular HttpClient services under `src/app/shared/Service`.
- Shared data models under `src/app/shared/Model`.
- Docker packaging and SPA route fallback through Nginx.

## Local setup

The project uses Angular 12. Its historical peer dependencies require `--legacy-peer-deps`; current OpenSSL versions also require the compatibility flag when building. Node.js 22 is used by the build workflow.

```sh
npm ci --legacy-peer-deps
NODE_OPTIONS=--openssl-legacy-provider npm start
```

Use the URL printed by the Angular CLI. The backend is a separate Spring Boot application. Set `apiBaseUrl` in `src/environments/environment.ts` and `environment.prod.ts` before running/building; the default is `http://localhost:8089/SpringMVC`. It replaces the original hard-coded private-network address. This frontend repository does not contain or start the backend.

## Build and container

```sh
NODE_OPTIONS=--openssl-legacy-provider npm run build
docker build -t purchasing-frontend .
docker run --rm -p 127.0.0.1:8080:80 purchasing-frontend
```

The Angular artifact is copied from `dist/crudtuto-Front` into Nginx. For a hosted environment, configure the browser-facing API URL and backend CORS before building. The Nginx file supports SPA routes; it does not configure a public API service or TLS.

The GitHub Actions workflow checks the frontend build. `npm test` invokes the original Karma/Jasmine harness; a passing build does not imply comprehensive feature tests.

## Status

Academic reference implementation with legacy Angular dependencies. This cleanup centralizes API configuration and documents the actual app; it does not upgrade the entire application to current Angular or certify production readiness. Original framework/template credits remain with their respective authors.
