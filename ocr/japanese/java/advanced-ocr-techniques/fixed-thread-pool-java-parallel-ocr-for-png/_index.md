---
category: general
date: 2026-02-17
description: 固定スレッドプールを使用したJavaで、PNG画像からテキストを抽出する並列OCR処理と、ExecutorServiceを適切にシャットダウンする方法を学びます。
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: ja
og_description: 固定スレッドプールを使用したJavaが、PNG画像からテキストを並列に抽出し、スキャンしたページのテキストを変換し、エグゼキュータサービスを安全にシャットダウンする方法を発見してください。
og_title: 固定スレッドプール Java – PNG 用並列 OCR
tags:
- java
- ocr
- multithreading
- aspose
title: 固定スレッドプール Java – PNG の並列 OCR
url: /ja/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – PNG の並列 OCR

たくさんの PNG ファイルで OCR を高速化するために **fixed thread pool java** を使用する方法を考えたことがありますか？このチュートリアルでは、**extract text from PNG** 画像を並列に処理し、**convert scanned pages text** を編集可能な文字列に変換し、作業が完了したら安全に **shut down executor service** する方法をご紹介します。

シングルスレッドのループが何分も続くのを見たことがあるなら、次のページが始まる前に現在のページが終わるのを待つフラストレーションが分かるはずです。良いニュースは、数行の Java と Aspose OCR を使えば、CPU コアすべてのパワーを解き放ち、スキャンしたページを検索可能なテキストに変換し、アプリケーションを応答性の高い状態に保てることです。

以下に、すぐに実行できる完全なサンプルと、各要素が重要な理由、よくある落とし穴、任意の OCR ライブラリに適用できるヒントを示します。

---

## 必要なもの

- **Java 17**（または最近の JDK） – コードは最新の `var` 構文を控えめに使用していますが、古いバージョンでも動作します。  
- **Aspose.OCR for Java** ライブラリ – Maven Central から取得するか、Aspose からトライアル版をダウンロードしてください。  
- 処理したい **PNG** ファイルのセット – スキャンした領収書、書籍のページ、スクリーンショットなどを想定しています。  
- Java の並行処理に関する基本的な知識 – 必須ではありませんが、あると便利です。

以上です。外部サービスも Docker も不要で、純粋な Java と少しのマルチスレッド魔法だけで完結します。

## Step 1: Aspose OCR の依存関係とライセンスを追加 (オプション)

まず、Aspose OCR の JAR がクラスパスに含まれていることを確認してください。Maven を使用している場合は、次を追加します：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

ライセンスを持っていない場合、ライブラリは評価モードで動作しますが、コードの挙動は同じです。プロダクションでの使用を推奨するライセンスのロード方法は、`Aspose.OCR.lic` をリソースフォルダーに配置し、以下を使用します：

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** ライセンスファイルはバージョン管理の外に置き、誤って公開されることを防ぎましょう。

## Step 2: Thread‑Safe `OcrEngine` インスタンスを作成

Aspose OCR の `OcrEngine` は、タスク間で同じインスタンスを再利用すればスレッドセーフです。1 回だけ作成すればメモリ節約になり、画像ごとにエンジンを再初期化するオーバーヘッドも回避できます。

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

なぜ再利用するのか？エンジンは言語モデルをメモリにロードする重厚な作業員と考えてください。画像ごとに新しいエンジンを生成するのは、ちっぽけな仕事ごとに新しい専門家を雇うようなもので、コストがかかりすぎます。

## Step 3: Fixed Thread Pool Java を設定

いよいよ本番の主役、**fixed thread pool java** の登場です。論理プロセッサ数に合わせてプールサイズを決めるので、各コアに仕事が割り当てられ、過剰なスレッド生成を防げます。

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

*fixed* プール（キャッシュプールではなく）を使用すると、リソース使用量が予測可能になり、数百枚の画像が一度に来ても「メモリ不足」スパイクを防げます。

## Step 4: 処理したい PNG ファイルをリスト (Extract Text from PNG)

OCR したい画像へのパスを収集します。実際のプロジェクトではディレクトリを走査したりデータベースから取得したりしますが、ここではいくつかの例をハードコードします。

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** ファイル拡張子 **png** は重要です。Aspose OCR は自動でフォーマットを検出しますが、JPEG や TIFF でも同様に処理可能です。

## Step 5: OCR タスクを送信 – Parallel OCR Processing

各画像は認識テキストを返す Callable になります。`OcrEngine` が共有されているため、タスクに渡すのはファイルパスだけで済みます。

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

なぜ `Future` でラップするのか？すべてのジョブを即座に発行し、後から提出順に結果を収集できるので、**convert scanned pages text** をドキュメントに戻す際にページ順を保持するのに最適です。

## Step 6: 結果を取得して表示 (Convert Scanned Pages Text)

各 `Future` が完了するのを待ち、出力を印刷します。`get()` 呼び出しは特定のタスクが完了するまでだけブロックし、プール全体を待つわけではありません。

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

典型的なコンソール出力は次のようになります：

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

結果をファイルに書き出したい場合は、`System.out.println` を `Files.writeString` 呼び出しに置き換えてください。

## Step 7: Executor Service をきれいにシャットダウン

すべてのタスクが完了したら、**shut down executor service** が重要です。これを行わないと、JVM が非デーモンスレッドを保持し続け、正常に終了できなくなります。

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

`awaitTermination` パターンは、強制終了する前にプールに残っている作業を完了させる機会を与えます。このステップを無視すると、長時間稼働するアプリケーションでメモリリークが発生しやすくなります。

## 完全動作例

すべてを組み合わせた完全なプログラムを以下に示します。`ParallelBatchDemo.java` にコピー＆ペーストして実行してください：

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}