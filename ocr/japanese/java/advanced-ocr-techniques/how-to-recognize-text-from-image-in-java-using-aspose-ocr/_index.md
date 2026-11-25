---
category: general
date: 2026-09-29
description: Java と Aspose OCR を使用して画像からテキストを認識する方法を学びましょう。このガイドでは、jpg からテキストを抽出する方法と
  OCR の精度を向上させる方法も紹介しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- extract text from jpg
- how to improve OCR accuracy
- Aspose OCR Java
- Java image processing
language: ja
lastmod: 2026-09-29
og_description: Aspose OCR を使用して Java で画像からテキストを認識します。ステップバイステップのチュートリアルに従い、JPG からテキストを抽出し、OCR
  の精度を向上させる方法を学びましょう。
og_image_alt: Java code screenshot that recognizes text from image using Aspose OCR
og_title: Javaで画像からテキストを認識する – 完全なAspose OCRガイド
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  headline: How to recognize text from image in Java using Aspose OCR
  type: TechArticle
- description: Learn how to recognize text from image with Java and Aspose OCR. This
    guide also shows how to extract text from jpg and how to improve OCR accuracy.
  name: How to recognize text from image in Java using Aspose OCR
  steps:
  - name: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
    text: '**Pre‑process the image** – apply contrast stretching or binarization using
      OpenCV before handing it to Aspose OCR. Cleaner edges give higher confidence.'
  - name: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
    text: '**Crop unnecessary margins** – the engine spends time analyzing blank space,
      which can lower the overall confidence score.'
  - name: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
    text: '**Choose the correct language pack** – loading only the languages you need
      speeds up recognition and reduces false positives.'
  - name: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
    text: '**Use the latest Aspose OCR version** – each release includes updated neural
      models that improve accuracy out‑of‑the‑box.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Aspose OCR を使用して Java で画像からテキストを認識する方法
url: /ja/java/advanced-ocr-techniques/how-to-recognize-text-from-image-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでAspose OCRを使用して画像からテキストを認識する方法

Javaアプリケーションで**画像からテキストを認識**する必要がある場合、このチュートリアルではすぐに実行できるソリューションを示します。jpgファイルからテキストを抽出し、GPUアクセラレーションを有効にし、スペル補正を適用して、一般的な質問である*OCR精度を向上させる方法*に答える方法が分かります。

このガイドでは、Mavenの設定、完全なソースコード、各構成オプションの説明、低品質画像の取り扱いに関するヒントなど、必要なすべてを網羅しています。最後まで実行すれば、認識されたテキストをコンソールに出力する動作プログラムが手に入ります。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* Java 17（またはそれ以降） – Aspose OCRはJava 8+をサポートしていますが、最新のランタイムの方がパフォーマンスが向上します。
* 依存関係管理のための Maven 3.8+。
* Aspose OCR for Java のライセンス（評価用の無料トライアルでも可）。  
* 明瞭で読みやすいテキストが含まれる JPG 画像（`sample.jpg`）。

