---
category: general
date: 2026-07-21
description: Java OCR を使用して画像からテキストを抽出します。PNG をテキストに変換する方法、PNG からテキストを読み取る方法、OCR 用に画像を読み込む方法、そして数ステップで画像に対して
  OCR を実行する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: ja
lastmod: 2026-07-21
og_description: Javaで画像からテキストを抽出する。このガイドでは、PNGをテキストに変換する方法、PNGからテキストを読み取る方法、OCR用に画像を読み込む方法、そして画像で効率的にOCRを実行する方法を紹介します。
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Javaで画像からテキストを抽出する – ステップバイステップ OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Javaで画像からテキストを抽出する – 完全OCRガイド
url: /ja/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像からテキストを抽出 – 完全OCRガイド

画像から **テキストを抽出** したいけど、どの Java ライブラリを選べばいいか分からないことはありませんか？レシートのデジタル化、PDF のスキャン、検索可能なアーカイブの構築など、PNG からテキストを取り出す作業は多くの開発者にとって日常的な課題です。

このチュートリアルでは、**PNG をテキストに変換**、**PNG からテキストを読み取る**、**OCR 用に画像をロード**、そして **画像上で OCR を実行** する手順を、数行のシンプルな Java コードで実装する方法を実践的に解説します。最後まで進めば、どのプロジェクトにも組み込める実行可能なプログラムが手に入ります。

## 作成するもの

以下の機能を持つ小さな Java コンソールアプリを作ります。

1. ディスク上の PNG ファイルを読み込む。  
2. 画像を OCR エンジン（Tess4J、Tesseract の Java ラッパー）に渡す。  
3. 認識されたテキストをコンソールに出力する。

外部サービスは使用せず、純粋な Java とオープンソースの OCR エンジンだけで完結します。

## 前提条件

- **Java 17** 以上（コードは古いバージョンでもコンパイルできますが、Java 17 で最新の言語機能が利用可能です）。  
- 依存関係管理に **Maven** または **Gradle**。  
- `sample.png` という名前のサンプル PNG を、`src/main/resources` など参照可能なフォルダに配置しておくこと。  
- Java の `main` メソッドと例外処理に関する基本的な知識。

これらが初めてでも心配はいりません。各ステップで簡単に復習します。

## 手順 1: プロジェクトを作成し OCR ライブラリを追加

まず Maven プロジェクト（または好みで Gradle）を作成し、Tess4J の依存関係を追加します。Tess4J は Tesseract のバイナリを自動で取得してくれます。

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Pro tip:** Gradle を使用する場合は、同等の行は `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'` です。

このライブラリを追加すると、**画像上で OCR を実行** するための `Tesseract` クラスが利用可能になります。

## 手順 2: OCR 用に画像をロード

次に **OCR 用に画像をロード** します。Tess4J は `java.awt.image.BufferedImage` を扱うので、`ImageIO` で PNG を読み込みます。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

上記メソッドは **OCR 用に画像をロード** するロジックをきれいに分離しており、テストがしやすくなります。コメントは元のスニペットを踏襲しつつ、明確さを加えています。

## 手順 3: 画像上で OCR を実行

画像がメモリ上にあるので、いよいよ **画像上で OCR を実行** します。`Tesseract` インスタンスがエンジンとなり、Tess4J に同梱されているデフォルトの英語データを使用します。

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

ここでは元の「手順 1」と「手順 4」を 1 つのメソッドに統合しました。`Tesseract` オブジェクトは軽量なので、コードをコンパクトに保つためです。コメントは依然として元の手順を参照しています。

## 手順 4: すべてをまとめる – main メソッド

最後に `main` で全体を結びつけます。ここで **PNG からテキストを読み取る** 処理を行い、結果をコンソールに表示します。

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

`mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"`（または Gradle の同等コマンド）を実行すると、次のような出力が得られるはずです。

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

この出力により、**画像からテキストを抽出**、**PNG をテキストに変換**、そして **PNG からテキストを読み取る** が 1 つの整ったプログラムで実現できたことが確認できます。

## よくあるエッジケースの対処

### 低品質画像

PNG がぼやけていたりコントラストが低いと OCR の精度が落ちます。簡単な対策として画像を前処理します。

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### 多言語サポート

Tess4J は多数の言語に対応しています。対応する `.traineddata` ファイルをダウンロードし、例えばスペイン語なら `tesseract.setLanguage("spa")` と指定します。

### 大容量 PDF やマルチページ画像

PDF 内の画像ファイルから **画像からテキストを抽出** したい場合は、まず PDFBox などで各ページを PNG に分割し、同じ OCR 処理に流し込みます。

## 完全動作サンプル（コード一式）

以下は実行可能な完全版 Java クラスです。`src/main/java/com/example/ocrdemo/OcrDemo.java` にコピペすればすぐに動作します。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

クラスを実行すると OCR 結果が出力され、**画像上で OCR を実行** し、PNG を編集可能なテキストに変換できたことが確認できます。

## まとめと次のステップ

軽量な Java 環境で **画像からテキストを抽出** する方法を学びました。これで **OCR 用に画像をロード**、**画像上で OCR を実行**、**PNG からテキストを読み取る** の基本が身につきました。

さらに踏み込むなら次のアイデアを試してみてください。

- **バッチ処理:** ディレクトリ内の PNG を順に処理し、結果を `.txt` ファイルに書き出す。  
- **データベース連携:** 抽出した文字列とメタデータを保存し、検索可能なアーカイブを構築。  
- **NLP と組み合わせ:** OCR 出力を感情分析モデルに渡し、即座にインサイトを取得。

これらの拡張は本チュートリアルで扱ったコア概念に基づいているので、すぐに実装に移れます。

---

*Happy coding! If you hit any snags

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}