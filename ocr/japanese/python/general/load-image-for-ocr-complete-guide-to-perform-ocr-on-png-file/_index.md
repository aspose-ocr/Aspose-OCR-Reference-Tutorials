---
category: general
date: 2026-06-25
description: aocr を使用したステップバイステップの Python チュートリアルで、OCR 用に画像を読み込み、PNG に対して OCR を実行します。デバッグ、ロギング、ベストプラクティスを学びましょう。
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: ja
og_description: OCR用に画像を読み込み、aocrを使用してPNGでOCRを実行します。このガイドでは、ロギング、画像の読み込み、認識をフルコードで解説します。
og_title: OCR用画像の読み込み – ステップバイステップ Python チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR用画像の読み込み – PNGファイルでOCRを実行する完全ガイド
url: /ja/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR用画像のロード – PNGファイルでOCRを実行する完全ガイド

**OCR用に画像をロード**したいけど、適切なデバッグ方法が分からないことはありませんか？ 多くのプロジェクトで最初の壁は、PNG をエンジンに取り込みつつ、内部で何が起きているかを確認できることです。

このチュートリアルでは、`aocr` ライブラリを使って **PNG で OCR を実行** するために必要なすべてを解説します。詳細な出力用ロガーの設定から実際の文字認識まで、ステップバイステップで進めます。最後まで読めば、任意の Python プロジェクトに組み込める再利用可能なスクリプトが手に入り、各要素がなぜ重要なのかも理解できるようになります。

## 学べること

- `aocr` ロガーを初期化して、すべてのステップを追跡できるようにする方法  
- `aocr.OcrEngine` で **OCR用画像をロード** する正確なコード  
- ログレベルを設定して、細かいデバッグ情報を取得する方法  
- エンジンを実行して **PNG で OCR を実行** し、結果を取得する手順  
- ファイルが見つからない、または未対応フォーマットなどの一般的な落とし穴への対処法  

`aocr` の事前知識は不要です。Python 3 が動作する環境と、読み取りたい画像さえあれば始められます。さあ、始めましょう。

![load image for OCR example](assets/load-image-ocr.png "Python で OCR 用画像をロードするイラスト")

## 前提条件

| 必要条件 | 重要な理由 |
|----------|------------|
| Python 3.8+ | `aocr` は最新のインタプリタを対象としており、型ヒントを使用します。 |
| `aocr` ライブラリインストール (`pip install aocr`) | パッケージが無いと、使用するクラスが存在しません。 |
| 読み取りたい PNG 画像 | 本チュートリアルは **PNG で OCR を実行** することに焦点を当てているため、PNG が必須です。 |
| ログディレクトリへの書き込み権限 | ロガーは `ocr_debug.log` を作成する必要があります。 |

これらが揃っていない場合は、今すぐインストールしてください。所要時間はわずかです。

```bash
pip install aocr
```

## 手順 1: OCR 用画像のロード – ロギングの初期化

画像に触れる前に、まずロガーを設定します。OCR のデバッグは、エンジンの動作が見えないと非常に厄介です。`aocr.Logging` クラスはすべてをファイルに書き出し、レベルを `DEBUG` に設定すれば内部呼び出しをすべて確認できます。

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**重要性:**  
OCR エンジンがファイルを見つけられなかったり、画像フォーマットが未対応だった場合、ロガーは例外スタックトレースを記録します。これにより、後で無限に推測する手間が省けます。

## 手順 2: PNG で OCR を実行 – エンジンの設定

ロガーが準備できたら、OCR エンジンに紐付けます。このステップでエンジンのすべての動作が記録されます。

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**プロのコツ:**  
同じ `ocr_engine` インスタンスを複数画像で再利用できます。ただし、バッチ処理する場合は前回の状態をクリアすることを忘れずに。

## 手順 3: OCR 用画像のロード – PNG ファイルを読み込む

チュートリアルの核心です：実際に **OCR用画像をロード** します。`load_image` メソッドはファイルパスを受け取り、内部で PNG をエンジンが理解できるビットマップにデコードします。

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### 注意すべきエッジケース

1. **ファイルが見つからない** – パスが間違っていると `aocr` は `FileNotFoundError` を送出します。ロガーはそれを記録しますが、以下のように捕捉することも可能です:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **未対応フォーマット** – PNG は広くサポートされていますが、破損したファイルは `UnsupportedFormatError` を引き起こすことがあります。その場合は、Pillow でクリーンな PNG に変換してからロードしてください。

## 手順 4: PNG で OCR を実行 – 認識を走らせる

画像がメモリ上にロードされたら、いよいよ **PNG で OCR を実行** できます。`recognize` メソッドはエンジンのパイプライン（前処理、セグメンテーション、分類）を起動し、結果オブジェクトにデータを格納します。

```python
# Execute the OCR process
ocr_engine.recognize()
```

この呼び出しの後、エンジンは認識されたテキストを保持しています。`result` 属性から取得できます:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**結果を確認すべき理由:**  
コントラストが低い画像では空文字列が返ることがあります。結果をすぐに確認すれば、再実行前に前処理（例: コントラスト増加）が必要かどうか判断できます。

## 手順 5: すべてをまとめる – 再利用可能な関数

各要素をひとつの関数にまとめれば、他のスクリプトやウェブサービスから簡単に呼び出せます。これにより **OCR用画像をロード** し、**PNG で OCR を実行** する一連の流れが一つのパッケージに収まります。

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

スクリプトを実行すると `logs` フォルダに詳細な `ocr_debug.log` が生成され、認識結果がコンソールに出力されます。これで **PNG で OCR を実行** するユーティリティが完成し、他プロジェクトでもインポートしてすぐにテキスト抽出が可能です。

## よくある質問と落とし穴

- **PNG を別の形式に変換する必要がありますか？**  
  通常は不要です。`aocr` は PNG をネイティブに扱いますが、画像が非常に大きい（>10 MP）場合は処理速度向上のために縮小を検討してください。

- **ロガーファイルが大きくなりすぎたらどうすれば？**  
  実行ごとにログをローテーションするか、パイプラインが安定したらレベルを `INFO` に下げてください。

- **ループで複数画像を処理できますか？**  
  可能です。各ファイルに対して `ocr_png` を呼び出せば、関数が毎回新しいロガーを作成し、ログが分離されます。

- **プレーンテキストではなくバウンディングボックスが欲しい場合は？**  
  `engine.result` には `boxes` と `confidences` も含まれます。レイアウト情報が必要な場合は `aocr` の `result.boxes` ドキュメントを参照してください。

## 結論

`aocr` ライブラリを使って **OCR用画像をロード** し、**PNG で OCR を実行** する方法と、デバッグが楽になる堅牢なロギング設定を習得しました。サンプル関数はワークフロー全体をカプセル化しているので、任意のプロジェクトに組み込んで即座にテキスト抽出を開始できます。

次のステップは？ JPEG や TIFF など別の画像タイプでエンジンを試し、精度の変化を観察したり、ノイズが多いスキャンに対してしきい値処理などの前処理技術を実験したりしてください。また、構造化データ（テーブル、フォーム）の抽出に興味がある場合は、`aocr` のレイアウト解析セクションをチェックすると、今回構築したものと相性が良いです。

Happy coding, and may your OCR pipelines be ever error‑free!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深掘りできるよう構成されています。各リソースには、ステップバイステップの解説と完全動作コード例が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}