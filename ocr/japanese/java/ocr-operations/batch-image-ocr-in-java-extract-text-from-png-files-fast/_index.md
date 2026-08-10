---
category: general
date: 2026-02-14
description: バッチ画像OCRを簡単に：Javaの並列処理を活用し、Aspose OCRでPNGファイルからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: ja
og_description: Aspose OCR の非同期 API を Java で使用し、PNG ファイルからテキストを抽出するバッチ画像 OCR チュートリアル
og_title: Javaによるバッチ画像OCR – 高速PNGテキスト抽出
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Javaによるバッチ画像OCR – PNGファイルからテキストを高速に抽出
url: /ja/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaでバッチ画像OCR – PNGファイルからテキストを高速抽出

PNGスキャンのフォルダーで **バッチ画像OCR** を実行したいけど速度が心配、ということはありませんか？ あなたは一人ではありません。実際のプロジェクト—請求書のデジタル化、スキャンした書籍のアーカイブ、領収書の処理—では、開発者は **PNGからテキストを抽出** する必要があり、かつ迅速かつ信頼性が求められます。  

良いニュースです。Aspose OCR の非同期 API を使えば、数行の Java コードで並列 OCR パイプラインを立ち上げることができます。このガイドでは、完全に実行可能なソリューションを順に解説し、各要素が重要な理由を説明し、結果の検証方法を示します。最後まで読むと、PNG ファイルのバッチ全体を並列に処理し、クリーンでスペルチェック済みのテキスト出力を得られる自己完結型プログラムが手に入ります。

## 学べること

- バッチ処理用の PNG ファイルを一覧取得する方法  
- 英語言語とスペル補正のために Aspose `OcrEngine` を設定する方法  
- `processAsync` を使用した非同期 OCR の実行と `Future` 結果の処理方法  
- 各画像の認識テキストを読み取り表示する方法  
- スケーリング、エラーハンドリング、パフォーマンス調整のヒント  

### 前提条件

- Java 8 以上がインストールされていること（コードは標準の `java.util.concurrent` パッケージを使用）  
- Aspose OCR for Java のライセンスまたは無料トライアル（Aspose のウェブサイトからダウンロード）  
- テスト用に数枚の PNG スクリーンショットまたはスキャンページが入ったフォルダー  

さあ、始めましょう。

## 手順 1 – バッチ用の PNG ファイルを集める

OCR エンジンが作業を開始する前に、処理すべき画像を把握する必要があります。最も簡単な方法は、絶対パスまたは相対パスの `List<String>` を作成することです。

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**この重要性:**  
リストを事前に作成しておくことで、エンジンは各ファイルを独立してスケジュールでき、真のバッチ処理の基盤となります。後でディレクトリを動的に走査する必要がある場合は、静的な `Arrays.asList` を `Files.walk` ストリームに置き換えるだけです。

## 手順 2 – Aspose OCR エンジンの初期化とチューニング

Aspose の `OcrEngine` は高度に設定可能です。ここでは言語を英語に設定し、スペル補正を有効にします—これら二つのオプションは、特にノイズの多い PNG スキャンから抽出されたテキストの品質を劇的に向上させます。

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**これらの設定の理由:**  
- **Language selection** はエンジンに使用すべき文字セットと辞書を指示し、誤認識を減らします。  
- **Spell correction** は一般的な OCR の誤読（例: “1” と “l”）を自動で修正し、出力の後処理が不要になります。

> **Pro tip:** 画像に複数の言語が含まれる場合は、`setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)` のようにリストで渡すことができます。

## 手順 3 – 非同期バッチ処理を開始する

`processAsync` で本格的な処理が行われます。これは `Future<List<OcrResult>>` を返し、メインスレッドは OCR がバックグラウンドで実行されている間も他の作業を続けられます。

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**非同期の理由:**  
OCR を順次実行すると非常に遅くなります—各 PNG が 1 秒以上かかることもあります。作業をスレッドプールに委譲することで、複数の CPU コアを活用し、総実行時間を大幅に短縮できます。

## 手順 4 – 結果が準備できたら取得する

