---
category: general
date: 2026-03-18
description: 基本的な OCR Python チュートリアルでは、TIFF をテキストに変換する方法、画像 OCR をロードする方法、GPU レイヤーを設定する方法、そして
  Aspose AI を使用して先頭のゼロを修正する方法を示します。
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: ja
og_description: 基本的なOCR Pythonチュートリアルでは、TIFFファイルをクリーンなテキストに変換する方法、画像の読み込み、GPUレイヤーの設定、先頭のゼロの修正について解説します。
og_title: 基本的なOCR Python – TIFFをテキストに変換
tags:
- OCR
- Python
- AI
- Aspose
title: 基本的な OCR Python – TIFF をテキストに変換
url: /ja/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – AI ポストプロセッシングで TIFF をテキストに変換

スキャンしたドキュメントで **basic ocr python** を実行する方法を探していますか？このガイドでは、Aspose OCR と AI ポストプロセッサーを使用して TIFF ファイルをクリーンで検索可能なテキストに変換する手順を説明します。

生の出力に誤字や奇妙な記号が多くて **convert TIFF to text** に苦労したことがあるなら、あなただけではありません。ここでは **load image OCR** の方法、エンジンを **set GPU layers** に調整する方法、そして請求書番号によく出る **fix leading zeroes** の方法も紹介します。

## 学べること

- 印刷文書用に Aspose OCR エンジンを初期化する方法。  
- TIFF ファイルから **load image OCR** を実行し、生のテキストを取得する正確な手順。  
- AI モデルを構成し、自動でダウンロードし、**setting GPU layers** で高速推論を実現する方法。  
- 組み込みのスペルチェックに加えて、**fixes leading zeroes** を行うカスタム関数の追加。  
- OCR 結果をクリーンアップし、リソースを適切に解放する方法。  

このチュートリアルの最後までに、任意の TIFF を洗練された検索可能なテキストに変換する、単一の再利用可能な Python スクリプトが手に入ります—手動でのコピー＆ペーストは不要です。  

### 前提条件

- マシンに Python 3.8+ がインストールされていること。  
- `aspose-ocr` パッケージ（`pip install aspose-ocr`）。  
- オプション: **set GPU layers** を使用したい場合は、少なくとも 4 GB VRAM を持つ GPU が必要です。指定しない場合、コードは自動的に CPU にフォールバックします。  

---

## basic ocr python – 画像をロードしてテキストを認識

最初に行うべきことは **load image OCR** で、エンジンがピクセルを読み取れるようにすることです。Aspose の `OcrEngine` は多くのフォーマットに対応していますが、ここではスキャンした請求書で最も一般的な TIFF に焦点を当てます。

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **プロのコツ:** マルチページ TIFF を扱う場合、Aspose は自動的に各ページを順番に処理するので、余分なループは不要です。

画像がロードされたので、基本的な認識パスを実行しましょう。

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

以下のような出力が得られます:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

文字の前にある *zeroes* に気づきましたか？これは典型的な OCR アーティファクトで、後でクリーンアップします。

![basic ocr python ワークフロー](/images/ocr-workflow.png "basic ocr python ワークフロー図")

---

## Step 2: TIFF をテキストに変換 – AI ポストプロセッサーの準備

生の OCR は有用ですが、ほとんどの本番パイプラインでは洗練されたバージョンが必要です。Aspose は `AsposeAI` ラッパーを提供しており、Hugging Face からモデルをダウンロードし、GPU 上で実行し、スペルチェックを自動的に適用できます。

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### `set GPU layers` が重要な理由

`gpu_layers` パラメータは、基盤となる GGUF モデルに GPU 上に保持するトランスフォーマーレイヤー数を指示します。レイヤーが多いほど推論は速くなりますが、VRAM 使用量が増えます。もし控えめなノートパソコンを使用している場合は、値を `10` に下げるか、CPU のみで実行するためにパラメータを省略してください。

---

## Step 3: スペルチェックと **fix leading zeroes** の適用

Aspose AI には組み込みのスペルチェッカーが搭載されており、ほとんどの英語の誤字を検出します。ただし、領域固有の修正（例: 請求書コードの先頭 `0` を `O` に変換するなど）にはカスタムポストプロセッサが必要です。

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **なぜこれが機能するか:** 正規表現は単語境界 (`\b`)、ゼロ、続いて正確に3つの大文字を探します。その後、ゼロを文字 “O” に置換します。他の奇妙なケースにもパターンを拡張できます（例: 誤読された数字のための `0[0-9]{2}`）。

---

## Step 4: AI ポストプロセッサで OCR 結果をクリーンアップ

ここで全てを組み合わせます：**basic ocr python** からの生文字列、スペルチェック、そしてゼロ修正。`run_postprocessor` メソッドは、下流システム向けに準備されたクリーンなバージョンを返します。

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

ポストプロセッサ適用後の典型的な出力:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

先頭のゼロが `O` に変換され、一般的な誤字が修正されていることが分かります。テキストは検索エンジンでのインデックス作成やデータ抽出パイプラインへの入力に適しています。

---

## Step 5: AI リソースを解放 – GPU を快適に保つ

長時間稼働するサービスで複数の OCR ジョブを実行している場合、終了時にモデルの GPU メモリを解放することがベストプラクティスです。

```python
ocr_ai.free_resources()
```

このステップを省略すると、特に **set GPU layers** を高い値に設定した場合、次回の呼び出しで “out‑of‑memory” エラーが発生する可能性があります。

---

## オプションのバリエーションとエッジケース

| 状況 | 変更点 |
|-----------|----------------|
| **手書き文書** | `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` を `PRINTED` の代わりに使用します。 |
| **GPU が利用できない** | `gpu_layers=0` を設定するか引数を省略します。モデルは CPU 上で実行されます（遅くなりますが安全）。 |
| **異なる言語** | Hugging Face のリポジトリ ID を言語固有のモデルに置き換えます。例: `microsoft/Florence-2-base`。 |
| **バッチ処理** | 手順を `for file in glob("*.tif"):` ループでラップし、結果をリストまたは CSV に蓄積します。 |
| **より複雑なゼロパターン** | `invoice_fix` に追加の正規表現を拡張します。例: 複数の先頭ゼロ用に `r"\b0+([A-Z]{2,})\b"`。 |

---

## 結論

ここまでで、TIFF をロードし、生テキストを抽出し、AI モデルでクリーンアップしながら **setting GPU layers** でパフォーマンスを向上させる **basic ocr python** パイプラインが完成しました。カスタムポストプロセッサは **fix leading zeroes** の方法を示しており、下流の分析を壊すことのある見落とされがちな小さな詳細です。

自由に実験してください：異なる量子化（精度向上のための `float16`）を試す、スペルチェックを領域固有の辞書に置き換える、または複数のカスタム修正を連鎖させるなど。パターンは変わりません—ロード、認識、AI の設定、ポストプロセス、クリーンアップです。

**次のステップ** としては、以下を検討できます:

- クリーンアップされた出力をデータベースまたは Elasticsearch インデックスに統合する。  
- 同じアプローチを使用して、マルチ言語 PDF の **convert TIFF to text** を実行する。  
- Flask または FastAPI を使って UI を追加し、非技術者がファイルをアップロードして即座にクリーンテキストを受け取れるようにする。  

コーディングを楽しんでください、そして OCR の結果が常に鮮明でゼロがない状態でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}