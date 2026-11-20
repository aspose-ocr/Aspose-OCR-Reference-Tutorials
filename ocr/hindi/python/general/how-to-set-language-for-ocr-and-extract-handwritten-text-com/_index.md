---
category: general
date: 2026-03-26
description: OCR इंजन में भाषा कैसे सेट करें और छवियों से हस्तलेखित पाठ निकालें –
  इमेज को टेक्स्ट में बदलने के लिए चरण‑दर‑चरण ट्यूटोरियल।
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: hi
og_description: OCR इंजन में भाषा कैसे सेट करें और छवियों से हस्तलिखित नोट्स निकालें।
  मिनटों में छवि को टेक्स्ट में बदलना सीखें।
og_title: OCR के लिए भाषा कैसे सेट करें – हस्तलिखित टेक्स्ट को आसानी से निकालें
tags:
- OCR
- Python
- Image Processing
title: OCR के लिए भाषा कैसे सेट करें और हस्तलिखित टेक्स्ट निकालें – पूर्ण गाइड
url: /hi/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR के लिए भाषा कैसे सेट करें और हस्तलेखित टेक्स्ट निकालें – पूर्ण गाइड

क्या आपने कभी सोचा है **भाषा कैसे सेट करें** अपने OCR इंजन में ताकि वह वास्तव में उन अक्षरों को समझे जो आपको चाहिए? शायद आपके पास किराने की सूची, मीटिंग नोट, या एक स्केची‑लुकिंग डायग्राम की फोटो है और आप टेक्स्ट नहीं निकाल पा रहे। अच्छी खबर? आपको कंप्यूटर विज़न में पीएचडी की ज़रूरत नहीं—सिर्फ कुछ पायथन लाइन्स और सही फ्लैग्स।

इस ट्यूटोरियल में हम **हस्तलेखित टेक्स्ट निकालने** के लिए PNG से इमेज को प्लेन टेक्स्ट में बदलने के सटीक कदमों को देखेंगे, और प्रत्येक सेटिंग के “क्यों” को समझाएंगे। अंत तक आप किसी भी प्रोजेक्ट में, चाहे वह नोट‑टेकिंग ऐप हो या बैच‑प्रोसेसिंग पाइपलाइन, हस्तलेखित नोट्स को पहचानने में सक्षम हो जाएंगे।

> **आपको क्या चाहिए**  
> • Python 3.8+ (कोड 3.10 पर भी काम करता है)  
> • `ocr` लाइब्रेरी (या कोई भी संगत रैपर जो `OcrEngine` एक्सपोज़ करता हो)  
> • एक सैंपल इमेज जैसे `note_handwritten.png` – कोई भी इमेज जिसमें विस्तारित लैटिन अक्षर हों, चलेगी।

चलिए शुरू करते हैं।

---

## भाषा कैसे सेट करें और हस्तलेखित पहचान सक्षम करें

सबसे पहले आपको OCR इंजन को बताना होगा कि वह किस वर्णमाला की अपेक्षा करे। यदि आप इस कदम को छोड़ देते हैं, तो इंजन डिफ़ॉल्ट रूप से एक सामान्य सेट उपयोग करता है जो अक्सर एक्सेंटेड अक्षरों या विशेष प्रतीकों को गलत पहचानता है।

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**यह क्यों महत्वपूर्ण है:**  
- **ExtendedLatin** उन अक्षरों को कवर करता है जैसे “ñ”, “ø”, और “ç”, जो कई यूरोपीय नोट्स में सामान्य हैं।  
- `recognize_handwritten` फ़्लैग बेसिक प्रिंट‑टेक्स्ट OCR से मॉडल को बदलकर एक न्यूरल नेटवर्क में स्विच करता है जो कर्सिव स्ट्रोक्स पर प्रशिक्षित है। बिना इस फ़्लैग के, इंजन आपके स्क्रिबल को शोर मानता है।

> **प्रो टिप:** यदि आप कई भाषाओं में दस्तावेज़ प्रोसेस कर रहे हैं, तो प्रत्येक भाषा के लिए अलग इंजन इंस्टैंसिएट करें या प्रत्येक कॉल से पहले डायनामिक रूप से `ocr_engine.language` बदलें। इससे अनावश्यक कैरेक्टर सेट लोड करने का ओवरहेड बचता है।

![Screenshot of OCR engine configuration showing how to set language](/images/ocr-set-language.png "How to set language on OCR engine")

*Image alt text: “OCR इंजन कॉन्फ़िगरेशन स्क्रीन पर भाषा कैसे सेट करें।”*

---

## PNG इमेज से हस्तलेखित टेक्स्ट निकालें

अब जब इंजन को पता है कि क्या देखना है, तो इमेज फीड करने का समय है। `recognize_image` मेथड एक रिच रिज़ल्ट ऑब्जेक्ट रिटर्न करता है; `text` एट्रिब्यूट वह प्लेन स्ट्रिंग रखता है जिसकी आपको ज़रूरत है।

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

जब आप स्क्रिप्ट चलाएंगे, तो आपको कुछ इस तरह दिखना चाहिए:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

यह आउटपुट साबित करता है कि आपने सफलतापूर्वक **इमेज को टेक्स्ट में बदल दिया** और इंजन ने आपके द्वारा सेट की गई भाषा को सम्मानित किया।

**आम गलतियाँ**  
- **गलत पाथ** – फ़ाइल लोकेशन दोबारा चेक करें; मिसिंग फ़ाइल पर `FileNotFoundError` उठता है।  
- **लो‑रेज़ोल्यूशन इमेज** – हस्तलेखित OCR 300 dpi से नीचे संघर्ष करता है। यदि आउटपुट गड़बड़ दिखे तो अपस्केल या री‑स्कैन करें।  
- **कलर इनवर्ज़न** – यदि बैकग्राउंड डार्क है और इंक लाइट, तो पहले रंग उलटें (`Pillow` मदद कर सकता है)।

