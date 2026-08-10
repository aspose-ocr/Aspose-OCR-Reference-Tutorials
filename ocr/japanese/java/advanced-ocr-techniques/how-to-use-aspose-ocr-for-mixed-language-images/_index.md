---
category: general
date: 2026-05-06
description: Aspose OCR を使用して画像からテキストを認識し、自動言語検出を有効にし、Java で OCR の速度を向上させる方法。
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: ja
og_description: Aspose OCR を使用して画像からテキストを迅速に認識し、自動言語検出を有効にし、Java で OCR の速度を向上させる方法。
og_title: 混合言語画像でAspose OCRを使用する方法
tags:
- Aspose
- OCR
- Java
- Image Processing
title: 混在言語画像で Aspose OCR を使用する方法
url: /ja/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 複数言語が混在した画像で Aspose OCR を使用する方法

画像に複数の言語が同時に含まれている場合に、**Aspose の使い方**でテキストを抽出できるか気になったことはありませんか？ あなた一人ではありません—開発者は、画像が英語、ロシア語、ヒンディー語、あるいは他のスクリプトを混在させると壁にぶつかることが頻繁です。 良いニュースは、Aspose OCR がこれをスムーズに処理し、言語セットを絞ることで **recognize text from image** をより高速に実行できることです。

このチュートリアルでは、**loads image for OCR** する完全な実行可能 Java サンプルを順に解説し、**automatic language detection** を有効にし、**improve OCR speed** するシンプルなコツをご紹介します。 最後まで読むと、抽出したテキストをコンソールに出力する自己完結型プログラムが手に入り、各設定がなぜ重要か理解できるようになります。

> **Prerequisites** – Java 17+ がインストールされていること、依存関係管理に Maven または Gradle を使用できること、そして Aspose OCR ライセンス（評価用の無料トライアルでも可）。他のライブラリは不要です。

---

## Step 1 – Add Aspose OCR to Your Project

**Aspose** を使用できるようにするには、ライブラリをクラスパスに追加する必要があります。Maven を使う場合は次のようになります。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Gradle を使う場合は次の通りです。

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** 常に最新の安定版リリースを使用してください。新しいバージョンには、**improve OCR speed** に直接影響するパフォーマンス向上が含まれていることが多いです。

---

## Step 2 – Create the OCR Engine Instance  

すべての Aspose OCR ワークフローの中心は `OcrEngine` です。インスタンス化はシンプルですが、エンジンは内部キャッシュを保持している点に留意してください。多数の画像で同一インスタンスを再利用すると、ライブラリがネイティブ初期化を繰り返さないため **improve OCR speed** が期待できます。

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Step 3 – **Load Image for OCR**  

Aspose は PNG、JPEG、TIFF、BMP など多数の画像形式をサポートしています。ここでは英語、ロシア語、ヒンディー語が混在した PNG を読み込む例を示します。`ImageStream.fromFile` ヘルパーはファイル I/O の詳細を抽象化し、画像を正しくエンジンにストリームします。

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **What if the image is in memory?** メモリ上の画像の場合は `ImageStream.fromByteArray(byte[])` を使用してください。バイトストリームとして画像を受け取る Web サービスに最適です。

---

## Step 4 – Enable Automatic Language Detection  

デフォルトでは Aspose OCR は単一言語を想定しているため、複数言語が混在した画像では文字化けが起きやすくなります。自動検出を有効にすると、エンジンは認識前に各テキストブロックのスクリプトを判別します。

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Step 5 – **Improve OCR Speed** by Restricting the Language Pool  

フルオートデテクトは Aspose がサポートするすべての言語（70 以上）を走査します。事前に想定される言語が分かっている場合は、エンジンにヒントを与えることで検索空間を縮小し、**improve OCR speed** が実現できます。

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Why does this help?** エンジンは不要な言語モデルをスキップするため、CPU サイクルとメモリを節約します。後から言語を追加したい場合は配列を更新するだけで、コードの書き換えは不要です。

---

## Step 6 – Perform the Recognition and **Recognize Text from Image**

いよいよ本格的な認識処理です。`recognize()` はプレーンテキスト、信頼度スコア、必要に応じてレイアウト情報を含む `OcrResult` オブジェクトを返します。

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Console Output

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

画像にノイズや傾きがある場合、該当行の信頼度が低くなることがあります。その際は、Aspose に渡す前に画像の前処理（デスキュー、二値化）を検討してください。

---

## Common Questions & Edge Cases

### What if the image is huge (e.g., >10 MP)?

大きな画像はメモリ消費が増え、処理速度が低下します。**improve OCR speed** の簡単な方法は、可読性を保ちつつ画像をダウンサンプリングすることです。

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### How do I handle right‑to‑left scripts like Arabic?

Aspose OCR はスクリプト方向を自動的に考慮しますが、後処理で `RightToLeft` フラグを設定すると便利な場合があります。

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Can I extract text from PDFs instead of images?

はい。各 PDF ページを画像に変換（Aspose PDF や任意のラスタライザ使用）し、同じ OCR パイプラインに渡すだけです。**recognize text from image** のロジックはそのまま適用できます。

---

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

ファイル名を `MixedLanguageDemo.java` として保存し、`javac` でコンパイル、`java MixedLanguageDemo` で実行してください。環境が正しく設定されていれば、コンソールに多言語テキストが表示されます。

---

## Conclusion

これで **how to use Aspose** で **recognize text from image** できるマルチランゲージ画像の処理方法、**automatic language detection** の有効化、そして言語プールを限定して **improve OCR speed** する実用的なコツが分かりました。上記のコードはそのままコピー＆ペースト可能で、ストリーム、バイト配列、あるいはウェブカメラのスナップショットから **load image for OCR** するシナリオにも応用できます。

次のステップとしては以下を試してみてください：

* 低品質スキャン向けに画像前処理（ノイズ除去、二値化）を追加する。  
* `OcrResult` を JSON にエクスポートし、下流サービスで利用する。  
* Spring Boot の REST エンドポイントに統合し、クライアントが画像をアップロードして即座に抽出テキストを取得できるようにする。

コーディングを楽しんで、OCR パイプラインが高速で正確、かつ多言語対応になることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}