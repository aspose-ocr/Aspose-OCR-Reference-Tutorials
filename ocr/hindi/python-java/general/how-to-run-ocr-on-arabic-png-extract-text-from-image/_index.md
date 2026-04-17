---
category: general
date: 2026-03-26
description: जानें कि अरबी PNG छवियों पर OCR कैसे चलाएँ और जल्दी से अरबी टेक्स्ट निकालें।
  यह गाइड चरण‑दर‑चरण Python कोड के साथ छवि को टेक्स्ट में बदलने को दर्शाता है।
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: hi
og_description: अरबी PNG छवियों पर OCR कैसे चलाएँ? अरबी टेक्स्ट निकालने, अरबी टेक्स्ट
  को पहचानने और पायथन का उपयोग करके छवि को टेक्स्ट में बदलने के लिए इस पूर्ण गाइड
  का पालन करें।
og_title: अरबी PNG पर OCR कैसे चलाएँ – छवि से पाठ निकालें
tags:
- OCR
- Python
- Arabic
title: अरबी PNG पर OCR कैसे चलाएँ – छवि से टेक्स्ट निकालें
url: /hi/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# अरबी PNG पर OCR चलाएँ – छवि से टेक्स्ट निकालें

क्या आपने कभी **how to run OCR** किसी ऐसी छवि पर करने के बारे में सोचा है जिसमें अरबी लिपि हो? शायद आपके पास कोई स्कैन किया हुआ रसीद, एक ऐतिहासिक पांडुलिपि, या बस सोशल‑मीडिया पोस्ट की स्क्रीनशॉट है और आपको टेक्स्ट को सर्चेबल फ़ॉर्मेट में चाहिए। आप अकेले नहीं हैं—दुनिया भर के डेवलपर्स राइट‑टू‑लेफ़्ट भाषाओं के साथ काम करते समय इसी समस्या का सामना करते हैं।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे **how to run OCR** एक PNG फ़ाइल पर, अरबी टेक्स्ट निकालेंगे, और परिणाम को कंसोल में प्रिंट करेंगे। कोई अस्पष्ट “डॉक्यूमेंटेशन देखें” लिंक नहीं; सिर्फ वह कोड जिसे आप कॉपी‑पेस्ट कर सकते हैं, साथ ही प्रत्येक लाइन क्यों महत्वपूर्ण है इसका विवरण। अंत तक आप **convert image to text** भरोसेमंद रूप से कर पाएँगे, भले ही स्रोत एक जटिल अरबी PNG हो।

> **आप क्या सीखेंगे**
> - अरबी के लिए Python OCR इंजन सेट‑अप करना  
> - PNG छवि लोड करना और सामान्य समस्याओं को संभालना  
> - अरबी टेक्स्ट पहचानना और आउटपुट की पुष्टि करना  
> - विभिन्न छवि गुणवत्ता से **extracting Arabic text** करने के टिप्स  

शुरू करने से पहले सुनिश्चित करें कि आपके पास Python 3.8+ इंस्टॉल है और `ocr` लाइब्रेरी का नवीनतम संस्करण (स्निपेट में उपयोग किया गया) उपलब्ध है। यदि आप वर्चुअल एन्वायरनमेंट उपयोग कर रहे हैं, तो अभी इसे एक्टिवेट करें—यह डिपेंडेंसीज़ को साफ़ रखता है।

## Prerequisites

- Python 3.8 या उससे नया  
- `ocr` पैकेज (`pip install ocr‑engine` – वास्तविक पैकेज नाम से बदलें)  
- एक अरबी PNG छवि (`arabic_doc.png`) जिसे आप रेफ़रेंस कर सकते हैं  
- Python फ़ंक्शन्स और क्लासेज़ की बुनियादी समझ  

बस इतना ही। कोई भारी फ्रेमवर्क नहीं, कोई Docker कंटेनर नहीं—सिर्फ साधा Python।

## Step 1: Install and Import the OCR Library

First things first. We need the OCR engine itself. The library we’ll use exposes an `OcrEngine` class with a straightforward API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Why import `Imaging` separately?* The `Imaging` submodule gives us a convenient `Image.load` method that understands PNG, JPEG, and TIFF out of the box. Skipping this step would force you to handle raw bytes yourself, which is unnecessary for most use‑cases.

