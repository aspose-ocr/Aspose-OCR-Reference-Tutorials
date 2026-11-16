---
category: general
date: 2026-03-28
description: PythonでROIをOCRする方法 – 特定の画像領域から正確にテキストを抽出するための前処理オプションの設定方法を学ぶ。
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: ja
og_description: PythonでROIをOCRする方法 – 本ガイドでは、定義された画像領域から信頼性の高いテキスト抽出を行うための前処理設定方法を示します。
og_title: PythonでROIをOCRする方法 – 前処理の設定方法
tags:
- OCR
- Python
- Aspose
title: PythonでROIをOCRする方法 – 前処理の設定方法
url: /ja/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PythonでROIをOCRする方法 – 前処理の設定方法

ノイズの多い請求書画像で、ページ全体をメモリに読み込まずに **how to OCR ROI** できるか、考えたことはありませんか？ あなただけではありません。実際のプロジェクトでは、顧客名、住所、合計金額など、ほんの数項目だけが必要なことが多く、文書全体をスキャンするのは過剰です。  

良いニュースがあります。Aspose OCR を使えば、エンジンに正確に **where to look** と指示し、さらに画像を事前にクリーンアップさせることができます。このチュートリアルでは、**how to set preprocessing** オプションの設定方法、Region of Interest（ROI）の定義方法、そして数行の Python でクリーンなテキストを抽出する手順を解説します。  

このガイドを終える頃には、任意の請求書、領収書、またはフォームから特定のブロックを抽出する、すぐに実行できるスクリプトが手に入ります。追加ツールは不要で、Aspose OCR と少しの Python ロジックだけで完結します。

---

## 必要なもの

- **Python 3.8+**（コードは最近のバージョンで動作します）  
- **Aspose OCR for Python via .NET** – `pip install aspose-ocr` でインストール  
- サンプル画像（例: `invoice.png`）を参照できるフォルダーに配置  
- Python の関数とオブジェクト指向構文に関する基本的な知識  

これらがすでに揃っているなら、素晴らしいです—すぐにコードに進みましょう。

![ROIボックスを示す how to OCR ROI 図](ocr-roi.png "How to OCR ROI の例")

*Alt text: 請求書画像上のROIボックスを示す how to OCR ROI 図*

---

## ステップ 1 – OCR エンジンの初期化 (How to OCR ROI)

エンジンに *where* を指示できるようになる前に、OCR プロセッサのインスタンスが必要です。このオブジェクトはすべての設定を保持し、認識処理を実行します。

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Why this matters*: `OcrEngine` クラスは重い処理（フォント検出、レイアウト解析など）を抽象化します。エンジンを一つだけ作成することで、画像ごとに重いリソースを再初期化する必要がなくなり、パフォーマンスが高速に保たれます。

---

## ステップ 2 – ソース画像の読み込み (How to OCR ROI)

Aspose Storage を使えば、画像の読み込みが簡単です。ファイルパスを指定すると、処理の準備ができた `Image` オブジェクトが取得できます。

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tip*: ストリーム（例: Web API 経由でアップロードされた画像）で作業している場合は、ファイルパスの代わりに `BytesIO` オブジェクトを `Image.load` に渡すことができます。

---

## ステップ 3 – Region of Interest（ROI）の定義

ここで核心の質問 **how to OCR ROI** に答えます：エンジンに関心のあるデータが入っている正確な矩形を指示します。各 ROI は左上隅（`x`, `y`）とサイズ（`width`, `height`）で定義されます。

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*ROI を使用する理由*  
- **Speed** – エンジンは画像の不要な部分をスキップします。  
- **Accuracy** – 小さな領域に集中することで、他のノイズが認識器を混乱させません。  
- **Flexibility** – 必要なだけ ROI を追加でき、エンジンは同じ順序で結果のリストを返します。

---

## ステップ 4 – OCR 精度向上のための前処理設定方法

