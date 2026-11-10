---
category: general
date: 2026-09-18
description: Aspose OCR を使用して Java で画像からテキストを抽出する方法を学びましょう。PNG、JPG、TIFF ファイルを一度の呼び出しで効率的にバッチ処理します。
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: バッチOCRで Java の画像からテキストを抽出する方法をマスターしましょう。Aspose OCR を使用して PNG、JPG、TIFF
  ファイルを一度の呼び出しで変換します。
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Javaで画像からテキストを抽出 – バッチOCRガイド
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: JavaでバッチOCRを使用して画像からテキストを抽出する方法
url: /ja/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでバッチOCRを使用して画像からテキストを抽出する方法

**画像からテキストを抽出**する必要があり、各ファイルごとにループを書くことなく迅速に行いたい場合、バッチOCRが解決策です。多くの実務プロジェクトでは、PNGのレシート、JPGのスクリーンショット、またはマルチページTIFFなど、スキャンされたフォルダーが渡され、これらを検索可能なテキストに変換する必要があります。Aspose OCRは、PNG、JPG、TIFFファイルを一括で処理する単一のメソッド呼び出しでこれを実現し、開発時間とCPUサイクルの両方を節約します。

## クイック回答
- **バッチOCRは何をしますか？** 1つのリクエストで�数の画像ファイルを処理し、各ファイルのテキストを返します。
- **対応しているフォーマットは何ですか？** PNG、JPG/JPEG、マルチページTIFFが標準でサポートされます。
- **別個のネイティブライブラリが必要ですか？** いいえ、Aspose OCR JARに必要なものはすべて含まれています。
- **スレッド数を制御できますか？** はい、バッチプロセッサで `setMaxParallelism` を使用します。
- **必要なJavaバージョンは？** Java 17以上。

## Aspose OCRとは？

Aspose OCRは、外部依存なしで画像ファイル内の印刷文字および手書き文字を認識するJavaライブラリです。60以上の言語をサポートし、バッチあたり最大100枚の画像を処理できるため、大規模な文書デジタル化に最適です。

## このチュートリアルでカバーする内容

画像パスのリストを読み込み、`OcrBatchProcessor` を作成し、並列度を調整し、単一の `recognize` 呼び出しを実行して抽出された文字列を出力します。最後には、PNG、JPG、TIFF ファイルから一括でテキストを抽出する実行可能なJavaプログラムが手に入ります。

- **バッチOCRの方法** は Aspose の `OcrBatchProcessor` を使用します。
- 異なるフォーマット（PNG、JPG、TIFF）の**画像からテキストを抽出**する方法。
- アプリの応答性を保つための並列度制御のヒント。
- コピー＆ペーストしてすぐに実行できる、完全な実行可能Javaプログラム。

Asposeの事前経験は不要です—基本的なJavaのインストールとお好みのIDEがあれば始められます。最後には、PNG、JPG、TIFF ファイルから一括でテキストを認識するための確固たる基盤が得られます。

---

![バッチOCRで複数の画像ファイルを処理する様子を示す図](/images/batch-ocr-diagram.png "バッチOCRの方法")

*画像の代替テキスト: 複数の画像ファイルが一緒に処理されるバッチOCRの図*

## 前提条件

| 要件 | 重要な理由 |
|-------------|----------------|
| Java 17以上 | Aspose OCRは最新のJVMを対象としています。 |
| MavenまたはGradle | Aspose OCRライブラリの追加を簡素化します。 |
| 基本的なJavaの知識 | コードの流れを理解するために必要です。 |
| サンプル画像のセット（`.png`, `.jpg`, `.tif`） | 抽出処理を実際に確認するためです。 |

これらがすでに揃っているなら、素晴らしいです—さっそく始めましょう。

## 手順 1: プロジェクトに Aspose OCR を追加する

最初に必要なのは Aspose OCR JAR です。Maven を使用する場合、以下を `pom.xml` に追加してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Gradle を好む場合、同等の設定は次のとおりです：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

依存関係を追加すると、**png からテキストを抽出**、**jpg からテキストを抽出**、**tiff からテキストを抽出**に必要なすべてが取り込まれます。追加のネイティブライブラリは不要です。

## 手順 2: 処理したい画像ファイルを定義する

ここで OCR エンジンに処理すべきファイルを指示します。ここが **バッチOCRの方法** が本当に活きるところです—パスのリストを渡すだけで、ライブラリが重い処理を行います。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **プロのコツ:** ファイルパスは絶対パスにするか、`Paths.get(...)` を使用して、異なる OS での予期せぬ問題を回避してください。

## 手順 3: バッチプロセッサを作成し、並列度を調整する

Aspose OCR には `OcrBatchProcessor` が同梱されており、複数の認識を並列で実行できます。スレッド数を制御することで、数十枚の画像がある場合でもアプリが CPU を占有しすぎるのを防げます。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

なぜ並列度を制限するのでしょうか？性能の低いノートパソコンでスレッドを過剰に起動すると、速度向上ではなく遅延が発生することがあります。`setMaxParallelism` を設定することで、速度と安定性のバランスを取れます。

