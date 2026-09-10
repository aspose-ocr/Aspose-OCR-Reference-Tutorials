---
category: general
date: 2026-09-10
description: Aspose OCR Java を使用して画像の OCR を実行します。JPEG からテキストを認識し、画像からテキストを抽出し、画像を効率的にテキストに変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: ja
lastmod: 2026-09-10
og_description: Aspose OCR Java を使用して画像の OCR を実行します。このチュートリアルでは、JPEG からテキストを認識し、画像からテキストを抽出し、数行のコードで画像をテキストに変換する方法を示します。
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Aspose OCRで画像のOCRを実行する – Javaガイド
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: JavaでAspose OCRを使用して画像のOCRを実行する方法
url: /ja/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでAspose OCRを使用して画像のOCRを実行する方法

Javaアプリケーションで画像ファイルの**perform OCR on image**が必要な場合、このガイドは完全な、すぐに実行できるソリューションを提供します。**recognize text from JPEG**ファイル、**extract text from image**データ、そして**convert image to text**をAspose OCRの最新APIを使用して行う方法がわかります。

このチュートリアルは、画像の読み込みから認識されたテキストの出力まで、必要な手順をすべて解説しますので、追加のリソースを探すことなくOCR機能を統合できます。Aspose OCR for Java ライブラリ以外に外部ツールは必要ありません。

## 本記事で達成できること

* **Load an image for OCR** をファイルシステムから直接読み込みます。  
* Aspose OCR の前処理（例：ノイズ除去）を有効にして精度を向上させます。  
* **Recognize text from JPEG** とその他のラスタ形式を認識します。  
* **Extract text from image** をコンソールに出力します。  
* 実稼働レベルのコードサンプルで **convert image to text** の方法を理解します。  

### 前提条件

* Java Development Kit (JDK) 8 以上。  
* Maven または Gradle を使用して依存関係を管理します（例では Maven を使用）。  
* 有効な Aspose OCR for Java ライセンス（または一時的な評価キー）。  
* `sample.jpg` という名前の画像ファイルを既知のディレクトリに配置します。  

> **Pro tip:** 最高の認識率を得るために、高解像度 JPEG（300 dpi 以上）を使用してください。  

## 手順 1: プロジェクトに Aspose OCR を追加する

Maven で依存関係を管理している場合、以下のスニペットを `pom.xml` に挿入してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Gradle の場合、以下を追加してください。

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

これらの座標は最新の安定版 Aspose OCR ライブラリを取得し、後で使用する前処理機能が含まれています。

## 画像で OCR を実行する – 手順ごとに

以下のセクションでは、完全なプログラムを分解して説明します。各ブロックはコピー、貼り付け、実行できる自己完結型のコードです。

### OCR 用に画像を読み込む

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*この点が重要な理由:*  
`ImageStream.fromFile` は JPEG の生バイトを読み取り、OCR エンジンのために準備します。このメソッドは Aspose OCR がサポートする任意のラスタ形式で動作するため、コードを変更せずに JPEG を PNG や BMP に置き換えることができます。

### OCR エンジンの作成と設定

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*この点が重要な理由:*  
`OcrEngine` をインスタンス化すると、コアの認識エンジンが確保されます。**denoise** フラグを有効にすると、特にスキャンした JPEG で文字検出を妨げることが多い視覚的ノイズが除去されます。

### JPEG からテキストを認識する

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*この点が重要な理由:*  
`engine.setImage` は画像データを OCR パイプラインにバインドします。`engine.recognize()` は完全な認識プロセスを実行し、抽出されたテキストと信頼度指標を含む `OcrResult` を返します。

### 画像からテキストを抽出して出力する

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*この点が重要な理由:*  
`result.getText()` は画像内容のプレーンテキスト表現を提供します。コンソールに出力することで **convert image to text** が成功したことが確認でき、この文字列をファイル、データベース、または下流サービスへリダイレクトできます。

## 完全な実行可能サンプル

以下は、すべての手順を組み込んだ完全な Java クラスです。`YOUR_DIRECTORY` を JPEG ファイルへの絶対パスに置き換えてください。

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### 期待される出力

`sample.jpg` にテキスト “Hello World” が含まれていると仮定すると、コンソールに次のように表示されます。

```
=== Recognized Text ===
Hello World
```

画像に複数行が含まれている場合、各行は出力でもそれぞれの行として表示されます。

## 一般的なバリエーションとエッジケース

| 状況                                 | 推奨の調整 |
|--------------------------------------|------------|
| **Low‑resolution JPEG** (≤150 dpi)   | `engine.getPreprocessing().setUpsample(true);` を増やして、認識前に Aspose がアップスケールできるようにします。 |
| **Colored background** (e.g., scanned forms) | `engine.getPreprocessing().setBinarize(true);` を有効にして、画像を白黒に変換します。 |
| **Non‑Latin script** (e.g., Cyrillic) | 言語を設定します: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`。 |
| **Large batch processing**           | 複数の画像で単一の `OcrEngine` インスタンスを再利用して、起動オーバーヘッドを削減します。 |
| **Need confidence scores**           | 文字ごとの信頼度値を取得するには `result.getConfidence()` にアクセスします。 |

これらの調整は、さまざまな条件下で **load image for OCR** を行いながら、**perform OCR on image** を確実に実行できることを示しています。

## パフォーマンス上の考慮点

* **Memory usage:** 各 `ImageStream` は画像全体をメモリに保持します。非常に大きなファイル（例: >10 MB）の場合、`ImageStream.fromByteArray` を使用して画像をチャンクでストリーミングすることを検討してください。  
* **Thread safety:** `OcrEngine` は *スレッドセーフではありません*。OCR タスクを並列化する場合は、スレッドごとに別々のインスタンスを作成してください。  
* **License mode:** 評価モードではセッションあたり処理できるページ数が制限されます。本番環境ではライセンス版を導入してください。

## 結論

これで、Aspose OCR を使用して Java で画像ファイルの **perform OCR on image** を実行する方法が分かりました。このチュートリアルでは、画像の読み込み、前処理の有効化、JPEG からのテキスト認識、テキストの抽出、画像からテキストへの変換を、シンプルな 1 つのプログラムでカバーしました。  

ここからは、**recognize text from JPEG** をバルクで実行したり、出力を検索インデックスに統合したり、OCR と自然言語処理を組み合わせてよりスマートな文書パイプラインを構築したりと、関連トピックを探求できます。前処理オプションを試して、特定の画像ソースに最適な精度を実現してください。

--- 

*コード出力を示す画像*  
![perform OCR on image Java example](image-placeholder.png){alt="Aspose OCR Java を使用した画像の OCR 実行"}

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose OCR を使用した画像テキスト認識 – 完全な Java OCR チュートリアル](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR を使用した言語別画像テキスト OCR の方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose OCR を使用した Java の画像 OCR 前処理 – 精度向上とテキスト抽出](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}