---
category: general
date: 2026-06-25
description: PythonでOCRを使用する方法 – OCR用に画像を読み込む方法、領域内のテキストを認識する方法、そして領域のテキストを素早く抽出する方法を学びましょう。
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: ja
og_description: PythonでOCRを使用する方法 – 画像を読み込み、特定の領域のテキストを認識し、請求書番号を抽出するステップバイステップガイド。
og_title: OCR Pythonの使い方：画像を読み込んで領域のテキストを抽出する
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR Pythonの使い方：画像を読み込んで領域のテキストを抽出する
url: /ja/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Python の使い方: 画像を読み込み、領域テキストを抽出する

**How to use OCR in Python** は思ったより簡単です。スキャンした請求書を見て、ページ全体を解析せずに請求書番号だけを取得したいと思ったことはありませんか？同じ悩みを抱える開発者は多く、光学文字認識に初めて触れるときにこの壁にぶつかります。このガイドでは、OCR 用に画像を読み込み、矩形を定義し、その領域のテキストを認識し、最終的に領域テキストを抽出する手順を解説します。最後まで読めば、必要なテキストの一部を抽出できる実行可能なスクリプトが手に入ります。

> *Pro tip:* PDF を扱う場合は、まず各ページを画像に変換しましょう—ほとんどの OCR ライブラリは PNG/JPEG に最適です。

## 必要なもの

- Python 3.8+（最新の安定版の使用を推奨）  
- `OcrEngine` クラスを提供する OCR ライブラリ（例: `pip install ocr-lib` でインストールできる **ocr**）  
- サンプル画像—ここでは、任意のフォルダーに配置した `invoice.png` を使用します  
- 矩形 (x, y, width, height) の基本的な知識  

重い依存関係は不要、GPU も不要です—純粋に CPU だけで動作するので、ポータブルです。

---

## OCR の使い方: エンジンの初期化 (ステップ 1)

Before any text can be read, you need an OCR engine instance. Think of it as the brain that will analyze pixel patterns.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

※重要性: エンジンを初期化すると言語モデルがロードされ、デフォルト設定が適用されます。このステップを省略すると、`recognize_region` を呼び出した瞬間に例外が発生します。

---

## OCR 用画像の読み込み (ステップ 2)

Now that the engine is ready, we feed it an image. The library’s `Image.load` method handles common formats and normalizes the bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

If the file isn’t found, Python will throw a `FileNotFoundError`. Make sure the path is absolute or relative to your script’s working directory.  

*Edge case:* Some OCR engines expect a grayscale image. If you notice poor accuracy, convert the image first:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## 領域内テキストの認識 (ステップ 3)

Defining the region is where you tell the engine *where* to look. The `Rectangle` takes floating‑point values for sub‑pixel precision, which can be handy when dealing with high‑resolution scans.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – 矩形の左上隅（ピクセル単位）  
- **width, height** – ボックスのサイズ  

これらの数値の取得方法がわからない場合は、任意の画像エディタ（例: GIMP や Paint.NET）で画像を開き、選択ツールで座標を確認すると簡単です。  

*Why not just OCR the whole page?* Limiting the area reduces noise, speeds up processing, and dramatically improves accuracy for small fields like invoice numbers.

---

## 領域テキストの抽出 (ステップ 4)

With the region set, ask the engine to recognize only that slice. The result object contains the raw text and confidence scores.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

If the OCR engine supports multiple languages, you can pass an optional language code:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Common pitfall:* Some engines return a list of words instead of a single string. In such cases, concatenate them:

```python
text = " ".join(region_result.words)
```

---

## 抽出した請求書番号の出力 (ステップ 5)

Finally, print—or store—the extracted text. You can also post‑process the string to remove stray whitespace or non‑numeric characters.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Running the script with a correctly aligned rectangle should yield something like:

```
Invoice number: 20231578
```

If you get garbage characters, double‑check the rectangle coordinates or consider increasing the image resolution.

---

## 完全な動作例

Putting it all together, here’s a self‑contained script you can copy‑paste and run:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Save the file as `extract_invoice.py`, replace `YOUR_DIRECTORY` with the actual folder, and run:

```bash
python extract_invoice.py
```

You should see the invoice number printed to the console.

---

## よくある質問

**Q: What if the invoice number is printed in a fancy font?**  
A: Most modern OCR engines handle a wide range of fonts, but you can boost accuracy by training a custom language model or pre‑processing the image (e.g., applying a threshold filter).

**Q: Can I extract multiple fields at once?**  
A: Absolutely. Define a list of `Rectangle` objects—one per field—and loop over them, storing each result in a dictionary.

**Q: Does this work on multi‑page PDFs?**  
A: Convert each page to an image first (using `pdf2image` or similar), then apply the same region‑based extraction per page.

---

## まとめ

In this tutorial we covered **how to use OCR** in Python to load an image, recognize text in a specific region, and extract that region’s text—perfect for pulling invoice numbers, order IDs, or any small data snippet from scanned documents. By isolating the area of interest you gain speed, accuracy, and less post‑processing hassle.

Ready for the next step? Try extending the script to handle **load image for OCR** from a folder of batch invoices, or experiment with **recognize text in region** for different fields like dates and totals. The same pattern applies—just change the rectangle coordinates.

If you ran into any snags or have ideas for improvement, drop a comment below. Happy coding, and may your OCR pipelines be ever accurate!

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR を使用した画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR で矩形を準備して画像からテキスト抽出する方法](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [AspOCR の使用方法: .NET 用画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}