## 手順 4: バッチOCR呼び出しを実行する

これが **バッチOCRの方法** の核心です：画像ごとに `RecognitionResult` オブジェクトのリストを返す単一の `recognize` 呼び出しです。  
`recognize` は提供された画像を処理し、抽出されたテキストを含む `RecognitionResult` オブジェクトのリストを返します。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

このメソッドはすべての画像が処理されるまでブロックし、テキストを返します。非ブロッキング動作が必要な場合は `CompletableFuture` でラップできますが、ほとんどのスクリプトでは同期呼び出しの方がコードをすっきりさせます。

## 手順 5: 抽出されたテキストを出力する

最後に、結果を反復処理して認識された文字列を表示します。これにより、さまざまなフォーマットの **画像からテキストを抽出** に成功したことが示されます。  
`RecognitionResult` は単一画像の OCR 出力を保持し、抽出されたテキストと信頼度スコアを含みます。

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### 期待される出力

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

OCR エンジンがファイルを読み取れない場合、`getText()` メソッドは空文字列を返すため、警告を記録する簡単なチェックを追加できます。

## 完全な動作例

すべてをまとめると、完全な実行可能な Java クラスがこちらです。`BatchOcrTutorial.java` という名前のファイルにコピーし、画像パスを調整して `javac && java` を実行してください。

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

実行すると、コンソールに各 PNG、JPG、TIFF ファイルの抽出テキストが表示されます—**バッチOCRの方法** が課題であるときにまさに必要なものです。

## よくある質問とエッジケース

### 画像が3枚以上ある場合は？

`imageFiles` リストにエントリを追加するだけです。バッチプロセッサは `setMaxParallelism` で設定したスレッドに自動的に作業を分配します。

### 画像がサブフォルダーにある場合、手動で各ファイルを列挙する必要がありますか？

`Files.list` はディレクトリ内のパスを遅延生成するストリームとして返します。

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

これによりコードは柔軟性を保ち、**バッチOCRの方法** を尊重したままです。

### 低信頼度の結果はどう処理しますか？

`getConfidence()` は認識されたテキストが正しい可能性を示す数値の信頼度を返します。

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCRは他の言語をサポートしていますか？

はい—`recognize` 呼び出しの前に `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（またはサポートされている任意の enum）を呼び出します。これにより英語以外にも対応でき、**画像からテキストを抽出** が真に多言語対応になります。

## パフォーマンスのヒント

* **バッチサイズが重要** – 大きなバッチはオーバーヘッドを減らしますが、非常に大きなリストはメモリを多く消費する可能性があります。バッチあたり 50〜200 枚でテストしてください。
* **並列度** – 4 コア CPU では通常 `setMaxParallelism(4)` が最高のスループットを提供します。サーバーの負荷に応じて調整してください。
* **画像前処理** – OCR 前に画像をグレースケールに変換したりコントラストを上げたりすると、特にノイズの多いスキャンで精度が向上します。

## 結論

これで、Aspose OCR を使用した Java における **バッチOCRの方法**、さまざまなフォーマットの **画像からテキストを抽出** 方法、そして並列度を制御する重要性が分かりました。完全なコード例は、PNG、JPG、TIFF ファイルから単一の効率的な呼び出しでテキストを認識することを示しています。

次のステップに進む準備はできましたか？OCR の出力を検索インデックス、データベース、または AI 要約ツールに流し込みましょう。PDF 入力（Aspose OCR は対応）を試したり、OpenCV などの画像前処理ライブラリと組み合わせて精度をさらに高めることも可能です。

コーディングを楽しんでください。そして、バッチOCRは頭痛の種である必要はありません。適切なツールと明確なパターンがあれば、画像の山をすぐに検索可能なテキストに変換できます。

## よくある質問

**Q: このコードはヘッドレスサーバーで実行できますか？**  
A: はい、Aspose OCR は純粋な Java で UI コンポーネントを必要としないため、ヘッドレス環境でも問題なく動作します。

**Q: 本番環境で使用するにはライセンスが必要ですか？**  
A: 本番展開には商用ライセンスが必要です。評価用に無料トライアルが利用可能です。

**Q: 対応しているオペレーティングシステムは？**  
A: Java 17+ が動作するすべての OS（Windows、Linux、macOS）をサポートします。

**Q: Aspose OCR が認識できる言語は何ですか？**  
A: 標準で 60 以上の言語をサポートしており、英語やスペイン語からアラビア語、中国語まで対応しています。

**Q: Aspose OCR が扱える最大ファイルサイズは？**  
A: 個々の画像ファイルは最大 200 MB までサポートされます。より大きなファイルは処理前に分割してください。

---

**最終更新日:** 2026-09-18  
**テスト環境:** Aspose OCR 24.9 for Java  
**作者:** Aspose

## 関連チュートリアル

- [画像からテキストを抽出 – Java 用 OCR 基礎](/ocr/java/ocr-basics/)
- [Java でバッチOCRする完全ガイド – テキスト抽出](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Java で画像 OCR を前処理して精度向上 – テキスト抽出](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}