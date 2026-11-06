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
| phpunit/phpunit | Testframework (PHPUnit 12 oder 13) |
| brianium/paratest | Parallele Tests (`php artisan test --parallel`) |

Nicht enthalten: `laravel/sail`. Bei Bedarf im Projekt selbst einbinden.

## Installation

**Nur als Dev-Abhängigkeit installieren.** Sonst landen die Werkzeuge auf dem Produktivserver.

```bash
composer require --dev ithilbert/dev-tools:^1.0
```

Wenn die Pakete vorher einzeln in `require-dev` stehen, dort entfernen.

Produktiv-Deployment immer mit `composer install --no-dev --optimize-autoloader`.

## Laravel Boost: nur MCP, keine Skills

Unsere Skills und Guidelines liegen im Projekt bzw. im Agent-Template. Boost soll nichts davon einspielen.

```bash
php artisan boost:install
```

Bei der Auswahl nur den **MCP-Server** aktivieren, **keine** Guidelines und **keine** Skills. Die Auswahl steht danach in `boost.json` und gilt auch für `boost:update`.

## Versionen und PHPUnit

Das Paket wird über Versions-Tags (`1.0.0`, `1.1.0` …) eingebunden, nicht über `dev-main`. *Warum:* Projekte mit `minimum-stability: stable` können `dev-main` nur mit `@dev` einbinden (excel-programmierer.com, Task #716).

PHPUnit 12 (ab 12.5.14) und PHPUnit 13 sind zugelassen. Welche Version installiert wird, legt das Projekt selbst fest, z. B. mit `"phpunit/phpunit": "^13.4"` in `require-dev`. paratest wird passend dazu aufgelöst.

### paratest höchstens 7.26.0 (wegen laravel/pao)

`brianium/paratest` ab 7.26.1 ist per `conflict` ausgeschlossen. *Warum:* laravel/pao (bis 1.1.5) baut `WrapperRunner::run()` von paratest nach und kennt das in 7.26.1 eingeführte `runTmpDir` nicht. In Agent-Sessions bricht dann jeder Parallellauf mit „Typed property … `$runTmpDir` must not be accessed before initialization“ ab (Task #834). pao steckt auch im Laravel-13-Skeleton, deshalb wird paratest begrenzt und nicht pao entfernt.

- PHPUnit 13 läuft damit mit paratest 7.26.0, also PHPUnit 13.4.x. PHPUnit 12 ist nicht betroffen (paratest 7.20).
- Nachteil: Der Sicherheitsfix aus paratest 7.26.1 fehlt (Worker-Dateien in einem privaten Ordner je Lauf). Er betrifft nur Rechner, auf denen mehrere Benutzer arbeiten. dev-tools läuft nur auf Entwicklerrechnern.
- Aufheben, sobald eine laravel/pao-Version `runTmpDir` unterstützt: `conflict` hier entfernen, pao-Untergrenze auf diese Version setzen, neuer Tag.

## Aktualisieren

- Werkzeug ergänzen oder Version anheben: hier in `composer.json` ändern, nach `main` pushen und einen neuen Tag setzen (neues Werkzeug: Minor, angehobene Version: Patch).
- In den Projekten: `composer update ithilbert/dev-tools --with-all-dependencies`.

## Lizenz

MIT
