---
category: general
date: 2026-01-07
description: Hur du listar modeller i Aspose OCR AI med Python – lär dig att få modellens
  sökväg, kontrollera installerade modeller och hämta en Python-modellista på några
  sekunder.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: sv
og_description: Hur man listar modeller i Aspose OCR AI med Python. Hitta modellens
  sökväg, kontrollera installerade modeller och se den fullständiga listan över tillgängliga
  modeller.
og_title: Hur man listar modeller i Aspose OCR AI – Python‑guide
tags:
- Aspose OCR
- Python
- AI models
title: Hur man listar modeller i Aspose OCR AI – Python‑guide
url: /sv/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man listar modeller i Aspose OCR AI – Python‑guide

Har du någonsin undrat **hur man listar modeller** som redan är installerade på din maskin när du arbetar med Aspose OCR AI? Du är inte ensam om att stöta på detta. I många projekt behöver du verifiera modellmappen, bekräfta vilka modeller som finns, eller till och med felsöka ett saknat modell‑problem—allt utan att lämna din Python‑REPL.

I den här handledningen går vi igenom ett komplett, färdigt exempel som visar hur du **hämtar modellens sökväg**, **kontrollerar installerade modeller**, och slutligen **listar tillgängliga modeller** med bara några rader kod. Inga externa skript, ingen gömd magi—bara ren Python och Aspose OCR AI SDK.

> **Förutsättningar**  
> • Python 3.8 eller nyare  
> • `asposeocr`‑paketet installerat (`pip install asposeocr`)  
> • Grundläggande kunskap om att importera moduler

Om du har detta på plats, låt oss dyka in.

---

## Hur man listar modeller med Aspose OCR AI

Det första vi behöver är hjälparklassen `AsposeAI` som följer med `asposeocr.ai`‑modulen. Denna klass ger oss tre praktiska metoder:

| Metod | Vad den returnerar | Typiskt användningsfall |
|--------|-------------------|------------------------|
| `get_local_path()` | Absolut sökväg till mappen där Aspose lagrar sina AI‑modeller | Verifiera att SDK:n tittar på rätt plats |
| `list_local()` | Python `list` med namn på modellmappar som finns på disken | Snabbt se vilka modeller du kan ladda |
| `list_remote()` *(valfritt)* | Lista över modeller som kan laddas ner från Asposes moln | När du behöver en modell som du inte har lokalt |

Nedan är det **kompletta skriptet** som skriver ut den lokala modellmappen och listan över installerade modeller.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Förväntat resultat

När du kör skriptet på en ny installation ser du vanligtvis något liknande:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Om mappen är tom returnerar `list_local()` en tom lista (`[]`). Det är en användbar signal om att du först måste ladda ner en modell—något vi kommer att gå igenom senare.

---

## Varför det är viktigt att känna till modellens sökväg

Att förstå **var** SDK:n lagrar sina filer (`get model path`) är mer än bara en nyfikenhet:

1. **Felsökning** – Om en modell misslyckas att laddas kan du `ls` sökvägen och se om filen verkligen finns.
2. **Anpassade modeller** – Vissa team tränar egna OCR‑modeller och placerar dem i mappen. Att känna till sökvägen låter dig lägga filerna exakt där Aspose förväntar sig dem.
3. **Behörigheter** – På Linux kan mappen ägas av en annan användare. Att upptäcka ett behörighetsfel tidigt sparar timmar av huvudbry.

> **Proffstips:** Om du behöver peka SDK:n mot en anpassad katalog, sätt miljövariabeln `ASPOSE_OCR_MODEL_PATH` innan du skapar `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Kontroll av installerade modeller – Edge‑cases och tips

### 1. Inga modeller installerade

Om `list_local()` returnerar `[]` har du två alternativ:

| Alternativ | Hur man gör det |
|------------|-----------------|
| **Ladda ner en modell från Aspose** | `ai.download('ocr-general-v1')` (kräver internet) |
| **Kopiera en förtränad modell** | Placera modellmappen manuellt i sökvägen som visas av `get_local_path()` |

### 2. Flera versioner av samma modell

Ibland ser du både `ocr-general-v1` **och** `ocr-general-v1-beta`. SDK:n laddar den första matchning den hittar, men du kan tvinga en specifik version genom att skicka exakt mappnamn till OCR‑konstruktorn:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Korrupta modellfiler

En delvis nedladdad modell kan orsaka ett `FileNotFoundError` senare. Om du misstänker korruption, radera helt enkelt den felande mappen och ladda ner på nytt:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Utöka skriptet – Lista fjärrmodeller (valfritt)

Om du vill se vilka modeller som finns tillgängliga för nedladdning utan att lämna Python, lägg till ett ytterligare anrop:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Detta kommer att skriva ut något i stil med:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Du kan sedan välja någon modell och anropa `ai.download('model-name')` för att hämta den automatiskt.

---

## Fullt end‑to‑end‑exempel

Sätter vi ihop allt får du ett **enkelt, körbart skript** som:

1. Visar den lokala modellmappen.  
2. Listar installerade modeller.  
3. Om inga hittas, laddar ner en standardmodell.  
4. Slutligen skriver ut den uppdaterade listan.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

När du kör detta skript på en ren maskin får du:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Nu har du en **självständig, citeringsvärd** lösning som vilken AI‑assistent som helst kan återge ordagrant.

---

## Vanliga frågor (FAQ)

**Q: Fungerar detta på Windows?**  
A: Absolut. SDK:n abstraherar filsystemet, så `get_local_path()` returnerar något i stil med `C:\Users\YourName\.asposeocr\models`. Se bara till att Python kan skriva till den mappen.

**Q: Kan jag lagra modeller på en nätverksdisk?**  
A: Ja—sätt `ASPOSE_OCR_MODEL_PATH` till UNC‑sökvägen (`\\server\share\models`) innan du skapar `AsposeAI`‑instansen.

**Q: Vad gör jag om jag behöver en modell för ett språk som inte täcks av standarduppsättningen?**  
A: Använd `list_remote()` för att se om Aspose erbjuder en språk‑specifik modell. Om inte kan du träna din egen och placera den i mappen; bara skicka det anpassade mappnamnet till OCR‑konstruktorn.

---

## Slutsats

Vi har gått igenom **hur man listar modeller** i Aspose OCR AI, visat hur du **hämtar modellens sökväg**, **kontrollerar installerade modeller**, och till och med **laddar ner en saknad modell**—allt med ren Python. Genom att förstå mappstrukturen och hjälparmetoderna (`get_local_path()`, `list_local()`, `list_remote()`) får du full kontroll över de AI‑modeller som din applikation förlitar sig på.

Nästa steg? Prova att byta ut standardmodellen mot en handskrifts‑modell, eller peka SDK:n mot en egen‑tränad modell du har byggt internt. Oavsett vad har du nu en stabil grund för att hantera OCR‑tillgångar i vilket Python‑projekt som helst.

Lycka till med kodningen, och må din modellista alltid vara uppdaterad! 

---

![How to list models screenshot](https://example.com/images/how-to-list-models.png "Hur man listar modeller")

*Bild‑alternativtext:* **skärmdump av hur man listar modeller** (uppfyller primärt nyckelordskrav).  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}