## Step 2: Create the OCR Engine Instance

Now we create an instance of the engine. Think of this object as the “brain” that will process the image.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** If you plan to process many images in a row, reuse the same `ocr_engine` instance. It caches language models, which speeds up subsequent recognitions.

## Step 3: Set the Language to Arabic

Arabic isn’t Latin; it has its own character set, right‑to‑left direction, and contextual shaping. That's why we must explicitly tell the engine which language model to load.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

If you forget this line, the engine defaults to English and you’ll get garbled output—something I’ve seen happen far too often.

## Step 4: Load Your PNG Image

Here’s where the **convert image to text** part really starts. We’ll load the PNG file that contains the Arabic script.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Common Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| Image is too dark | Output contains many blanks | Pre‑process with Pillow (`ImageEnhance.Brightness`) |
| PNG has an alpha channel | Some OCR engines mis‑read transparent pixels | Convert to RGB (`image.convert("RGB")`) before loading |
| Text is rotated | Recognized text is upside‑down | Rotate the image (`image.rotate(90, expand=True)`) before passing to the engine |

## Step 5: Run the Recognition Process

With everything set, we finally ask the engine to do its job.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

The `recognize` method returns an object that holds the raw Unicode string, confidence scores, and bounding boxes. For most developers, the plain text is all you need.

## Step 6: Output the Recognized Arabic Text

Now we print the result. In a real application you might write to a file, a database, or feed it into a translation API.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

When you run the script, you should see the Arabic characters displayed in your console (make sure your terminal supports Unicode). If you see question marks or empty strings, double‑check the language setting and image quality.

### Expected Output

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

If the output looks similar to the line above, congratulations—you’ve successfully **extracted Arabic text** from a PNG!

## Full Working Example

Below is the entire script, ready to copy‑paste. Replace `YOUR_DIRECTORY/arabic_doc.png` with the path to your own file.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Run it with `python run_ocr.py` (or whatever you named the file). If everything is installed correctly, you’ll see the Arabic sentence printed to the console.

## How to Run OCR on Different Image Formats

The same code works for JPEG, TIFF, or BMP—just change the file extension. The `Image.load` method automatically detects the format, so you can **convert image to text** without any extra code.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Remember, the quality of the source image heavily influences the accuracy of the **recognize Arabic text** step. High‑resolution, low‑compression images give the best results.

## Extract Text from PNG: Tips for Better Accuracy

1. **DPI Matters** – Aim for at least 300 dpi. Lower DPI often leads to missed characters.  
2. **Contrast is King** – Use image‑processing tools (e.g., OpenCV) to increase contrast before feeding the image to the OCR engine.  
3. **Noise Removal** – Small speckles can confuse the model; median filtering helps.  

Here’s a quick snippet using Pillow to improve a PNG before OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Frequently Asked Questions

**Q: Does this work with right‑to‑left languages other than Arabic?**  
A: Absolutely. Just change the language code (`"ar"` → `"he"` for Hebrew, `"fa"` for Persian) and the engine will load the appropriate model.

**Q: What if I need to extract text from multiple PNGs in a folder?**  
A: Loop over the files, reuse the same `ocr_engine` instance, and collect results in a list or write each to a separate `.txt` file.

**Q: Can I get confidence scores for each word?**  
A: Yes. `ocr_result` often exposes a `get_confidences()` method. Pair each confidence with the corresponding word for quality control.

## Next Steps

Now that you know **how to run OCR** on Arabic PNGs, consider these follow‑up ideas:

- **Batch processing:** Combine the script with `os.listdir` to **extract Arabic text** from an entire directory.  
- **Post‑processing:** Use the `arabic_reshaper` and `python-bidi` libraries to correctly display right‑to‑left output in PDFs.  
- **Integration:** Feed the extracted text into a search index (e.g., Elasticsearch) to make scanned documents searchable.  

Each of these topics builds on the fundamentals covered here, and they’ll help you turn a simple **convert image to text** script into a production‑ready pipeline.

---

![अरबी PNG पर OCR चलाने का तरीका](
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}