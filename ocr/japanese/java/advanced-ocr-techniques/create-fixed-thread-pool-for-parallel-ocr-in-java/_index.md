---
category: general
date: 2026-05-03
description: Javaで固定スレッドプールを作成し、画像からテキストを迅速に抽出します。OCRの実行方法、画像をテキストに変換する方法、そして並列OCR処理でパフォーマンスを向上させる方法を学びましょう。
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: ja
og_description: Javaで固定スレッドプールを作成し、画像からテキストを迅速に抽出します。OCRの実行方法、画像をテキストに変換する方法、そして並列OCR処理でパフォーマンスを向上させる方法を学びましょう。
og_title: Javaで並列OCRのための固定スレッドプールを作成する
tags:
- Java
- OCR
- Multithreading
title: Javaで並列OCRのための固定スレッドプールを作成する
url: /ja/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで並列OCRのための固定スレッドプールを作成する

OCRジョブを高速化するために **固定スレッドプールを作成** したいと思ったことはありませんか？でもどこから始めればいいか分からない…という方は多いです。画像が多いプロジェクトでは、ボトルネックはシングルスレッドのOCR呼び出しです。その解決策は意外とシンプルで、ワーカースレッドのプールを立ち上げ、ファイルを並列に処理させるだけです。  

このチュートリアルでは、Aspose OCR を使用して **画像からテキストを抽出** する方法、**OCR を効率的に実行** する方法、そして CPU を過度に使用せずに **画像をテキストに変換** する方法を学びます。最後には、サンプル画像数枚で **並列OCR処理** を実演する、すぐに実行できる Java プログラムが手に入ります。

## 作成するもの

小さなコンソールアプリを作ります。

* 画像パスのリストを読み取ります（PNG、JPG、TIFF、BMP）。
* **CPUコア数に合わせた固定スレッドプールを作成** します。
* 各画像に対して OCR タスクをディスパッチします。
* 認識されたテキストを収集し、コンソールに出力します。
* エグゼキュータをきれいにシャットダウンします。

外部のビルドツールや高度なフレームワークは不要です—純粋な Java と Aspose OCR ライブラリだけです。Java 8 以上と適切な IDE があればすぐに始められます。

## 前提条件

* **Java Development Kit (JDK) 8 以上** – コードはラムダ式を使用しているため、古いバージョンではコンパイルできません。
* **Aspose OCR for Java** – Aspose のウェブサイトから JAR をダウンロードするか、Maven (`com.aspose:aspose-ocr`) で取得してください。
* テスト画像が数枚入ったフォルダー（コードは `YOUR_DIRECTORY` を指しています）。
* Java の並行処理に関する基本的な知識（残りは本チュートリアルで解説します）。

> *Pro tip:* Maven を使用している場合は、依存関係を `pom.xml` に追加し、IDE にクラスパスの管理を任せてください。  

---

## 手順 1: 必要なインポートを追加する

まず、必要なクラスをスコープに持ち込みます。これは単なる定型文ではなく、各インポートが JVM に OCR エンジン、画像処理ユーティリティ、そして **固定スレッドプール** インスタンスを作成できる並行処理ツールの場所を教える役割を持ちます。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – コア OCR API。
* `java.util.*` – 画像パスや結果を格納するコレクション。
* `java.util.concurrent.*` – `ExecutorService` と `Future` を含む並行処理パッケージ。

## 手順 2: 処理する画像を定義する

次に、**画像からテキストを抽出** したいファイルのリストを作ります。`Arrays.asList` を使うことでコードが簡潔になり、ロジックの他の部分を変更せずに自分のディレクトリに差し替えることができます。

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

エントリを自由に追加してください。スレッドプールは CPU コア数に応じて自動的にスケールします。

## 手順 3: CPU コア数に合わせて **固定スレッドプールを作成**

これがチュートリアルの核心です。ランタイムに利用可能なコア数を問い合わせ、`Executors` ファクトリにそのサイズのプールを作成させます。なぜ固定かというと、スレッド数を予測可能に保つことで、OS のリソースを枯渇させる恐れのある「スレッド爆発」を防げるからです。

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` は論理コア数（ハイパースレッドを含む）を返します。
* `newFixedThreadPool(coreCount)` は CPU の容量を超えないことを保証し、並列で **OCR を実行** する最も安全な方法です。

## 手順 4: 各画像に対して OCR タスクを送信する

ここでは、各ファイルパスを **OCR を実行** し、テキストを認識して結果を返す Callable に変換します。ラムダ式内で新しい `OcrEngine` をインスタンス化している点に注目してください—これによりエンジンの状態をスレッド間で共有することによる安全性の問題を回避できます。

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* 各 `submit` 呼び出しはラムダ式をプールに渡し、アイドルスレッドでスケジュールされます。
* `Future<String>` オブジェクトにより、後で認識されたテキストを取得でき、必要に応じて順序を保ちます。

## 手順 5: 認識されたテキストを取得して表示する

すべてのタスクがキューに入ったら、`Future` リストを反復し、`get()` を呼び出して各 OCR ジョブが完了するまで待機します。ここが **画像をテキストに変換** するステップが実際に見える部分で、`engine.getText()` 呼び出しが生の文字列を返します。

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

典型的なコンソール出力は次のようになります：

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

ファイルが失敗した場合（たとえば破損しているなど）、`Failed:` で始まりパスが続く行が表示されます—デバッグに便利です。

## 手順 6: Executor Service をクリーンアップする

プールのシャットダウンを忘れないでください。さもなければ、JVM がまだ作業があると考えてプロセスが終了しません。適切にシャットダウンすれば、実行中のタスクが完了してからプロセスが終了します。

```java
executor.shutdown();
```

`awaitTermination` を呼び出してタイムアウトを設定することもできますが、ほとんどのコマンドラインユーティリティでは単純な `shutdown()` で十分です。

## 完全な動作例

以下に、完全な実行可能プログラムを示します。`ParallelOcrTutorial.java` という名前のファイルにコピー＆ペーストし、画像パスを調整した上で、通常通り `javac` と `java` を実行してください。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**期待される結果:** 各画像のテキスト内容がコンソールに `imagePaths` リストと同じ順序で出力されます。画像の処理に失敗した場合は、空行の代わりに失敗通知が表示されます。

## よくある質問とエッジケース

### スレッド数より画像が多い場合は？

固定スレッドプールは余剰タスクを自動的にキューに入れます。スレッドが現在の OCR ジョブを完了すると、次のタスクを取得します。このキューイング動作が **並列 OCR 処理** の本質で、CPU を過負荷にせず最大スループットを実現します。

### 言語を変更できますか？

もちろんです。`engine.getLanguage().setEnglish(true);` を目的の言語フラグに置き換えてください。例: `setFrench(true)`、または `recognize()` の前に複数のセッターを呼び出して複数言語を有効にできます。

### 非常に大きな画像を扱うには？

大きなファイルはスレッドごとに多くのメモリを消費します。`OutOfMemoryError` が発生した場合は、エンジンに渡す前に画像を縮小するか、`-Xmx` でヒープサイズを増やすことを検討してください。別のアプローチとして **キャッシュスレッドプール** を使用する方法があります (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}