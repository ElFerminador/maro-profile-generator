# Maro Profile Generator

Ein regelbasierter Profil-Generator für die [Maro Model 1](https://maro.coffee) Espressomaschine.

Inspiriert vom [Espresso Profile Generator](https://decentespresso.com/blog/espresso_profile_generator_preview) von Stéphane Ribes (ursprünglich für Decent Espresso) — neu gebaut für die Stage-Semantik der Maro.

## Was es macht

Du beantwortest ein paar Fragen zu deiner Bohne (Röstgrad, Herkunft, was du hervorheben oder vermeiden möchtest, Dosis, Frische der Bohnen), und das Tool generiert dir ein passendes 4-Stage-Profil im Maro-Format — mit Druck- oder Flussprofil pro Stage, Limits und Stop-Bedingungen.

Das Profil bekommst du in zwei Formen:

- **Druck/Fluss-Kurve** zur Vorschau
- **Stage-Karten** im exakten Wortlaut wie im Maro Home Extreme Mode ("X ml/s in Ys mit einem Limit von Y bar"), zum Abtippen in die Maschine

Dazu eine Begründung "Warum dieses Profil?" und ein Mahlgrad-Hinweis je nach Bohnen-Alter.

## Live

➜ **[hier ausprobieren](https://ElFerminador.github.io/maro-profile-generator/)**

## Was es nicht ist

- **Kein offizielles Maro-Tool.** Inoffiziell, privat gebaut.
- **Kein JSON-Import nach Maro.** Da Maro Home aktuell keinen Profil-Import unterstützt, ist der Output zum Abtippen gedacht.
- **Kein Ersatz für Erfahrung.** Die Regeln sind Heuristiken, keine harte Wissenschaft. Sieh die Vorschläge als Ausgangspunkt für eigene Experimente.

## Technik

Eine einzige HTML-Datei. Keine Dependencies (ausser Google Fonts). Kein Build-Step. Läuft auf GitHub Pages, Netlify, oder lokal per Doppelklick.

- Vanilla JavaScript für die Regel-Engine
- Inline-SVG für das Druck/Fluss-Diagramm
- CSS Custom Properties für Hell/Dunkel-Theme (Auswahl wird in `localStorage` gespeichert)
- Vollständig auf Deutsch

## Regel-Engine kurz erklärt

Pro Eingabe-Dimension werden Basis-Werte (Temperatur, Peak-Druck, Pre-Infusion-Zeit, Brew-Ratio, Modus-Bias) angepasst. Zum Beispiel:

| Eingabe | Effekt |
|---|---|
| Helle Röstung | +2 °C, längere Pre-Infusion, niedrigerer Peak |
| Dunkle Röstung | −2 °C, sanfterer Peak |
| Floral hervorheben | Flow-Bias, tieferer Druck, längere PI |
| Body hervorheben | Pressure-Bias, höherer Peak |
| Bitterkeit vermeiden | Decline-Stage mit niedrigerem End-Druck |
| Frische Bohnen | Längere PI gegen CO₂-Channeling, gröber mahlen |
| Alte Bohnen | Wärmer, feiner mahlen |

Daraus wird ein 4-Stage-Profil generiert: Pre-Infusion → Sättigung → Haupt-Extraktion → Decline.

## Selbst hosten

```bash
git clone https://github.com/USERNAME/maro-profile-generator.git
```

Datei in den Browser ziehen — fertig. Oder auf GitHub Pages aktivieren (Settings → Pages → Branch `main` / `(root)`).

## Anpassen

Das gesamte Regelwerk steckt in der Funktion `buildProfile()` in der HTML-Datei. Wer eigene Heuristiken hat, kann die Werte direkt dort tunen.

## Credits

- Konzept: [Stéphane Ribes](https://www.thepickychemist.com/) (Decent Espresso Profile Generator)
- Maschine: [Maro Coffee Engineering GmbH](https://maro.coffee)
- Diese Adaption: hobby-mässig, ohne Garantie auf irgendwas.

## Lizenz

MIT.
