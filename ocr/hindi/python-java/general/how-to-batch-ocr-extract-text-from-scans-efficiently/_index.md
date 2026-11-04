---
category: general
date: 2026-04-26
description: Python में अपने दस्तावेज़ों को बैच OCR करके स्कैन से टेक्स्ट निकालना
  सीखें। JSON आउटपुट के लिए OcrEngine के साथ चरण‑दर‑चरण बैच प्रोसेसिंग जानें।
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: hi
og_description: कैसे एक ही स्क्रिप्ट में अपने स्कैन किए गए फ़ाइलों को बैच OCR करके
  स्कैन से टेक्स्ट निकालें। पूर्ण कोड, टिप्स और किनारी मामलों का समाधान।
og_title: बैच OCR कैसे करें – तेज़ पायथन गाइड
tags:
- OCR
- Python
- Automation
title: बैच OCR कैसे करें – स्कैन से टेक्स्ट को कुशलता से निकालें
url: /hi/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कैसे बैच OCR करें – स्कैन से टेक्स्ट को प्रभावी ढंग से निकालें

क्या आपने कभी सोचा है **कैसे बैच OCR** करके बड़ी मात्रा में स्कैन किए गए PDF को बिना पागल हुए निकालें? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते हैं, *“एक ही बार में स्कैन से टेक्स्ट कैसे निकालें?”* अच्छी खबर यह है कि कुछ पंक्तियों का Python कोड इस थकाऊ काम को एक सुगम, स्वचालित पाइपलाइन में बदल सकता है।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य समाधान से गुजरेंगे जो **स्कैन से टेक्स्ट निकालता है**, परिणामों को JSON के रूप में सहेजता है, और अंत में एक त्वरित sanity check देता है। कोई बाहरी सेवा नहीं, कोई जादू नहीं—सिर्फ साधारण Python, `OcrEngine` क्लास, और थोड़ा फ़ोल्डर प्लंबिंग।

## आप क्या सीखेंगे

- एक पूरी तरह कार्यशील स्क्रिप्ट जो **बैच OCR** को किसी भी इमेज फ़ोल्डर पर चलाती है।
- प्रत्येक पंक्ति के *क्यों* मौजूद है, न कि केवल *क्या* करता है, की स्पष्ट व्याख्याएँ।
- खाली फ़ोल्डर, गैर‑इमेज फ़ाइलें, और बड़े बैच को संभालने के टिप्स।
- यह सत्यापित करने का तरीका कि JSON आउटपुट में वास्तव में निकाला गया टेक्स्ट है।

### पूर्वापेक्षाएँ (बुनियादी न्यूनतम)

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | आधुनिक सिंटैक्स और टाइप हिंट्स |
| `OcrEngine` लाइब्रेरी (या संगत रैपर) | मुख्य OCR कार्यक्षमता |
| स्कैन की गई इमेज फ़ाइलों (PNG, JPG, TIFF) वाला डायरेक्टरी | इनपुट डेटा |
| आउटपुट फ़ोल्डर के लिए लिखने की अनुमति | JSON परिणाम सहेजना |

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

![how to batch OCR workflow](image-placeholder.png){alt="बैच OCR कैसे करें कार्यप्रवाह"}

## चरण 1 – OCR इंजन को इनिशियलाइज़ करें (how to batch OCR)

किसी भी चीज़ को प्रोसेस करने से पहले, हमें OCR इंजन का एक इंस्टेंस चाहिए। इसे वह “दिमाग” समझें जो प्रत्येक इमेज को पढ़ेगा और टेक्स्ट निकालेगा। इसे एक बार इनिशियलाइज़ करके पूरे बैच में पुनः उपयोग करना सबसे कुशल पैटर्न है।

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **एक ही इंस्टेंस को पुनः उपयोग क्यों करें?**  
> हर फ़ाइल के लिए नया इंजन बनाना भारी मॉडल को मेमोरी में बार‑बार लोड करेगा, जिससे बैच काफी धीमा हो जाएगा। एक ही इंस्टेंस मॉडल को RAM में रखता है और आप हजारों इमेज को बिना noticeable slowdown के प्रोसेस कर सकते हैं।

