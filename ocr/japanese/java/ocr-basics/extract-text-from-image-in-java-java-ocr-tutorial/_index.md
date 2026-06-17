---
category: general
date: 2026-03-07
description: Java OCRで画像からテキストを抽出します。OCR用に画像を読み込む方法、言語を設定する方法、そして数分で完了する完全なJava OCRチュートリアルの実行方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: ja
og_description: Java OCR を使用して画像からテキストを抽出します。このチュートリアルでは、OCR 用に画像を読み込む方法、言語を設定する方法、そして
  Java OCR のチュートリアルをステップバイステップで実行する方法を示します。
og_title: Javaで画像からテキストを抽出 – 完全OCRガイド
tags:
- OCR
- Java
- Image Processing
title: Javaで画像からテキストを抽出する – Java OCRチュートリアル
url: /ja/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像からテキストを抽出する – 完全OCRガイド

Javaで **画像からテキストを抽出** したいと思ったことはありませんか？ ただ、どこから始めればいいか分からないこともあるでしょう。あなただけではありません—開発者はスキャンした看板、レシート、手書きメモを検索可能な文字列に変換しようとするたびに、同じ壁にぶつかります。  

良いニュースです。数分で、カンナダ語、英語、またはサポートされている任意の言語を読み取る OCR パイプラインを構築できます。このチュートリアルでは **load image for OCR** を行い、エンジンを設定し、**Java OCR tutorial** を実演します。コードをコピー＆ペーストしてすぐに実行できます。

## このガイドでカバーする内容

We'll start by listing the tools you’ll need, then dive straight into a **step‑by‑step** implementation. By the end you’ll be able to:

* 画像ファイルを Java の `ImageInputStream` にロードする。
* OCR エンジンを特定の言語（例ではカンナダ語）を認識するように設定する。
* 認識プロセスを実行し、抽出されたテキストを出力する。
* 設定を調整して精度を向上させ、一般的な落とし穴に対処する。

外部ドキュメントは不要です—必要なものはすべてここにあります。  

**Prerequisites**: Java 17 以上、Maven または Gradle などのビルドツール、そして `OcrEngine` クラスを提供する OCR ライブラリ（例として仮想の *SimpleOCR* SDK）です。Maven を使用している場合は、後述の依存関係を追加してください。

---

## Step 1 – プロジェクトを設定し OCR ライブラリを追加する

コードを書く前に、プロジェクトが OCR クラスを認識できるようにします。Maven を使用する場合は、以下のスニペットを `pom.xml` に追加してください。

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Gradle を使用する場合は、同等の設定は次の通りです。

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Pro tip:** ライブラリのバージョンは常に最新に保ちましょう。新しいリリースでは、精度向上につながる言語モデルの改善が含まれていることが多いです。

依存関係が解決したら、IDE をリフレッシュし、コーディングの準備が整います。

## Step 2 – 必要なクラスをインポートする

以下はサンプルで必要となるインポートの全リストです。意図的に最小限に抑えているので、各クラスの役割がはっきり分かります。

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Why these imports?** `OcrEngine` と `OcrResult` は OCR プロセスの中心であり、`ImageInputStream` はファイル読み取りのボイラープレートを抽象化します。`java.nio.file.Paths` を使用することで、コードが OS に依存しなくなります。

## Step 3 – OCR 用に画像をロードする

ここで多くの人が躓く部分があります：エンジンに正しい画像フォーマットを渡すことです。OCR SDK は `ImageInputStream` を期待しており、これはディスク上の任意のファイルから取得できます。

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Edge case:** 画像が破損している、またはサポートされていない形式（例：GIF）の場合、コンストラクタは `IOException` をスローします。呼び出しを try‑catch ブロックでラップするか、事前にファイルを検証してください。

## Step 4 – エンジンを特定の言語で認識するように設定する

