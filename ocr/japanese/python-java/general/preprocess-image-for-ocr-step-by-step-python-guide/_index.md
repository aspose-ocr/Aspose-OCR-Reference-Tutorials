---
category: general
date: 2026-06-22
description: PythonでAspose OCRを使用して、画像からテキストを抽出し、OCR精度を向上させるために画像を前処理します。完全な実行可能サンプルが含まれています。
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: ja
og_description: OCR用に画像を前処理し、画像からテキストを抽出し、Aspose OCRでOCR精度を向上させます。Pythonで完全なワークフローを学びましょう。
og_title: OCR用画像前処理 – 完全Pythonチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR用画像前処理 – ステップバイステップ Python ガイド
url: /ja/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像前処理 – 完全 Python チュートリアル

もし **OCR 用画像前処理** が必要なら、ノイズの多いスキャン、傾いたページ、あるいは協調しない低コントラストの写真に直面したことがあるでしょう。画像からテキストを抽出しようとして、文字化けした結果になることはありませんか？ そんな時に、しっかりした前処理チェーンが、数語の読めるテキストと、完全な文字起こしの悪夢との違いを生み出します。

このガイドでは、Aspose OCR for Python を使用して **画像からテキストを抽出** し、さらに **OCR の精度を向上** させる方法を示す、完全なエンドツーエンドの例を順に解説します。曖昧な説明はありません—コピー＆ペーストできるコード、各行の背後にある考え方、実際のケースに役立つヒントだけを提供します。

## 本チュートリアルで得られるもの

- ノイズの多いドキュメントを読み込み、クリーンアップし、認識されたテキストを出力する、すぐに実行できる Python スクリプト。  
- 各前処理フィルタがなぜ重要か、パラメータをどのように調整すべきかの理解。  
- 大量の斑点ノイズ、極端な回転、低コントラストスキャンなど、一般的な落とし穴への対処戦略。  

### 前提条件

| 要件 | 重要性 |
|------|--------|
| Python 3.8+ | Aspose OCR の wheel は最新のインタプリタを対象としています。 |
| `aspose-ocr` パッケージ (`pip install aspose-ocr`) | `OcrEngine`、`ImagePreprocessor`、フィルタクラスを提供します。 |
| サンプル画像 (例: `noisy-document.jpg`) | 前処理による効果を示すために、意図的に乱れた画像を使用します。 |
| Python 関数の基本的な知識 | スクリプトを自分のパイプラインに合わせて調整しやすくなります。 |

> **プロのコツ:** Windows を使用している場合は、バージョン衝突を防ぐために仮想環境内でスクリプトを実行してください。

---

## Aspose OCR (Python) を使用した画像前処理

以下はチュートリアルの核心部分です—ステップバイステップでコードを分解します。各セクションでは **何を** 行っているか、そして **なぜ** 行っているかを説明するので、後でパイプラインを調整する際に推測する必要はありません。

![preprocess image for OCR example](ocr-preprocess.png){alt="OCR 用画像前処理の例"}

### ステップ 1 – OCR エンジンの初期化とソース画像の読み込み

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **なぜ** `OcrEngine`？ それは認識器、言語設定、（後で）前処理器をカプセル化します。  
- **なぜ** `ImageStream.from_file`？ ファイルタイプの処理を抽象化し、コード変更なしで JPEG から PNG に切り替えられます。

### ステップ 2 – 画像をクリーンアップする前処理チェーンの構築

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**これらのフィルタが OCR 精度を向上させる方法:**  
- **Deskew** は文字分割を混乱させる一般的な「ページが傾いている」問題を除去します。  
- **Despeckle** は低品質スキャナで生じる斑点に対処します。強度を上げるとノイズが多く除去されますが、細部が失われる可能性があります。  
- **ContrastBoost** は暗い文字を明るい背景から際立たせ、ほとんどの OCR エンジンで効果的です。

