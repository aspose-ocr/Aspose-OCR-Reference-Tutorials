---
category: general
date: 2026-06-22
description: Erstelle durchsuchbare PDFs in Python mit OCR – lerne, wie du ein Bild
  in PDF umwandelst, Text in PDFs erkennst und deinen Arbeitsablauf automatisierst.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: de
og_description: Erstelle durchsuchbare PDFs in Python mit OCR. Folge diesem Schritt‑für‑Schritt‑Tutorial,
  um ein Bild in ein PDF zu konvertieren, Text im PDF zu erkennen und die Dokumentenverarbeitung
  zu automatisieren.
og_title: Durchsuchbares PDF in Python erstellen – Vollständiger OCR-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Durchsuchbare PDF in Python erstellen – Vollständiger OCR-Leitfaden
url: /de/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbare PDF in Python erstellen – Vollständiger OCR-Leitfaden

Haben Sie jemals **create searchable PDF** aus einem gescannten Vertrag erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an dieselbe Grenze, wenn sie versuchen, ein Bitmap‑Bild in ein text‑durchsuchbares Dokument zu verwandeln. Die gute Nachricht: Mit einem kleinen Python‑Skript können Sie **convert image to PDF**, die OCR‑Engine jedes Wort erkennen lassen und erhalten Sie eine perfekt durchsuchbare Datei.

In diesem Tutorial führen wir Sie durch den gesamten Prozess, von der Installation der richtigen Bibliothek bis zum Umgang mit Sonderfällen wie mehrseitigen Dokumenten. Am Ende können Sie **ocr image to pdf**, **recognize text pdf** durchführen und den Workflow in größere Automatisierungspipelines integrieren.

## Was Sie benötigen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes auf Ihrem Rechner haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.8 oder neuer | Moderne Syntax und bessere Typ‑Hinweise |
| `ocr` Python package (or any compatible OCR SDK) | Stellt `OcrEngine`, `ImageStream` und PDF‑Ausgabe bereit |
| Ein gescanntes Bild (JPEG, PNG oder TIFF) | Die Quelle, die Sie konvertieren werden |
| Schreibzugriff auf einen Ordner für das Ausgabe‑PDF | Damit Sie die erzeugte Datei speichern können |

