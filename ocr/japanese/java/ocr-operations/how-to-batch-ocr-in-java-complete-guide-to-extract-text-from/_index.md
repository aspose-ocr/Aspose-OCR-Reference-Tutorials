---
category: general
date: 2026-02-09
description: Aspose OCR を使用して Java でバッチ OCR を学びましょう。画像からテキストを抽出し、PNG、JPG、TIFF ファイルのテキストを一度の呼び出しで認識します。
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: ja
og_description: JavaでバッチOCRをマスターしましょう。このチュートリアルでは、Aspose OCRを使用してPNG、JPG、TIFF画像からテキストを抽出する方法を、分かりやすいコード例とともに紹介します。
og_title: JavaでバッチOCRを行う方法 – 画像からテキストを効率的に抽出する
tags:
- OCR
- Java
- Aspose
title: JavaでバッチOCRを行う方法 – 画像からテキストを抽出する完全ガイド
url: /ja/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでバッチOCRを行う方法 – 画像からテキストを抽出する完全ガイド

たくさんの画像をそれぞれループを書かずに **バッチOCRのやり方** できるか、考えたことはありませんか？ あなただけではありません。実際のプロジェクトでは、PNG のレシートや JPG のスクリーンショット、さらにはマルチページの TIFF など、スキャンされた画像が入ったフォルダーが渡され、テキストを素早く取得する必要があります。  

良いニュースは、Aspose OCR がまさにそれを実現できることです。PNG、JPG、TIFF ファイルから一度にテキストを認識する単一のメソッド呼び出しだけで済みます。このチュートリアルでは、プロジェクトのセットアップから結果の出力までの全工程を順を追って解説し、すぐに画像からテキストを抽出できるようにします。

## このチュートリアルでカバーする内容

* **バッチOCRのやり方** を Aspose の `OcrBatchProcessor` を使用して
* さまざまな形式（PNG、JPG、TIFF）の **画像からテキストを抽出する方法** 
* アプリの応答性を保つための並列処理制御のヒント
* すぐにコピー＆ペーストして実行できる、完全な実行可能な Java プログラム

Aspose の事前経験は不要です—基本的な Java 環境とお好みの IDE があれば始められます。最後まで読めば、PNG、JPG、TIFF ファイルを大量に認識するための確固たる基礎が身につきます。

---

![Diagram illustrating how to batch OCR multiple image files](/images/batch-ocr-diagram.png "バッチOCR")

*画像の代替テキスト: 複数の画像ファイルが一緒に処理される様子を示すバッチOCR図*

## 前提条件

| 必要条件 | 重要な理由 |
|-------------|----------------|
| Java 17 以上 | Aspose OCR は最新の JVM を対象としています。 |
| Maven または Gradle | Aspose OCR ライブラリの追加が簡単になります。 |
| 基本的な Java 知識 | コードの流れを理解するために必要です。 |
| サンプル画像のセット（`.png`, `.jpg`, `.tif`） | 抽出結果を実際に確認するために使用します。 |

これらがすでに揃っているなら、さっそく始めましょう。

## Step 1: Add Aspose OCR to Your Project

最初に必要なのは Aspose OCR の JAR です。Maven を使う場合は `pom.xml` に以下を追加します：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Gradle を好む場合は同等の記述は次の通りです：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

この依存関係を追加すると、**recognize text from png**、**recognize text from jpg**、**recognize text from tiff** に必要なすべてが自動的に取得されます。追加のネイティブライブラリは不要です。

## Step 2: Define the Image Files You Want to Process

次に OCR エンジンに処理させるファイルを指定します。ここが **バッチOCRのやり方** の真価です—パスのリストを渡すだけで、ライブラリが重い処理をすべて引き受けます。

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro tip:** ファイルパスは絶対パスで指定するか、`Paths.get(...)` を使用して OS 間の予期せぬ問題を回避してください。

## Step 3: Create the Batch Processor and Tune Parallelism

