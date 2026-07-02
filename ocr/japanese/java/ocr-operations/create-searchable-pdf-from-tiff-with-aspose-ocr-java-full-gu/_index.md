---
category: general
date: 2026-06-28
description: Aspose OCR を使用して Java でマルチページ TIFF から検索可能な PDF を作成します。TIFF を PDF に変換し、OCR
  テキストレイヤーを追加して即座に検索できるようにする方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: ja
og_description: Aspose OCR を使用して Java で TIFF 画像から検索可能な PDF を作成します。このガイドでは、TIFF を PDF
  に変換し、検索可能な文書用に OCR テキストレイヤーを PDF に追加する方法を示します。
og_title: Aspose OCR（Java）でTIFFから検索可能なPDFを作成
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: Aspose OCR (Java) で TIFF から検索可能な PDF を作成する – 完全ガイド
url: /ja/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR (Java) を使用して TIFF から検索可能な PDF を作成する – 完全ガイド

スキャンした TIFF から **検索可能な PDF** を作成したいが、サードパーティ製ツールで時間を費やしたくない、ということはありませんか？ あなただけではありません。開発者は常に、かさばる画像ファイルを実際に検索できる PDF に変換する信頼できる方法を必要としています。

このチュートリアルでは、**TIFF を PDF に変換** するだけでなく、**OCR テキストレイヤー PDF を追加** して、数行の Java コードで本当に検索可能なドキュメントを作成する実践的なエンドツーエンドソリューションを解説します。

## 学べること

- Aspose OCR for Java のセットアップとライセンスの適用方法（任意ですが推奨）。  
- `OcrEngine` を使用した **TIFF を PDF に変換** の正確な手順。  
- `PdfExportOptions` を設定して、生成されたファイルに見えない検索可能テキストレイヤーを含める方法—実務でいう **add OCR text layer PDF** の意味。  
- 期待される出力と、すべてが正しく動作したかを確認する簡単なチェック。

Aspose の事前知識は不要です。基本的な Java 開発環境（JDK 8 以上と任意の IDE）さえあれば始められます。

---

## Step 1: プロジェクトの準備と Aspose OCR ライセンスの適用  

OCR API を呼び出す前に、Aspose OCR の JAR をクラスパスに追加する必要があります。商用ライセンスをお持ちの場合は、`.lic` ファイルをアクセス可能な場所に配置し、`License` クラスでそのパスを指定してください。この手順は必須ではなく、評価モードでも動作しますが、ライセンスを適用すると透かしが除去され、すべての機能が解放されます。

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **プロのコツ:** ライセンスファイルはソース管理の外に置き、誤って公開されないようにしましょう。

---

## Step 2: OCR エンジンのインスタンス化  

`OcrEngine` オブジェクトを作成することが、**検索可能な PDF を作成** する最初の実装ステップです。エンジンはすべての OCR 設定を保持し、後で変換処理を実行します。

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

なぜエンジンを別にするのか？ 同じ設定を複数ファイルで使い回すことができ、数十枚の TIFF をバッチ処理する際に便利です。

---

## Step 3: マルチページ TIFF の読み込み  

Aspose OCR ならマルチページ TIFF の読み込みがとても簡単です。ファイルパスを `OcrInput` オブジェクトに追加するだけで、ライブラリが自動的にページを検出しキューに入れます。

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

もし **TIFF を PDF に変換** する際にページ単位で処理したい場合は、ループ内で `ocrInput.add(pageStream)` を呼び出すことも可能です—Aspose は各呼び出しを別ページとして扱います。

---

## Step 4: PDF エクスポートオプションの設定 – OCR テキストレイヤーの追加  

ここが **add OCR text layer pdf** の魔法がかかるポイントです。いくつかのフラグを切り替えるだけで、元のビットマップを埋め込み（視覚的な忠実度を保持）つつ、検索エンジンがインデックスできる隠しテキストレイヤーを生成します。

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: PDF がスキャン画像と全く同じ見た目になることを保証します。  
- `setCreateSearchablePdf(true)`: 見えないテキストオーバーレイを作成します—これが **add OCR text layer pdf** の核心です。  

下記のようにメタデータ（author, title, subject）を設定すれば、後々の文書管理が楽になります。

---

## Step 5: OCR を実行し、検索可能な PDF をエクスポート  

ここで全体を結びつけます。`recognizeAndExportPdf` メソッドが重い処理を担い、各 TIFF ページに対して OCR を実行し、視覚画像を書き込み、検索可能テキストを重ね合わせます。

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

コンソールに成功メッセージが表示されたら、**検索可能な PDF を作成** したことになります。生成された `searchable.pdf` を任意の PDF ビューアで開き、`Ctrl+F` で元画像に含まれる単語を検索してみてください。即座にヒットするはずです。

---

## 結果の検証 – 簡易チェックリスト  

1. **視覚的忠実度** – `setEmbedOriginalImage` により、PDF は元の TIFF と見た目が一致していること。  
2. **検索可能性** – ビューアの検索機能を使い、隠しテキストレイヤーがマッチを返すこと。  
3. **メタデータ** – PDF プロパティを開き、先ほど設定した author と title が正しく反映されていること。  

これらのチェックのいずれかが失敗した場合は、`setCreateSearchablePdf(true)` が有効か、ライセンス（ある場合）が評価モードで制限がかかっていないかを再確認してください。

---

## エッジケースとよくある質問  

### TIFF が単一ページの場合は？  

同じコードで動作します。Aspose は単一ページ TIFF を要素が 1 つのコレクションとして扱うため、特別な処理は不要です。

### OCR 言語は制御できますか？  

はい。`recognizeAndExportPdf` を呼び出す前にエンジンの言語を設定します：

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

`English` をサポートされている任意の言語列挙子に置き換えてください。

### 元画像を埋め込まずにファイルサイズを削減したい場合は？  

`pdfOptions.setEmbedOriginalImage(false)` と設定すれば OK です。PDF には検索可能テキストレイヤーだけが含まれ、サイズが大幅に縮小しますが、視覚的表現は失われます。

### 生成された PDF はすべてのプラットフォームで本当に検索可能ですか？  

最新の PDF リーダー（Adobe Acrobat、Foxit、ブラウザ内ビューワー）はテキストレイヤーを認識します。古い軽量ビューアは無視する可能性があるため、対象プラットフォームでのテストを推奨します。

---

## 完全動作サンプル  

以下に、実行可能な完全な Java クラスを示します。プレースホルダーのパスを実際のものに置き換え、Aspose OCR の JAR をプロジェクトに追加して実行してください。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**期待されるコンソール出力:**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

`searchable.pdf` を開き、元の TIFF に含まれる任意の単語を検索してみてください。これで **検索可能な PDF を作成** できました！

---

## まとめ  

本稿では、Aspose OCR for Java を利用して TIFF から **検索可能な PDF** を作成する、実践的かつ本番環境でも使える手順を一通り解説しました。`PdfExportOptions` を適切に設定すれば、**add OCR text layer PDF** が自動的に行われ、静的画像が即座に検索可能な文書へと変換されます。

さらに踏み込むなら、以下の点を試してみてください。

- カスタムページサイズや DPI 設定で **TIFF を PDF に変換**。  
- OCR 後に透かしやデジタル署名を追加。  
- シンプルな `for` ループでフォルダ内の TIFF を一括処理。  

これらの拡張は本ガイドで学んだコア概念に基づくので、スムーズに移行できるはずです。

質問や問題があればコメントで教えてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}