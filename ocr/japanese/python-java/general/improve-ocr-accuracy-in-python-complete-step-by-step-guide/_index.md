---
category: general
date: 2026-05-31
description: Pythonで画像を前処理し、OCRの精度を向上させましょう。画像ファイルからテキストを抽出する方法、PNGからテキストを認識する方法、そして結果を高めるコツを学びます。
draft: false
keywords:
- improve OCR accuracy
- preprocess image for OCR
- extract text from image
- recognize text from PNG
- image preprocessing for text
language: ja
og_description: テキストのために画像前処理を適用して、PythonでOCR精度を向上させましょう。このガイドに従って、画像ファイルからテキストを抽出し、PNGからのテキスト認識を簡単に行いましょう。
og_title: PythonでOCR精度を向上させる – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  headline: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Improve OCR accuracy with Python by preprocessing images for OCR. Learn
    how to extract text from image files, recognize text from PNG, and boost results.
  name: Improve OCR Accuracy in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Loads the PNG into memory
    text: Loads the PNG into memory
  - name: Applies denoise and deskew based on our settings
    text: Applies denoise and deskew based on our settings
  - name: Runs the neural‑network or classic pattern matcher
    text: Runs the neural‑network or classic pattern matcher
  - name: Packages the output into `recognition_result`
    text: Packages the output into `recognition_result`
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: PythonでOCRの精度を向上させる – 完全ステップバイステップガイド
url: /ja/python-java/general/improve-ocr-accuracy-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでOCR精度を向上させる – 完全ステップバイステップガイド

OCR精度を **向上させよう** としたのに文字化けしたことはありませんか？ あなただけではありません。多くの開発者が、画像がノイズだらけだったり、傾いていたり、コントラストが低すぎると壁にぶつかります。朗報です！ いくつかの前処理テクニックを使えば、ぼやけたスクリーンショットでもクリーンな機械可読テキストに変えることができます。

このチュートリアルでは、**画像をOCR用に前処理**し、認識エンジンを実行し、最終的に **画像からテキストを抽出** する実践的な例を順を追って解説します（対象はPNG）。最後まで読めば、**PNGからテキストを認識** する方法と、成功率の高い再利用可能なコードスニペットを手に入れられます。

## 学べること

- OCRエンジンにとって画像前処理が重要な理由  
- 効果が大きい前処理モード（ノイズ除去、傾き補正）  
- Pythonで `OcrEngine` インスタンスを設定する方法  
- **画像からテキストを抽出** する完全実行可能スクリプト  
- 回転スキャンや低解像度画像などのエッジケースへの対処法  

OCR SDK 以外の外部ライブラリは不要ですが、Python 3.8 以上と、読み取り対象の PNG 画像が必要です。

---

![Diagram showing steps to improve OCR accuracy in Python](image.png "Improve OCR accuracy workflow")

*Alt text: OCR精度向上ワークフロー図（前処理と認識のステップを示す）*

## 前提条件

- Python 3.8 以上がインストール済み  
- `OcrEngine`、`OcrEngineSettings`、`ImagePreprocessMode` を提供する OCR SDK にアクセスできること（以下のコードは汎用 API を使用しています。必要に応じてベンダー提供のクラスに置き換えてください）  
- 読み取り対象の PNG 画像（`input.png`）を参照できるフォルダーに配置してあること  

仮想環境を使用している場合は、今すぐ有効化してください。特別なことは不要で、`python -m venv venv && source venv/bin/activate` で OK です。

---

## Step 1: OCRエンジンインスタンスの作成 – OCR精度向上の第一歩

まず最初に必要なのは OCR エンジンオブジェクトです。ピクセルを読み取り文字に変換する「脳」のようなものです。

```python
# Step 1: Initialise the OCR engine
ocr_engine = OcrEngine()
```

**ポイント**: エンジンが無ければ前処理を適用できず、画像はそのまま認識器に渡されます。これは精度が最も低くなる典型的なケースです。

---

## Step 2: 対象PNGの読み込み – PNGからテキストを認識する準備

次にエンジンに処理対象のファイルを指定します。PNG はロスレス形式なので、JPEG に比べて若干有利です。

