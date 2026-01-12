---
category: general
date: 2026-01-12
description: Lernen Sie, wie Sie Informationen von AsposeAI anzeigen, indem Sie lokale
  Modelle auflisten, den Modellnamen, die Größe und den zuletzt verwendeten Zeitstempel
  in einem klaren Python‑Beispiel zeigen.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: de
og_description: 'Wie man Informationen von AsposeAI anzeigt: lokale Modelle auflisten,
  Modellname, Größe und zuletzt verwendeten Zeitstempel anzeigen, mit einer vollständigen
  Python-Anleitung.'
og_title: Wie man Informationen anzeigt – Lokale Modelle, Name, Größe, zuletzt verwendet
tags:
- AsposeAI
- Python
- Model Management
title: Wie man Informationen anzeigt – Lokale Modelle, Name, Größe, zuletzt verwendet
url: /de/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# So zeigen Sie Informationen an – Lokale Modelle auflisten, Name, Größe, zuletzt verwendet

Schon mal überlegt, **wie man Informationen** aus Ihrer AsposeAI‑Installation anzeigt, ohne durch Logs oder die UI zu wühlen? Sie sind nicht allein. In vielen Data‑Science‑Pipelines ist das Erste, was Sie brauchen, ein schneller Überblick darüber, welche Modelle auf Ihrem Rechner liegen, wie sie heißen, wie groß sie sind und wann Sie sie zuletzt verwendet haben.

Genau das werden wir behandeln: ein kompakter, End‑to‑End‑Python‑Snippet, das **lokale Modelle auflistet**, dann **den Modellnamen anzeigt**, **die Modellgröße zeigt** und **Zeitstempel des letzten Zugriffs** ausgibt. Keine externen Bibliotheken, keine versteckte Magie – nur der AsposeAI‑Client, den Sie bereits besitzen.

Am Ende dieses Tutorials können Sie den Code in jedes Skript einfügen, ausführen und sofort eine übersichtliche Tabelle Ihrer lokal zwischengespeicherten Modelle erhalten. Das ist ideal, um Umgebungen zu prüfen, Gesundheits‑Dashboards zu erstellen oder einfach die Neugier zu befriedigen, was auf der Festplatte liegt.

## Voraussetzungen

- Python 3.8 oder neuer (das Beispiel verwendet f‑Strings, daher ist 3.6+ zwingend erforderlich)
- `asposeai`‑Paket installiert (`pip install asposeai`)
- Eine funktionierende AsposeAI‑Lizenz oder ein Testschlüssel (der Client übernimmt die Anmeldedaten aus Umgebungsvariablen oder einer Konfigurationsdatei)

Wenn Sie diese Punkte bereits erfüllt haben, super – lassen Sie uns loslegen.

## Schritt 1: So zeigen Sie Informationen an – Initialisieren des AsposeAI‑Clients

Bevor wir **lokale Modelle auflisten** können, benötigen wir ein Client‑Objekt, das mit der AsposeAI‑Runtime kommuniziert. Dieser Schritt ist die Grundlage; ohne ihn würde der restliche Code einen `NameError` auslösen.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Warum das wichtig ist*: Durch die Initialisierung des Clients wird eine Sitzung mit der lokalen Inferenz‑Engine aufgebaut, wobei notwendige native Bibliotheken geladen werden. Außerdem wird überprüft, dass Ihre Lizenz aktiv ist, wodurch kryptische Fehler später beim Abfragen von Modellen vermieden werden.

> **Pro‑Tipp**: Wenn Sie dies auf einem CI‑Server ausführen, setzen Sie `ASPOSEAI_LICENSE` in der Umgebung, damit der Client ohne interaktive Eingabeaufforderungen starten kann.

## Schritt 2: Lokale Modelle auflisten – Verfügbare Modelle abrufen

Jetzt, da der Client bereit ist, können wir **lokale Modelle auflisten**. Die Methode `list_local()` gibt eine Sammlung von Objekten zurück, die Eigenschaften wie `name`, `size_mb` und `last_used` bereitstellen.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Was im Hintergrund passiert*: `list_local()` durchsucht das Verzeichnis, in dem AsposeAI Modell‑Dateien cached (`~/.asposeai/models` standardmäßig) und erstellt leichte Metadaten‑Objekte. Das ist schnell, weil die Modell‑Gewichte nicht geladen werden – es wird nur ein kleines JSON‑Manifest gelesen.