> **エッジケース:** 文書がすでに完全に真っ直ぐであれば、`Deskew()` をスキップして数ミリ秒の処理時間を節約できます。

### ステップ 3 – 前処理器をエンジンに接続

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

これで `ocr_engine.recognize()` が実行されるたびに、最初に定義した順序で3つのフィルタが適用されます。順序は重要です：**デスクュー（deskew）をデスぺックル（despeckle）より先に** 行う必要があります。さもなければ、斑点フィルタが回転したエッジをノイズと誤認識する可能性があります。

### ステップ 4 – OCR を実行し、画像からテキストを抽出

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- `recognize()` 呼び出しは、純粋なテキストだけでなく、信頼度スコア、バウンディングボックス、言語情報も保持する `RecognitionResult` オブジェクトを返します。  
- ここでは単純な文字列だけが必要ですが、`recognition_result.get_confidence()` を調べることで **OCR 精度向上** の簡易チェックが可能です。

### ステップ 5 – 出力を確認し、精度向上のために微調整

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

出力にまだ文字化けが含まれる場合は、以下の調整を検討してください。

| 問題 | 推奨修正 |
|------|----------|
| テキストがまだぼやけている | `ContrastBoost(level)` を 2.0 に増やすか、デスぺックルの前に `ocr.Filters.GaussianBlur(radius=1)` を追加します。 |
| 余計な文字が多すぎる | `Despeckle(strength)` を 3 に上げるか、`ocr.Filters.RemoveLines()` を挿入して水平線を除去します。 |
| 傾きが残る | `ocr.Filters.Deskew(max_angle=5)` を呼び出して、軽度の回転のみを補正対象にします。 |

## 完全な実行可能スクリプト

`ocr_preprocess.py` という名前のファイルに以下のブロックをコピーしてください。`YOUR_DIRECTORY/noisy-document.jpg` を実際の画像パスに置き換え、`python ocr_preprocess.py` を実行します。

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

ノイズが多く、やや回転した JPEG でこのスクリプトを実行すると、クリーンで読みやすいテキストが得られます—これは、適切に設計された前処理チェーンが **OCR 精度を大幅に向上** させることを示しています。

## よくある質問と回答

**Q: マルチページ PDF でも動作しますか？**  
A: はい。各ページを画像に変換（例: `pdf2image` を使用）し、ループで同じパイプラインに流します。各ページに同じ `preprocess image for OCR` 手順が適用されます。

**Q: 文書が英語以外の言語の場合はどうすればよいですか？**  
A: 認識前に言語を設定します：`engine.set_language(ocr.Language.FRENCH)`。前処理フィルタは同じままで、言語モデルだけが変更されます。

**Q: さらにフィルタをチェーンできますか？**  
A: もちろんです。`ImagePreprocessor` は拡張可能で、`add_filter` を再度呼び出すだけです。ドットが多い背景には `ocr.Filters.MedianFilter(kernel=3)` が有用です。

## まとめ

私たちは **OCR 用画像前処理** を行い、Aspose のエンジンを実行し、**画像からテキストを抽出** しました。また、**OCR 精度向上** のためのいくつかのコツも紹介しました。完全な例はどのプロジェクトにもすぐに組み込め、モジュラーなフィルタ設計により、データに応じてステップを入れ替え、追加、削除できます。

次に、以下を検討してください：

- `concurrent.futures` を使用した数十件のスキャンの **バッチ処理**。  
- スペルチェックライブラリ（例: `pyspellchecker`）で **ポストプロセッシング** を行い、OCR が導入した誤字を修正。  
- Flask や FastAPI を使ってスクリプトをウェブサービスに **統合** し、オンデマンド OCR マイクロサービスに変換。

実際に試してフィルタ強度を調整し、認識率が上がるのを確認してください。問題があればコメントを残してください—ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれ、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR を使用した画像からテキスト抽出 – ステップバイステップガイド](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [.NET 用 AspOCR の使用方法：画像 OCR フィルタの前処理](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [画像からテキスト抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}