---
category: general
date: 2026-03-26
description: Python OCR का उपयोग करके छवि से तालिकाएँ निकालें और छवि को स्प्रेडशीट
  में बदलें। जानें कि OCR के लिए छवि कैसे लोड करें, तालिकाएँ पढ़ें और तालिका डेटा
  निकालें।
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: hi
og_description: Python OCR के साथ छवि से तालिकाएँ निकालें। यह गाइड दिखाता है कि OCR
  के लिए छवि कैसे लोड करें, तालिकाएँ पढ़ें, और उन्हें स्प्रेडशीट में बदलें।
og_title: इमेज से टेबल निकालें – पूर्ण OCR ट्यूटोरियल
tags:
- OCR
- Python
- Data Extraction
title: छवि से तालिकाएँ निकालें – चरण‑दर‑चरण OCR गाइड
url: /hi/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इमेज से टेबल निकालें – पूर्ण OCR ट्यूटोरियल

क्या आपको कभी **extract tables from image** करने की ज़रूरत पड़ी है लेकिन शुरू कहाँ से करें, यह नहीं पता था? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब PDF या स्क्रीनशॉट में तालिका डेटा होता है जिसे संपादन योग्य पंक्तियों और स्तंभों में बदलना होता है। अच्छी खबर? कुछ पायथन कोड की पंक्तियों को एक मजबूत OCR इंजन के साथ मिलाकर, आप उस चित्र को सेकंडों में एक उपयोगी स्प्रेडशीट में बदल सकते हैं।

इस ट्यूटोरियल में हम OCR के लिए इमेज लोड करने, पहचान इंजन चलाने, और प्रत्येक टेबल को पंक्ति दर पंक्ति निकालने की प्रक्रिया देखेंगे। अंत तक आप **convert image to spreadsheet** करने में सक्षम होंगे, और आप यह भी देखेंगे कि **ocr read tables** और **ocr extract table data** कैसे किया जाता है आगे की प्रोसेसिंग के लिए। कोई छिपा जादू नहीं, बस स्पष्ट, चलाने योग्य कोड जो आप आज ही अपने प्रोजेक्ट में जोड़ सकते हैं।

---

## आप क्या चाहिए

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित उपलब्ध हैं:

- **Python 3.9+** – नवीनतम स्थिर रिलीज़ सबसे अच्छा काम करता है।
- The **`ocr`** लाइब्रेरी (या कोई भी संगत OCR SDK जो `OcrEngine`, `Image`, और टेबल‑संबंधित मेथड्स प्रदान करता हो)। इसे `pip install ocr‑sdk` से इंस्टॉल करें (वास्तविक पैकेज नाम से बदलें)।
- एक इमेज फ़ाइल (`.png`, `.jpg`, आदि) जिसमें स्पष्ट रूप से प्रिंटेड टेबल हो।  
- वैकल्पिक: **pandas** यदि आप निकाले गए डेटा को सीधे CSV या Excel फ़ाइल में लिखना चाहते हैं (`pip install pandas`)।

सब कुछ तैयार है? बढ़िया—चलें शुरू करते हैं।

---

## चरण 1: OCR SDK को इम्पोर्ट करें और अपना वातावरण तैयार करें

सबसे पहले: हमें OCR क्लासेज़ को अपने स्क्रिप्ट में लाना है और एक छोटा हेल्पर सेट अप करना है जो बाद में कच्चे टेबल डेटा को DataFrame में बदल देगा।

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Why this matters:** `ocr` को इम्पोर्ट करने से हमें `OcrEngine`, `Imaging.Image`, और उन टेबल ऑब्जेक्ट्स तक पहुंच मिलती है जिनपर हम इटररेट करेंगे। `pandas` एक्सट्रैक्शन के लिए आवश्यक नहीं है, लेकिन यह “convert image to spreadsheet” भाग को सरल बनाता है।

---

## चरण 2: वह इमेज लोड करें जिसे आप प्रोसेस करना चाहते हैं

अब हम वास्तव में **load image for OCR** करेंगे। SDK एक `Image` ऑब्जेक्ट की अपेक्षा करता है, इसलिए हम अपने फ़ाइल पाथ को हेल्पर मेथड `Image.load()` से रैप करेंगे।

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tip:** अपनी इमेज फ़ाइलें एक समर्पित फ़ोल्डर (`assets/` या `data/`) में रखें और रिलेटिव पाथ्स का उपयोग करें। इससे स्क्रिप्ट विभिन्न मशीनों पर पोर्टेबल रहती है।

---

## चरण 3: पहचान प्रक्रिया चलाएँ

इमेज अटैच होने के बाद, हम अंततः इंजन को **ocr read tables** बता सकते हैं। `recognize()` कॉल एक रिज़ल्ट ऑब्जेक्ट लौटाता है जिसमें इंजन द्वारा खोजी गई सभी चीज़ें होती हैं—टेक्स्ट ब्लॉक्स, लाइन्स, और हमारे लिए सबसे महत्वपूर्ण, टेबल्स।

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Why we check:** कुछ इमेज में शोर हो सकता है या टेबल की बॉर्डर धुंधली हो सकती है, जिससे इंजन उन्हें मिस कर सकता है। एक वार्निंग लॉग करने से आपको शुरुआती फीडबैक मिलती है बिना स्क्रिप्ट को तोड़े।

---

## चरण 4: प्रत्येक टेबल की पंक्तियों और कोशिकाओं को निकालें

