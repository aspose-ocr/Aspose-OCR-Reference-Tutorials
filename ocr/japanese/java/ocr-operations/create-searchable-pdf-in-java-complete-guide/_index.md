---
category: general
date: 2026-07-05
description: Aspose OCR を使用して Java で検索可能な PDF を作成します。PDF 内の画像を圧縮する方法、スキャン画像を PDF に変換する方法、フォント埋め込みを無効にしてファイルサイズを小さくする方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: ja
og_description: Aspose OCR を使用して Java で検索可能な PDF を作成します。このチュートリアルでは、PDF 内の画像を圧縮する方法、スキャン画像を
  PDF に変換する方法、フォント埋め込みを無効にする方法を示します。
og_title: Javaで検索可能なPDFを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Javaで検索可能なPDFを作成する – 完全ガイド
url: /ja/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで検索可能なPDFを作成 – 完全ガイド

スキャンしたドキュメントから **create searchable PDF** を作成したいと思ったことはありませんか？しかし「どうやってやるのか」につまずいてしまうことも多いですよね。多くのプロジェクトで、TIFFやJPEGを実際に検索できるPDFに変換することは *必須* の機能です。特に **compress images in PDF** でファイルサイズを抑えたい場合は重要です。

このチュートリアルでは、Aspose OCR for Java を使用したハンズオンの例を順に解説します。最後まで読むと、**convert scanned image to PDF** の方法、**compress images in PDF** 設定の調整、さらには **disable font embedding PDF** で数キロバイト削減する方法が正確に分かります。余計な説明は省き、すぐにコードベースに組み込める完全な実行可能ソリューションを提供します。

## 学べること

- Javaプロジェクトで Aspose OCR エンジンを設定する。
- TIFF（または任意のラスタ画像）に対して OCR を実行する。
- `PdfSaveOptions` を設定して **compress images in PDF** と **disable font embedding PDF** を有効にする。
- 結果を **searchable PDF** として保存し、すぐにインデックス付けや検索ができるようにする。

**前提条件**

- Java 8 以降がインストールされていること。
- 依存関係管理に Maven または Gradle を使用すること（Maven の例を示します）。
- 処理対象となるスキャン画像ファイル（TIFF、PNG、または JPEG）。

これらが揃っていれば、さっそく始めましょう。

![検索可能なPDF作成ワークフロー – Java OCRからPDFへの変換](/images/create-searchable-pdf-workflow.png "Aspose OCR を使用して検索可能なPDFを作成する手順を示す図")

## 手順 1: Aspose OCR の依存関係を追加

まず、Aspose OCR ライブラリをプロジェクトに取り込みます。Maven を使用する場合、`pom.xml` に以下を追加してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle を使用したい場合、同等の設定は次の通りです：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **プロのコツ:** Aspose のリリースノートをチェックしてください。新しいバージョンは OCR 精度のパフォーマンス向上をもたらすことが多いです。

## 手順 2: OCR エンジンの初期化

`OcrEngine` をインスタンス化するだけで OCR エンジンを作成できます。このオブジェクトは画像の読み込みからテキスト抽出までのすべてを処理します。

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

なぜ専用のエンジンが必要なのか？Aspose は重い処理（画像前処理、言語モデル）をアプリの他の部分から分離しているため、重いリソースを再初期化せずに複数のファイルで同じ `engine` を再利用できます。

## 手順 3: スキャン画像に対して OCR を実行

ここでエンジンにスキャンしたファイルを渡します。`recognizeImage` メソッドは抽出されたテキストとレイアウト情報を保持する `RecognitionResult` を返します。

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **画像が TIFF でない場合は？**  
> Aspose OCR は一般的なラスタ形式を自動的に検出するので、コードを変更せずに JPEG、PNG、または BMP を指定できます。

## 手順 4: PDF 保存オプションの設定（画像圧縮とフォント埋め込みの無効化）

