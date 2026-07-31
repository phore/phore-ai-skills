---
name: phore-dev-lib
description: Unterstützt die Entwicklung von PHP 8 Phore Libraries mit Source-Root src/, PHPUnit-Tests unter test/ und projektbegleitender .ai-usage-info.md über den Skill update-ai-usage-info.
---

# Phore Dev Lib

Dieser Skill unterstützt bei der Entwicklung, Pflege und Qualitätssicherung von PHP-8-basierten Phore Libraries.

Phore Libraries sind Composer-Pakete mit folgendem Standardlayout:

- Source Root: `src/`
- Tests: `test/` mit PHPUnit
- Projektbeschreibung für KI-Agenten: `.ai-usage-info.md`, gepflegt mit dem Skill `update-ai-usage-info`

## Wann verwenden?

Verwende diesen Skill, wenn an einer PHP8 Phore Library gearbeitet wird, insbesondere bei:

- Implementierung oder Refactoring von Klassen, Interfaces, Traits oder globalen Funktionen unter `src/`.
- Erstellung, Anpassung oder Ausführung von PHPUnit-Tests unter `test/`.
- Prüfung von Composer-Autoloading, Namespaces und Paketstruktur.
- Aktualisierung der `.ai-usage-info.md` nach API-Änderungen.
- Vorbereitung von Pull Requests, Releases oder technischen Aufräumarbeiten.

## Projektkontext erfassen

1. Lies zuerst `composer.json` und prüfe den Projektnamen
2. Prüfe die Quellstruktur unter `src/`.
3. Prüfe vorhandene Tests unter `test/`.
4. Prüfe vorhandene Konfigurationen wie:
   - `phpunit.xml` 

Liest nur die Dateien ein, die notwendig sind. Vermeide es unnötig alle Dateien zu laden, um die Performance zu verbessern.

## Entwicklungsregeln

- Schreibe PHP-Code für PHP 8 und berücksichtige die in `composer.json` gesetzte Mindestversion.
- Halte Namespaces exakt synchron mit `composer.json` / PSR-4-Autoloading.
- Lege produktiven Code ausschließlich unter `src/` ab.
- Lege PHPUnit-Tests unter `test/` ab.
- Erfinde keine öffentlichen APIs, wenn die Aufgabe nur Bugfixing oder Wartung verlangt.
- Bevorzuge klare, kleine Klassen und Funktionen mit expliziten Typen.
- Nutze `declare(strict_types=1);`, wenn dies im Projekt üblich ist.
- Halte bestehende Code-Style-Konventionen des Projekts ein.
- Vermeide unnötige neue Dependencies.

## Tests und Qualitätssicherung

Nach Codeänderungen:

1. Führe nach Möglichkeit die vorhandenen Test-Scripts aus, z. B.:
   - `composer test`
   - `vendor/bin/phpunit`
   - `vendor/bin/phpunit -c phpunit.xml`
2. Falls keine Dependencies installiert sind, prüfe zuerst, ob `composer install` sinnvoll und erlaubt ist.
3. Wenn Tests nicht ausführbar sind, dokumentiere knapp den Grund.
4. Ergänze oder aktualisiere PHPUnit-Tests für geändertes Verhalten.
5. Tests sollen reale öffentliche APIs testen, nicht unnötig interne Implementierungsdetails.

## .ai-usage-info.md aktualisieren

Wenn durch die Arbeit öffentliche Klassen, Funktionen, Beispiele oder zentrale Nutzungsmuster geändert werden, verwende zusätzlich den Skill `update-ai-usage-info`.

## Typischer Ablauf

1. Prüfe die Aufgabenstellung und den Projektkontext. Korrigiere ggf. Typos im prompt z.B. `exaples` → `examples`.
2. Prüfe die Quellstruktur und vorhandene Tests.
3. Prüfe die vorhandene `.ai-usage-info.md` und aktualisiere sie nur, wenn sich durch die Änderungen relevante öffentliche APIs oder Nutzungsmuster geändert haben.



## Dies darfst Du nicht

Niemals darfst du:
- Direkt in `/vendor/` oder `/node_modules/` schreiben.

## Helper functions / methods

Helper methoden oder funktionen, die in mehr als einer Klasse genutzt werden sollten unter einer Helper-Klasse als statische Methode
angelegt werden.

Sind komplexe Abläufe nötig, sollten komplette logikabschnitte in eigene Funktionsklassen ausgelagert werden. 

Vermeide es, private helper methoden, die nur in einer methode genutzt werden anzulegen. Packe diese besser in die Methode selbst, um die Lesbarkeit zu erhöhen.


## Exceptions

Nutze wo geht Exceptions. Teste php funktionen auf Rückgabewerte und wirf Exceptions bei Fehlern. Verwende niemals
exit() die() order trigger_error() ohne zu fragen. Wenn Custom Exceptions definiert sind, nutze diese. Wenn keine Custom Exceptions definiert sind, nutze die Standard Exceptions.

## Environment-Variablen

Greife niemals direkt auf Environment-Variablen zu außer dies ist explizit gewünscht.

## Unittests

Lege Unittests ausschließlich unter `test/` ab. Vermeide es, Tests in `src/` zu platzieren.

Unterscheide Unittests und Integrationstest.

- Lege wenige tests an, die die Kernfunktionalität der Library abdecken.

## Antwortstil

- Sprache: Deutsch, sofern der Benutzer nichts anderes verlangt.
- Nenne geänderte Dateien klar mit Pfad.
- Fasse technische Entscheidungen kurz zusammen.
- Gib Testbefehle und Ergebnisse an.
- Weise auf nicht ausgeführte Prüfungen samt Grund hin.
