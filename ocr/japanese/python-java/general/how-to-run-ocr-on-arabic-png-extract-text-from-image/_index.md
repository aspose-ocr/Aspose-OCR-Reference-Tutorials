---
category: general
date: 2026-03-26
description: アラビア語のPNG画像に対してOCRを実行し、アラビア語テキストを迅速に抽出する方法を学びましょう。このガイドでは、ステップバイステップのPythonコードで画像をテキストに変換する手順を示します。
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: ja
og_description: アラビア語のPNG画像でOCRを実行する方法は？この完全ガイドに従って、アラビア語テキストを抽出・認識し、Pythonを使用して画像をテキストに変換しましょう。
og_title: アラビア語PNGでOCRを実行する方法 – 画像からテキストを抽出
tags:
- OCR
- Python
- Arabic
title: アラビア語PNGでOCRを実行する方法 – 画像からテキストを抽出
url: /ja/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# アラビア語 PNG で OCR を実行する方法 – 画像からテキストを抽出

アラビア文字が含まれる画像で **OCR を実行する方法** を知りたくありませんか？スキャンした領収書や歴史的な写本、あるいはソーシャルメディアの投稿のスクリーンショットなど、検索可能な形式でテキストが必要になることがあります。右から左へ書く言語を扱う際に、この問題に直面する開発者は世界中にいます。

このチュートリアルでは、PNG ファイルに対して **OCR を実行し** アラビア語テキストを抽出し、コンソールに結果を出力する完全な実行可能サンプルを順を追って解説します。「ドキュメントを参照してください」的な曖昧なリンクはありません。コピー＆ペーストできるコードと、各行が何をしているのかの説明だけです。最後まで読めば、**画像からテキストへ変換** を信頼性高く行えるようになります。

> **学べること**
> - アラビア語用の Python OCR エンジンのセットアップ  
> - PNG 画像の読み込みと一般的な落とし穴の対処  
> - アラビア語テキストの認識と出力の検証  
> - さまざまな画像品質から **アラビア語テキストを抽出** するためのヒント  

始める前に、Python 3.8 以上がインストールされていて、スニペットで使用している `ocr` ライブラリの最新バージョンが入っていることを確認してください。仮想環境を使っている場合は、今すぐアクティベートしましょう。依存関係が整理されます。

## 前提条件

- Python 3.8 以上  
- `ocr` パッケージ（`pip install ocr‑engine` – 実際のパッケージ名に置き換えてください）  
- アラビア語の PNG 画像（`arabic_doc.png`）を参照できる場所に配置  
- Python の関数やクラスに関する基本的な知識  

以上です。重いフレームワークや Docker コンテナは不要、純粋な Python だけです。

## 手順 1: OCR ライブラリのインストールとインポート

まずは OCR エンジン自体が必要です。今回使用するライブラリはシンプルな API を持つ `OcrEngine` クラスを提供します。

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*なぜ `Imaging` を別途インポートするのか？* `Imaging` サブモジュールは PNG、JPEG、TIFF を自動で認識できる便利な `Image.load` メソッドを提供します。このステップを省くと、生バイトを自分で処理しなければならず、ほとんどのユースケースで不要です。

## 手順 2: OCR エンジンインスタンスの作成

次にエンジンのインスタンスを作ります。このオブジェクトが画像を処理する「脳」になります。

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **プロのコツ:** 連続して多数の画像を処理する場合は、同じ `ocr_engine` インスタンスを再利用してください。言語モデルがキャッシュされ、以降の認識が高速化します。

## 手順 3: 言語をアラビア語に設定

アラビア語はラテン文字とは異なり、独自の文字セット・右から左への方向・文脈依存の字形があります。そのため、エンジンに明示的に言語モデルをロードさせる必要があります。

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

この行を忘れると、エンジンはデフォルトで英語を使用し、文字化けした出力になります。実際に多くのケースで見られる問題です。

## 手順 4: PNG 画像を読み込む

ここからが **画像からテキストへ変換** の本格的な開始です。アラビア文字が入った PNG ファイルをロードします。

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### よくあるエッジケース

