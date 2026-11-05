---
category: general
date: 2026-06-06
description: JavaでOCRを実行する方法 – 画像からテキストを素早く抽出し、画像をテキストに変換し、シンプルなコード例を使ってJPGからテキストを読み取る。
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: ja
og_description: JavaでOCRを実行する方法 – 画像からテキストを抽出し、画像をテキストに変換し、JPGからテキストを読み取る方法を、すぐに実行できるサンプルで学びましょう。
og_title: JavaでOCRを実行する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: JavaでOCRを実行する方法 – 画像からテキストを抽出する完全ガイド
url: /ja/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRを実行する方法 – 画像からテキストを抽出する完全ガイド

スマートフォンで撮影した写真に対して **OCR を実行する方法** を考えたことがありますか？ あなただけではありません。レシートスキャンアプリを作る場合でも、スキャンした PDF からテキストを抽出したいだけの場合でも、Javaで **OCR を実行する方法** はすぐに役立つスキルです。このチュートリアルでは、実用的な例として **画像ファイルからテキストを抽出** し、**画像をテキストに変換** し、さらに数行のコードで **JPG からテキストを読み取る** 方法を示します。

> *プロのコツ:* 同じアプローチは PNG、BMP、または OCR エンジンがサポートする任意の形式でも機能します—ファイル名を差し替えるだけです。

## JavaでOCRを実行する方法 – 概要

光学文字認識（OCR）は、文字の画像を実際の検索可能なテキストに変換する技術です。Java エコシステムには Tesseract、Asprise、商用 SDK など複数のライブラリがあり、すべて似たようなワークフローを提供します：画像を読み込み、エンジンに期待する言語を指定し、認識を実行し、結果を取得します。以下では例を分かりやすくするために汎用的な `OcrEngine` クラスを使用しますが、同じパターンに従う任意の実装に置き換えることができます。

### 学べること

- OCR ライブラリをインストールする（はい、**ocr in java** は思ったより簡単です）。
- OCR エンジンのインスタンスを作成し、設定する。
- JPG（または任意の画像）を読み込み、言語を設定する。
- 画像を処理し、**extract text from image** ファイルからテキストを抽出する。
- 認識された文字列をコンソールに出力する。

最後まで読むと、任意のプロジェクトにすぐに組み込んで実行できる、自己完結型の Java プログラムが手に入ります。

![OCR 実行例](ocr-example.png "JavaでのOCR実行イラスト")

## ステップ 1 – OCR ライブラリのインストールとインポート (ocr in java)

Java のコードを書く前に、実際に重い処理を行うライブラリが必要です。Maven を使用している場合は、次のように依存関係を追加します（`com.example.ocr` は選択した SDK の実際のグループ ID に置き換えてください）。

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Gradle を好む場合は、次のようにします：

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

JAR がクラスパスに追加されたら、必要なクラスをインポートします：

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **なぜ重要か:** 正しいクラスをインポートすることで “cannot find symbol” エラーを防ぎ、IDE が快適に動作します—**convert image to text** を試みているときにインポートが欠けているより苛立たしいことはありません。

## ステップ 2 – OCR エンジンインスタンスの作成 (how to perform OCR)

ライブラリの準備ができたら、エンジンを起動します。エンジンはピクセルを見て文字を推測する脳のようなものです。

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

エンジンの作成は通常コストが低く、ほとんどの SDK は内部バッファを遅延割り当てするため、バッチ処理を行う場合でも同じインスタンスを多数の画像で安全に再利用できます。

## ステップ 3 – 画像の読み込みと言語設定 (extract text from image)

次のステップは、エンジンに読み取らせる対象を与えることです。ここではディスクから JPEG を読み込み、OCR エンジンにテキストがモンゴル語（ISO 639‑2 コード “mon”）であることを伝えます。パスや言語コードは使用ケースに合わせて変更できます。

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **補足:** 言語を設定しない場合、エンジンはデフォルトで英語を使用します。実際のテキストがキリル文字や他のスクリプトの場合、精度が大幅に低下する可能性があります。可能な限り正しい言語を指定してください。

## ステップ 4 – 画像を処理して結果を取得 (convert image to text)

画像と設定した言語が揃ったら、エンジンに処理を依頼します。`process()` 呼び出しは OCR アルゴリズムを実行し、認識された文字列と信頼度スコアを含む `OcrResult` オブジェクトを返します。

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

内部では、エンジンが前処理（傾き補正、二値化、ノイズ除去）を行うことがあるため、これらのステップを自分で実装する必要はありません。そのため、最新の OCR ライブラリは **convert image to text** タスクに対して非常に使いやすいのです。

## ステップ 5 – 抽出したテキストの出力 (read text from jpg)

最後に、結果からプレーンテキストを取り出し、何らかの有用な処理を行います。このデモでは単にコンソールに出力しますが、ファイルに書き込んだり、検索インデックスに投入したり、別のサービスに渡したりすることも可能です。

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

この一行だけで、**read text from jpg**（またはサポートされている任意の形式）に成功したことが確認できます。出力が文字化けしている場合は、言語コードと画像品質を再確認してください。

## 完全な動作例（すべてのステップを統合）

以下は、すべての要素を結合した、完全で実行可能な Java クラスです。`OcrDemo.java` という名前のファイルにコピーし、画像パスと使用言語を調整した後、`javac OcrDemo.java && java OcrDemo` を実行してください。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 期待される出力

`input.jpg` にモンゴル語のフレーズ “Сайн байна уу?” が含まれている場合、コンソールには次のように表示されます：

```
=== Recognized Text ===
Сайн байна уу?
```

画像がぼやけているか言語コードが間違っている場合、文字化けした文字や空文字列が表示されます—次に説明する一般的な落とし穴です。

## よくある落とし穴とその対処法

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| 文字化けしたキリル文字 | 言語コードが誤っている（デフォルトで英語になる） | `ocrEngine.getSettings().setLanguage("mon")` もしくは適切なコードを設定してください。 |
| 出力が全くない | 画像パスが間違っているかファイルが読めない | パスを確認し、ファイルが存在し、プロセスに読み取り権限があることを確認してください。 |
| 精度が低い（<70 %） | 画像のコントラストが低い、または回転している | 画像を前処理してください：コントラストを上げ、傾きを補正し、またはエンジンに渡す前にグレースケールに変換します。 |
| `OutOfMemoryError` が大きな PDF で発生 | 高解像度ページを一度に多数読み込んでいる | ページを1つずつ処理するか、OCR 前に画像を縮小してください。 |

### プロのコツ: バッチ処理

大量に **extract text from image** ファイルを処理する必要がある場合は、コアロジックをループで囲んでください：

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

このスニペットは、単一の JPG からスキャンしたフォルダ全体へとスケールアップするのがいかに簡単かを示しています。

## 次のステップ – さらに学ぶべきことは？

- **Language Packs:** ほとんどの OCR SDK では追加の言語データファイルをダウンロードできます。新しいパックを追加することで、英語やモンゴル語以外の言語でも **convert image to text** が可能になります。
- **PDF OCR:** このコードを Apache PDFBox と組み合わせて

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [画像からテキスト抽出 – Aspose.OCR for Java の OCR 基礎](/ocr/english/java/ocr-basics/)
- [Aspose.OCR BufferedImage を使用した Java での画像からテキストへの変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR を使用した言語付き画像テキスト OCR の方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}