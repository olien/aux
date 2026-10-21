# Changelog

## 1.4.0 – 2026-10-21

### Neu
- **Lesemaske**: dunkelt die Seite ab, nur ein Streifen (120 px) um Maus, Finger oder Tastatur-Fokus bleibt hell. Schliesst sich mit dem Lese-Lineal gegenseitig aus.
- **Graustufen** (Toggle) und **Helligkeit** (Stepper −2 … +2). Beide sind mit den Kontrastmodi kombinierbar, die Filter werden zu einem einzigen `filter` zusammengesetzt.
- **Zurücksetzen-Button** im festen Footer des Panels, löscht auch den gespeicherten Zustand (`localStorage`).
- Das Panel ist jetzt ein **Off-Canvas** über die volle Seitenhöhe (fährt von der Seite des Widgets ein).
- Aktive Optionen sind zusätzlich zur Farbe durch Häkchen und stärkeren Rahmen markiert.
- Stepper-Beschriftungen für Screenreader sind übersetzbar (`decrease` / `increase`).
- Cache-Buster (`?v=<Änderungszeit>`) an CSS- und JS-URLs.
- Barrierefreiheit des Widgets selbst:
  - Das Widget ist der erste Tab-Stopp der Seite (liegt vor `<body>`), statt erst nach allen Seitenelementen erreichbar zu sein.
  - Optionsgruppen (Profile, Kontrast, Textausrichtung, Stepper, Position) sind als `role="group"` mit Namen ausgezeichnet.
  - Schalter 44×24 px (WCAG 2.2 Zielgröße), Rahmen der Bedienelemente mit mindestens 3:1 Kontrast, keine Schrift unter 12 px.
  - Unterstützung für Windows-Kontrastmodus (`forced-colors`): Schalter und Häkchen bleiben sichtbar.
  - Die Meldung „Widget ausgeblendet“ wird als `role="status"` angekündigt.
  - `Strg/⌘ + Alt + A` öffnet und schliesst jetzt auch das Panel, wenn das Widget sichtbar ist.
  - **Textleser-Statusleiste**: Solange der Textleser aktiv ist (er fängt Klicks auf Links und Buttons ab), zeigt eine Leiste am unteren Rand den Zustand an (`role="status"`) und bietet „Beenden“. `Esc` beendet den Textleser ebenfalls.
  - **Schriftgrössen folgen der Browser-Einstellung**: Das Panel skaliert mit der Standard-Schriftgrösse des Browsers (`max(14px, 0.875rem)`, also nie kleiner als 14 px, auch auf Seiten mit `html { font-size: 62.5% }`).
- **Konfiguration**: Warnung im Backend, wenn die Button-Farbe weniger als 3:1 Kontrast zu Weiss hat (weisses Icon, Fokusring, Aktiv-Markierungen; WCAG 1.4.11). Neue Methode `Aux::contrastRatio()`, neuer Sprachschlüssel `aux_button_color_warning`.

### Geändert
- Der dekorative Männchen-Icon im Panel-Header entfällt (der Button trägt es bereits); die sichtbare Überschrift bleibt als Name des Panels.
- Emoji-Icons der Profile, Schliessen- und Reset-Button durch Inline-SVGs (Stroke-Stil) ersetzt, alle mit `aria-hidden="true"`.
- **Hoher Kontrast** arbeitet jetzt mit Farbüberschreibung (weiss auf schwarz, gelbe Links, weisse Rahmen) statt mit `contrast()`-Filter. Der Filter machte helle Elemente noch heller und damit unsichtbar.
- Das Widget liegt als Kind von `<html>` (nicht mehr in `<body>`); Filter liegen auf `<body>`. Dadurch wird das Widget nie mitgefiltert; die bisherige Positions-Korrektur (`applyContrastPositionFix`) und das Gegen-Invertieren des Widgets entfallen.
- Zurücksetzen setzt auch die Widget-Position auf die Server-Vorgabe zurück.
- Optik überarbeitet: ein einheitlicher Radius (6 px, Schalter und Haken bleiben rund), einheitliches Abstandsraster (4 / 8 / 16 / 20 px), Bedienelemente mit gleicher Höhe, ruhigere Farben (`#111827` / `#4b5563`), Aktiv-Farbe leitet sich per `color-mix` aus der Button-Farbe ab. Der Button ist ein abgerundetes Quadrat statt eines Kreises. Kontrast, Zielgrössen und Häkchen bleiben unverändert.
- Stepper zeigen positive Werte mit Vorzeichen (`+1`).
- Auf Smartphones (bis 420 px) nutzt das Panel die volle Breite.
- **Unabhängig vom `<meta name="viewport">` der Seite**: Das Widget richtet sich am sichtbaren Viewport aus (`visualViewport`) und gleicht dessen Skalierung aus. Auch auf Seiten ohne Viewport-Meta (Handy rechnet dann mit ~980 px Breite) oder bei Pinch-Zoom bleiben Button und Panel in normaler Grösse an derselben Stelle sichtbar. Die Breite des Panels richtet sich nach dem Viewport statt nach `100vw`.
- Stepper (Helligkeit, Textgrösse, Zeilen- und Buchstabenabstand) stehen als Zeile: Beschriftung links, Bedienelement rechts.

### Behoben
- Erste Reihe der Profil-Kacheln wurde vom Header überdeckt: Panel ist jetzt Flex-Spalte (Header fix / Inhalt scrollt / Footer fix).
- Fokus sprang beim Öffnen nicht ins Panel (`visibility`-Übergang), und beim Schliessen über den Schliessen-Button nicht zurück auf den Öffnen-Button.
- Dyslexie-Schrift, Zeilen-/Buchstabenabstand, Textausrichtung und „Animationen stoppen“ wirkten auch auf das Widget selbst (Text lief aus dem Panel). Die Regeln gelten jetzt nur noch für `body`.
- Stepper-Beschriftungen waren fest auf Deutsch kodiert.
- Die Focus-Hervorhebung (orangefarbener Ring) wirkte auch auf die Bedienelemente des Widgets und überlagerte dessen eigenen Fokusring. Sie gilt jetzt nur noch für die Seite.
- Das Lese-Lineal folgt jetzt auch dem Finger (`touchmove`), nicht nur der Maus.
- Auf Geräten ohne Maus oder Trackpad (`any-pointer: fine` trifft nicht zu) wird „Cursor vergrössern“ nicht mehr angezeigt.
- Typ-Annotationen in `Aux.php` ergänzt (`inject()`, `getTranslations()`), das AddOn ist damit auf PHPStan Level 6 (Rexstan) ohne Funde.
- Reset und Textleser warfen in Browsern ohne `speechSynthesis` einen Fehler.

## 1.3.1

Vorherige Version (siehe Git-Historie).
