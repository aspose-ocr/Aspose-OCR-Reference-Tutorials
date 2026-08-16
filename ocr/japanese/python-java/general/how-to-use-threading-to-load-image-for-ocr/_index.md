---
category: general
date: 2026-04-26
description: PythonでOCR用に画像をロードするためのスレッド活用方法。コールバック、バックグラウンドスレッド、画像ロードを使った非同期OCR処理を数ステップで学ぼう。
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: ja
og_description: PythonでOCR用に画像を読み込む際のスレッド活用方法。このガイドでは、コールバックとバックグラウンド実行を備えた完全な実行可能サンプルを示します。
og_title: OCRのために画像を読み込む際のスレッド活用方法
tags:
- Python
- Threading
- OCR
- Image Processing
title: OCR用に画像を読み込む際のスレッド活用方法
url: /ja/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スレッドを使って OCR 用画像を読み込む方法

アプリがフリーズせずに **スレッドを使って** OCR 用の画像を読み込む方法を知りたくありませんか？ デスクトップスキャナを作るときでも、ウェブサービスでも、膨大な画像を処理するシンプルなスクリプトでも、同じシナリオが出てきます。 良いニュースは、数行の Python と適切なスレッドパターンさえあれば、OCR エンジンが魔法をかけている間も UI をサクサク動かせるということです。

このチュートリアルでは、完結したエンドツーエンドの例を順に解説します。大きな PNG を読み込み、バックグラウンドスレッドで OCR を開始し、コールバックで結果を処理します。最後まで読めば、 **スレッドの使い方** だけでなく、 **OCR 用画像の読み込み** をクリーンで再利用可能な方法で実装できるようになります。

## 必要なもの

- Python 3.9+（使用している構文は最近のバージョンであればすべて動作します）
- 画像処理用 `pillow`（`pip install pillow`）
- Tesseract OCR の薄いラッパー `pytesseract`（`pip install pytesseract`）
- マシンにインストールされた Tesseract OCR エンジン（[tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract) からダウンロード）
- 処理したい大きな画像ファイル（このガイドでは `large_image.png` を使用）

余計なフレームワークは不要、async/await も不要です。古典的な `threading` とコールバックだけで完結します。

## 手順 1: バックグラウンド実行のために threading モジュールをインポートする（必須）

最初に `threading` モジュールをインポートします。これにより `Thread` クラスが利用でき、任意の関数を別 OS スレッドで実行できます。

```python
import threading
```

*なぜ重要か*: メインスレッドで OCR を実行すると、プログラム（特に GUI）は OCR が終わるまでフリーズします。処理をバックグラウンドスレッドに委譲すれば、メインスレッドは UI の更新やユーザー入力の処理、他タスクの開始などが自由に行えます。

## 手順 2: OCR 完了時に呼び出されるコールバックを定義する

コールバックとは、別のコードが処理完了時に呼び出す関数のことです。ここでは認識結果のテキストを表示しますが、保存したりネットワーク送信したり、UI ウィジェットを更新したりすることも可能です。

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*プロのコツ*: コールバックは軽量に保ちましょう。コールバック内部で重い処理を行うと、スレッド化の意味がなくなり（多くの場合メインスレッドがブロックされます）ます。

## 手順 3: 処理したい画像を読み込む

画像の読み込みは OCR とは別の関心事ですが、全体のワークフローの一部です。Pillow を使えば簡単に行えます。

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*ここで行う理由*: 画像が巨大な場合、メインスレッドで読み込むだけでも一瞬のカクつきが起きます。実際のアプリでは画像読み込み自体もスレッドにオフロードすることが多いですが、ここでは分かりやすさのため同期的に行っています。

## 手順 4: 小さな OCR エンジンラッパーを作成する

元のスニペットは `engine.process_async` を使用していました。ここでは内部でスレッドを起動し、完了時に渡されたコールバックを呼び出す小さなクラスで同等の動作を再現します。

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*説明*:
- `_run_ocr` が実際の重い処理を担当します。
- `process_async` は `Thread` オブジェクトを生成し、デーモンとしてマーク（スレッドが残っていてもインタプリタが終了できるように）してから開始します。
- コールバックには OCR テキストまたはエラーメッセージが渡されます。

## 手順 5: すべてを結びつけ、OCR 実行中に他の作業を行う

ここで全体の流れを組み立てます。画像を読み込み、エンジンをインスタンス化し、非同期 OCR を発火させ、メインスレッドは別の作業（ここではメッセージの出力）を続けます。

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**期待される出力（抜粋）**:

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

OCR が失敗した場合、コールバックはテキストの代わりにエラーメッセージを出力します。

---

## なぜこのアプローチが単純なループより優れているのか

- **応答性**: メインスレッドは OCR 呼び出しでブロックされないため、大きな画像でも数秒かかる処理を実行できます。
- **スケーラビリティ**: 複数の `SimpleOcrEngine` インスタンスをそれぞれ別スレッドで起動すれば、画像バッチを同時に処理できます。
- **関心の分離**: 読み込み、処理、結果ハンドリングが明確に分かれているため、テストや保守が容易です。

## よくある落とし穴と回避策

| 落とし穴 | 起こること | 対策 |
|---------|------------|------|
| スレッドを *daemon* に設定し忘れる | メイン処理が終了しても OCR スレッドが残り、スクリプトがハングする | `worker.daemon = True` を設定 **または** 終了前に `join()` する |
| 結果をグローバル変数で保持しロックを使わない | 複数スレッドが同時に書き込むと競合が起きデータが壊れる | コールバックで結果を渡す（今回のやり方）か、`queue.Queue` などスレッド安全なコンテナを使用 |
| メインスレッドで巨大画像を読み込む | OCR が始まる前に UI がフリーズする | 画像読み込みもスレッドにオフロードするか、遅延読み込みを利用 |
| ワーカースレッド内で例外を捕捉しない | 例外が無視されスレッドが黙って終了し、結果が得られなくなる | OCR ロジックを `try/except` で包み、エラーをコールバックへ転送 |

## このパターンの拡張例

- **進捗報告**: OCR スレッドから `queue.Queue` を使って途中経過（パーセンテージ）をメインスレッドへ送信する。
- **スレッドプール**: バッチ処理では個別 `Thread` の代わりに `concurrent.futures.ThreadPoolExecutor` を利用する。
- **GUI 連携**: Tkinter や PyQt アプリでは、`after()`（Tkinter）や `QTimer.singleShot`（Qt）でコールバックをスケジュールし、UI 更新がメインスレッドで行われるようにする。

## 完全動作サンプル（コピペ用）

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}