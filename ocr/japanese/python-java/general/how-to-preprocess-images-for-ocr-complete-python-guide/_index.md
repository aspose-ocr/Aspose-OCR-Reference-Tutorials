---
category: general
date: 2026-06-06
description: Python を使った OCR 用画像の前処理方法。Otsu 法で画像を二値化する方法、スキャンした文書の傾きを補正する方法、そしてドイツ語テキストの
  OCR 精度を向上させる方法を学びます。
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: ja
og_description: PythonでOCR用に画像を前処理する方法。このチュートリアルでは、Otsu法を用いた画像の二値化、スキャンした文書の傾き補正、そしてドイツ語画像のOCR精度を向上させる方法を示します。
og_title: OCR用画像の前処理方法 – 完全Pythonガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: OCRのための画像前処理方法 – 完全Pythonガイド
url: /ja/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像前処理の完全ガイド（Python）

画像を OCR 用に **前処理する方法** を知りたくありませんか？テキストがくっきりと抽出できるようにしたいですよね。特にノイズが多いドイツ語のスキャンページは、どの OCR エンジンにとっても悪夢です。朗報です！数ステップの賢い前処理で、ぼやけた斑点だらけのスキャンを、機械が読み取りやすいクリーンな画像に変えることができます。

このチュートリアルでは、Python を使って **画像を OCR 用に前処理する方法** を実例で解説します。**Otsu による二値化**、**スキャン文書の傾き補正（デスキュー）**、そして **ドイツ語画像からテキストを抽出** する際の **OCR 精度向上** のポイントを学びます。余計な説明は省き、すぐにコピー＆ペーストできる実働スクリプトを提供します。

## 必要なもの

- **Python 3.9+**（最近のバージョンならどれでも可）
- `OcrEngine` クラスを提供する OCR ライブラリ – デモでは汎用的な `ocr` パッケージを想定しています。`pip install ocr-lib` でインストールしてください。
- テスト用のノイズが多いドイツ語スキャン画像（`noisy_german_scan.tif`）
- Python 関数の基本的な理解（`def` が書ければ問題なし）

> **プロのコツ:** 別の OCR SDK（例: `pytesseract` 経由の Tesseract）を使う場合でも、概念は同じです。メソッド名だけ置き換えてください。

## ソリューションの概要

1. **OCR エンジンのインスタンスを作成**  
2. **認識言語をドイツ語に設定**  
3. **デスキュー、デノイズ、二値化（Otsu）、コントラスト伸長を含むカスタム前処理パイプラインを構築**  
4. **パイプラインをエンジンに登録** して、すべての画像が自動的に通過するようにする  
5. **ノイズの多いドイツ語スキャンに対して OCR を実行**  
6. **抽出されたテキストを出力** して結果を確認  

以下で各ステップを分解し、**なぜ重要か** を説明しながら、必要なコードを示します。

![how to preprocess images for OCR example](image.png "how to preprocess images for OCR example")

## ステップ 1: OCR エンジンのインスタンスを作成

まずはエンジンがなければ何も起きません。`OcrEngine` オブジェクトは、以降のすべての処理を統括するエントリーポイントです。

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*重要ポイント:* エンジンの初期化で内部リソース（言語モデルなど）が確保され、後からカスタムパイプラインを付けられるクリーンな状態になります。

## ステップ 2: 認識言語をドイツ語に設定

OCR の精度は言語に大きく依存します。エンジンにドイツ語を期待させることで、正しい文字セットとモデルが有効になります。

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

この設定を省くと、エンジンはデフォルトで英語になる可能性があり、ウムラウト（ä, ö, ü）や ß が正しく認識されません。ドイツ語スキャンではよくある落とし穴です。

## ステップ 3: カスタム前処理パイプラインを構築

ここが **画像を OCR 用に前処理する方法** の核心です。4 つの変換をチェーンします。