---

## हेल्पर फ़ंक्शन का उपयोग करके इमेज को टेक्स्ट में बदलें

यदि आप दर्जनों फ़ाइलों पर OCR चलाने की योजना बना रहे हैं, तो लॉजिक को एक रियूज़ेबल फ़ंक्शन में रैप करें। इससे कोड टेस्ट करना और अन्य पाइपलाइन के साथ इंटीग्रेट करना आसान हो जाता है।

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

हेल्पर **हस्तलेखित टेक्स्ट निकालने** की लॉजिक को अलग करता है, इसलिए आप इसे Flask एंडपॉइंट, CLI टूल, या बैच जॉब से बिना हर बार कॉन्फ़िगरेशन लिखे कॉल कर सकते हैं।

---

## वास्तविक दुनिया के परिदृश्यों में हस्तलेखित नोट्स को पहचानें

नीचे कुछ स्थितियाँ दी गई हैं जहाँ आपको **हस्तलेखित नोट्स को पहचानना** पड़ सकता है और यह सेटअप कैसे अनुकूल होता है:

| परिदृश्य | भाषा क्यों महत्वपूर्ण है | सुझाया गया बदलाव |
|----------|------------------------|-------------------|
| **बहुभाषी किराने की सूचियाँ** | आइटम्स में एक्सेंट हो सकते हैं (जैसे “crème”) | प्रत्येक सूची के लिए `ocr_engine.language` बदलें या यदि सपोर्टेड हो तो `ocr.Language.AutoDetect` उपयोग करें |
| **क्लासरूम व्हाइटबोर्ड फ़ोटो** | चॉक से फेड स्ट्रोक्स बनते हैं | इमेज को इंजन में फीड करने से पहले कंट्रास्ट बढ़ाएँ |
| **मेडिकल प्रिस्क्रिप्शन** | हस्तलेख बहुत गंदा होता है | दवा के नामों के लिए स्पेल‑चेक डिक्शनरी के साथ OCR को पेयर करें |

इन सभी मामलों में, मूल कदम—**भाषा कैसे सेट करें**, हस्तलेखित मोड एनेबल करें, और `recognize_image` कॉल करें—एक समान रहते हैं। यही स्थिरता इस अप्रोच को मजबूत और मेंटेन करने में आसान बनाती है।

---

## एज केस और एडवांस्ड टविक्स

1. **बैच प्रोसेसिंग** – इंजन को एक बार लोड करें, फ़ाइलों पर लूप चलाएँ, और केवल आवश्यकता पड़ने पर `language` एट्रिब्यूट बदलें। इससे इनिशियलाइज़ेशन ओवरहेड कम होता है।  
2. **नॉन‑लैटिन स्क्रिप्ट्स** – यदि आपको सिरिलिक या अरबी प्रोसेस करनी है, तो `ExtendedLatin` को उपयुक्त एन्नम से बदलें (जैसे `ocr.Language.Cyrillic`)। पैटर्न वही रहता है।  
3. **पार्शियल रिकग्निशन** – कभी‑कभी बहुत छोटे स्ट्रोक्स के लिए इंजन खाली स्ट्रिंग रिटर्न करता है। एक त्वरित वैलिडेशन (`if not result.text.strip(): …`) आपको सेकेंडरी मॉडल पर फ़ॉल्बैक करने या यूज़र को री‑स्कैन करने के लिए प्रॉम्प्ट देता है।  
4. **परफ़ॉर्मेंस प्रोफ़ाइलिंग** – बड़े डेटासेट के लिए `recognize_image` कॉल का टाइम लें। यदि यह बॉटलनेक बनता है, तो `concurrent.futures.ThreadPoolExecutor` के साथ पैरेललाइज़ करने पर विचार करें।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा स्क्रिप्ट है जिसे आप `handwritten_ocr.py` नाम की फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। इसमें आर्ग्यूमेंट पार्सिंग शामिल है ताकि आप कमांड लाइन से किसी भी इमेज को पॉइंट कर सकें।

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

इसे इस तरह चलाएँ:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

आपको पहले के स्निपेट जैसा ही आउटपुट दिखना चाहिए, जिससे पुष्टि होगी कि आपने सफलतापूर्वक **इमेज को टेक्स्ट में बदला** और **हस्तलेखित नोट्स को पहचान लिया**।

---

## निष्कर्ष

हमने **OCR इंजन पर भाषा कैसे सेट करें**, हस्तलेखित‑टेक्स्ट फ़्लैग को ऑन किया, और एक रियूज़ेबल फ़ंक्शन बनाया जो किसी भी इमेज से **हस्तलेखित टेक्स्ट निकालता** है। ऊपर बताए गए कदमों को फॉलो करके आप भरोसेमंद रूप से **इमेज को टेक्स्ट में बदल** सकते हैं, चाहे वह एक सिंगल नोट हो या स्कैन किए गए दस्तावेज़ों का विशाल आर्काइव।

अब विभिन्न भाषा पैक्स के साथ प्रयोग करें, इमेज की फ़ोल्डर को बैच‑प्रोसेस करें, या इस लॉजिक को वेब सर्विस में इंटीग्रेट करें जो JSON रिज़ल्ट रिटर्न करे। मूल बातें वही रहती हैं, और `ocr` लाइब्रेरी की लचीलापन आपको लगभग किसी भी यूज़‑केस के लिए अनुकूल बनाता है।

एज केस, परफ़ॉर्मेंस, या स्क्रिप्ट को अन्य भाषाओं में एक्सटेंड करने के बारे में सवाल हैं? कमेंट करें या GitHub पर मुझे पिंग करें – हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}