## चरण 2 – अपने स्कैन फ़ोल्डर की ओर इशारा करें (extract text from scans)

आपके स्कैन डिस्क पर कहीं मौजूद हैं। स्क्रिप्ट को बताइए कि उन्हें कहाँ ढूँढना है। एब्सोल्यूट पाथ का उपयोग करने से “फ़ाइल नहीं मिली” जैसी आश्चर्यजनक समस्याएँ नहीं आतीं, भले ही स्क्रिप्ट किसी अलग वर्किंग डायरेक्टरी से चलायी जाए।

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **प्रो टिप:**  
> यदि आप Windows पर हैं, तो फॉरवर्ड स्लैश (`/`) `os.path.abspath` के साथ बिल्कुल ठीक काम करते हैं, इसलिए आपको बैकस्लैश एस्केप करने की ज़रूरत नहीं है।

## चरण 3 – JSON परिणामों के लिए गंतव्य चुनें

संभवतः आप OCR परिणामों के लिए एक साफ़ फ़ोल्डर चाहते हैं। आउटपुट को स्रोत से अलग रखने से बाद में साफ‑सफ़ाई आसान हो जाती है या JSON को किसी अन्य पाइपलाइन में फीड किया जा सकता है।

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **फ़ोल्डर को प्रोग्रामेटिकली क्यों बनाएं?**  
> यह सुनिश्चित करता है कि यदि डायरेक्टरी मौजूद नहीं है तो स्क्रिप्ट क्रैश न हो, और `exist_ok=True` ऑपरेशन को idempotent बनाता है—स्क्रिप्ट को कई बार चलाने पर भी त्रुटि नहीं आती।

## चरण 4 – बैच प्रोसेस चलाएँ (how to batch OCR)

अब मुख्य भाग: `ocr_engine` को बताना कि वह `input_dir` में हर फ़ाइल पर जाए, OCR चलाए, और JSON को `output_dir` में डंप करे। `format="json"` फ़्लैग इंजन को परिणाम को एक संरचित तरीके से सीरियलाइज़ करने को कहता है, जिसे डाउनस्ट्रीम टूल्स पसंद करते हैं।

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### पर्दे के पीछे क्या हो रहा है?

1. **फ़ाइल खोज** – इंजन `input_folder` को रीकर्सिवली स्कैन करता है, हिडन फ़ाइलों को छोड़ता है।  
2. **फ़ाइल वैलिडेशन** – केवल समर्थित इमेज एक्सटेंशन (`.png`, `.jpg`, `.tif`, आदि) को OCR मॉडल को भेजा जाता है।  
3. **OCR निष्पादन** – प्रत्येक इमेज को OCR इंजन को भेजा जाता है; टेक्स्ट, confidence स्कोर, और लेआउट डेटा कैप्चर होते हैं।  
4. **JSON सीरियलाइज़ेशन** – परिणाम को उसी बेस नेम लेकिन `.json` एक्सटेंशन के साथ `output_folder` में लिखा जाता है।

> **एज केस हैंडलिंग:**  
> - **खाली फ़ोल्डर:** इंजन “No files found” लॉग करता है और सुगमता से रिटर्न करता है।  
> - **करप्ट इमेज:** फ़ाइल को स्किप करता है, `batch_errors.log` में एक एरर एंट्री रिकॉर्ड करता है, और आगे बढ़ता है।  
> - **बड़ा बैच (10k+ फ़ाइलें):** मेमोरी उपयोग कम रहता है क्योंकि प्रत्येक इमेज को स्वतंत्र रूप से प्रोसेस किया जाता है।

## चरण 5 – रूपांतरण समाप्ति की पुष्टि करें

एक साधारण `print` स्टेटमेंट कंसोल में तुरंत फीडबैक देता है। प्रोडक्शन पाइपलाइन में आप इसे लॉगिंग कॉल या ईमेल नोटिफिकेशन से बदल सकते हैं।

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

जब आप वह लाइन देखते हैं, तो आप सुरक्षित रूप से `json_output` फ़ोल्डर को देख सकते हैं। प्रत्येक JSON फ़ाइल लगभग इस तरह दिखेगी:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

