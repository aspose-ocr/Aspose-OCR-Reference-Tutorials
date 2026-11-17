---
category: general
date: 2026-11-17
description: Javaで画像に対してOCRを実行し、シンプルなコード例を使って写真からテキストを抽出する方法を学びましょう。画像読み込みに関するJavaのヒントも含まれています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: ja
lastmod: 2026-11-17
og_description: Javaで画像にOCRを実行し、テキストを素早く抽出する方法。このガイドに従って画像をJavaで読み取り、すぐに実行できるサンプルで画像をテキストに変換しましょう。
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Javaで画像にOCRを実行する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Javaで画像に対してOCRを実行する方法 – ステップバイステップガイド
url: /ja/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像のOCRを実行する方法 – ステップバイステップガイド

画像で **OCR の実行方法** が必要な場合、このチュートリアルでは Java で実行可能な完全なソリューションを示します。画像ファイルの読み込み方法、OCR エンジンの設定方法、エンジンが認識したテキストの抽出方法が分かります。

スキャンした文書、領収書、スクリーンショットなどを扱う際は、視覚的なコンテンツを検索可能なテキストに変換する必要があることが多いです。本ガイドでは、画像の読み込みから抽出テキストの出力までのすべての手順を解説し、サポートされていないファイル形式や null 結果といった一般的な落とし穴にも対処します。

## Prerequisites

開始する前に、以下が揃っていることを確認してください。

* Java Development Kit (JDK) 8 以上がインストールされていること。
* OCR ライブラリを取得するためのビルドツール（Maven または Gradle）。
* 処理したい画像ファイル（JPEG、PNG、BMP）。

コードは **`com.asprise.ocr` パッケージの OCR ライブラリ** を使用しています。これは単一の JAR で済み、主要なプラットフォームすべてで動作します。インポート文とエンジン初期化コードを差し替えることで、他のプロバイダー（Tesseract、Google Vision など）に置き換えることができます。

## Step 1: Add the OCR dependency

Maven を使用している場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Gradle を使用している場合は、`build.gradle` にこの行を追加します。

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

これらの行により、**read image Java** のコードがコンパイルでき、実行時に OCR エンジンが利用可能になります。

## Step 2: Read the image with Java

画像ファイルの読み込みは、あらゆる **extract text image** ワークフローにおける最初の具体的なステップです。Java の組み込みクラス `ImageIO` がほとんどの一般的な形式を処理します。

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Why this matters:** `ImageIO.read` はサポートされていない形式や破損したファイルに対して `null` を返します。上記のメソッドは問題をログに記録し `null` を返すので、次のステップで適切に対処できます。

## Step 3: Create and configure the OCR engine

OCR エンジンは認識すべき言語を把握している必要があります。言語を設定することで、特に英語以外の文書に対して精度が大幅に向上します。

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Why this matters:** エンジンの起動は比較的重い操作です。そのため、バッチ処理を行う場合は一度作成したインスタンスを再利用すべきです。

## Step 4: Perform OCR and convert the image to text

画像がロードされ、エンジンの準備が整ったら、認識ステップを実行できます。これが **OCR の実行方法** の核心です。

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Edge‑case handling:** 画像が `null` の場合、メソッドは `NullPointerException` をスローせず空文字列を返します。これにより、ユーザー提供のファイルを扱う際のコードがより堅牢になります。

## Step 5: Display the extracted text

最後に、結果をコンソールに出力するか、別のコンポーネント（例：データベースや UI ウィジェット）に渡します。

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

`java OcrDemo sample.jpg` でプログラムを実行すると、コンソールに認識された文字が表示されます。これで **convert image to text** のサイクルが完了です。

### Expected output

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

画像に読み取れる文字が含まれていない場合、プログラムは `(no text detected)` と出力します。

## Common variations and how to adapt them

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **Different language** | `"eng"` を `"spa"`（スペイン語）や `"fra"`（フランス語）などに置き換える | 英語以外の言語で書かれた文書 |
| **Batch processing** | ファイルパスのリストをループし、同じ `Ocr` インスタンスを再利用する | 大量のスキャンページを処理する場合 |
| **Higher accuracy** | `Ocr.SPEED_SLOW` を使用するか、`ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` で数字のみのスキャンを有効にする | OCR の品質が重要なケース（例：請求書番号） |
| **Tesseract alternative** | インポートを `net.sourceforge.tess4j.Tesseract` に変更し、初期化コードを調整する | すでに Tesseract に依存しているプロジェクト |

## Pro tips

* エンジンに渡す前に **大きな画像をリサイズ** してください。OCR の速度はピクセル数に比例します。
* ソースがノイズの多い場合は、OpenCV などのライブラリを使って **前処理**（グレースケール化、コントラスト強調）を行いましょう。
* 短時間に多数呼び出す場合は **OCR エンジンをキャッシュ** してください。エンジンの起動・停止にはオーバーヘッドがかかります。
* 特定の形式（例：日付、電話番号）を期待する場合は、正規表現で **結果を検証** しましょう。

## Conclusion

これで **Java で画像の OCR を実行する方法** が分かりました。ファイルの読み込みから抽出テキストの表示まで、**read image Java**、**extract text image**、**convert image to text**、**image to text java** のテクニックを網羅し、実務シナリオ向けの実践的なヒントも提供しました。

今後は以下のことが可能です。

* アップロードを受け取る Web サービスに OCR ステップを組み込む。
* 出力を検索インデックスと統合し、スキャン文書の全文検索を実現する。
* 多言語対応やカスタム文字セットなど、より高度な OCR オプションを探求する。

Happy coding, and enjoy turning pictures into searchable text!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [JavaでOCRを使用する方法 – スペル補正付き画像テキスト抽出](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Aspose OCR を使った Java の画像からテキストへの変換 – 完全ガイド](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Java で OCR に GPU を有効化する方法 – 画像からテキスト抽出](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}