ほとんどの OCR エンジンは多言語サポートを備えています。精度を上げるために、エンジンに対象言語を明示的に指定すべきです。ここではカンナダ語の言語コード `"kn"` を使用します。

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Why set the language?** 文字セットを限定することで、特に似たような字形が多いスクリプトの場合、誤認識（false positives）を減らすことができます。

言語を切り替える必要がある場合は、コード文字列を変更するだけで、他の変更は不要です。

## Step 5 – OCR プロセスを実行しテキストを抽出する

画像がロードされ、エンジンが設定されたら、実際の認識は単一のメソッド呼び出しで行えます。結果オブジェクトはプレーンテキストと、オプションで信頼度スコアを提供します。

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Common question:** *OCR が空文字列を返した場合は？*  
> 通常、画像の品質が低すぎる（ぼやけ、コントラスト低下）か、言語が正しく設定されていないことが原因です。画像を前処理（コントラスト上げ、二値化）するか、言語コードを再確認してください。

## Step 6 – 結果を表示する

最後に、コンソールに出力を表示します。実際のアプリケーションでは、データベースに保存したり、検索インデックスに流し込んだりすることもあります。

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Expected Output

ソース画像にカンナダ語のフレーズ “ಕರ್ನಾಟಕ” (Karnataka) が含まれている場合、コンソールには次のように表示されます。

```
Extracted text:
ಕರ್ನಾಟಕ
```

以上です—任意の言語や画像ソースに適応できる、完全な **use OCR in Java** ワークフローです。

---

## 完全な動作例

以下はコンパイル可能な完全なプログラムです。`YOUR_DIRECTORY` を画像ファイルへの実際のパスに置き換えてください。

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Tip:** 本番コードでは、複数の画像に対して単一の `OcrEngine` インスタンスを再利用することを検討してください。繰り返し作成するとコストがかかります。

---

## よくある質問とエッジケース

### ノイズの多い写真で精度を上げるには？

- **Pre‑process** 画像：グレースケールに変換、メディアンフィルタ適用、またはコントラストを上げる。
- **Resize** 画像を少なくとも 300 DPI にリサイズします。ほとんどの OCR エンジンはこの解像度を想定しています。
- 期待される出力が分かっている場合は、文字のホワイトリストを設定します（例：数字のみ）。

### PDF にもこのアプローチを使えますか？

はい。PDFBox や iText を使って各ページを画像として抽出し、同じパイプラインに流し込めば利用できます。コードは同一で、画像ソースが変わるだけです。

### 1 つの画像で複数言語を認識したい場合は？

多くの SDK では、カンマ区切りのリスト（例：`"en,kn"`）を渡すことができ、エンジンは提供されたスクリプトのいずれかにマッチしようとします。

### 信頼度スコアを取得する方法はありますか？

`OcrResult` には多くの場合 `getConfidence()` メソッドがあり、各行に対して 0 から 1 の浮動小数点数を返します。低信頼度の結果を除外するのに利用してください。

---

## 次のステップ

Java で **画像からテキストを抽出** できるようになったので、以下を検討してみてください：

- **Batch processing** – 画像フォルダをループし、結果を CSV に書き出す。
- **Integration with Apache Tika** – OCR と文書解析を組み合わせ、統合検索インデックスを構築する。
- **Server‑side API** – OCR ロジックを REST エンドポイントで公開する（Spring Boot なら簡単）。
- **Alternative libraries** – オープンソースが必要なら `tess4j` 経由で Tesseract を試す。

これらのトピックはすべて、この **java ocr tutorial** で扱った基本概念に基づいているので、自由に実験しコードを拡張してください。

---

## 結論

本稿では、**画像からテキストを抽出** する完全な Java の例を通して、**load image for OCR** の方法、言語設定の構成、そして **use OCR in Java** で可読文字列を取得する手順を示しました。このスニペットは自己完結型で、エラーを適切に処理し、最小限の手間で任意の Java プロジェクトに組み込めます。  

ぜひ試してみて、言語コードを調整すれば、スキャンした文書を検索可能なデータに変換できるようになります。コーディングを楽しんでください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}