Aspose OCR には `OcrBatchProcessor` が用意されており、複数の認識を並列で実行できます。スレッド数を制御することで、画像が多数あるときにアプリが CPU を独占しすぎるのを防げます。

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

なぜ並列度を制限するのでしょうか？ 低スペックのノートパソコンでスレッドを増やしすぎると、速度向上どころか逆に遅くなることがあります。`setMaxParallelism` を設定すれば、速度と安定性のバランスを取れます。

## Step 4: Run the Batch OCR Call

**バッチOCRのやり方** の核心はここです：画像ごとに `RecognitionResult` オブジェクトを返す単一の `recognize` 呼び出しです。

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

このメソッドはすべての画像が処理されるまでブロックし、完了後にテキストを返します。非同期が必要な場合は `CompletableFuture` でラップできますが、ほとんどのスクリプトでは同期呼び出しの方がコードがすっきりします。

## Step 5: Print the Extracted Text

最後に結果をイテレートして認識された文字列を表示します。これにより、さまざまな形式の **画像からテキストを抽出する** に成功したことが確認できます。

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Expected Output

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

OCR エンジンがファイルを読めなかった場合、`getText()` メソッドは空文字列を返すので、簡単なチェックを入れて警告をログに出すことができます。

## Full Working Example

すべてをまとめた、すぐに実行可能な Java クラスを示します。`BatchOcrTutorial.java` という名前で保存し、画像パスを調整したうえで `javac && java` を実行してください。

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

実行すると、各 PNG、JPG、TIFF ファイルの抽出テキストがコンソールに出力されます—**バッチOCRのやり方** が頭に浮かんだときにまさに必要な結果です。

## Common Questions & Edge Cases

### 画像が3枚以上ある場合は？

`imageFiles` リストにエントリを追加するだけです。バッチプロセッサは `setMaxParallelism` で設定したスレッド数に合わせて自動的に作業を分割します。

### 画像がサブフォルダーにある—手動で一覧にする必要がありますか？

特定の拡張子を持つすべてのファイルをプログラムで収集できます：

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

この方法ならコードが柔軟になり、**バッチOCRのやり方** を引き続き尊重できます。

### 信頼度の低い結果はどう処理すべき？

`RecognitionResult` には `getConfidence()` メソッドがあります。閾値以下の結果を除外し、DPI を上げて再試行するロジックを組み込めます：

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR は他の言語をサポートしていますか？

はい。`recognize` 呼び出しの前に `ocrProcessor.setLanguage(OcrLanguage.Spanish)`（またはサポートされている任意の enum）を呼び出すだけで、英語以外にも対応できます。これにより **画像からテキストを抽出する** が真に多言語対応になります。

## Performance Tips

* **Batch size matters** – バッチが大きいほどオーバーヘッドが減りますが、リストが非常に大きいとメモリ消費が増えることがあります。50〜200 枚程度でテストしてみてください。
* **Parallelism** – 4 コア CPU では `setMaxParallelism(4)` が一般的に最高のスループットを示します。サーバーの負荷に応じて調整してください。
* **Image preprocessing** – OCR 前に画像をグレースケール化したりコントラストを上げたりすると、特にノイズが多いスキャンで精度が向上します。

## Conclusion

これで Java で Aspose OCR を使った **バッチOCRのやり方**、さまざまな形式の **画像からテキストを抽出する** 方法、そして並列度を制御する重要性が分かりました。完全なコード例は PNG、JPG、TIFF ファイルを単一の効率的な呼び出しで認識する方法を示しています。

次のステップに進みませんか？ OCR の出力を検索インデックスやデータベース、あるいは AI 要約ツールに流し込んでみましょう。PDF 入力（Aspose OCR がサポート）や OpenCV などの画像前処理ライブラリと組み合わせれば、さらに高精度が期待できます。

Happy coding, and remember—batch OCR doesn’t have to be a headache. With the right tools and a clear pattern, you’ll be turning piles of pictures into searchable text in no time.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}