अब आप इन JSON फ़ाइलों को डेटाबेस, सर्च इंडेक्स, या किसी भी डाउनस्ट्रीम एनालिटिक्स टूल में फीड कर सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न (और त्वरित उत्तर)

**प्रश्न: अगर मुझे इमेज के बजाय PDF प्रोसेस करने हैं तो क्या करें?**  
उत्तर: पहले प्रत्येक PDF पेज को इमेज में बदलें (जैसे `pdf2image` का उपयोग करके) और उत्पन्न PNG/JPG फ़ाइलों को `input_dir` में रखें। बैच OCR लॉजिक वही रहता है।

**प्रश्न: क्या मैं आउटपुट फ़ॉर्मेट को प्लेन टेक्स्ट में बदल सकता हूँ?**  
उत्तर: बिल्कुल। `format="json"` को `format="txt"` से बदलें और इंजन केवल निकाले गए टेक्स्ट वाला `.txt` फ़ाइल लिखेगा।

**प्रश्न: मेरे स्कैन कई सब‑फ़ोल्डरों में हैं—क्या स्क्रिप्ट रीकर्स करेगा?**  
उत्तर: हाँ। `batch_process` डिफ़ॉल्ट रूप से डायरेक्टरी ट्री को वॉक करता है। अगर आप फ्लैट आउटपुट चाहते हैं, तो `flatten=True` सेट करें (यदि लाइब्रेरी सपोर्ट करती है) या JSON फ़ाइल नामों को पोस्ट‑प्रोसेस करें।

**प्रश्न: मैं गैर‑लैटिन स्क्रिप्ट्स को कैसे हैंडल करूँ?**  
उत्तर: `OcrEngine` को भाषा पैरामीटर के साथ इनिशियलाइज़ करें, जैसे `OcrEngine(lang="spa+eng")`। बैच लूप को कोई बदलाव नहीं चाहिए।

## प्रो टिप्स & सामान्य जाल

- **बैच साइज महत्वपूर्ण है:** अगर आपको CPU स्पाइक्स दिखें, तो फ़ाइलों के बीच `time.sleep(0.1)` जोड़कर प्रोसेस को थ्रॉटल करें।  
- **लॉगिंग:** `print` कॉल को Python के `logging` मॉड्यूल से बदलें ताकि टाइमस्टैम्प और एरर लेवल कैप्चर हो सके।  
- **फ़ाइल नाम टकराव:** अगर दो स्कैन का बेस नेम समान है लेकिन अलग‑अलग सब‑फ़ोल्डर में हैं, तो JSON फ़ाइलें एक‑दूसरे को ओवरराइट कर देंगी। आउटपुट नेम में रिलेटिव पाथ का हैश जोड़ें ताकि टकराव न हो।  
- **मेमोरी लीक:** कुछ OCR बैक‑एंड नेटिव रिसोर्सेज़ को पकड़ कर रखते हैं। यदि लाइब्रेरी क्लीन‑अप मेथड देती है तो स्क्रिप्ट के अंत में `ocr_engine.close()` कॉल करें।

## पूर्ण स्क्रिप्ट – कॉपी & पेस्ट के लिए तैयार

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**अपेक्षित कंसोल आउटपुट**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

आप किसी भी फ़ाइल को `json_output` में टेक्स्ट एडिटर से खोलकर या Python में लोड करके JSON की पुष्टि कर सकते हैं:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

आपको कंसोल में कच्चा OCR‑निकाला गया टेक्स्ट प्रिंट हुआ दिखेगा।

## निष्कर्ष

हमने अभी **कैसे बैच OCR** करके स्कैन की गई इमेज की पूरी डायरेक्टरी को प्रोसेस किया और **स्कैन से टेक्स्ट** को साफ़, मशीन‑रीडेबल JSON फ़ाइलों में निकाला। यह तरीका जानबूझकर सरल है: इंजन को एक बार सेट‑अप करें, फ़ोल्डर की ओर इशारा करें, और लाइब्रेरी को भारी काम करने दें। अब आप आगे कर सकते हैं:

- JSON को प्लग‑इन करें

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}