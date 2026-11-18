---
category: general
date: 2026-06-06
description: Aspose OCR for Java を使用してスキャン画像からテキストを抽出します。並列処理で TIFF ファイルからテキストを認識する方法を学びましょう。
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: ja
og_description: Aspose OCRでスキャン画像からテキストを抽出します。このガイドでは、Javaを使用してTIFFファイルからテキストを効率的に認識する方法を示します。
og_title: スキャン画像からテキストを抽出 – Aspose OCR Java チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Javaでスキャン画像からテキストを抽出する – 完全なAspose OCRガイド
url: /ja/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スキャン画像からテキストを抽出 – 完全な Aspose OCR ガイド

スキャン画像から **テキストを抽出** したいと思ったことはありませんか？しかし「どうやって？」で行き詰まっていませんか？あなただけではありません。古いアーカイブをデジタル化したり、請求書からデータを抽出したり、検索可能な PDF ライブラリを構築したりする場合、TIFF スキャンから信頼できるテキストを取得するのは課題となります。  

良いニュースです：Aspose OCR for Java を使えば、数行のコードで **tiff からテキストを認識** でき、エンジンを少数の CPU コアに限定することでさらに速度を向上させることができます。このチュートリアルでは、ライブラリの設定から結果の処理までの全工程を解説するので、すぐに動作するサンプルをコピー＆ペーストできます。

## このチュートリアルでカバーする内容

- Aspose OCR for Java のインストール (Maven または手動 JAR)
- 大きなスキャン TIFF 画像の読み込み
- エンジンを最大 4 スレッドで使用するように設定 (並列 OCR)
- OCR プロセスを実行し、抽出したテキストを出力
- 一般的な落とし穴 (メモリ、マルチページ TIFF) と回避方法
- パフォーマンス向上のヒント: `setMaxThreads` の調整タイミング

このチュートリアルの最後までに、**スキャン画像からテキストを抽出** できるようになり、プロダクションパイプラインで *tiff からテキストを認識* する際にスレッド数を調整する重要性が理解できるようになります。

![スキャン画像からテキストを抽出した例](example.png "スキャンされた TIFF 画像から抽出されたテキストを示すスクリーンショット")

## 前提条件

始める前に、以下が揃っていることを確認してください：

1. **Java Development Kit (JDK) 8+** – 任意の最新バージョンで動作します。
2. **Maven**（または手動で JAR を追加できる環境） – 簡単のため Maven を使用します。
3. **Aspose OCR for Java** ライセンス（無料評価版でも動作しますが、透かしが付加されます）。
4. 処理したい **大きな TIFF スキャン**（例: `large_scan.tif`）。

これらのいずれかに心当たりがなくても心配いりません—各ステップは以下で説明します。

## ステップ 1: Aspose OCR をプロジェクトに追加

### Maven ユーザー

`pom.xml` に以下の依存関係を追加してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### 手動 JAR 設定

Aspose のウェブサイトから最新の `aspose-ocr-xx.jar` をダウンロードし、クラスパスに配置してください。  

> **プロのコツ:** JAR を `libs/` フォルダーに保管し、IDE のプロジェクト設定で参照してください。これにより、後で「class not found」のエラーを防げます。

## ステップ 2: シンプルな Java クラスを作成

`src/main/java` フォルダーに `ParallelOcrDemo.java` という名前のファイルを作成します。このクラスが OCR ワークフロー全体を保持します。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **スレッドを制限する理由:** デフォルトでは Aspose OCR はすべてのコアを使用しようとし、共有マシン上の他のサービスがリソース不足になる可能性があります。`setMaxThreads(4)` を設定すると、エンジンは最大4つの並列ワーカーで実行され、ほとんどの最新 CPU で目に見える速度向上が得られますが、リソースを独占しません。

## ステップ 3: コンパイルと実行

プロジェクトのルートでターミナルを開き、以下を実行してください：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Maven を使用しない場合は、`javac` でコンパイルし、実行してください：

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### 期待される出力

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

コンソールには、スキャンされたページ上のテキストがプレーンテキストとして表示されます。画像に複数ページが含まれる場合、Aspose OCR は順番に結合して出力します。

## ステップ 4: マルチページ TIFF の処理（エッジケース）

一般的なシナリオは **マルチページ TIFF** です—スキャンした本を想像してください。デフォルトでは `OcrInputImage` は最初のフレームのみを読み取ります。すべてのページを処理するには、`FileInputStream` と共に `OcrInputImage` を使用し、マルチページサポートを有効にします：

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

これで `ocrEngine.process()` は、すべてのページの結合テキストを含む単一の `OcrResult` を返します。

## ステップ 5: 認識精度の微調整

**文字化け** や欠落した単語が見られる場合は、以下の調整を試してください：

| Setting | 機能 | 使用するタイミング |
|---------|------|-------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | 英語の言語モデルを強制します（英語スキャンに対して高速かつ高精度） | 文書が英語のみの場合 |
| `ocrEngine.getSettings().setResolution(300)` | 認識前に低解像度画像を拡大します | 200 DPI 未満のスキャン |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | ノイズやアーティファクトの除去を試みます | ノイズが多いスキャン |

例のスニペット：

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## ステップ 6: 結果をファイルへエクスポート

デモではコンソールへの出力で問題ありませんが、本番コードでは通常、出力を有用な場所に書き込みます：

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

これで検索インデックス、データベース、または下流の分析パイプラインに投入できるプレーンテキストファイルが得られます。

---

## よくある質問 (FAQ)

**Q: PNG や JPEG ファイルでも動作しますか？**  
A: もちろんです。`OcrInputImage` は Java の ImageIO が読み取れるすべての形式を受け付けます。パスのファイル拡張子を置き換えるだけです。

**Q: サーバーに 8 コアがありますが、`setMaxThreads(8)` にすべきですか？**  
A: 設定は可能ですが、他のサービスも CPU サイクルを必要とすることを忘れないでください。専用の OCR ワーカーの場合、目安は「総コア数 – 1」です。

**Q: OCR の結果が空の場合はどうすればいいですか？**  
A: 画像が完全に白くないか、正しい言語が設定されているか、解像度が少なくとも 200 DPI であるかを確認してください。低品質のスキャンは、Aspose OCR に渡す前に前処理（傾き補正、コントラスト強化）が必要なことが多いです。

---

## まとめ

私たちは Aspose OCR for Java を使用して **スキャン画像からテキストを抽出** しました。また、並列処理で **tiff からテキストを認識** する効率的な方法も理解できました。完全なコードは上記のスニペットにあり、すぐに自分のプロジェクトにコピー＆ペーストできます。

### 次にやることは？

- **バッチ処理**: TIFF ディレクトリをループし、各結果を個別のファイルに保存します。  
- **Elasticsearch との統合**: 抽出したテキストをインデックス化し、高速な全文検索を実現します。  
- **言語検出の追加**: マルチリンガル文書には `OcrLanguage.AutoDetect` を使用します。  

これらのアイデアを試すことで、膨大なスキャン書類を検索可能で活用できるデータにすぐに変換できます。

コーディングを楽しんでください。問題が発生したら遠慮なくコメントを残してください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.OCR for Java で tiff を認識する方法](/ocr/english/java/ocr-operations/recognize-tiff/)
- [テキスト画像抽出 – Aspose.OCR for Java の OCR 基礎](/ocr/english/java/ocr-basics/)
- [Aspose.OCR Detect Areas モードで Java の画像からテキストを抽出](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}