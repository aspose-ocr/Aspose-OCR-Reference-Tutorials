---
category: general
date: 2026-01-12
description: Aspose OCR を使用して Python で画像からテキストを抽出します。非同期コードでスキャン画像をテキストに変換する方法を数分で学びましょう。
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: ja
og_description: Aspose OCR を使用した Python で画像からテキストを抽出します。このチュートリアルでは、非同期関数を使ってスキャン画像をテキストに変換する方法を示します。
og_title: Pythonで画像からテキストを抽出 – 非同期OCRガイド
tags:
- python
- ocr
- async
title: 画像からテキストを抽出する Python – 非同期 OCR ガイド
url: /ja/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する Python – 非同期 OCR ガイド

スキャンしたドキュメントを **画像からテキストを抽出する Python** スクリプトで扱いたいけど、OCR の部分で行き詰まったことはありませんか？ あなただけではありません。多くの開発者が、スキャンした文書を検索可能なテキストに変換しようとして壁にぶつかります。

このチュートリアルでは、Aspose OCR の非同期 API を使用して **スキャンした画像をテキストに変換** する完全な実行可能サンプルを段階的に解説します。最後まで読めば、どのプロジェクトにも組み込める単一関数が手に入り、OCR に数秒かかってもアプリが応答し続けられる理由が理解できるでしょう。

## 前提条件

始める前に、以下が揃っていることを確認してください。

- Python 3.8+ がインストール済み（非同期機能は最低 3.7 が必要です）
- `asposeocr` パッケージ（`pip install asposeocr`） – 本チュートリアルで使用するライブラリです
- スキャンした画像ファイル（TIFF、PNG、JPEG など、Aspose OCR がサポートする形式）
- `asyncio` の基本的な知識（なくても大丈夫です – 各ステップで説明します）

追加のシステム依存関係は不要です。Aspose OCR が必要なものはすべてバンドルしています。

![非同期 OCR フローを示す図 – 画像からテキストを抽出する Python](https://example.com/async-ocr-diagram.png "非同期 OCR フロー – 画像からテキストを抽出する Python")

## 手順 1 – 非同期ヘルパー関数のセットアップ  

このソリューションの核心は、画像を読み込み OCR を開始し、結果を待機する `async` 関数です。関数を非同期に保つことで、OCR エンジンがバックグラウンドで動作している間に他のコルーチン（例: さらにファイルをダウンロード）を実行できます。

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**ポイント:** `Future` を返すことで、Aspose OCR は別スレッドプールで重い処理を行います。`await` によりイベントループが解放され、アプリは軽快に動作し続けます。多数の画像を同時に処理したい場合は、`asyncio.gather` で複数の `async_ocr` 呼び出しをスケジュールすれば完了です。

## 手順 2 – イベントループでコルーチンを実行  

ヘルパー関数ができたら、実際に実行します。`asyncio.run` は新しいイベントループを作成し、コルーチンを走らせ、すべてをきれいに終了させます。

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**プロのコツ:** これをより大きな非同期アプリケーション（例: FastAPI）に組み込む場合は、`asyncio.run` の代わりに `await async_ocr(...)` を直接呼び出します。

## 手順 3 – 出力を確認  

スクリプトを実行すると、次のような出力が得られるはずです。

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

出力が文字化けしている場合は、以下を再確認してください。

1. 画像が鮮明で、過度に圧縮されていないこと。  
2. 正しい言語が選択されていること（`ocr.Language.ENGLISH` は多くのラテン系テキストで有効）。  
3. ファイルパスが正しく、ファイルが読み取り可能であること。

## 手順 4 – エッジケースの処理  

### 複数言語  

英語以外の言語で **スキャンした画像をテキストに変換** したい場合は、言語プロパティを変更するだけです。

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### 大容量ファイル  

非常に大きな TIFF の場合は、OCR に渡す前にリサイズするか、低解像度の PNG に変換するとよいでしょう。これによりメモリ使用量が抑えられ、処理速度が向上します。

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### エラーハンドリング  

ネットワークやライセンス関連のエラーを捕捉するために、OCR 呼び出しを `try/except` ブロックでラップします。

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## 手順 5 – スケールアップ: 多数の画像を同時並行で処理  

関数が非同期であるため、OCR ジョブを一度に多数起動できます。

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

このパターンは、OCR エンジンが並列で動作している間に CPU を有効活用し、総処理時間を大幅に短縮します。

## 結論  

これで、Aspose OCR の非同期 API を活用した堅牢な **画像からテキストを抽出する Python** ソリューションが手に入りました。完全なサンプルは次のことを示しています。

1. OCR エンジンを初期化し、言語を選択する。  
2. `process_async` で非同期に OCR を開始する。  
3. イベントループをブロックせずに結果を待機する。  
4. 大容量ファイルや多言語対応などの一般的な落とし穴に対処する。  

コードは以下のような用途に自由に適用できます – ドキュメント管理システム、検索インデクサ、シンプルなコマンドラインユーティリティなど。次のステップとしては:

- 抽出したテキストをデータベースに保存し、全文検索を実装する。  
- `PyPDF2` などを使って検索可能な PDF を生成する。  
- FastAPI などのウェブフレームワークと統合し、RESTful OCR サービスを提供する。

コーディングを楽しみながら、スキャン画像を検索可能で編集可能なテキストに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}