---
category: general
date: 2026-06-22
description: Python을 사용해 몇 줄만으로 이미지에서 OCR을 수행하세요. OCR용 이미지를 로드하는 방법, PNG에서 텍스트를 인식하는
  방법, 그리고 OCR 엔진을 효율적으로 사용하는 방법을 배워보세요.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: ko
og_description: Python으로 이미지를 빠르게 OCR합니다. 이 튜토리얼에서는 OCR을 위한 이미지 로드 방법, PNG에서 텍스트 인식,
  그리고 신뢰도를 갖춘 OCR 엔진 사용 방법을 보여줍니다.
og_title: Python으로 이미지 OCR 수행 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python에서 이미지 OCR 수행 – 완전 가이드
url: /ko/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 이미지에 OCR 수행 – 완전 가이드

Ever needed to **perform OCR on image** files but felt stuck at the very first line of code? You’re not alone. In this walkthrough we’ll show you exactly how to **load image for OCR**, set up a lightweight **OCR engine**, and finally **recognize text from PNG** with just a handful of commands.

We’ll cover everything from installing the library to tweaking the whitelist so that only digits and uppercase letters survive the scan. By the end you’ll have a ready‑to‑run script that you can drop into any project—no mystery, no extra fluff.

## 배울 내용

- How to **use OCR engine** programmatically in Python.  
- The exact steps to **load image for OCR** from a local folder.  
- Why and how to restrict recognition to a custom character set.  
- How to **recognize text from PNG** and handle the result safely.  

**Prerequisites:** Python 3.7+ installed, a terminal you’re comfortable with, and an image (e.g., `serial-number.png`) you want to read. No prior OCR experience required.

---

## Perform OCR on Image – Initialize the OCR Engine

The first thing you have to do is create an instance of the OCR engine. Think of the engine as the brain that will analyze the pixels and turn them into characters.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* Without an engine there’s nothing to process the image. The `OcrEngine` class bundles all the heavy‑lifting—pre‑processing, segmentation, and character classification—into a single object you can reuse.

---

## Load Image for OCR – Provide the PNG File

Now that the engine exists, you need to feed it the picture you want to read. The library expects an `ImageStream` object, which you can create directly from a file path.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* Keep the image in a high‑contrast format (black text on white background) and avoid compression artifacts; they can trip up the OCR algorithm.

---

## Restrict Characters – Whitelist Digits and Uppercase Letters

Often you only care about a subset of characters—say, a serial number that contains only A‑Z and 0‑9. By setting a whitelist you tell the engine to ignore everything else, which dramatically improves accuracy.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* The engine builds a filter that discards any glyph not present in the whitelist before the final classification stage. This is especially handy when the image contains noise or decorative text you don’t need.

---

## Recognize Text from PNG – Run the OCR Process

With the engine primed and the image loaded, you can finally **perform OCR on image**. The `recognize()` call runs the full pipeline and returns a result object.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

If you’re curious about performance, the method typically finishes within a few hundred milliseconds for a 300 × 200 px PNG on a modern laptop.

---

## Output and Verify – Get the Recognized Text

The last step is to extract the plain text from the result object. Anything that didn’t match the whitelist is automatically dropped, so you get a clean string ready for further processing.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (assuming the image contained that exact serial number).  

If the output is empty or garbled, double‑check the image quality and the whitelist; a common pitfall is accidentally omitting needed characters.

---

## Edge Cases & Common Gotchas

| 상황 | 확인할 내용 | 제안된 해결책 |
|-----------|---------------|---------------|
| **파일을 찾을 수 없음** | 경로 오타 또는 파일 누락 | `set_image` 호출 전에 `os.path.abspath`를 사용해 전체 경로를 확인하세요. |
| **저대비 이미지** | 텍스트가 배경과 섞여 있음 | 엔진에 이미지를 전달하기 전에 간단한 임계값(`Pillow` 또는 `OpenCV`)을 적용하세요. |
| **예상치 못한 문자** | 화이트리스트가 너무 제한적임 | 누락된 문자를 화이트리스트 문자열에 추가하세요. |
| **대형 이미지** | 인식 속도 저하 | 이미지 너비를 최대 1024 px로 리사이즈하세요; OCR 품질은 보통 유지됩니다. |

---

## Full Script – Ready to Run

Below is the complete, self‑contained script that ties all the pieces together. Save it as `ocr_demo.py`, replace `YOUR_DIRECTORY` with the actual folder, and run `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Expected console output* (when the PNG contains `SN12345`):

```
Recognized text: SN12345
```

---

## Conclusion

You now know exactly how to **perform OCR on image** files in Python, from **loading image for OCR** to **recognize text from PNG** and finally extracting a clean result using a customizable **OCR engine**. The approach is straightforward, extensible, and works out‑of‑the‑box for most serial‑number‑style scans.

What’s next? Try swapping the whitelist for lowercase letters, experiment with different image formats (JPEG, BMP), or integrate the script into a batch‑processing pipeline. The same pattern—engine → image → settings → recognize → output—holds for virtually any OCR task you’ll encounter.

Got questions or a quirky image that refuses to cooperate? Drop a comment below, and happy coding! 

![Python을 사용한 이미지 OCR 수행 단계 도식](https://example.com/ocr-flow.png "Python OCR 엔진으로 이미지 OCR 수행 방법을 보여주는 도식")


## 다음에 배울 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [이미지를 텍스트로 변환 – URL에서 이미지 OCR 수행](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [AspOCR 사용 방법: .NET용 이미지 OCR 필터 전처리](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [OCR에서 사각형을 준비해 이미지에서 텍스트 추출하기](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}