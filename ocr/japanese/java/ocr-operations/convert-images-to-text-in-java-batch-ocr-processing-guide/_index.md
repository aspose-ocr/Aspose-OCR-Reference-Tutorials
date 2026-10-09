---
category: general
date: 2026-01-02
description: Aspose OCR を使用して Java で画像をテキストに変換します。バッチ OCR 処理をマスターし、フォルダーから画像を読み取り、拡張子でファイルをフィルタリングします。
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: ja
og_description: Javaで画像を素早くテキストに変換します。このチュートリアルでは、バッチOCR処理、フォルダーからの画像読み込み、拡張子でのファイルフィルタリングについて解説します。
og_title: Javaで画像をテキストに変換 – 完全バッチOCRガイド
tags:
- OCR
- Java
- Aspose
title: Javaで画像をテキストに変換 – バッチOCR処理ガイド
url: /ja/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像をテキストに変換 – バッチOCR処理ガイド

画像をテキストに**変換**したいが、一度に何十ものファイルをどう扱うか分からないことはありませんか？開発者はPNG、JPG、その他のスキャン画像からデータを抽出する作業に常に頭を悩ませています。良いニュースです。Aspose OCR を使えば、数分でバッチOCR処理パイプラインを構築でき、フォルダー構造から画像を読み取り、拡張子でファイルをフィルタリングして必要なものだけを処理できます。

このチュートリアルでは、ディレクトリを走査し、すべての `.png` または `.jpg` を抽出し、各画像を Aspose OCR に非同期で送信し、元の順序で抽出されたテキストを出力する、自己完結型の Java プログラムを作成します。最終的に、**画像をテキストに変換**するスケール処理が必要な任意のプロジェクトに組み込める再利用可能なスニペットが手に入ります。

---

![画像をテキストに変換する例](https://example.com/convert-images-to-text.png "PNG ファイルから変換されたテキストを示す Java コンソール出力のスクリーンショット")

## 作成するもの

- スレッド間で共有される単一の `AsposeOCR` エンジン（効率的でスレッドセーフ）。  
- OCR ジョブを並列に実行し、**バッチ OCR 処理**に最適な `ParallelRecognizer`。  
- `java.nio.file.Files` を使用して **フォルダーから画像を読み取る** ロジック。  
- JPG も処理しつつ、**PNG ファイルからテキストを抽出**するシンプルなフィルタ。  
- リソースリークを防ぐための内部スレッドプールのクリーンなシャットダウン。

### 前提条件

- Java 17（または最近の LTS バージョン）。  
- Aspose OCR ライブラリを取得するための Maven または Gradle。  
- 処理したい PNG/JPG 画像が入ったフォルダー。  
- Java ストリームの基本的な知識—特別な知識は不要です。

> **プロのコツ:** まだライセンスを持っていない場合、Aspose はテスト用に無料の一時キーを提供しています。

## ステップ 1 – プロジェクトのセットアップと Aspose OCR の追加

まず、Maven（または Gradle）で新しいプロジェクトを作成します。`pom.xml` に Aspose OCR の依存関係を追加します:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Why this matters:** 依存関係を事前に宣言することで、コンパイラが `AsposeOCR`、`ParallelRecognizer`、関連クラスを認識できるようになります。また、すべてのマシンで同じバージョンが使用されることが保証され、再現性のある **バッチ OCR 処理** に不可欠です。

ビルドが完了したら IDE をリフレッシュし、`External Libraries` 配下に Aspose パッケージが表示されるはずです。

## ステップ 2 – 画像をテキストに変換 – OCR エンジンの初期化

実行全体で **1 つ** の OCR エンジンインスタンスだけが必要です。スレッド間で共有することで、メモリ使用量が削減され、エンジンが言語パックを一度だけロードするため高速化します。

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

> **Explanation:** `ParallelRecognizer` はエンジンをスレッドプールでラップします。多数のファイルを送信すると、各ファイルが独自のワーカースレッドを取得し、マルチコア CPU で真の並列処理が可能になります。

## ステップ 3 – フォルダーから画像を読み取る – ディレクトリツリーの走査

次に、**フォルダーから画像を読み取る** 必要があります。`Files.walk` API を使えばワンライナーで実装できますが、ここでは **PNG のみからテキストを抽出** したい場合のフィルタも追加します。

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

> **Why we filter here:** `filter` を使用すると **拡張子でファイルをフィルタリング** でき、後続の不要な I/O を大幅に削減できます。また、コードが読みやすくなり、複雑な正規表現を使う必要がなくなります。

## ステップ 4 – バッチ OCR 処理 – ジョブを非同期で送信

ファイルリストが準備できたら、各パスを `ParallelRecognizer` にプッシュします。`recognizeAsync` メソッドは `Future<OcrResult>` を返し、後で結果を取得できるように保存します。

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

> **What’s happening under the hood?** 各呼び出しはタスクを Recognizer の内部 ExecutorService にキューイングします。タスクは並列に実行されるため、100 枚の画像があるフォルダーでも、シングルスレッドのループに比べてごく短時間で処理できます。

## ステップ 5 – 結果を元の順序で取得 – ファイル順序を保持

`imagePaths` と同じ順序で Future を保存したので、リストを順に走査して `get()` を呼び出すだけで済みます。この呼び出しは対象画像が完了するまでブロックするだけなので、余計な管理なしで順序が保たれます。

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

**サンプルコンソール出力**（簡略化）:

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

> **Edge case handling:** 特定の画像で例外（破損ファイル、未対応フォーマット）が発生した場合は捕捉して残りの処理を続行します。これは信頼性の高い **バッチ OCR 処理** パイプラインに必須の習慣です。

## ステップ 6 – クリーンアップ – Recognizer のシャットダウン

内部スレッドプールを必ずシャットダウンしてください。そうしないと JVM が終了時にハングする可能性があります。

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

以上です！このプログラムは任意のディレクトリを走査し、PNG/JPG ファイルをフィルタリングし、並列で OCR を実行し、結果を出力します。

## 完全な動作例

以下はコピー＆ペーストで使用できる完全な Java クラスです。`"YOUR_DIRECTORY"` を画像フォルダーへのパスに置き換えて、IDE またはコマンドラインから実行してください。

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

クラスを実行すると、コンソールに抽出された文字列が次々と表示され、**画像をテキストに変換**したことを実感できるでしょう。

## よくある質問 (FAQ)

**Q: PDF や TIFF も処理できますか？**  
A: もちろんです。Aspose OCR は多数のフォーマットに対応しているので、ステップ 2 のフィルタに適切な拡張子を追加するだけで処理できます。

**Q: スペイン語など別の言語が必要な場合は？**  
A: `RecognitionLanguage.ENGLISH` を `RecognitionLanguage.SPANISH` に変更してください。言語パックがインストールされていることを確認してください（Aspose は主要な言語をほぼすべて同梱しています）。

**Q: フォルダーにサブフォルダーが含まれています—スキャンされますか？**  
A: はい。`Files.walk` はツリー全体を再帰的に走査するため、すべてのネストされた PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}