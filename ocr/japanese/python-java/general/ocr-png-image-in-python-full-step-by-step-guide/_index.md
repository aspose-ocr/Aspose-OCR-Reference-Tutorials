---
category: general
date: 2026-06-06
description: PythonでPNG画像のOCR – 画像からテキストを抽出する方法を学び、PythonのOCRサンプルを実行し、さらには古代ギリシャ語のテキストまで簡単に読むことができます。
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: ja
og_description: PythonでのOCR PNG画像の解説。このガイドでは、画像からテキストを抽出する方法、PythonのOCR例を実行する方法、そして古代ギリシャ語を簡単に読む方法を示します。
og_title: PythonでPNG画像のOCR – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: PythonでPNG画像のOCR – 完全ステップバイステップガイド
url: /ja/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCR PNG画像 – 完全ステップバイステップガイド

Pythonスクリプトだけで **OCR PNG image** ファイルを処理する方法を考えたことはありませんか？スキャンした古代写本がたくさん入ったフォルダーがあり、**extract text from image** ファイルを手作業で入力せずに取得したいかもしれません。良いニュースは、コンピュータビジョンの博士号は不要で、数行のコードと適切なライブラリさえあれば、数秒で古代ギリシャ語を読むことができるということです。

このチュートリアルでは、PNG からテキストを認識し、言語をギリシャ語（ポリトニック）に設定して結果を出力する **python OCR example** を順を追って解説します。最後まで読むと、**recognize image text** のやり方、一般的な落とし穴の対処法、他の言語や画像形式へのスクリプトの拡張方法が正確に分かります。

## What You’ll Learn

- Python OCR ライブラリ（pytesseract + Tesseract OCR）のインストールと設定方法
- OCR エンジンのインスタンス作成と PNG ファイルの読み込み
- 言語をギリシャ語ポリトニックに設定して **read ancient greek** を実現する方法
- 認識結果の出力と典型的な問題のトラブルシューティング
- 複数の PNG をバッチ処理したり、別の言語に切り替える方法の拡張

### Prerequisites

| 要件 | 重要な理由 |
|------|------------|
| Python 3.8+ | モダンな構文と型ヒント |
| `pytesseract` パッケージ | Tesseract エンジンの薄いラッパー |
| Tesseract OCR バイナリ（≥ 5.0） | 実際に重い処理を行うエンジン本体 |
| Greek language data (`grc.traineddata`) | **read ancient greek** を正しく行うために必要 |
| 解析したい PNG 画像（例: `ancient_greek.png`） | **ocr png image** デモの対象 |

Python 側は次のコマンドでインストールできます：

```bash
pip install pytesseract Pillow
```

Ubuntu/macOS ではエンジン本体を次のように追加します：

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Greek ポリトニックの学習データのダウンロードを忘れずに：

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(パスは環境により異なる場合があります。必要に応じて `TESSDATA_PREFIX` を調整してください。)*

---

## OCR PNG Image: Create the Engine Instance

最初に必要なのは Tesseract とやり取りするオブジェクトです。`pytesseract` ではモジュールレベルの関数でエンジンにアクセスしますが、分かりやすさのために小さなクラスでラップします。これは元のスニペットで見た「エンジン」概念を模倣したものです。

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**ラップする理由**  
- 元のスニペットと同じ公開 API を保ち、移行をスムーズにするため。  
- 後からロギングやエラーハンドリングを追加しやすくするため。  
- 上級開発者が評価する良い OOP 実践を示すため。

---

## Extract Text from Image: Set the Language to Greek Polytonic

エンジンが用意できたら、どの言語を認識させるかを指定します。ギリシャ語ポリトニックは標準の “greek” データではカバーできないアクセントがあるため、`grc` の学習ファイルを指す必要があります。

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

別の言語で **extract text from image** を行いたい場合は、`"grc"` を `"eng"`（英語）や `"fra"`（フランス語）など、インストール済みの言語コードに置き換えるだけです。同じ行がどの言語でも機能します。

---

## Recognize Image Text: Run the OCR on a PNG

言語設定が済んだら PNG をエンジンに渡します。元の例はハードコードされたパスでしたが、ここでは `Path` オブジェクトを使って柔軟性を持たせます。

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tips & Edge Cases**

- **File not found** – `try/except FileNotFoundError` でラップし、分かりやすいメッセージを出す。  
- **Low‑resolution PNG** – OCR 前に Pillow でリサイズや二値化など前処理を検討。  
- **Non‑Greek text** – 言語が合わないと精度が大幅に低下します。必ず対象言語を合わせましょう。

---

## Output the Recognized Text

最後に結果を出力します。実際のプロジェクトではデータベースや CSV、あるいは翻訳パイプラインに渡すこともあるでしょう。

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

クリアな古代ギリシャ語の碑文をスキャンした画像でスクリプトを実行すると、以下のような出力が得られます：

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

出力が文字化けしている場合は、**greek.traineddata** が正しいフォルダーにあるか、PNG がノイズ過多でないかを再確認してください。

---

## Full Working Example (All Steps in One Script)

以下は完成形のスクリプトです。`ocr_greek.py` として保存し、`python ocr_greek.py` で実行してください。

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Expected output**（抜粋）：

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

正しくギリシャ文字が表示されれば、Python で **ocr png image** を実行できたことになります。おめでとうございます！

---

## Common Questions & Pro Tips

### How do I improve accuracy on a noisy PNG?

- 画像をグレースケールに変換: `img = img.convert('L')`  
- 二値化し閾値を適用: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`  
- `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)` で拡大

これらの手順で **recognize image text** の失敗ケースをクリーンな結果に変えることができます。

### Can I process a whole folder of PNGs?

もちろんです。`recognize_image` 呼び出しを `Path.glob("*.png")` のループで包み、結果を辞書に格納するか CSV に書き出すだけです。

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### What if I need to extract numbers only?

`image_to_string` にカスタム **config** 文字列を渡します：

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

これでテーブルやシリアル番号、タイムスタンプなど数字だけを含む **extract text from image** が可能になります。

### Is there a way to get confidence scores?

はい、`pytesseract.image_to_data` を使うと単語ごとの信頼度（confidence）を含む TSV が返ります。低信頼度のトークンを除外して最終文字列を組み立てることができます。

---

## Extending the Tutorial

基本をマスターしたら、以下の関連トピックにも挑戦してみてください。

- **Batch OCR with multiprocessing** – 大量の PNG コーパスを高速化  
- **Hybrid OCR + NLP pipelines** – 抽出した古代ギリシャ語を自動で現代英語に翻訳  
- **Alternative engines** – `easyocr` や `opencv` ベースの手法を特定ユースケースで試す  
- **Cloud OCR services** – Google Vision、Azure Computer Vision、AWS Textract でサーバーレスにスケール

これらはすべて、今回扱った **python ocr example** を土台にしているので、次のステップへスムーズに進めます。

---

## Conclusion

シンプルなスニペットを、Python で堅牢な **ocr png image** ワークフローに変換しました。`OcrEngine` を作成し、言語をギリシャ語ポリトニックに設定し、PNG を読み込んで結果を出力することで、**extract text from image**、**recognize image text**、さらには **read ancient greek** まで実現できました。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで学んだテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [画像からテキストを抽出する Aspose OCR – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR 画像認識でしきい値を設定する方法](/ocr/english/net/ocr-settings/set-threshold-value/)
- [複数言語に対応した Aspose OCR でテキスト画像を認識する](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}