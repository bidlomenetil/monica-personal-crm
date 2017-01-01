# Monica personal CRM

Personal relationship management application with a Laravel/PHP backend and a Vue/Inertia frontend.

This repository is a separately imported source snapshot of [monica](https://github.com/monicahq/monica). Upstream contributors created the imported application; local work is recorded in the commits after the source import. See [Upstream source](UPSTREAM_SOURCE.md) for attribution.

## Read the history accurately

The local history starts with a source import on November 3, 2026. The parent year directory and the “Original project year” field do not establish a historical contribution date or a release tag. The imported upstream commit and release are not recorded in the available provenance file.

## Navigate the source

| Path | Responsibility |
| --- | --- |
| [app/](app/) | Domain and application logic |
| [routes/](routes/) | HTTP routes |
| [resources/](resources/) | Frontend and view resources |
| [database/](database/) | Migrations and seeders |
| [tests/](tests/) | PHP test suites |

## Prepare development

Read `composer.json`, `package.json`, `.tool-versions`, and `.env.example.sail`. Configure PHP extensions and an isolated local database before using Laravel commands. The root `yarn test` script runs `migrate:fresh` against the testing connection and reseeds it; use a disposable test database only.

The commands below are existing project entry points, to run after their toolchain, dependency, and service prerequisites are ready:

```sh
yarn build
yarn lint
yarn test
```

## Validation scope

The documentation change was checked for local link targets, manifest command references, and whitespace errors. Application builds, dependency installation, and service-backed test suites were not run for this documentation change. These instructions do not establish deployment readiness.

## Preserve upstream licensing

Missing upstream license notices were restored from the official repository. [License restoration](LICENSE_RESTORATION.md) records the retrieval revision, exact source URLs, and SHA-256 hashes. That revision does not identify the imported application snapshot. Read per-file and subtree notices as well as the root license before redistribution. This documentation does not change the license of imported code.

## Install and run locally

Prepare the PHP runtime/extensions from `composer.json` and the pinned Yarn version. Create a local environment and install dependencies:

```sh
cp .env.example.sail .env
composer install
yarn install --immutable
php artisan key:generate
```

Edit `.env` for local database and service credentials. The Compose definition provides the Sail application, database, cache, queue, and mail services; its application image uses the installed `vendor/laravel/sail` runtime:

```sh
./vendor/bin/sail up -d
./vendor/bin/sail artisan migrate
yarn dev
```

Use a new development database for initial migrations. The Vite command serves frontend development assets while Sail serves the PHP application. `yarn test` rebuilds and seeds the testing database; it must never target production data.

## Plan a deployment

Review `scripts/docker/` and the `docker:build` package script for the application container build. Set application URL and keys, persist database/storage data, and run queue workers and scheduled tasks. Development Sail settings and mail services need environment-specific production replacements.