| 問題 | 症状 | 対策 |
|------|------|------|
| 画像が暗すぎる | 出力に空白が多くなる | Pillow の `ImageEnhance.Brightness` で前処理 |
| PNG にアルファチャンネルがある | 一部の OCR エンジンが透明ピクセルを誤認識 | `image.convert("RGB")` で RGB に変換してからロード |
| テキストが回転している | 認識結果が逆さまになる | `image.rotate(90, expand=True)` で回転させてからエンジンに渡す |

## 手順 5: 認識プロセスを実行

すべての準備が整ったら、エンジンに仕事を依頼します。

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

`recognize` メソッドは、生の Unicode 文字列、信頼度スコア、バウンディングボックスを保持したオブジェクトを返します。ほとんどの開発者にとってはプレーンテキストだけで十分です。

## 手順 6: 認識されたアラビア語テキストを出力

結果をコンソールに表示します。実際のアプリではファイルやデータベースに書き込んだり、翻訳 API に渡したりすることもあります。

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

スクリプトを実行すると、ターミナルにアラビア文字が表示されます（端末が Unicode に対応していることを確認してください）。もし「?」や空文字列が出たら、言語設定と画像品質を再確認してください。

### 期待される出力

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

上記のような出力が得られたら、**PNG からアラビア語テキストを抽出** できています。おめでとうございます！

## 完全動作サンプル

以下がコピー＆ペースト可能な全スクリプトです。`YOUR_DIRECTORY/arabic_doc.png` を自分のファイルパスに置き換えてください。

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

`python run_ocr.py`（またはファイル名に合わせて）で実行します。すべて正しくインストールされていれば、コンソールにアラビア語の文が表示されます。

## 異なる画像フォーマットで OCR を実行する方法

同じコードは JPEG、TIFF、BMP でも動作します。拡張子を変えるだけです。`Image.load` メソッドが自動でフォーマットを検出するので、**画像からテキストへ変換** する際に追加コードは不要です。

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

ソース画像の品質は **アラビア語テキストを認識** する精度に大きく影響します。高解像度・低圧縮の画像が最も効果的です。

## PNG からテキストを抽出するための精度向上ヒント

1. **DPI が重要** – 少なくとも 300 dpi を目指す。DPI が低いと文字が抜けやすくなる。  
2. **コントラストが鍵** – OCR エンジンに渡す前に、OpenCV などでコントラストを上げる。  
3. **ノイズ除去** – 小さな斑点がモデルを混乱させることがあるので、メディアンフィルタで除去する。  

以下は Pillow を使って PNG を前処理し、OCR にかける簡単なスニペットです。

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## よくある質問

**Q: アラビア語以外の右から左への言語でも使えますか？**  
A: もちろんです。言語コードを `"ar"` から `"he"`（ヘブライ語）や `"fa"`（ペルシア語）に変更すれば、エンジンは適切なモデルをロードします。

**Q: フォルダ内の複数 PNG からテキストを抽出したい場合は？**  
A: ファイルをループし、同じ `ocr_engine` インスタンスを再利用して、結果をリストに集めるか、各 `.txt` ファイルに書き出します。

**Q: 各単語の信頼度スコアを取得できますか？**  
A: できます。`ocr_result` は通常 `get_confidences()` メソッドを提供します。各単語に対応する信頼度と組み合わせて品質管理に活用してください。

## 次のステップ

**アラビア語 PNG に対して OCR を実行** できるようになったので、以下のアイデアを検討してみてください。

- **バッチ処理:** `os.listdir` と組み合わせてディレクトリ全体から **アラビア語テキストを抽出** する。  
- **後処理:** `arabic_reshaper` と `python-bidi` ライブラリを使い、PDF で右から左の出力を正しく表示。  
- **統合:** 抽出したテキストを検索インデックス（例: Elasticsearch）に投入し、スキャン文書を検索可能にする。  

これらのトピックは本稿で扱った基礎の上に構築でき、シンプルな **画像からテキストへ変換** スクリプトを本番環境向けパイプラインへと拡張できます。

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}