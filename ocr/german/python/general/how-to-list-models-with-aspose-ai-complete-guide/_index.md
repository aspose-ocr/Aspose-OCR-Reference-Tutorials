---
category: general
date: 2026-07-05
description: Wie man Modelle mit Aspose AI auflistet, automatisches Herunterladen
  aktiviert und ein Hugging‑Face‑Modell in Python herunterlädt. Folgen Sie diesem
  Schritt‑für‑Schritt‑Tutorial, um den Cache einzurichten und noch heute Aspose AI
  zu nutzen.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: de
og_description: Wie man Modelle mit Aspose AI auflistet, automatisches Herunterladen
  aktiviert und ein Hugging‑Face‑Modell herunterlädt. Erfahren Sie, wie Sie den Cache
  einstellen und Aspose AI in Minuten nutzen.
og_title: Wie man Modelle mit Aspose AI auflistet – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Wie man Modelle mit Aspose AI auflistet – kompletter Leitfaden
url: /de/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Modelle mit Aspose AI auflistet – Vollständige Anleitung

Wie man Modelle mit Aspose AI auflistet, ist eine Frage, die sofort auftaucht, sobald Sie anfangen, mit großen Sprachmodellen in Python zu experimentieren. In diesem Tutorial führen wir Sie durch das Aktivieren des **auto download**, das Konfigurieren eines lokalen Caches und das Abrufen eines Modells direkt von Hugging Face – damit Sie sofort loslegen können, ohne Dateien manuell suchen zu müssen.

Falls Sie sich jemals gefragt haben *„wie verwende ich Aspose für OCR‑gesteuerte KI?“* oder *„wie richte ich den Cache für Modelldateien am einfachsten ein?“*, sind Sie hier genau richtig. Am Ende haben Sie ein voll funktionsfähiges Skript, das jedes lokal gespeicherte Modell auflistet, fehlende automatisch herunterlädt und Ihnen exakt zeigt, wo die Dateien auf der Festplatte liegen.

---

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.9 oder neuer (die Bibliothek nutzt Typ‑Hints, die einen aktuellen Interpreter erfordern)
- `pip`‑Zugriff, um das **Aspose OCR**‑Paket (`aocr`) zu installieren.  
  ```bash
  pip install aocr
  ```
- Eine Internetverbindung für den ersten Download von Hugging Face.
- Einen Ordner, in dem Sie den Model‑Cache speichern möchten (z. B. `./model_cache`).

Das war’s – keine zusätzlichen Docker‑Container, keine schweren virtuellen Umgebungen über eine saubere Python‑Installation hinaus.

---

## ## Wie man Modelle mit Aspose AI auflistet

Der Kern dieses Leitfadens ist die Fähigkeit, **Modelle** aufzulisten, die Aspose AI lokal gecached hat. Sobald der Cache eingerichtet ist, kann die Bibliothek alles aufzählen, was sie kennt, was Debugging und Versionskontrolle zum Kinderspiel macht.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Warum das funktioniert:**  
- `AsposeAI()` erstellt den High‑Level‑Einstiegspunkt, der mit der zugrunde liegenden Inferenz‑Engine kommuniziert.  
- `AsposeAIModelConfig()` enthält alle einstellbaren Parameter; das Setzen von `allow_auto_download` auf `"true"` weist die Bibliothek an, fehlende Dateien automatisch aus dem angegebenen Repository zu holen.  
- `directory_model_path` ist das *Cache‑Verzeichnis* – der Ort, an dem alle heruntergeladenen Binärdateien liegen.  
- `initialize()` wendet die Konfiguration an und führt den ersten Download aus, falls der Cache leer ist.  
- Schließlich scannt `list_local()` den Cache‑Ordner und gibt eine Python‑Liste von Modell‑Identifikatoren zurück, die wir ausgeben.

### Erwartete Ausgabe (erstes Durchlauf)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Wenn Sie das Skript erneut ausführen, überspringt die Bibliothek den Download und listet einfach das bereits vorhandene Modell auf, was beweist, dass **wie man den Cache setzt** sich bei nachfolgenden Durchläufen auszahlt.

---

## ## Automatisches Herunterladen für fehlende Modelle aktivieren

Oft arbeiten Sie mit mehreren Modellen in verschiedenen Projekten. Das manuelle Herunterladen jedes Modells von Hugging Face kann mühsam sein. Durch das Aktivieren von auto download übernimmt Aspose AI die schwere Arbeit.

```python
cfg.allow_auto_download = "true"
```

> **Profi‑Tipp:** Lassen Sie `allow_auto_download` **nur** in Entwicklungs‑ oder CI‑Umgebungen auf `"true"` gesetzt. In der Produktion sollten Sie den Cache möglicherweise sperren, um unerwarteten Netzwerkverkehr zu vermeiden.

Wenn Sie es später ausschalten wollen, setzen Sie das Flag einfach vor einem erneuten Aufruf von `initialize()` auf `"false"`.

---

## ## Hugging Face Modell on‑the‑fly herunterladen

Die Zeile

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