スキャナーやスマートフォンから直接取得した画像は、しばしば歪み、低コントラスト、または不均一な照明に悩まされます。Aspose OCR は `PreprocessingOptions` オブジェクトを提供し、認識実行前に一般的な修正を有効にできます。

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*How this helps*:  
- **Deskew** – 文字形状を曖昧にする傾きを除去します。  
- **Binarize** – カラーノイズを減らし、OCR エンジンにクリーンな二値画像を提供します。  
- **Contrast** – 薄い筆跡を強調し、特に薄れた領収書に有効です。

これらのフラグを試してみてください—1つをオフにして出力が変わるか確認します。これが **how to set preprocessing** を効果的に行うコツです。

---

## ステップ 5 – 定義した ROI のみで OCR を実行

エンジン、画像、ROI、前処理が準備できたら、`recognize` を呼び出す時です。このメソッドは `OcrResult` オブジェクトを返し、`regions` コレクションを含みます—各エントリは提供した ROI の順序と一致します。

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Behind the scenes*: エンジンは各 ROI を切り取り、前処理パイプラインを適用し、クリーンなスニペットで認識モデルを実行します。リストを渡したため、結果は同じ順序を保持し、後処理がシンプルになります。

---

## ステップ 6 – 抽出したテキストの読み取りと利用 (How to OCR ROI)

最後に、`regions` リストを反復処理し、認識された文字列を出力（または保存）します。`Region` オブジェクトは Unicode 結果を保持する `text` プロパティを公開しています。

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**期待される出力（例）**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

テキストが文字化けしている場合は、**how to set preprocessing** を見直してください：`contrast` を上げるか、カラーのロゴに対しては `binarize` を無効にしてみてください。

---

## よくある落とし穴とプロのコツ

| 問題 | 発生原因 | 修正（How to Set Preprocessing） |
|-------|----------------|--------------------------------|
| 文字が歪んで意味不明になる | `deskew` が無効または画像が過度に回転している | `preprocessing_options.deskew = True` を有効にする |
| 数字が点や乱れたマークになる | コントラストが低い、または過剰な二値化 | `contrast` を下げる（例: `1.2`）または `binarize = False` に設定 |
| ROI の座標が数ピクセルずれる | DPI やスキャナーのスケーリングが異なる | ツール（例: Paint.NET）で正確なピクセル位置を測定するか、各 ROI に小さな余白（`+5` ピクセル）を追加 |
| 領域の結果が空になる | ROI が画像範囲外 | `source_image.width`、`source_image.height` で画像サイズを確認 |

---

## ソリューションの拡張 (How to OCR ROI in Different Scenarios)

- **Dynamic ROIs**: 請求書のレイアウトが可変の場合、まず全ページの OCR を素早く実行してキーワード（“Customer:”、 “Address:”）を検出し、リアルタイムで ROI を算出できます。  
- **Batch Processing**: 上記の手順を関数にまとめ、画像フォルダーをループ処理します。メモリ使用量を抑えるために同じ `ocr_engine` インスタンスを再利用することを忘れずに。  
- **Exporting to JSON**: 出力を印刷する代わりに、辞書を作成して `json.dumps` でダンプします。これにより、ERP システムへの連携など下流の統合が簡単になります。

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## 結論

これで、Pythonで **how to OCR ROI** を実行し、最適な精度のために **how to set preprocessing** をマスターした完全な実行可能サンプルが手に入りました。エンジンを関心のある正確な矩形に限定し、事前に画像をクリーンアップすることで、より高速でクリーンな結果が得られます—請求書の自動化、フォームのデジタル化、またはページの一部だけが重要なシナリオに最適です。

次のステップに進む準備はできましたか？別の文書タイプに合わせて ROI 座標を調整したり、`sharpen` や `noise_reduction` などの追加前処理フラグを試してみてください。Aspose OCR の柔軟性により、実質的にあらゆる画像品質にパイプラインをカスタマイズできます。

問題が発生した場合は、コンソール出力で空の領域がないか確認し、前処理設定を見直してください。コーディングを楽しんで、OCR が常に正確でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}