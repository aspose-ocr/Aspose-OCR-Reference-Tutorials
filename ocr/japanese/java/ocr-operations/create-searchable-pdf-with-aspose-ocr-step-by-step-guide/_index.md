---
category: general
date: 2026-01-02
description: Aspose OCR を使用して、スキャン画像 PDF から検索可能な PDF を作成します。OCR 言語の設定方法、テキストレイヤー PDF
  の埋め込み方法、高圧縮 PDF オプションの適用方法を学びます。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: ja
og_description: 検索可能なPDFをすばやく作成します。このガイドでは、スキャンした画像PDFを変換し、テキストレイヤーを埋め込み、OCR言語を設定し、高圧縮PDFを有効にする方法を示します。
og_title: Aspose OCRで検索可能なPDFを作成する – 完全ガイド
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Aspose OCRで検索可能なPDFを作成する – ステップバイステップガイド
url: /ja/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能な PDF の作成 – 完全プログラミングチュートリアル

スキャンした画像から **検索可能な PDF** を作成したいが、どこから始めればよいかわからないことはありませんか？ 多くの文書中心のワークフローでは、画像だけの PDF は検索やインデックス作成にとって行き止まりです。  

良いニュースは、Aspose OCR を使えば **スキャン画像 PDF** を数行の Java コードで完全に検索可能な文書に変換できることです。このチュートリアルでは、OCR エンジンの初期化、高圧縮 PDF 設定の構成、隠しテキスト層の埋め込み、そして適切な OCR 言語の選択まで、すべての手順を詳しく解説します。

このガイドの最後まで読むと、検索可能な PDF を生成する実行可能なプログラムが手に入り、任意の検索エンジンや文書管理システムに問題なく投入できるようになります。

---

## 検索可能な PDF の作成 – 概要

コードに入る前に、**検索可能な PDF** が実際に何を意味するのかを明確にしておきましょう。検索可能な PDF には、以下の 2 つの平行レイヤーが存在します。

1. **ビジュアルレイヤー** – 元のスキャン画像（またはレンダリングされたページ）。  
2. **テキストレイヤー** – OCR によって抽出された、目に見えないが機械可読な文字列。

Adobe Reader でテキストを選択できるのは、画像ではなく隠しテキストレイヤーと対話しているからです。この二層構造が **embed text layer PDF** 機能を実現します。

---

## Aspose OCR を使用したスキャン画像 PDF の変換

最初に必要なのは、PDF に変換したいスキャン画像（PNG、JPEG、TIFF）です。Aspose OCR はその画像を読み取り、OCR を実行し、結果を PDF ライターに渡します。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**このコードが機能する理由:**  
- `setCreateSearchablePdf(true)` が Aspose に隠しテキストレイヤーの生成を指示し、**embed text layer pdf** の要件を満たします。  
- `setCompressionLevel(9)` が **high compression pdf** の範囲にファイルサイズを縮小し、OCR 精度を犠牲にしません。  
- `RecognitionLanguage.ENGLISH` の引数は **set OCR language** の指定方法を示しています。必要に応じてフランス語やドイツ語などに置き換えられます。

---

## 高圧縮 PDF 設定

大量のスキャン PDF はすぐに数百メガバイトに膨れ上がります。Aspose は PDF レベルで動作するシンプルな圧縮 API を提供しています。`setCompressionLevel` メソッドは 0（圧縮なし）から 9（最大圧縮）までの値を受け取ります。

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

いくつかのポイント:

- **ロスレス画像フォーマット**（PNG）をテキストが多いスキャンに使用し、写真には JPEG を選択してください。  
- カスタムフォントを埋め込む場合は **フォントサブセット化** を有効にします—検索可能な PDF を作成すると Aspose が自動的に処理します。  
- 各変更後に **出力サイズをテスト** してください。レベル 8 の圧縮で品質低下がほとんどなく 10 % 程度サイズが削減できることがあります（レベル 9 と比較して）。

---

## 検索可能性のためのテキストレイヤー埋め込み PDF

`setCreateSearchablePdf(true)` 呼び出しを省略すると、見た目は問題ないものの内容を検索できません。隠しテキストレイヤーは、認識された各文字をページ上の位置にマッピングすることで作成されます。

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**注意点:**  

- **混在言語ドキュメント** – 言語ごとに OCR を 2 回実行し、テキストレイヤーをマージする必要があります。  
- **複雑なレイアウト**（表、マルチカラム） – Aspose はかなりの精度で処理しますが、隠しテキストを表示できる PDF ビューア（例: Adobe Acrobat の「Edit PDF」モード）で出力を必ず確認してください。

---

## 正確な認識のための OCR 言語設定

OCR エンジンの精度は、期待する言語の指定に大きく依存します。Aspose には組み込みの言語セットがあり、カスタム言語パックも追加可能です。

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**言語を変更すべきタイミング:**  

- 文書に **非ラテン文字**（キリル文字、アラビア文字など）が含まれる場合 – 適切な `RecognitionLanguage` に切り替えます。  
- 混在言語ページ – `recognizeImageAndSave` を異なる言語で 2 回呼び出し、結果の PDF をマージします。

---

## 完全サンプルの実行

以下は実行可能なフルプログラムです。プレースホルダーのパスを実際のファイル位置に置き換え、Aspose OCR JAR がクラスパスに含まれていることを確認した上で実行してください。

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**期待される出力:** プログラム実行時にコンソールに次のように表示されます。

```
Searchable PDF created.
```

`searchable.pdf` を任意の PDF ビューアで開き、テキスト選択を試すと、見えないレイヤーが機能していることが確認できます。これで **create searchable pdf** がスキャン画像から正常に作成できました。

---

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*上記のスクリーンショット（プレースホルダー）は、スキャンページ上でテキストが選択可能な PDF ビューアの様子を示すものです。*

---

## 結論

Aspose OCR を使用して **検索可能な PDF** を作成するために必要なすべての手順を網羅しました:

- OCR エンジンの初期化。  
- `recognizeImageAndSave` に PNG/JPEG を渡して **スキャン画像 PDF の変換**。  
- `setCreateSearchablePdf(true)` で **テキストレイヤー埋め込み PDF** を実現。  
- `setCompressionLevel(9)` で **高圧縮 PDF** を生成し、軽量化を維持。  
- 正確な認識のために適切な `RecognitionLanguage` を **set OCR language** で指定。

ここからはバッチ処理や異なる言語、複数ページの結合などを試してみてください。同じパターンはスペイン語や日本語など他の言語でも機能します—`RecognitionLanguage` 列挙体を差し替えるだけです。

ご質問や問題があればコメントでお知らせください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}