ここが二次的なキーワードが活きるポイントです。Aspose に **compress images in PDF** と **disable font embedding PDF** を指示します。これらの設定は最終的なファイルサイズを削減し、数十冊のドキュメントを配布する際に便利です。

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**画像を圧縮する理由は？**  
スキャンしたページは高解像度であることが多く、品質を 80 % に圧縮すると、10 ページの PDF が 12 MB から 3 MB 未満に減少し、視覚的な損失はほとんど感じられません。

**フォント埋め込みを無効にする理由は？**  
OCR エンジンが標準システムフォント（Arial や Times New Roman など）を使用している場合、埋め込む必要はありません。無効にすることで、特に大量のバッチ処理でファイルサイズをさらに削減できます。

## 手順 5: OCR 結果を検索可能な PDF として保存

最終ステップでは、元画像、抽出されたテキスト層、そして先ほど設定した PDF オプションをすべて結合します。

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

`document.pdf` を Adobe Reader や最新のビューアで開くと、元のスキャン画像 **と** 見えないテキスト層が表示されます。検索ボックスに単語を入力すると一致箇所がハイライトされます—まさに “create searchable pdf” が約束する動作です。

### 期待される出力

有効な TIFF でプログラムを実行すると、以下のような出力が得られます：

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

PDF を開き、`Ctrl+F` を押して、スキャンページに含まれる単語を入力すると、正しい位置にジャンプします。これが成功した **create searchable pdf** ワークフローの特徴です。

## よくある落とし穴と回避方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **空白 PDF** | `PdfSaveOptions` が `saveAsSearchablePdf` に渡されていないため。 | `PdfSaveOptions` を受け取るオーバーロードを呼び出すことを確認してください。 |
| **文字化け** | OCR 言語が設定されていない（デフォルトは英語）。 | `recognizeImage` の前に `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` を使用してください。 |
| **ファイルサイズが大きい** | `setCompressImages(false)` または `setEmbedFonts(true)` が設定されているため。 | 上記のように両方のフラグを設定したままにしてください。 |
| **画像の歪み** | `setImageQuality` が低すぎる（<50）ため。 | 70‑90 の範囲で設定するとバランスが良いです。 |

## 例の拡張

**convert scanned image to PDF** ができ、サイズも制御できるようになったので、次のことを検討できるでしょう：

- **バッチ処理**: `for(File f : folder.listFiles())` ループでフォルダ内のスキャンを処理する。
- Aspose PDF の `PdfDocument.addWatermarkText` を使用して **ウォーターマーク** を追加する。
- OCR テキストをインデックスシステム用の **プレーン .txt** ファイルにエクスポートする（`result.getText().writeToFile("doc.txt")`）。

これらすべての拡張は同じ `OcrEngine` インスタンスを再利用するため、メモリ使用量が低く抑えられます。

## 完全な実行可能コード

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

これを IDE にコピー＆ペーストし、`YOUR_DIRECTORY` を実際のパスに置き換えて実行してください。すべて正しく設定されていれば、画像圧縮とフォント埋め込み無効化のおかげで軽量な **searchable PDF** が得られます。

## 結論

ここまでで、Aspose OCR を使用して Java で **create searchable pdf** ファイルを作成するために必要なすべてを網羅しました。エンジンの初期化、OCR の実行、**compress images in pdf** と **disable font embedding pdf** の調整、そして検索可能なドキュメントの保存まで、各ステップの *理由* も併せて説明しました。

次の課題に挑みますか？OCR 言語パックの追加、フォルダ全体のバッチ処理、または注釈付きで PDF を重ねることに挑戦してみてください。ここで習得した基礎があれば、これらの拡張も簡単です。

質問や独自のテクニックを共有したい方は、下にコメントを残してください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Java 用 Aspose.OCR で PDF テキストを認識 – OCR 操作](/ocr/english/java/ocr-operations/)
- [Java 用 Aspose.OCR で PDF ドキュメントを OCR 認識](/ocr/english/java/ocr-operations/recognize-pdf/)
- [.NET で Aspose.OCR を使用して PDF を OCR する方法](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}