Wenn Sie das SDK noch nicht installiert haben, führen Sie aus:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv .venv`), um Abhängigkeiten übersichtlich zu halten.

## Überblick über den Workflow

1. **Create an OCR engine instance** – das Gehirn hinter der Erkennung.  
2. **Load the image** you want to process. – Laden Sie das Bild, das Sie verarbeiten möchten.  
3. **Configure the engine** to emit a searchable PDF rather than plain text. – Konfigurieren Sie die Engine, um ein durchsuchbares PDF anstelle von Klartext auszugeben.  
4. **Prepare an in‑memory stream** that will hold the PDF bytes. – Bereiten Sie einen In‑Memory‑Stream vor, der die PDF‑Bytes hält.  
5. **Run the recognition** – the engine reads the image, extracts text, and writes the PDF. – Führen Sie die Erkennung aus – die Engine liest das Bild, extrahiert Text und schreibt das PDF.  
6. **Persist the PDF to disk** so you can open it in any viewer. – Speichern Sie das PDF auf der Festplatte, damit Sie es in jedem Viewer öffnen können.

Das ist die ganze Geschichte in sechs Code‑Zeilen. Lassen Sie uns jeden Schritt im Detail betrachten.

---

## Durchsuchbare PDF erstellen – Schritt‑für‑Schritt Python OCR‑Tutorial

### Schritt 1: OCR‑Engine initialisieren

Das Erste, was Sie tun, ist ein `OcrEngine`‑Objekt zu erstellen. Stellen Sie sich das vor wie das Einschalten eines Scanners, der bereit ist, Ihr Bild zu lesen.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Warum das wichtig ist:** Das Instanziieren der Engine reserviert interne Puffer und lädt Sprachdaten. Wenn Sie diesen Schritt überspringen, führt das später zu einem `NoneType`‑Fehler, wenn Sie versuchen, das Bild zu setzen.

### Schritt 2: Das Bild laden, das Sie konvertieren möchten

Als Nächstes übergeben wir der Engine einen Bild‑Stream. Der Helfer `ImageStream.from_file` liest die Datei und verpackt sie in ein Format, das die OCR‑Engine versteht.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Sonderfall:** Wenn Ihre Quelle ein mehrseitiges TIFF ist, verwenden Sie stattdessen `ocr.MultiPageImageStream.from_file`. Die Engine behandelt jede Seite automatisch als separate PDF‑Seite.

### Schritt 3: Der Engine mitteilen, ein durchsuchbares PDF auszugeben

Standardmäßig geben viele OCR‑SDKs Klartext aus. Wir müssen das Ausgabeformat auf PDF umstellen, damit die resultierende Datei sowohl visuell als auch durchsuchbar ist.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **Was passiert im Hintergrund?** Die Engine bettet nun eine unsichtbare Textebene hinter das Bitmap ein, sodass Sie nach Wörtern suchen können, genau wie in einem nativen PDF.

### Schritt 4: Einen In‑Memory‑Stream für die PDF‑Daten vorbereiten

Anstatt direkt auf die Festplatte zu schreiben, erfassen wir das PDF in einem `MemoryStream`. Das hält die I/O schnell und ermöglicht es Ihnen, die Bytes bei Bedarf woanders hinzuleiten (z. B. Upload zu S3).

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Schritt 5: Die Erkennung ausführen und das PDF schreiben

Jetzt wird die schwere Arbeit erledigt. Der Aufruf `recognize` liest das Bild, führt OCR aus und streamt das durchsuchbare PDF in `pdf_stream`.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Häufiges Problem:** Wenn Sie vergessen, `engine.recognize` aufzurufen, bleibt `pdf_stream` leer und ein Versuch, es zu speichern, löst einen `ValueError` aus. Überprüfen Sie immer `pdf_stream.length`, falls Sie verifizieren müssen, dass Daten erzeugt wurden.

### Schritt 6: Das erzeugte PDF in einer Datei speichern

Abschließend schreiben wir die Bytes aus dem Memory‑Stream auf die Festplatte. Die resultierende Datei kann in Adobe Reader, Preview oder jedem PDF‑Viewer mit Volltextsuche geöffnet werden.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Ergebnis, das Sie sehen werden:** Öffnen Sie das PDF, drücken Sie `Ctrl+F`, geben Sie ein Wort ein, das im Original‑Scan vorkommt, und beobachten Sie, wie der Viewer es sofort hervorhebt. Das ist das Kennzeichen eines **searchable PDF**.

## Bild in PDF konvertieren – Einstellungen für beste Ergebnisse anpassen

Wenn Ihr Hauptziel einfach **convert image to PDF** ohne OCR ist, können Sie Schritt 3 überspringen und das Ausgabeformat auf `ocr.OutputFormat.IMAGE_PDF` setzen. Die Engine bettet das Bitmap als PDF‑Seite ein, ohne eine versteckte Textebene.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Verwenden Sie diesen Modus, wenn Sie eine getreue visuelle Kopie benötigen, aber die Durchsuchbarkeit egal ist – beispielsweise für Archivierungszwecke, bei denen OCR nicht erforderlich ist.

## Text‑PDF erkennen – Sprachpakete hinzufügen und DPI steuern

Für ein robustes **recognize text PDF**‑Erlebnis sollten Sie die folgenden optionalen Anpassungen in Betracht ziehen:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Warum DPI anpassen?** Eine höhere Auflösung liefert der OCR‑Engine mehr Pixel zum Analysieren, wodurch Fehlinterpretationen bei Scans niedriger Qualität reduziert werden.

## Python OCR PDF – Integration in größere Pipelines

Jetzt, da Sie **python ocr pdf** in wenigen Zeilen ausführen können, stellen Sie sich vor, diese Logik in eine Flask‑API einzubetten:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Dieser kleine Endpunkt ermöglicht es einem Client, ein Bild per POST zu senden und sofort ein **searchable PDF** zu erhalten – perfekt für SaaS‑Dokumentenverarbeitungsdienste.

## Häufige Fallstricke bei **ocr image to pdf**

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Leere PDF‑Seiten | Bild nicht geladen (`engine.set_image` mit falschem Pfad aufgerufen) | Pfad überprüfen und `os.path.abspath` verwenden |
| Kein durchsuchbarer Text | Ausgabeformat ist noch auf `IMAGE_PDF` eingestellt | Rufen Sie explizit `set_output_format(ocr.OutputFormat.PDF)` auf |
| Verzerrte Zeichen | Falsches Sprachpaket | Laden Sie die korrekte Sprache mit `settings.set_language("eng")` |
| Langsame Verarbeitung bei großen Dateien | Verwendung der Standard‑DPI (72) bei hochauflösenden Bildern | DPI auf 300 erhöhen oder Seiten einzeln stapelweise verarbeiten |

## Vollständiges, ausführbares Beispiel (zum Kopieren‑Einfügen bereit)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Führen Sie das Skript aus, öffnen Sie das erzeugte PDF und versuchen Sie, nach einem Wort zu suchen, von dem Sie wissen, dass es im Original‑Scan vorkommt. Wenn alles reibungslos funktioniert hat, haben Sie gerade **create searchable pdf** mit Python gemeistert.

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **create searchable PDF**‑Dateien mit einer Python‑OCR‑Bibliothek zu erstellen: die Engine initialisieren, ein Bild laden, die PDF‑Ausgabe konfigurieren, das Ergebnis streamen und schließlich auf die Festplatte speichern. Sie haben auch gesehen, wie man **convert image to PDF** verwendet und die Feinabstimmung von **

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [PDF‑Text erkennen – OCR‑Operationen mit Aspose.OCR für Java](/ocr/english/java/ocr-operations/)
- [Wie man PDF in .NET mit Aspose.OCR OCR‑t](/ocr/english/net/text-recognition/recognize-pdf/)
- [Bilder zu PDF in C# konvertieren – Mehrseitiges OCR‑Ergebnis speichern](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}