यहीं पर असली जादू होता है। हम प्रत्येक डिटेक्टेड टेबल पर इटररेट करेंगे, प्रत्येक पंक्ति निकालेंगे, फिर प्रत्येक सेल का टेक्स्ट। अंदरूनी लिस्ट कॉम्प्रिहेंशन कोड को संक्षिप्त बनाता है, फिर भी हम प्रवाह को समझाएंगे।

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**क्या हो रहा है?**  

- `enumerate(..., start=1)` लॉगिंग के लिए हमें एक उपयोगी टेबल नंबर देता है।  
- `row_obj.get_cells()` प्रत्येक सेल ऑब्जेक्ट लौटाता है; `cell.get_text()` OCR‑डिकोडेड स्ट्रिंग प्राप्त करता है।  
- हम पंक्तियों को `rows_data` में स्टोर करते हैं, फिर उन्हें `pandas.DataFrame` को देते हैं जो स्वचालित रूप से कॉलम्स को एलाइन करता है।  
- `print` ब्लॉक मूल स्निपेट में दिखाए गए **essential output** को प्रतिबिंबित करता है, ताकि आप तुरंत परिणाम सत्यापित कर सकें।

**Edge case handling:** यदि किसी पंक्ति में अन्य पंक्तियों की तुलना में अलग संख्या में सेल्स हैं, तो `pandas` गायब स्थानों को `NaN` से भर देगा। यदि आप खाली स्ट्रिंग्स पसंद करते हैं तो बाद में `df.fillna('')` से DataFrame को साफ़ कर सकते हैं।

---

## चरण 5: निकाली गई टेबल्स को स्प्रेडशीट में सहेजें

अब जब हमारे पास DataFrames की लिस्ट है, उन्हें Excel वर्कबुक (या CSV फ़ाइलों) में बदलना बहुत आसान है। यह “convert image to spreadsheet” लक्ष्य को पूरा करता है।

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Why Excel?** अधिकांश बिज़नेस यूज़र्स `.xlsx` को पसंद करते हैं। यदि आप CSV पसंद करते हैं, तो लूप को `df.to_csv(f"table_{idx}.csv", index=False)` से बदल दें।

---

## पूर्ण, तैयार‑चलाने‑योग्य स्क्रिप्ट

सब कुछ मिलाकर, यहाँ पूरा प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं।

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Expected console output** (मान लेते हैं कि एक सरल 2×3 टेबल है):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

और आपको स्क्रिप्ट फ़ोल्डर में `extracted_tables.xlsx` मिलेगा, प्रत्येक टेबल अपने अलग शीट पर होगी।

---

## अक्सर पूछे जाने वाले प्रश्न और सुझाव

| Question | Answer |
|----------|--------|
| **क्या मैं कोई अलग OCR लाइब्रेरी उपयोग कर सकता हूँ?** | बिल्कुल। पैटर्न वही रहता है: इमेज लोड करें → पहचान करें → `get_tables()` पर इटररेट करें। केवल इम्पोर्ट और ऑब्जेक्ट नाम बदलें। |
| **अगर मेरी इमेज शोरयुक्त है तो क्या करें?** | OCR इंजन को फीड करने से पहले OpenCV (थ्रेशहोल्डिंग, डेस्क्यू) के साथ प्री‑प्रोसेस करें। शोर कम करने से अक्सर **ocr extract table data** की सटीकता बढ़ती है। |
| **क्या मुझे `openpyxl` इंस्टॉल करना चाहिए?** | हां, `pandas` एक्सेल आउटपुट के लिए इसे बैकएंड में उपयोग करता है। `pip install openpyxl` से इंस्टॉल करें। |
| **मैं मर्ज्ड सेल्स को कैसे हैंडल करूँ?** | कुछ SDKs `cell.is_merged()` प्रदान करते हैं; आप इसे मैन्युअली डिटेक्ट करके मर्ज्ड रेंज में वैल्यू को फैलाने के लिए उपयोग कर सकते हैं। |
| **क्या केवल विशिष्ट टेबल्स को निकालने का कोई तरीका है?** | `table_obj.get_confidence()` से फ़िल्टर करें या प्रोसेसिंग से पहले हेडर कीवर्ड्स चेक करके फ़िल्टर करें। |

---

## समापन

अब आपके पास **extract tables from image** के लिए एक पूर्ण, एंड‑टू‑एंड समाधान है, परिणाम को एक साफ़ स्प्रेडशीट में बदलें, और एक ही चित्र में कई टेबल्स को भी हैंडल करें। यह स्क्रिप्ट दिखाती है कि कैसे **load image for OCR**, **ocr read tables**, और **ocr extract table data** किया जाता है, जबकि वास्तविक दुनिया के विविधताओं के लिए पर्याप्त लचीला रहता है।

अगला क्या? OCR इंजन को एक PDF पेज इमेज के रूप में फीड करने की कोशिश करें, या विभिन्न भाषाओं और फ़ॉन्ट्स के साथ प्रयोग करें। आप DataFrames को सीधे डेटाबेस या रिपोर्टिंग टूल में भी पाइप कर सकते हैं—आपकी कल्पना ही सीमा है।

यदि आपको यह गाइड उपयोगी लगा, तो इसे साझा करने, SDK वाले रिपॉज़िटरी को स्टार देने, या अपने ट्रिक्स के साथ टिप्पणी छोड़ने में संकोच न करें। कोडिंग का आनंद लें, और आपकी टेबल्स हमेशा सही ढंग से पार्स हों!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}