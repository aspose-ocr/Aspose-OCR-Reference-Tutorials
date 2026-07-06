---
category: general
date: 2026-03-18
description: 画像に対してOCRを実行し、テキストを素早く抽出します。OCR用に画像を読み込む方法、OCRエンジンの作成方法、そして言語オプションでOCR精度を向上させる方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: ja
og_description: この詳細なガイドで画像のOCRを実行しましょう。OCR用に画像を読み込む方法、OCRエンジンの作成、そして信頼できるテキスト抽出のためにOCR精度を向上させる方法を学びます。
og_title: 画像でOCRを実行する – 完全プログラミングチュートリアル
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: 画像でOCRを実行する – ステップバイステップガイド
url: /ja/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行する – 完全プログラミングチュートリアル

画像から **OCR を実行** したいけど、どのライブラリを選べばいいか、信頼できる結果を得るにはどうすればいいか分からないことはありませんか？このガイドでは、**画像からテキストを抽出** するために必要なすべてを、画像の読み込みから言語オプションの調整まで、ステップバイステップで解説します。**OCR の精度を向上させる** 方法も随所に紹介します。

**画像を OCR 用にロードする** 方法、**OCR エンジンを作成する** 方法、各設定がなぜ重要かを説明します。最後には、認識されたテキストを出力する実行可能なスクリプトが完成し、各行の「なぜ」も理解できるようになります。さっそく始めましょう。

## 必要なもの

- Python 3.8+（コードは f‑strings と型ヒントを使用しています）
- 仮想の `ocr_lib` パッケージ – `pip install ocr_lib` でインストール
- 明瞭な印刷文字が含まれる画像ファイル（例: `lab_report.png`）
- 基本的なテキストエディタまたは IDE（VS Code、PyCharm などお好みのもの）

これらがすでに揃っていれば完了です。まだの場合は python.org から Python を取得し、pip コマンドを実行してください。数分で準備できます。

![perform OCR on image example](/images/ocr-example.png)

*Alt text: 画像で OCR を実行する – 抽出されたテキストを示すサンプル出力。*

## Step 1: OCR エンジンを作成 – Python で **OCR エンジンを作成する** 方法

認識を行う前に、ライブラリは設定と実行時状態を保持するエンジンオブジェクトを必要とします。エンジンは操作の「脳」と考えてください。

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**なぜ重要か:** エンジンを早めにインスタンス化しておくと、後から言語オプションを付加でき、内部モデルがキャッシュされるため、次回以降の呼び出しが高速になります。

## Step 2: OCR 用に画像をロードする – 正しい **画像を OCR 用にロードする** 方法

エンジンができたら、次は読み込む対象を渡す必要があります。`setImageFromFile` メソッドはファイルシステム上のパスを受け取ります。パスは絶対でも相対でも構いませんが、スクリプトの作業ディレクトリからの相対である必要があります。

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**プロのコツ:** 絶対パスまたは `os.path.join` を使用して、スクリプトを別フォルダから実行したときに「ファイルが見つからない」エラーを防ぎましょう。

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Step 3: OCR 精度を向上させる – **言語オプション** を調整して **OCR 精度を向上させる**

デフォルトの OCR は動作しますが、ラボ用語などドメイン固有の語彙は誤認識しやすいです。カスタム辞書とブラックリストを提供することで、たとえば「0」と「O」の混同といったミスを減らせます。

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**なぜ効果があるか:** 辞書は OCR モデルに「HPLC」は有効なトークンであることを教え、単語が意味不明に分割されるのを防ぎます。ブラックリストは曖昧な記号をノイズとして扱うよう指示し、直接 **OCR 精度を向上させます**。

## Step 4: 画像で OCR を実行する – コアの **画像で OCR を実行する** 呼び出し

エンジンが準備でき、画像が添付されたら、実際にテキスト認識を行います。このステップは `OcrResult` オブジェクトを返し、生テキスト、信頼度スコア、バウンディングボックスなどを取得できます。

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

画像がぼやけている場合、結果の信頼度が低くなります。これは画像を前処理（コントラスト増加など）してからエンジンに渡すべきサインです。

## Step 5: 画像からテキストを抽出する – 最終的な文字列を取得

最後に、`OcrResult` からテキスト表現を取得します。`getText()` メソッドはプレーンテキストの文字列を返し、ファイル保存やデータベースへの投入など、後続処理にすぐ使えます。

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**期待される出力:** `lab_report.png` にシンプルな表が含まれていると仮定すると、次のような結果が得られるかもしれません。

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

これで **画像からテキストを抽出する** パートは完了です。

## 完全動作例 – すべてをまとめる

以下は、前述の各セクションをつなげた単一スクリプトです。`run_ocr.py` にコピペして、`python run_ocr.py` を実行してください。

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### 簡易検証チェックリスト

| ✅ | Item |
|---|------|
| ✔️ | エンジンが作成されている（`create OCR engine`） |
| ✔️ | 画像がロードされている（`load image for OCR`） |
| ✔️ | 言語オプションが設定されている（`improve OCR accuracy`） |
| ✔️ | OCR が実行されている（`perform OCR on image`） |
| ✔️ | テキストが抽出されている（`extract text from image`） |

スクリプトを実行し、コンソールを確認してください。「OCR Output」ブロックにレポートの内容が表示されれば、**画像で OCR を実行した**ことになります。

## よくある落とし穴と回避策

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **ぼやけた入力** | OCR モデルが文字を判別できない | OpenCV で前処理：`cv2.GaussianBlur` や DPI の増加 |
| **言語設定が間違っている** | デフォルト言語が英語以外に設定されている可能性 | `engine.setLanguage("eng")` を `recognize()` の前に呼び出す |
| **辞書に欠けている用語** | ドメイン固有の単語が文字化けする | Step 3 のように `setDictionary` で追加 |
| **ブラックリストの文字が原因** | 重要な記号が除外されている | 必要に応じてブラックリストを調整 |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}