これらが不足している場合は、JDK を [oracle.com/java](https://www.oracle.com/java/technologies/downloads/) からインストールし、Apache のサイトにある Maven インストールガイドに従ってください。

## プロジェクトにAspose OCRを追加する

`pom.xml`（既存のものに追加しても可）を作成し、Aspose OCR の依存関係を含めます。

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <dependencies>
    <dependency>
      <groupId>com.aspose</groupId>
      <artifactId>aspose-ocr</artifactId>
      <version>23.12</version> <!-- latest stable at time of writing -->
    </dependency>
  </dependencies>
</project>
```

`mvn clean compile` を実行してライブラリをダウンロードします。この依存関係には、GPU 使用やスペル補正に必要なすべてのネイティブバイナリが含まれています。

## ステップ 1: 画像からテキストを認識するOCRエンジンの設定

最初に行うことは `OcrEngine` のインスタンスを作成することです。このオブジェクトが OCR パイプライン全体を統括します。

```java
// Step 1: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

エンジンを作成しただけでは画像はロードされません。内部リソースの準備だけが行われます。この分離により、同じエンジンを複数の画像で再利用でき、バッチ処理に便利です。

## ステップ 2: 処理速度向上のためにGPUアクセラレーションを有効にする

マシンに対応する GPU がある場合、GPU をオンにすると認識時間が最大 70 % 短縮できます。これは速度面で*OCR精度を向上させる方法*に直接答えるもので、性能低下なしに高解像度画像を扱えるようになります。

```java
// Step 2 (optional): Use GPU if available
engine.getConfiguration().setUseGpu(true);
```

> **Pro tip:** ヘッドレスサーバーで実行する場合は、CUDA ドライバーがインストールされていることを確認してください。インストールされていないと CPU にフォールバックし、エラーは発生しません。

## ステップ 3: OCR精度向上のためにスペル補正を有効にする

スペル補正は軽量な言語モデルで、一般的な認識ミス（例: “l0ve” → “love”）を修正します。これを有効にすることは、印刷テキストに対して*OCR精度を向上させる方法*の最も効果的な手段の一つです。

```java
// Step 3 (optional): Enable spell correction
engine.getConfiguration().setSpellCorrector(true);
```

手書きのスキャンノートを処理する場合は、モデルが印刷フォント向けに調整されているため、この機能を無効にした方が良いことがあります。

## ステップ 4: JPG画像からテキストを抽出するために画像をロードする

画像ファイルをロードします。`ImageStream.fromFile` ヘルパーは Aspose OCR がサポートする任意の形式を受け付けますが、例では最も一般的な Web 形式である JPG に焦点を当てています。

```java
// Step 4: Load the image that contains the text to be recognized
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

**Why JPG?** JPEG 圧縮は OCR を混乱させるアーティファクトを生むことがあります。精度を最大化するには、DPI が少なくとも 300 の画像を使用し、過度な圧縮は避けてください。PNG や TIFF がある場合は `fromFile` に直接渡せば、コードを変更する必要はありません。

## ステップ 5: OCRを実行し、認識されたテキストを取得する

最後に `recognize()` を呼び出し、結果を出力します。このメソッドは生テキスト、信頼度スコア、各単語のバウンディングボックスを含む `OcrResult` オブジェクトを返します。

```java
// Step 5: Run OCR and get the result
OcrResult result = engine.recognize();
System.out.println("=== Recognized text ===");
System.out.println(result.getText());
```

### 期待される出力

```
=== Recognized text ===
Welcome to Aspose OCR demo.
This text was extracted from a JPG image.
```

出力に文字化けが含まれる場合は、**ステップ 3**（スペル補正）を見直し、画像が DPI 推奨値を満たしているか確認してください。

## 一般的なバリエーションとエッジケース

| 状況 | 推奨調整 |
|-----------|------------------------|
| **低解像度画像 (< 150 DPI)** | エンジンに渡す前に画像を拡大するか、`engine.getConfiguration().setScaleFactor(2.0)` を使用してエンジン内部でリサンプリングさせます。 |
| **多言語ドキュメント** | `engine.getConfiguration().setLanguage("eng,spa")` を設定し、英語とスペイン語の辞書を同時にロードします。 |
| **大量のファイルをバッチ処理** | 同じ `OcrEngine` インスタンスを再利用し、各新ファイルごとに `engine.setImage(...)` を呼び出すだけにします。これによりネイティブライブラリの再ロードが回避できます。 |
| **メモリ制約のある環境** | GPU を無効化 (`setUseGpu(false)`) し、スペル補正も無効化 (`setSpellCorrector(false)`) して RAM 使用量を削減します。 |
| **JPG ではなく PNG からテキスト抽出** | コード変更は不要です。`fromFile` に `.png` パスを指定するだけで、ライブラリが自動的に形式を検出します。 |

## OCR精度を向上させるためのプロのヒント

1. **画像の前処理** – OpenCV を使ってコントラスト伸張や二値化を行い、Aspose OCR に渡す前にエッジをクリアにします。これにより信頼度が上がります。  
2. **不要な余白をトリミング** – エンジンは空白領域の解析にも時間を費やすため、全体の信頼度スコアが低下することがあります。  
3. **正しい言語パックを選択** – 必要な言語だけをロードすれば認識速度が向上し、誤検出が減ります。  
4. **最新の Aspose OCR バージョンを使用** – 各リリースには更新されたニューラルモデルが含まれ、箱出しの精度が向上しています。

## 完全な実行可能サンプル

以下はすべての手順をまとめた完全な Java クラスです。`SimpleOcr.java` として保存し、画像パスを調整した上で `mvn exec:java -Dexec.mainClass=SimpleOcr` を実行してください。

```java
import com.aspose.ocr.*;

public class SimpleOcr {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: (Optional) Enable GPU acceleration for faster processing
        engine.getConfiguration().setUseGpu(true);

        // Step 3: (Optional) Enable spell correction to improve OCR accuracy
        engine.getConfiguration().setSpellCorrector(true);

        // Step 4: Load the image that contains the text to be recognized
        // This example extracts text from jpg, but any supported format works.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 5: Perform OCR and retrieve the recognized text
        OcrResult result = engine.recognize();

        System.out.println("=== Recognized text ===");
        System.out.println(result.getText());
    }
}
```

プログラムを実行すると認識されたテキストがコンソールに出力され、**画像からテキストを認識**する方法、**JPG からテキストを抽出**する方法、そして **OCR精度を向上させる方法** の主要テクニックを習得したことが確認できます。

## 結論

本チュートリアルでは、Aspose OCR を使用した Java における**画像からテキストを認識**する方法、**JPG からテキストを抽出**する方法、そして *OCR精度を向上させる方法* に関する実践的な手段を学びました。このアプローチは完全に自己完結型で、Maven 依存関係、JPEG ファイル、いくつかの設定フラグさえあれば開始できます。

次に検討できるステップ：

* Aspose PDF を使って認識テキストを検索可能な PDF に変換する。  
* シンプルなループでフォルダ内の画像を一括処理（バッチ OCR）。  
* Spring Boot の REST エンドポイントに OCR エンジンを組み込み、オンデマンドで画像処理を提供する。

画像品質、言語パック、ハードウェア設定を変えて実験し、各要素が OCR パフォーマンスに与える影響を確認してください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}