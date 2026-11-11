---
category: general
date: 2026-03-26
description: Pythonで画像を回転させ、OCRを実行する方法を学びましょう。このガイドでは、OCRのための画像前処理方法と、画像から効率的にテキストを抽出する方法も紹介しています。
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: ja
og_description: Aspose OCR を使用して画像を正しく回転させ、画像からテキストを認識する方法。OCR 用に画像を前処理し、画像からテキストを抽出するステップバイステップのチュートリアルをご覧ください。
og_title: 画像の回転とOCRの実行方法 – 完全Pythonガイド
tags:
- Aspose
- Python
- Image Processing
- OCR
title: PythonでAsposeを使用して画像を回転し、OCRを実行する方法
url: /ja/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python で Aspose を使用して画像を回転し OCR を実行する方法

画像を **回転させて** OCR エンジンがテキストを正しく読み取れるようにしたことはありますか？たとえば、フォームをスキャンしたら横向きになっていたり、カメラで撮影した画像が時計回りに 90° 回転している場合です。その場合、人間の目には問題なく見えても OCR エンジンは文字化けしてしまいます。解決策は簡単です。画像の向きを修正し、必要な領域を切り抜き、テキストを抽出するだけで、Python と Aspose ライブラリ数行で完了します。

このチュートリアルでは、回転した TIFF の読み込み、向きの補正、**OCR 用の画像前処理**、そして最終的に **画像からテキストを認識** するまでの全工程を解説します。最後まで読めば、**OCR を実行する方法** と **画像からテキストを抽出する方法** がマスターできます。

## 必要なもの

- Python 3.8 以上（どの最近のバージョンでも可）
- `asposeocrjava` と `asposeimaging` パッケージ（`pip` でインストール）
- 回転が必要なサンプル画像（例: `rotated_form.tif`）
- 画像処理に対する少しの好奇心

重いフレームワークは不要です。Aspose の 2 つのパッケージと少しの Python ロジックだけで完結します。

---

## 手順 1: Aspose パッケージのインストール（OCR の実行方法）

**画像を回転**したり **画像からテキストを認識**したりする前に、実際に処理を行うライブラリを用意します。

```bash
pip install asposeocrjava asposeimaging
```

> **プロのコツ:** 社内プロキシ環境下にいる場合はコマンドに `--proxy http://proxy:port` を付加してください。これらのパッケージは Aspose の .NET/Java コアをラップした純粋な Python ライブラリなので、インストールはほぼ瞬時に完了します。

---

## 手順 2: ソースファイルを読み込み回転させる – 「画像を回転する」コアステップ

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **なぜ回転が必要か?** 多くの OCR エンジンはテキストが左から右、上から下へ流れることを前提としています。ビットマップが横向きだと、エンジンは意味不明な文字列を返すか、何も認識できません。回転させてピクセルグリッドを期待される読取順序に合わせることで、精度が劇的に向上します。

> **エッジケース:** 画像が 90°、180°、270° のどれで回転すべきか不明な場合は、`source_image.width` と `source_image.height` を比較するか、EXIF の向きタグを利用してください。Aspose の `rotate_flip` メソッドは `ROTATE_180` や `ROTATE_270_CLOCKWISE` もサポートしています。

> **画像プレビュー（任意）:**  
> ![画像回転の例](/assets/rotate-demo.png "画像を回転する – 回転前と回転後")

---

## 手順 3: 関心領域を切り抜く – OCR 用画像前処理

ページ全体ではなく、署名欄や数字ブロックなど小さな領域だけが必要なことが多いです。切り抜くことでノイズが減り、**OCR の実行方法** が高速化します。

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **なぜ切り抜くのか?** 画像サイズを縮小すると OCR エンジンの探索領域が狭まるため、誤検出が減り処理時間も短縮されます。また、元画像に透かしや余計なグラフィックが含まれている場合、エンジンが混乱するのを防げます。

> **ヒント:** 複数のフィールドがある場合は、異なる矩形で切り抜きステップを繰り返し、各領域ごとに OCR を実行してください。

---

## 手順 4: OCR エンジンの初期化 – 「OCR の実行方法」コア

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **内部的に何が起きているか:** Aspose OCR は Tesseract と独自の画像解析を組み合わせて動作します。エンジンを一度だけインスタンス化し、複数画像で再利用する方が、毎回新規オブジェクトを作成するより効率的です。

---

## 手順 5: 切り抜いた画像を渡してテキストを認識 – 画像からテキストを抽出する方法

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### 期待される出力

ROI に「Invoice #12345 – Paid」という文言が含まれていれば、次のような結果が得られます。

```
Invoice #12345 – Paid
```

OCR がうまく認識できない場合、余計なスペースや文字の誤認識（例: “Invo1ce #I2345 – Pa1d”）が出ることがあります。そこで **OCR 用画像前処理** のテクニック、たとえばコントラスト調整や二値化を適用します。Aspose にはステップ 5 の前にチェーンできる追加フィルタが用意されていますが、上記の基本フローでほとんどのクリーンなスキャンは処理可能です。

---

## 手順 6: オプション – OCR 設定の微調整（高度な「OCR の実行方法」）

特定言語での精度向上や、不要な文字を無視したい場合はエンジンを調整できます。

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **使用シーン:** 文書に装飾記号が多数含まれ、認識から除外したい場合に有効です。ブラックリストを設定すると誤検出が減ります。

---

## 完全なエンドツーエンドスクリプト

すべてを統合した、**画像を回転**し、**OCR 用画像前処理** を行い、最終的に **画像からテキストを認識** する実行可能スクリプトは以下の通りです。

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

このスクリプトを実行すると、認識結果がコンソールに出力され、処理された ROI のビジュアルが `processed_roi.png` として保存されます。PNG を開いて回転と切り抜きが期待通りに行われたか確認してください。

---

## よくある質問と落とし穴

| 質問 | 回答 |
|----------|--------|
| **画像がすでに正しい向きだった場合は?** | 回転ステップは冪等ではありません。正しい向きの画像を 90° 回転させると明らかに崩れます。したがって `source_image.width` と `height` を比較するか、EXIF の向き情報を利用してから `rotate_flip` を呼び出すべきです。 |
| **OCR の出力に余計な改行が入る。** | `result.get_text().replace("\n", " ").strip()` で整形するか、`ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` を有効にしてください。 |
| **PDF を直接処理できるか?** | はい。Aspose Imaging は PDF ページを画像として読み込めます（`Image.load("file.pdf")`）。その後は同じ回転・OCR 手順を適用します。 |
| **多数のファイルをバッチ処理したい。** | ディレクトリを走査するループで `ocr_rotated_image` を呼び出すか、`concurrent.futures` を使って並列化してください。 |
| **英語以外の言語を扱うには?** | `ocr_engine.get_recognition_settings().set_recognition_language("fr")` のように認識言語を設定すれば、フランス語などにも対応できます。 |

---

## 結論

**画像を正しく回転**させ、**画像前処理で関心領域を切り抜き**、そして **OCR を実行**して **画像からテキストを抽出**する方法を学びました。提示したスクリプトは実務でそのまま使えるワークフローで、任意の自動化パイプラインに組み込めます。

さらに踏み込むなら、以下を試してみてください。

- **画像強調**（コントラスト、二値化）を OCR 前に実施
- **複数 ROI の抽出**でフォーム内の複数フィールドを処理
- **フォルダ単位のバッチ処理**で大量スキャン文書を一括処理
- **下流システムとの連携**（例: 抽出データをデータベースに投入）

コードを自分のユースケースに合わせてカスタマイズし、楽しいコーディングを！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}