```python
# Step 2: Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

画像が別の場所にある場合はパスを調整してください。エンジンはサポートされている形式であれば何でも受け付けますが、PNG は文字エッジの細部を保持しやすいという利点があります。

---

## Step 3: 前処理の設定 – OCR用に画像を前処理

ここが本番です。設定オブジェクトを作成し、ノイズ除去で斑点を除去し、傾き補正で斜め文字を自動的に水平にします。

```python
# Step 3: Prepare preprocessing settings to improve accuracy
preprocess_settings = OcrEngineSettings()
preprocess_settings.preprocess_mode = (
    ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
)
```

### なぜ Denoise + Deskew が重要か？

- **Denoise**: ランダムなピクセルノイズはパターンマッチングアルゴリズムを混乱させます。除去することで文字が鮮明になります。  
- **Deskew**: たった 2 度の傾きでも信頼度が大幅に低下します。傾き補正でベースラインを揃えると、認識器がフォントを正確にマッチさせやすくなります。

画像が特に暗い場合は `ImagePreprocessMode.CONTRAST_ENHANCE` などのフラグを追加で試すと良いでしょう。利用可能なモードは SDK のドキュメントに一覧があります。

---

## Step 4: エンジンへ設定を適用 – 前処理をOCRに紐付け

設定オブジェクトをエンジンに割り当てることで、次回の認識実行時に先ほど定義した変換が自動的に適用されます。

```python
# Step 4: Apply the settings to the engine
ocr_engine.settings = preprocess_settings
```

このステップを省略すると、エンジンはデフォルト設定（多くの場合「前処理なし」）にフォールバックし、**OCR精度が低下** します。

---

## Step 5: 認識プロセスの実行 – 画像からテキストを抽出

すべてが接続されたら、エンジンに仕事を依頼します。呼び出しは同期的で、認識された文字列を含む結果オブジェクトが返ります。

```python
# Step 5: Run the recognition process
recognition_result = ocr_engine.recognize()
```

内部ではエンジンが次の手順を実行します：

1. PNG をメモリにロード  
2. 設定に基づきノイズ除去と傾き補正を適用  
3. ニューラルネットまたは従来のパターンマッチャで認識  
4. 出力を `recognition_result` にパッケージ化  

---

## Step 6: 認識結果の出力 – 改善効果を確認

抽出した文字列をコンソールに出力します。実際のアプリではファイルやデータベースに保存したり、別サービスに渡したりすることもあります。

```python
# Step 6: Output the recognized text
print(recognition_result.text)
```

### 期待される出力例

画像に「Hello, OCR World!」という文が含まれていれば、次のように表示されます：

```
Hello, OCR World!
```

テキストがきれいに出力されていることが分かりますね。余計な記号や文字化けがないのは、**テキスト用画像前処理** が正しく機能した結果です。

---

## プロ向けヒント & エッジケース

| 状況 | 調整すべき項目 | 理由 |
|-----------|----------------|-----|
| 非常に低解像度の PNG（≤ 72 dpi） | `ImagePreprocessMode.SUPER_RESOLUTION` が利用可能なら追加 | アップサンプリングで認識器に与えるピクセル数を増やす |
| 文字が 5° 超で回転している | デスクエア許容範囲を上げるか、`Pillow` で事前に回転させる | 大きな角度は自動デスクエアが追いつかないことがある |
| 背景にパターンが多い | `ImagePreprocessMode.BACKGROUND_REMOVAL` を有効化 | テキスト以外のノイズが誤認識されるのを防止 |
| 多言語文書 | `ocr_engine.language = "eng+spa"` などに設定 | 正しい文字セットを選択することで全体的な精度が向上 |

**OCR精度を向上させる** には一律の解決策はありません。データセットに合わせて前処理フラグを調整する必要があります。

---

## 完全スクリプト – コピー＆ペーストで即利用

以下は本チュートリアルで説明したすべての手順を組み込んだ、実行可能なサンプルです。`improve_ocr_accuracy.py` として保存し、`python improve_ocr_accuracy.py` で実行してください。

```python
"""
Improve OCR Accuracy in Python – Full Example
Author: Your Name (2026)
Requires: OCR SDK providing OcrEngine, OcrEngineSettings, ImagePreprocessMode
"""

# Import the necessary classes from the OCR SDK
from ocr_sdk import OcrEngine, OcrEngineSettings, ImagePreprocessMode

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the PNG you want to read
    image_path = "YOUR_DIRECTORY/input.png"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure preprocessing: denoise + deskew
    preprocess_settings = OcrEngineSettings()
    preprocess_settings.preprocess_mode = (
        ImagePreprocessMode.DENOISE | ImagePreprocessMode.DESKEW
    )

    # 4️⃣ Apply the settings
    ocr_engine.settings = preprocess_settings

    # 5️⃣ Run recognition
    recognition_result = ocr_engine.recognize()

    # 6️⃣ Print the extracted text
    print("=== Recognized Text ===")
    print(recognition_result.text)

if __name__ == "__main__":
    main()
```

実行するとコンソールに **画像からテキストを抽出** した結果がすぐに表示されます。出力が期待と異なる場合は、上記「プロ向けヒント」表にあるように `preprocess_mode` フラグを調整してみてください。

---

## まとめ

本稿では、Python を使って **OCR精度を向上させる** 実践的なレシピを紹介しました。`OcrEngine` を作成し、PNG を読み込み、**OCR用に画像を前処理** し、最終的に **PNGからテキストを認識** することで、元画像が完璧でなくても安定して **画像からテキストを抽出** できるようになります。

次のステップは？ 画像のバッチ処理をループで回し、結果を CSV に保存したり、追加の前処理モード（コントラスト強調など）を試したりしてみましょう。同様の手順は PDF、スキャン領収書、手書きメモにも応用できます—入力形式を変えて設定だけ調整すれば OK です。

特定の画像タイプについて質問がある、あるいはウェブサービスへの組み込み方を知りたいときはコメントで教えてください。一緒にシナリオを検討します。コーディングを楽しんで、OCR の結果が常にクリアになることを願っています！

## 次に学ぶべきこと

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}