出力を利用する準備ができたら、単に `Future` の `get()` を呼び出します。この呼び出しは OCR が完了するまでだけブロックし、入力リストと同じ順序の `OcrResult` オブジェクトのリストを返します。

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**タイムアウトの処理:**  
無限にブロックするのを避けたい場合は、`ocrFuture.get(60, TimeUnit.SECONDS)` を使用し、`TimeoutException` を捕捉してフォールバックを実装します。

## 手順 5 – 各 PNG の認識テキストを表示する

結果が得られたら、それらをイテレートし、抽出されたテキストと元のファイル名を一緒に出力します。ここで初めて **PNG からテキストを抽出** します。

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**期待される出力例**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

OCR エンジンがページを認識できない場合、対応する `getText()` は空文字列を返します—本番コードでは常にチェックすべきです。

## 完全な動作例

以下は、すべての要素を組み合わせた完全な実行可能プログラムです。`ParallelOcrDemo.java` という名前のファイルに貼り付け、`YOUR_DIRECTORY` を PNG フォルダーへのパスに置き換えて、`javac ParallelOcrDemo.java && java ParallelOcrDemo` を実行してください。

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### デモの実行

1. **コンパイル** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **実行** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

各 PNG のファイル名の後に抽出されたテキストがハイフンで区切られて表示されます。  

> **Note:** `LicenseException` が発生した場合は、エンジンを作成する前に Aspose のライセンスをロードしてください：

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## スケールアップ – 実務向けバッチ OCR のヒント

| Situation | Recommendation |
|-----------|----------------|
| **Hundreds of PNGs** | スレッドプールサイズを `ocrEngine.setThreadPoolSize(8)` で増やす（CPU コア数に合わせてさらに増やす） |
| **Memory constraints** | ファイルを小さなチャンク（例: 50 枚ずつ）で処理し、各チャンク後に `OcrResult` リストを解放する |
| **Variable image quality** | `setPreprocessingOptions` を有効にして、認識前に自動回転、デスキュー、コントラスト強調を行う |
| **Multiple languages** | `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` を呼び出し、必要に応じてカスタム辞書を設定する |
| **Error handling** | `ocrFuture.get()` を `try‑catch` で `ExecutionException` を捕捉し、バッチ全体を中断せずに失敗したファイルをログに記録する |

## よくある質問

**Q: JPEG や TIFF ファイルでも動作しますか？**  
A: もちろんです。`processAsync` メソッドは Aspose OCR がサポートするすべての形式（PNG、JPEG、TIFF、BMP など）を受け付けます。リスト内のファイル拡張子を変更するだけです。

**Q: レイアウト（テーブル、カラム）を保持したい場合は？**  
A: Aspose OCR は `getLayoutResult()` メソッドを提供しており、位置データを返します。各単語のバウンディングボックスを解析することでテーブルを再構築できます。

**Q: サーバーレスプラットフォームで実行できますか？**  
A: はい。Aspose ライブラリを含む JAR をパッケージ化し、AWS Lambda、Azure Functions、Google Cloud Functions にデプロイすれば実行できます。OCR スレッドプール用に十分なメモリ割り当てを確保することを忘れないでください。

## 結論

これで、Aspose OCR の非同期 API を利用し、Java で PNG ファイルからテキストを効率的に **抽出** する完全な自己完結型 **バッチ画像 OCR** ソリューションが手に入りました。本チュートリアルでは、ファイルリストの準備、言語とスペルチェックの設定、並列処理の開始、結果の処理、そして本番環境向けにパイプラインをスケールさせる方法まで網羅しました。

次のステップに進みませんか？言語をフランス語に変更したり、カスタム辞書で実験したり、出力を検索可能な ElasticSearch インデックスに統合したりしてみてください。高速バッチ OCR と最新の Java 並行処理を組み合わせれば、可能性は無限です。

コーディングを楽しんでください。そして、テキスト抽出が迅速かつ正確でありますように！ 

![Diagram showing parallel OCR workers handling multiple PNG files](/images/batch-ocr-diagram.png){: .center alt="複数の PNG ファイルを処理する並列 OCR ワーカーを示す図"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}