Falls Sie sich jemals fragen, ob ein bestimmtes Modell bereits gecached ist, ist dieser Aufruf der schnellste Weg, dies zu bestätigen.

## Schritt 3: Modellnamen anzeigen, Modellgröße zeigen und letzten Zugriff anzeigen

Mit den Modellen in der Hand **zeigen wir schließlich Informationen** an, indem wir über die Sammlung iterieren und jedes Attribut ausgeben. Hier **zeigen wir den Modellnamen**, **die Modellgröße** und **den letzten Zugriff** in einer übersichtlichen Zeile an.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Erwartete Ausgabe** (Ihre Zeitstempel werden abweichen):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Warum wir es so formatieren*: Der Bindestrich (`–`) trennt die Felder zur besseren Lesbarkeit, und die Kopfzeile macht die Konsolenausgabe scan‑freundlich. Wenn Sie später ein maschinenlesbares Format benötigen (CSV, JSON), können Sie den `print`‑Aufruf leicht durch `writer.writerow` oder `json.dump` ersetzen.

### Umgang mit Randfällen

- **Keine Modelle gecached** – `list_local()` gibt eine leere Liste zurück. Die Schleife wird einfach übersprungen, sodass nur die Kopfzeile bleibt. Sie könnten eine Absicherung hinzufügen:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Fehlende Attribute** – In seltenen Fällen kann ein Manifest beschädigt sein. Der Zugriff auf `model_info.last_used` könnte einen `AttributeError` auslösen. Wickeln Sie das `print`‑Statement in ein `try/except`, wenn Sie solche Probleme erwarten.

- **Große Modelldirektoren** – Wenn Sie Hunderte von Modellen haben, sollten Sie die Ausgabe paginieren oder in eine Datei schreiben, anstatt sie in die Konsole zu drucken.

## Visuelle Zusammenfassung (Optional)

Wenn Sie einen schnellen visuellen Hinweis bevorzugen, zeigt das Diagramm unten den Ablauf von der Client‑Initialisierung bis zur finalen Anzeige.

![Diagramm, das zeigt, wie Informationen vom AsposeAI‑Client angezeigt werden](/images/how-to-display-info.png "Diagramm zur Anzeige von Informationen")

*Alt‑Text*: **how to display info** – schematischer Ablauf der AsposeAI‑Client‑Initialisierung, Modellauflistung und Informationsanzeige.

## Vollständiges funktionierendes Skript

Wenn wir alles zusammenfügen, hier das komplette, sofort ausführbare Skript:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Speichern Sie dies als `list_models.py`, machen Sie es ausführbar (`chmod +x list_models.py`) und führen Sie es aus:

```bash
./list_models.py
```

Sie werden die zuvor gezeigte übersichtliche Liste sehen.

## Fazit

Wir haben gezeigt, **wie man Informationen** aus AsposeAI **durch Auflisten lokaler Modelle**, anschließend **Anzeige des Modellnamens**, **Anzeige der Modellgröße** und **Anzeige des letzten Zugriffs** ausgibt. Der Ansatz ist leichtgewichtig, erfordert nur das Standard‑`asposeai`‑Paket und kann in jede Automatisierungspipeline oder Debug‑Sitzung eingebunden werden.

Ab hier könnten Sie:

- Die Ausgabe nach CSV exportieren für Tabellen‑Analyse (`csv`‑Modul).
- Die Zeitstempel in ein Monitoring‑Dashboard einspeisen, um bei veralteten Modellen Alarm zu schlagen.
- Dieses Skript mit `aspose_ai.download()` kombinieren, um Modelle, die eine Weile nicht verwendet wurden, automatisch zu aktualisieren.

Denken Sie daran, klare Sichtbarkeit über Ihr Modell‑Inventar spart Zeit, reduziert Speicherüberfluss und hält Ihre KI‑Dienste reibungslos am Laufen. Probieren Sie das Skript aus, passen Sie die Formatierung nach Ihrem Geschmack an und lassen Sie es zu einem festen Bestandteil Ihrer Werkzeugkiste werden.

Viel Spaß beim Coden, und mögen Ihre Modelle stets frisch sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}