---
category: general
date: 2026-08-28
description: Aspose OCRを使用してJavaでpng画像からテキストを抽出する方法を学びます。このチュートリアルでは、batch OCR processing、folderから画像を読み込む方法、extensionでファイルをフィルタリングする方法をカバーしています。
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aspose OCRを使用してJavaでpng画像からテキストを抽出する方法を学びます。このチュートリアルでは、batch OCR
  processing、folderから画像を読み込む方法、extensionでファイルをフィルタリングする方法をカバーしています。
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Javaでpngからテキストを抽出する方法 – batch OCR guide
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Javaでpngからテキストを抽出する方法 – batch OCR guide
url: /ja/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaでpngからテキストを抽出する方法 – バッチOCRガイド

pngファイルからテキストを抽出する必要があったが、数枚以上の画像に対してスケールさせる方法が分からない場合、ここが適切な場所です。多くの開発者は単一画像のOCR呼び出しから始めますが、フォルダーが数十、数百のファイルに増えるとすぐにパフォーマンスの壁にぶつかります。Aspose OCR for Java を使用すれば、ディレクトリを走査し、対象とする画像タイプだけをフィルタリングし、並列で認識を実行し、結果を元のファイル順と同じ順序で返す堅牢なバッチOCRパイプラインを構築できます。このガイドの最後までに、**バッチOCR処理** を信頼性かつ効率的に行う、すぐに使用できる Java スニペットが手に入ります。

