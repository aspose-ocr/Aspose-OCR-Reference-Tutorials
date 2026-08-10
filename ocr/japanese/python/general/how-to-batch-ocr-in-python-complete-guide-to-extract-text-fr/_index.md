---
category: general
date: 2026-06-28
description: PythonでバッチOCRを行う方法—画像からテキストを抽出し、スキャンしたページをバッチOCR処理でテキストに変換する。
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: ja
og_description: PythonでバッチOCRを行う方法、画像からテキストを抽出する方法、そして効率的なバッチOCR処理でスキャンしたページをテキストに変換する方法を学びましょう。
og_title: PythonでバッチOCRを実行する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: PythonでバッチOCRを行う方法 – 画像からテキストを抽出する完全ガイド
url: /ja/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでバッチOCRを行う方法 – 画像からテキストを抽出する完全ガイド

If you're wondering **how to batch OCR in Python**, you're in the right place. This tutorial shows you a quick way to **extract text from images** and **convert scanned pages to text** using a single OCR engine instance. No more copy‑pasting one file after another—let the code do the heavy lifting.

> **プロのコツ:** 純粋な Python ライブラリを好む場合は、`OcrEngine` を `pytesseract.image_to_string` に置き換えてください。周囲のロジックは同じままです。

## 必要なもの

* Python 3.9+ がインストールされていること（コードは 3.8 でも動作しますが、3.9+ では最新の型ヒント機能が利用できます）。
* 最新の OCR ライブラリ—ここでは **Aspose.OCR for Python via .NET** を使用し、元のスニペットに示された `OcrEngine` クラスを公開しています。  
  ```bash
  pip install aspose-ocr
  ```
* スキャンしたページが入ったフォルダー（`page1.png`、`page2.png`、…）。Pillow が開ける形式であれば PDF、TIFF、BMP でも問題ありません。
* 少しだけ好奇心—画像からテキストへの自動化をまだ行ったことがなければ、バッチOCRがなぜゲームチェンジャーになるかをご覧いただけます。

## PythonでバッチOCRを行う方法 – ステップバイステップガイド

Below is the complete, runnable script. Every line is commented so you can see *why* each piece matters, not just *what* it does.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### 期待される出力

Running the script against a folder with three PNG scans produces something like:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

The preview shows the first 200 characters of each page, and the full text lives in the `ocr_output` directory.

## 単一エンジンで画像からテキストを抽出する

Why do we create **one** `OcrEngine` and reuse it? Instantiating the engine can be expensive because it loads language packs and native DLLs. By sharing the same instance across the batch, you:

* **メモリ節約** – リソースは RAM に 1 つだけ保持されます。
* **速度向上** – エンジンが温まった状態を保ち、再初期化を回避します。
* **一貫性の維持** – 同じ認識設定がすべてのページに適用され、同一レイアウトの **画像からテキストを抽出** したい場合に重要です。

If you need to tweak recognition (e.g., enable spell‑check or change the language), do it *before* calling `recognize_batch`. All subsequent pages will inherit those settings automatically.

## スキャンページを効率的にテキストへ変換する

The heart of the problem—**convert scanned pages to text**—is solved by `engine.recognize_batch(images)`. Under the hood the library processes each image in a background thread pool, so you get near‑linear scaling on multi‑core machines. A few things to keep in mind:

* **画像品質が重要** – 300 dpi 以上が最良の結果をもたらします。スキャンが低解像度の場合は、エンジンに渡す前に Pillow でアップサンプリングすることを検討してください。
* **カラー vs. グレースケール** – OCR エンジンは通常 8 ビットグレースケールで高速に動作します。前処理ステップを追加できます：  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **言語サポート** – Aspose.OCR は 40 以上の言語に対応しています。英語以外を使用する場合は、バッチ呼び出しの前に `engine.language = "eng"` や `"fra"` などに設定してください。

## バッチOCR処理のベストプラクティス

Even though the code above is already concise, production‑grade batch OCR often requires a few extra safeguards:

| 懸念点 | 推奨アプローチ |
|---------|----------------------|
| **大規模バッチ（500 ファイル以上）** | メモリ使用量を抑えるため、100〜200枚の画像ごとに分割してください。 |
| **破損または非対応ファイル** | `load_images` ヘルパーはすでに例外を捕捉し警告を記録します。さらに、問題のあるファイルをスキップまたは移動するフォールバックを実装できます。 |
| **進捗モニタリング** | ライブラリが画像単位のコールバックを提供している場合、`recognize_batch` を各画像処理後に yield するループでラップしてください。 |
| **ポストプロセッシング** | 結果文字列に対してスペルチェックや正規表現によるクリーンアップを実行し、検索性を向上させます。 |
| **並列処理** | マルチノード環境がある場合、フォルダーをワーカーに分散し、最後に `.txt` 出力をマージしてください。 |

These tips help you scale **batch OCR processing** from a handful of pages to thousands without crashing your script.

## よくある質問

**Q: これを直接 PDF に使えますか？**  
A: もちろんです。まず各 PDF ページを画像に変換（例：`pdf2image` を使用）し、得られたリストを `recognize_batch` に渡してください。パイプラインの残りは変更不要です。

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR を使用した画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [フォルダー上で OCR 操作を使用して画像からテキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET を使用して ZIP アーカイブからテキストを抽出する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}