| 変換 | 内容 | 効果 |
|------|------|------|
| **Deskew** | 画像を水平に回転させる（最大 5°） | スキャンは完璧に揃っていることは稀です。傾きを除去することで文字分割が容易になります。 |
| **Denoise** | ランダムな斑点を低減（強度 0.7） | ノイズは偽のエッジを生み、OCR が文字と誤認する原因になります。 |
| **Binarize (Otsu)** | Otsu 法で白黒二値化 | クリーンな二値画像は、前景（文字）と背景のコントラストを最大化します。 |
| **Contrast Stretch** | ダイナミックレンジを拡張 | 薄い筆跡や古い文書の可読性が向上します。 |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### スキャン文書の傾き補正（デスキュー）の方法

上記の `deskew` 呼び出しが **スキャン文書の傾き補正（デスキュー）** の具体例です。内部ではハフ変換で支配的なテキストライン角度を推定し、画像を回転させます。回転角が 5° を超える場合は `max_angle` を上げてください。ただし過度な回転はアーティファクトの原因になるので注意が必要です。

### Otsu による二値化

`binarize(method="otsu")` 行は **Otsu による二値化** の直接的な回答です。Otsu のアルゴリズムはクラス間分散を最小化する閾値を算出し、暗い文字と明るい背景という二峰性ヒストグラムに最適です。

## ステップ 4: パイプラインをエンジンに登録

ここで作成したパイプラインを OCR エンジンに結び付け、すべての入力画像が自動的に前処理されるようにします。

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*重要ポイント:* 登録しなければエンジンは生のスキャンをそのまま処理し、先ほど設定したクリーニングは無視されます。このステップが **OCR 精度を向上させる方法** の鍵です。

## ステップ 5: ノイズの多いドイツ語スキャンからテキストを認識

すべてを組み合わせます。エンジンにノイズの多いドイツ語画像を渡し、重い処理を任せます。

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

パフォーマンスが気になる場合は、呼び出し時間を測定できます。

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## ステップ 6: 認識結果を出力

最後に抽出された文字列を表示します。これが **ドイツ語画像からテキストを抽出** する直接的な答えです。

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### 期待される出力例

サンプルスキャンに「Die schnelle braune Füchsin springt über den faulen Hund.」という文が含まれていると仮定すると、次のような出力が得られるはずです。

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

出力にまだ文字化けが残る場合は、`denoise` の強度を調整するか、`max_angle` を大きくしてデスキューを強化してください。

## よくある落とし穴と対処法

- **言語モデルが欠如:** `set_recognition_language(Language.GERMAN)` を忘れるとウムラウトが抜け落ちます。呼び出しを必ず確認してください。  
- **過度なデノイズ:** 強度が 0.9 を超えると細い筆跡が消えてしまいます。多くの場合は 0.5‑0.7 が安全です。  
- **ファイル形式の不一致:** マルチページ TIFF に弱いエンジンがあります。マルチページ文書は単ページファイルに分割してから処理しましょう。  
- **パイプラインの順序:** 示した順序（デスキュー → デノイズ → 二値化 → コントラスト伸長）は意図的です。二値化を先に行うとノイズが固定化され、後から除去できません。必ずデノイズを先に実行してください。

## パイプラインの拡張（次のステップは？）

ベースラインができたら、以下のような拡張を検討できます。

- **形態学的オープニング**で微小ブロブを除去（`.morph_open(kernel=3)`）  
- **言語モデル統合**で事後補正（`ocr_engine.apply_spellcheck()`）  
- **バッチ処理の並列化**（`concurrent.futures`）で大規模データセットを高速化  

これらはすべて **画像を OCR 用に前処理する方法** の核を保ちつつ、**OCR 精度を向上させる方法** をさらに強化します。

## 結論

本稿では **画像を OCR 用に前処理する方法** を、エンジン作成・ドイツ語設定・Otsu による二値化・スキャン文書の傾き補正・テキスト抽出という 6 ステップで網羅しました。これらを実行すれば、認識品質が目に見えて向上し、手作業での修正が激減します。

ぜひ自分のスキャンでスクリプトを試し、パラメータを調整して結果を確かめてみてください。特定の前処理に関する質問があればコメントで教えてください。一緒に深掘りしていきましょう。

Happy coding, and may your OCR be ever accurate!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能習得や別実装への展開に役立ちます。

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}