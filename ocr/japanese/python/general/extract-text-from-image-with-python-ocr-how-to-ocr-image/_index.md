---
category: general
date: 2026-05-31
description: Python の aocr ライブラリを使用して画像からテキストを抽出します。数行のコードで画像の OCR 方法、OCR 用画像の読み込み、特殊文字の認識を学びましょう。
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: ja
og_description: Python の aocr ライブラリを使用して画像からテキストを抽出します。このガイドでは、画像の OCR 方法、OCR 用の画像の読み込み、そして特殊文字を素早く認識する方法を示します。
og_title: Python OCRで画像からテキストを抽出 – 画像のOCR方法
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Python OCRで画像からテキストを抽出 – 画像をOCRする方法
url: /ja/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する Python OCR – 画像の OCR 方法

**画像からテキストを抽出**したいけれど、「Ł」や「Ž」や「ß」などの特殊文字に対応できるライブラリが分からない、ということはありませんか？実際のプロジェクトでは、スキャンしたレシートや多言語の看板、歴史的文書などで **特殊文字を認識**できるかどうかが、使えるデータセットになるか行き詰まるかの分かれ目になることが多いです。

良いニュースです！Python の数行と軽量な **aocr** パッケージさえあれば、どんな画像でも検索可能なテキストに変換できます。以下では、実行可能な完全なスクリプトと、各ステップの **なぜそれが必要か** を解説するので、単なるコピペにとどまらず、実際に何が起きているかを理解できます。

## このチュートリアルで学べること

- **aocr** ライブラリのインストールとインポート  
- OCR 用に画像を読み込む方法（よくある落とし穴を含む）  
- エンジンを実行して **画像をテキストに変換**する手順  
- 結果の表示と特殊文字出力の取り扱い  
- 多言語対応やエラーハンドリングのための基本フローの拡張  

このガイドを最後まで読めば、任意の言語の **画像からテキストを抽出**できるようになり、デフォルト設定でうまくいかない場合の調整方法も分かります。

## 前提条件

| 前提条件 | 重要な理由 |
|----------|------------|
| Python 3.8+ | aocr は最新の型ヒント機能に依存しています |
| `pip` アクセス | ライブラリをインストールするため |
| サンプル画像（例: `multilingual.png`） | 特殊文字のデモに使用します |
| 仮想環境の基本的な知識（任意） | 依存関係を整理しやすくします |

Tesseract のような重い外部ツールは不要です—**aocr** はすぐに使える高速ニューラルエンジンを同梱しています。

---

## 手順 1: aocr ライブラリをインストール

まずターミナル（または IDE のコンソール）を開き、次のコマンドを実行します。

```bash
pip install aocr
```

*プロのコツ:* 複数プロジェクトを並行して扱う場合は、先に仮想環境を作成すると便利です。

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

これにより OCR 関連の依存関係がシステム全体から分離され、後々のトラブルを防げます。

---

## 手順 2: OCR 用に画像を読み込む

パッケージの準備ができたら、**画像を OCR 用に読み込む**必要があります。`OcrEngine` クラスはファイルへのパスを受け取るので、画像が存在し読み取り可能であることを確認してください。

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **なぜ重要か:**  
> - `load_image` はファイルの存在確認やサポート形式のチェックを行います。  
> - 生文字列 (`r"..."`) を使うことで、Windows パスのエスケープ文字バグを回避できます。  
> - 画像が巨大な場合、aocr は自動でダウンサンプリングし、メモリ使用量を抑えます。  

`FileNotFoundError` が出たら、パスと拡張子（PNG、JPEG、BMP のいずれか）を再確認してください。

---

## 手順 3: OCR を実行 – 画像をテキストに変換

メモリ上に画像がロードされたら、次の呼び出しで **特殊文字を認識**し、Unicode 文字列を生成します。

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

裏側では、aocr が多言語データセットで学習した軽量な畳み込みリカレントネットワークを走らせています。そのため、キリル文字、拡張ラテン文字、さらにはマイナーなグリフまで正しく表示されます。

---

## 手順 4: 抽出したテキストを表示

最後に結果を出力します。エンジンが解読できたすべての文字が表示され、厄介なアクセント記号も含まれます。

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**サンプル出力**（実際の結果は画像内容に依存します）:

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*画像例:*  
![画像からテキストを抽出した例の出力](https://example.com/ocr-output.png "画像からテキストを抽出した例の出力")

> **注意:** `print` はモダンな Python ではデフォルトで UTF‑8 エンコーディングです。そのため、ほとんどの端末で特殊文字が正しく表示されます。文字化けする場合は、コンソールを UTF‑8 に設定するか、`encoding='utf-8'` でファイルに書き出してください。

---

## 手順 5: エッジケースと一般的な落とし穴の対処

### 5.1 低解像度画像

画像が 150 dpi 未満だと OCR 精度が大幅に低下します。簡単な対策は、aocr に渡す前に画像をアップスケールすることです。

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 言語検出が正しくない

aocr は自動で言語を検出しますが、結果を改善したい場合は特定のスクリプトを強制指定できます。

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

サポートされている言語コード例: `eng`, `deu`, `fra`, `rus`, `spa` など。

### 5.3 ノイズや背景パターン

背景がノイズだらけだとモデルが混乱します。OpenCV で二値化前処理を行うと効果的です。

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## 完全スクリプト – ワンクリックで実行

以下は **完全に実行可能なサンプル** です。`ocr_demo.py` として保存し、`python ocr_demo.py` を実行してください。

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

実行例:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

コンソールに抽出された文字が表示され、**画像からテキストを抽出**し **特殊文字を認識**できたことが確認できます。

---

## よくある質問

**Q: PDF でも使えますか？**  
A: 直接はできません。まず `pdf2image` などで PDF ページを画像に変換し、各画像を aocr に渡してください。

**Q: aocr は Tesseract と比べてどれくらい速いですか？**  
A: 典型的な 300 dpi スキャンの場合、aocr はモダンなノートパソコンで約 0.3 秒で 1 ページを処理します。デフォルト設定の Tesseract の約 2 倍の速度です。

**Q: フォルダ内の画像をバッチ処理できますか？**  
A: もちろん可能です。`main` 関数を `Path(folder).glob("*.png")` のループで回し、結果を CSV にまとめれば完了です。

---

## まとめ

これで Python の aocr ライブラリを使った **画像からテキストを抽出** のエンドツーエンドワークフローが完成しました。ファイルの読み込みから Unicode 出力まで、各ステップを丁寧に解説したので、レシートスキャンサービスや多言語文書アーカイブなど、さまざまなプロジェクトに応用できます。

次に検討すべき関連トピック:

- **PDF 用に画像をテキストへ変換**（`pdf2image` + OCR）  
- **手書きノートの特殊文字を認識**（`ocr_engine.set_dpi(600)` を試す）  
- **Web API で画像を OCR**（Flask + aocr）  

ぜひ試してみて、言語設定を調整しながらデータを即座に検索可能にしてください。質問や面白いユースケースがあればコメントで教えてください—ハッピーコーディング！

## 次に学ぶべきこと

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}