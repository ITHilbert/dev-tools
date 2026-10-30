# ithilbert/dev-tools

Sammelpaket (Composer-Metapackage) mit den gemeinsamen Entwicklerwerkzeugen aller Laravel-Projekte der IT-Hilbert GmbH. Es enthält keinen Code, nur Abhängigkeiten mit zentral gepflegten Versionen.

**Nur für Laravel 13.** Ältere Laravel-Versionen sind per `conflict` ausgeschlossen.

## Enthalten

| Paket | Zweck |
|---|---|
| laravel/boost | MCP-Server für KI-Agenten (Artisan, Datenbank, Doku) |
| laravel/pao | Testausgabe für KI-Agenten |
| laravel/pint | Code-Style |
| larastan/larastan | Statische Analyse (PHPStan) |
| laravel/pail | Log-Ausgabe im Terminal |
| barryvdh/laravel-debugbar | Debugbar im Browser |
| nunomaduro/collision | Fehlerausgabe in der Konsole |
| mockery/mockery | Mocks für Tests |
| fakerphp/faker | Testdaten für Factories |
| phpunit/phpunit | Testframework (PHPUnit 12) |
| brianium/paratest | Parallele Tests (`php artisan test --parallel`) |

Nicht enthalten: `laravel/sail`. Bei Bedarf im Projekt selbst einbinden.

## Installation

**Nur als Dev-Abhängigkeit installieren.** Sonst landen die Werkzeuge auf dem Produktivserver.

```bash
composer require ithilbert/dev-tools:dev-main --dev
```

Wenn die Pakete vorher einzeln in `require-dev` stehen, dort entfernen.

Produktiv-Deployment immer mit `composer install --no-dev --optimize-autoloader`.

## Laravel Boost: nur MCP, keine Skills

Unsere Skills und Guidelines liegen im Projekt bzw. im Agent-Template. Boost soll nichts davon einspielen.

```bash
php artisan boost:install
```

Bei der Auswahl nur den **MCP-Server** aktivieren, **keine** Guidelines und **keine** Skills. Die Auswahl steht danach in `boost.json` und gilt auch für `boost:update`.

## Aktualisieren

Es gibt keine Tags. Projekte binden `dev-main` ein, wie die übrigen `ithilbert/*`-Pakete.

- Werkzeug ergänzen oder Version anheben: hier in `composer.json` ändern und nach `main` pushen.
- In den Projekten: `composer update ithilbert/dev-tools --with-all-dependencies`.

## Lizenz

MIT
