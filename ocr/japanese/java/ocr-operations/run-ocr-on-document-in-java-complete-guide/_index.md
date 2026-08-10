---
category: general
date: 2026-06-16
description: Java を使って数ステップで文書の OCR を実行しましょう。OCR の設定方法、TIFF からの文字認識、マルチページ画像からのテキスト抽出について学べます。
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: ja
og_description: Javaで文書のOCRを実行します。このガイドでは、OCRの設定方法、TIFFファイルからのテキスト認識、マルチページ画像からのテキスト抽出について説明します。
og_title: Javaで文書にOCRを実行する – ステップバイステップチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: JavaでドキュメントのOCRを実行する – 完全ガイド
url: /ja/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでドキュメントのOCRを実行する – 完全ガイド

ドキュメントファイルに **OCR を実行** したいけど、どこから始めればいいか分からないことはありませんか？ あなたは一人ではありません。古いアーカイブをデジタル化したり、スキャンしたフォームからデータを抽出したりする際に、画像から信頼できるテキストを取得するのは一般的な課題です。

このチュートリアルでは、実用的なエンドツーエンドの例を通して **OCR の設定方法**、**TIFF からのテキスト認識**、そして **マルチページ文書からのテキスト抽出** を、わずかな Java コード行だけで実現する方法を解説します。余計な説明は省き、すぐにプロジェクトに組み込める動作するソリューションをご提供します。

## 学べること

- Java で OCR エンジンのインスタンスを設定する方法  
- マルチページ TIFF 画像を読み込んで処理する方法  
- スレッド数を設定してエンジンを最適化する方法（「OCR の設定方法」）  
- 認識を実行し、抽出されたテキストを出力する方法  
- 大容量ファイルやメモリ制限といったエッジケースの扱い方  

このガイドを終える頃には、**ドキュメント画像に対して OCR を自信を持って実行できる**ようになり、PDF、PNG、あるいはライブカメラストリームへの拡張に向けた確固たる基盤が手に入ります。

## 前提条件

- Java 17 以上（コードは簡潔さのために `var` キーワードを使用しています）  
- `OcrEngine` クラスを提供する OCR ライブラリ（例: *Aspose.OCR for Java* または *Tesseract‑Java* ラッパー）  
- `multi_page.tif` という名前のマルチページ TIFF ファイルを既知のディレクトリに配置しておくこと  

OCR ライブラリがまだない場合は、`pom.xml`（Maven）または `build.gradle`（Gradle）に追加してください。正確な座標はベンダーによりますが、ほとんどの場合単一の JAR を参照すれば済みます。

---

## Step 1: Initialize the OCR Engine – How to Run OCR on Document

まず最初に、重い処理を担うエンジンオブジェクトが必要です。これは操作の「脳」に相当します。

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Why this matters:** `OcrEngine` はすべての認識設定、言語パック、ハードウェア利用オプションをカプセル化します。一度作成して複数の画像で再利用する方が、毎回インスタンス化するよりも効率的です。

---

## Step 2: Load the Multi‑Page TIFF – Extract Text from Multi‑Page Images

次に、エンジンに処理対象のファイルを指示します。TIFF はスキャン文書でよく使われる形式で、単一ファイルに複数ページを格納できます。

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro tip:** TIFF がネットワーク共有上にある場合は、`ImageStream.fromUrl(...)` を使用してください。これにより、OCR 開始前にファイル全体をメモリにコピーする必要がなくなります。

---

## Step 3: How to Configure OCR for Maximum Throughput

デフォルトの OCR ライブラリは単一スレッドで動作することが多く、マルチコアマシンではボトルネックになります。ここで **「OCR の設定方法」** のパズルのピースをはめます。

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Why this works:** 論理プロセッサ数に合わせてスレッド数を設定することで、OCR エンジンは異なるページを並列に処理できます。4 コアのラップトップでは、マルチページ文書の処理速度がおおよそ 3〜4 倍向上します。  
> **Edge case:** Docker コンテナなど CPU クォータが制限された環境では、利用可能なコア数よりも少ないスレッド数を手動で上限設定する必要があります。例: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Step 4: Recognize Text from TIFF – The Core OCR Call

すべてが接続されたら、いよいよ認識を実行します。この一呼び出しで TIFF の各ページを走査し、言語モデルを適用して合成結果を返します。

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **What’s happening under the hood?** エンジンは TIFF を個別のラスタ画像に分割し、各画像を OCR ニューラルネットに渡してテキスト出力を結合します。ページ単位の詳細が必要な場合は、`result.getPages()` が `OcrPageResult` オブジェクトのリストを返します。

---

## Step 5: Output the Recognized Text – Verify the Extraction

最後に、抽出されたテキストをコンソールに出力します。実際のアプリケーションでは、データベースや JSON ファイルに書き込むことが多いでしょう。

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Expected output (truncated):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

文字化けが出てクリーンな文字列が得られない場合は、正しい言語パックがインストールされているか、画像がノイズ過多でないかを再確認してください。デスキューや二値化といった前処理を行うと、精度が大幅に向上します。

---

## Handling Large Multi‑Page Files – Tips for Extraction

基本フローは示しましたが、実務で扱う文書は巨大になることがあります。以下の追加ポイントを検討してください。

1. **ストリーム処理** – 一部の OCR SDK は、TIFF 全体をメモリに読み込むのではなく、ページごとにストリームで供給できる機能を提供しています。`engine.setImageStream(...)` のように `InputStream` を受け取るメソッドを探してみてください。  
2. **メモリ制限** – `OutOfMemoryError` が発生したら、スレッド数を減らすか、JVM ヒープを増やします（例: `-Xmx2g`）。  
3. **ポストプロセッシング** – 正規表現や自然言語処理ライブラリを使って改行を整形したり、ヘッダー/フッターを除去したり、特定フィールド（例: 請求書番号）を抽出したりできます。

---

## Full Working Example (All Steps Combined)

以下は完成形の Java クラスです。そのまま IDE に貼り付け、パッケージやインポートを調整して実行してください。

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro tip:** `recognize()` 呼び出しを `try‑catch` ブロックでラップし、`OcrException` を適切に処理すると、破損した画像ファイルに遭遇した際にも安定します。

---

## Conclusion

本稿では、Java を用いて **ドキュメント画像に OCR を実行** する方法を、エンジン初期化からマルチページテキスト抽出まで網羅的に解説しました。**OCR の設定方法** を理解すれば、最新 CPU の性能を最大限に引き出せますし、**TIFF からのテキスト認識** と **マルチページからのテキスト抽出** の手順は、あらゆる文書デジタル化プロジェクトの堅実な土台となります。

次は何をすべきでしょうか？ TIFF を PDF に置き換えてみる、カスタム言語モデルで実験する、あるいは出力を検索インデックスに流し込むなど、基盤ができた今なら可能性は無限です。

使用している OCR ライブラリが別の API を提供している場合など、質問や問題があればコメントで教えてください。楽しいコーディングを！スキャンしたページを検索可能なテキストに変換する喜びをぜひ体感してください。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを踏まえてさらに深く学べる関連トピックです。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれています。

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}