![画像をテキストに変換する例](https://example.com/convert-images-to-text.png "PNGファイルから変換されたテキストを示すJavaコンソール出力のスクリーンショット")

## クイック回答
- **OCRを処理するライブラリは何ですか？** Aspose OCR for Java.
- **PNGとJPGを同時に処理できますか？** Yes – the sample filters both extensions.
- **OCRエンジンはスレッドセーフですか？** A single shared `AsposeOCR` instance is safe for concurrent use.
- **テスト用にライセンスが必要ですか？** A free temporary key is available from Aspose.
- **サブフォルダーは自動的にスキャンされますか？** `Files.walk` traverses the whole tree recursively.

## pngからテキストを抽出するとは？

`extract text from png` は、Portable Network Graphics ファイルに光学文字認識（OCR）を適用し、表示された文字を検索可能で編集可能な文字列に変換するプロセスを指します。Aspose OCR のエンジンはピクセルデータを読み取り、グリフ形状を識別し、単一のメソッド呼び出しで Unicode テキストを返します。

## なぜ Aspose OCR for Java を使用するのか？

Aspose OCR は **30 以上の言語** をサポートし、標準的な 8 コアサーバー上で **1 分あたり最大 500 枚の画像** を処理でき、**200 MB** までのファイルを画像全体をメモリに読み込まずに扱えます。これらの数値化された性能により、メモリ制限に悩むことなく、一般的なハードウェア上で大規模なバッチジョブを信頼して実行できます。

## 前提条件
- Java 17（または最近の LTS バージョン）。
- 依存関係管理のための Maven または Gradle。
- 処理したい PNG/JPG 画像が入ったディレクトリ。
- Java ストリームと `java.nio.file` パッケージの基本的な知識。
- （オプション）評価用の Aspose OCR 一時ライセンスキー。

> **プロのコツ:** 無料の一時キーは 30 日で期限切れになりますが、テスト用にフル API アクセスが可能です。

## プロジェクトのセットアップと Aspose OCR の追加方法

まず、Maven（または Gradle）プロジェクトを作成し、`pom.xml` に Aspose OCR の依存関係を追加します：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **なぜ重要か:** 依存関係を事前に宣言することで、コンパイラが `AsposeOCR`、`ParallelRecognizer`、および関連クラスを認識できるようになります。また、すべてのマシンで同じバージョンが使用されることが保証され、再現性のある **バッチOCR処理** にとって重要です。

ビルドが完了したら IDE をリフレッシュしてください。**External Libraries** の下に Aspose パッケージが表示されるはずです。

## OCRエンジンの初期化方法 – 単一インスタンスを共有

`AsposeOCR` は Aspose OCR ライブラリが提供する主要な OCR エンジンのクラスです。実行全体で **1** つの OCR エンジンインスタンスだけが必要です。スレッド間で共有することで、メモリを節約し、エンジンが言語パックを一度だけロードするため速度が向上します。

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` はスレッドセーフなので、ワーカースレッドプールを管理する `ParallelRecognizer` に安全に渡すことができます。

> **説明:** `ParallelRecognizer` はエンジンをスレッドプールでラップします。多数のファイルを送信すると、各ファイルに専用のワーカースレッドが割り当てられ、マルチコア CPU で真の並列処理が可能になります。

## フォルダーから画像を読み込む方法 – ディレクトリツリーを走査

`Files.walk` は、ファイルツリーを再帰的に走査し、`Path` オブジェクトのストリームを返す Java NIO のメソッドです。ここでは **フォルダーから画像を読み込む** 必要があり、すべての PNG または JPG を収集します。`Files.walk` API によりワンライナーで実装できますが、必要に応じて **pngからテキストを抽出** するフィルタを追加します。

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **ここでフィルタリングする理由:** `filter` を使用すると、**拡張子でファイルを早期にフィルタリング** でき、後の不要な I/O を削減します。また、コードが読みやすくなり、複雑な正規表現は不要です。

## OCRジョブを非同期に送信する方法

`recognizeAsync` は画像を OCR エンジンに非同期処理として送信し、保留中の結果を表す `Future<OcrResult>` を返します。ファイルリストが準備できたら、各パスを `ParallelRecognizer` に渡します。`recognizeAsync` メソッドは後で取得できるように `Future<OcrResult>` を返します。

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **内部で何が起きているか？** 各呼び出しは recognizer の内部エグゼキュータサービスにタスクをキューイングします。タスクは並列に実行されるため、100 枚の画像があるフォルダーでも、シングルスレッドループの数分の一の時間で処理できます。

## ファイル順序を保ちつつ結果を取得する方法

`Future<OcrResult>` は非同期 OCR タスクの結果を保持し、認識されたテキストを取得するための `get()` メソッドを提供します。`imagePaths` と同じ順序で futures を保存したため、リストを単に反復し `get()` を呼び出すだけで済みます。この呼び出しは該当画像が完了するまでだけブロックするため、余分な管理なしで順序が保たれます。

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**サンプルコンソール出力** (省略)

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **エッジケースの処理:** 特定の画像で例外（破損ファイル、サポート外形式）が発生した場合、例外を捕捉して残りの処理を続行します。これは信頼性のある **バッチOCR処理** パイプラインに不可欠な習慣です。

## リソースのクリーンアップ – recognizer のシャットダウン方法

`ParallelRecognizer.shutdown()` は内部スレッドプールを停止し、アプリケーションが終了する前にすべての OCR タスクが完了することを保証します。内部スレッドプールのシャットダウンを忘れないでください。忘れると JVM が終了時にハングする可能性があります。

```java
recognizer.shutdown();
```

以上です！このプログラムは任意のディレクトリを走査し、PNG/JPG ファイルをフィルタリングし、並列で OCR を実行し、元の順序で結果を出力します。

---

## 完全な動作例（コピー＆ペースト）

以下は完全な実行可能な Java クラスです。`"YOUR_DIRECTORY"` を画像フォルダーへのパスに置き換え、IDE またはコマンドラインから実行してください。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

クラスを実行すると、コンソールに抽出された文字列が表示され、I/O でブロックするループを書かずに **画像をテキストに変換** できたことを祝福できます。

---

## よくある質問 (FAQs)

**Q: PDF や TIFF も処理できますか？**  
A: もちろんです。Aspose OCR は 30 以上のフォーマット（PDF、TIFF、BMP、GIF など）をサポートしているので、ディレクトリ走査ステップのフィルタに目的の拡張子を追加するだけです。

**Q: 英語以外の言語、例えばスペイン語が必要な場合は？**  
A: `RecognitionLanguage.ENGLISH` を `RecognitionLanguage.SPANISH`（またはサポートされている任意の言語）に変更します。言語パックはライブラリに同梱されているため、追加のダウンロードは不要です。

**Q: フォルダーにサブフォルダーが含まれています—スキャンされますか？**  
A: はい。`Files.walk` はツリー全体を再帰的に走査するため、すべてのネストされた PNG/J

**Q: 200 MB を超える非常に大きな画像はどう扱いますか？**  
A: `ocrEngine.setUseStreaming(true)` を呼び出してストリーミングモードを有効にします。これによりエンジンは画像をチャンクで読み込み、ピークメモリ使用量を大幅に削減します。

**Q: 同時に実行する OCR スレッド数を制限する方法はありますか？**  
A: はい。`ParallelRecognizer` を構築する際に、第二引数として希望する最大スレッド数を渡します（例: `new ParallelRecognizer(ocrEngine, 4)`）。

---

**最終更新:** 2026-08-28  
**テスト環境:** Aspose OCR for Java 24.10  
**作者:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## 関連チュートリアル

- [Java バッチ OCR 処理ガイドで画像をテキストに変換](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Java で画像からテキストを読み取る 完全 Aspose OCR ガイド](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR を使用して画像からテキストを抽出 – 許可文字](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}