teilt Aspose AI mit, aus welchem Remote‑Repository es ziehen soll. Die Bibliothek unterstützt jedes öffentliche Modell auf Hugging Face, das eine GGUF‑Datei bereitstellt. Möchten Sie ein anderes Modell? Tauschen Sie die Repo‑ID aus:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Wenn Sie das Skript ausführen, prüft Aspose AI den Cache:

- **Falls das Modell existiert**, wird es sofort geladen.  
- **Falls nicht**, löst das auto‑download‑Flag einen Download aus, speichert die Datei unter `directory_model_path` und registriert sie zur sofortigen Nutzung.

Dieser Ansatz eliminiert den zweistufigen „Download‑dann‑Ausführen“-Prozess, den viele Tutorials verlangen.

---

## ## Wie man Aspose AI nach dem Auflisten des Modells verwendet

Modelle aufzulisten ist nur die halbe Geschichte. Sobald Sie wissen, dass ein Modell vorhanden ist, können Sie mit der Inferenz beginnen:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Warum das wichtig ist:**  
- `run_inference()` abstrahiert Tokenisierung, Batching und GPU‑Handling.  
- Indem Sie den *Modellnamen* übergeben, den Sie von `list_local()` erhalten haben, stellen Sie sicher, dass der Inferenzaufruf exakt die Datei auf der Festplatte verwendet.

---

## ## Cache‑Standort für mehrere Projekte festlegen

Wenn Sie mehrere Projekte jonglieren, möchten Sie vielleicht für jedes einen eigenen Cache‑Ordner haben. Das Feld `directory_model_path` ist einfach ein String, sodass Sie es dynamisch zusammenbauen können:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Jetzt erhält jedes Projekt einen isolierten Unterordner (`./model_cache/sentiment_analysis`), was Versionskonflikte verhindert und das Aufräumen erleichtert.

---

## ## Häufige Fallstricke und wie man sie vermeidet

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| **`PermissionError` beim Zugriff auf den Cache** | Cache‑Ordner gehört einem anderen Benutzer (häufig auf geteilten Servern) | Ordner manuell mit richtigen Berechtigungen erstellen: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Modell erscheint nicht in `list_local()`** | `allow_auto_download` ist auf `"false"` gesetzt und das Modell ist noch nicht gecached | Flag vorübergehend einschalten, einmal ausführen, dann bei Bedarf wieder ausschalten |
| **Unerwartete Modellversion** | Zwei verschiedene Repos teilen denselben Namen, aber unterschiedliche Dateien | Exakte Repo‑ID (inkl. Tag/Commit) festlegen oder den Cache sperren, indem auto‑download nach dem ersten erfolgreichen Pull deaktiviert wird |
| **Out‑of‑memory‑Fehler** | Große GGUF‑Dateien auf einer Maschine ohne ausreichend RAM/VRAM | Ein kleineres Modell verwenden (z. B. `Qwen2.5-1.5B`) oder `cfg.device = "cpu"` setzen, um CPU‑Inference zu erzwingen |

---

## ## Vollständiges Skript zum Kopieren und Einfügen

Unten finden Sie das komplette, sofort ausführbare Beispiel, das alle oben genannten Konzepte integriert. Speichern Sie es als `list_models_demo.py` und führen Sie es mit `python list_models_demo.py` aus.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Das Ausführen** erzeugt eine Ausgabe, die der vorherigen Beispielausgabe ähnelt, gefolgt von einer knappen Antwort des Modells. Ersetzen Sie die Eingabeaufforderung gern durch beliebigen Text – dies ist der schnellste Weg zu prüfen, ob das Modell nach dem **wie man Modelle auflistet** wirklich nutzbar ist.

---

## ## Zusammenfassung

Wir haben alles behandelt, was Sie benötigen, um **Modelle mit Aspose AI aufzulisten**, vom Aktivieren des **auto download** über das Konfigurieren eines persistenten **Caches** bis hin zum Abrufen eines **Hugging Face Modells** bei Bedarf. Die wichtigsten Erkenntnisse:

1. Erstellen Sie ein `AsposeAI`‑Objekt und ein `AsposeAIModelConfig`.  
2. Setzen Sie `allow_auto_download = "true"` und verweisen Sie `directory_model_path` auf einen Ordner Ihrer Wahl.  
3. Initialisieren Sie die KI und rufen Sie `list_local()` auf, um genau zu sehen, was gecached ist.  
4. Verwenden Sie den aufgelisteten Modellnamen für Inferenz – und Sie sind bereit, reale Anwendungen zu bauen.

---

## Was kommt als Nächstes?

- **Experimentieren Sie mit verschiedenen Modellen** – tauschen Sie `cfg.hugging_face_repo_id` gegen ein anderes Repository aus und beobachten Sie, wie sich die Liste ändert.  
- **Cache verfeinern**  

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man OCR‑Bilder stapelt mit List in Aspose.OCR für .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Wie man Aspose OCR Lizenz setzt und in Java verifiziert](/ocr/english/java/ocr-basics/set-license/)
- [Wie man Text aus Bild extrahiert mit Aspose.OCR für .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}