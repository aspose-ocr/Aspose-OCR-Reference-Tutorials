---
category: general
date: 2026-06-16
description: Javaで画像ファイルに対してOCRを実行する方法を学びましょう。このチュートリアルでは、PNGからテキストを認識すること、画像からテキストを抽出すること、画像をテキストに変換すること、そしてOCR用に画像を読み込むことを取り上げています。
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: ja
og_description: Java を使用して画像の OCR を実行します。このガイドでは、PNG からテキストを認識し、画像からテキストを抽出し、すぐに実行できるサンプルで画像をテキストに変換する方法を示します。
og_title: Javaで画像のOCRを実行する – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Javaで画像のOCRを実行する – 完全ステップバイステップガイド
url: /ja/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像のOCRを実行する – 完全ステップバイステップガイド

画像ファイルで **perform OCR on image** を実行する必要があったことはありますか？どの Java ライブラリを選べばよいか分からないこともあるでしょう。レシートスキャナーや文書アーカイバを作る場合でも、単に画像を検索可能なテキストに変換したいだけでも、Javaで **perform OCR on image** を学ぶことは便利なスキルです。

このチュートリアルでは、**perform OCR on image** ファイルに必要なすべての手順を解説します：画像の読み込み、エンジンの設定、テキストの認識、そして最終的に結果を出力します。最後まで読むと、**recognize text from PNG** ファイル、**extract text from image** ソース、そして **convert image to text** を数行のコードで実現できるようになります。

## 前提条件

- Java 17 以上（コードは最新の JDK でコンパイル可能です）
- Maven がインストール済み（またはお好みのビルドツール）
- Java の基本構文に慣れていること
- テスト用の PNG ファイル（ここでは `hello.png` と呼びます）

> **Pro tip:** PNG が手元にない場合は、テキストのスクリーンショットを撮り、`resources` フォルダに `hello.png` として保存すれば作成できます。

## 作成するもの

`OcrDemo` という名前の小さなコンソールアプリケーションです：

1. **Loads image for OCR** – ディスクから PNG を読み込みます。  
2. **Performs OCR on image** – Tess4J 経由で Tesseract エンジンを使用します。  
3. **Extracts text from image** – 認識された内容を `String` として取得します。  
4. コンソールに結果を出力します。

さあ、始めましょう。

## Step 1: Set Up the Project and Add Tess4J

まず、Maven プロジェクト（または好みで Gradle）を作成します。人気の Tesseract OCR エンジンをラップした Tess4J 依存関係を追加してください。

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Why Tess4J?** アクティブに保守されており、クロスプラットフォームで動作し、**perform OCR on image** タスク向けのクリーンな Java API を提供します。

## Step 2: Prepare the Image‑Loading Logic

次に、**load image for OCR** するヘルパーメソッドを書きます。このメソッドは Java の `ImageIO` を使って PNG を `BufferedImage` に読み込みます。

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

メソッド名が **load image for OCR** の意図を明確に表しているので、コードが自己文書化されています。

## Step 3: Configure the OCR Engine to **Perform OCR on Image**

画像が用意できたら、`Tesseract` インスタンスを作成し、自動言語検出を有効にして `doOCR` を呼び出します。これが **perform OCR on image** データを処理する核心部分です。

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Why enable auto‑detect?** エンジンが画像に最適な言語モデルを自動で選択できるため、英語と他のスクリプトが混在する **convert image to text** のケースで特に有用です。

## Step 4: Put It All Together – The Main Application

以下がエントリーポイントです。**recognize text from PNG**、**extract text from image** を行い、最終的に結果をコンソールに出力します。完全に実行可能なサンプルです。

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Expected Output

`hello.png` に “Hello, OCR world!” というフレーズが含まれている場合、コンソールには次のように表示されます：

```
=== Recognized Text ===
Hello, OCR world!
```

画像の品質により出力は若干異なることがありますが、PNG に埋め込んだテキストが表示されるはずです。

## Step 5: Handling Common Edge Cases

### 5.1 Dealing with Low‑Resolution Images

元の PNG がぼやけていると OCR の精度が低下します。簡単な対策として、エンジンに渡す前に画像を拡大すると効果的です：

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

`engine.recognize(image)` の前に `upscale(image, 2)` を呼び出して結果を改善してください。

### 5.2 Multi‑Language Documents

フランス語やドイツ語のテキストが混在する場合は、`setLanguage` に言語コードを追加するだけです：

```java
tesseract.setLanguage("eng+fra+deu");
```

エンジンはこれらの言語モデルを組み合わせて **extract text from image** を試みます。

### 5.3 Skipping Empty Pages

スキャンした PDF のページが空白の PNG として出力されることがあります。空画像を検出すれば処理時間を節約できます：

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Step 6: Packaging and Running the Application

1. **Compile:** `mvn clean compile`  
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

` t​essdata` フォルダ（言語ファイルが格納されている）をコンパイル済み JAR の隣に配置するか、`OcrEngine` で絶対パスを指定してください。

## Conclusion

これで、Java を使って **perform OCR on image** ファイルを処理するための堅牢で本番環境向けのパターンが完成しました。**loading image for OCR** から **recognize text from PNG** まで、**extract text from image**、**convert image to text** の方法と、低解像度スキャンや多言語コンテンツといった難しいシナリオへの対処法を網羅しました。

次に試してみると良いでしょう：

- **Batch processing** – PNG ディレクトリをループし、各結果を `.txt` ファイルに書き出す。  
- **PDF generation** – 抽出したテキストを検索可能な PDF に埋め込む。  
- **Cloud OCR services** – ローカルの Tesseract パフォーマンスを Google Vision や Azure Cognitive Services などの API と比較する。

自由に実験し、パラメータを調整し、成果を共有してください。コーディングを楽しみ、画像が常にクリーンで検索可能なテキストに変換されますように！

![画像で OCR ワークフローを示す図](https://example.com/ocr-workflow.png "画像で OCR を実行する例")

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}