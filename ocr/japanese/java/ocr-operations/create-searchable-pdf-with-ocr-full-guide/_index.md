---
category: general
date: 2026-06-22
description: JavaでOCRを使用して検索可能なPDFを作成する。圧縮を無効にする方法と、スキャンした画像PDFをすばやく検索可能なPDFに変換する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: ja
og_description: JavaでOCRを使用して検索可能なPDFを作成します。このガイドでは、圧縮を無効にする方法、スキャン画像PDFを変換する方法、圧縮なしでPDFを生成する方法を示します。
og_title: OCRで検索可能なPDFを作成 – 完全なJavaチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: OCRで検索可能なPDFを作成する – 完全ガイド
url: /ja/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCRで検索可能なPDFを作成 – 完全ガイド

バッチでスキャンした画像から **create searchable PDF** を作成したいと思ったことはありませんか？同じ壁にぶつかる開発者は多いです。出力が巨大で読めない塊になってしまうことがよくあります。

このチュートリアルでは、Java OCRエンジンを使用して **create searchable PDF** を作成し、スキャン画像PDFを **convert scanned image PDF** し、さらに **disable compression** して元のサイズを保つ方法を、クリーンなエンドツーエンドの例で解説します。最後まで読むと、実行可能なスニペットと、各設定がなぜ重要かの理解が得られます。

## 学べること

* OCRエンジンを **ocr to searchable pdf** に設定する方法。  
* PDF圧縮をオフにして **pdf without compression** を取得する理由と手順。  
* スキャン画像をOCR処理し、**searchable PDF** として保存する完全なJavaプログラム。  
* 複数ページのスキャンや低解像度ソースなど、エッジケースへの対処法。  

**前提条件** – Java 8以上がインストールされていること、対応するOCR SDK（コードはABBYY FineReader Engine APIを使用していますが、`setOutputFormat` と `setPdfCompression` を提供する任意のライブラリでも概念は同じです）。IntelliJ IDEA や Eclipse といったIDEがあると便利ですが、シンプルなテキストエディタでも構いません。

---

![検索可能なPDFのワークフロー](image-placeholder.png "スキャン画像から最終PDFまでの create searchable pdf プロセスを示す図")

## Step 1: OCRエンジンを **Create Searchable PDF** に設定

最初にOCRエンジンに期待する出力形式を指示する必要があります。デフォルトでは多くのSDKがプレーンテキストやラスタPDFを出力しますが、これは検索可能ではありません。形式を切り替えるだけで重い処理が自動的に行われます。

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*重要ポイント*: `PDF_SEARCHABLE` フラグは、スキャン画像の下に見えないテキスト層を埋め込むようエンジンに指示します。検索ツールはこの層をインデックス化できるため、Adobe Reader で開いたときと同様に検索可能になります。

## Step 2: 圧縮を無効化 – **How to Disable Compression** を正しく行う

このステップを省略すると、エンジンは各ページを圧縮して容量を削減しますが、圧縮により細部がぼやけ、後で高解像度画像を抽出したい場合に問題になります。

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**プロのコツ**: 法的文書や医療スキャンなど、ピクセル単位で正確さが求められる場合は圧縮を無効にすることが必須です。ファイルサイズは大きくなりますが、元の寸法と鮮明さを保持できます。

## Step 3: OCRを実行し、結果のドキュメントを取得

エンジンが出力形式と画像処理方法を把握したら、認識を実行できます。呼び出しは `PdfDocument` オブジェクトを返し、保存やさらに操作する準備が整います。

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*内部で何が起きているか* エンジンは各入力ページを処理し、文字認識を行い、画像上に隠れたテキスト層を貼り付けます。複数ページがある場合は自動的に連結されます。

## Step 4: **Searchable PDF** をディスクに保存

最後に、メモリ上のPDFをファイルに書き出します。書き込み権限のある場所を選び、意味のあるファイル名を付けてください。

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

`searchable.pdf` をビューアで開くと、可視コンテンツは元のスキャン画像のままですが、テキストの選択や検索が可能になっていることに気付くでしょう。

### 完全動作サンプル

以下は、上記4ステップをすべて組み合わせた自己完結型のJavaクラスです。コピー＆ペーストして、入力パスを調整し、そのまま実行できます。

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**期待される出力** – プログラム実行後、コンソールに上記メッセージが表示され、`YOUR_DIRECTORY` に `searchable.pdf` が生成されます。任意のPDFリーダーで開くと以下が可能です。

* テキストのハイライト  
* 組み込み検索（Ctrl + F）で単語を検索  
* 必要に応じて隠れたテキスト層をエクスポート  

---

## なぜ圧縮を無効化するのか？ **PDF Without Compression** の理解

「圧縮は常に良いことでは？」と疑問に思うかもしれません。答えはケースバイケースです。

| 状況 | 圧縮を保持 (`NORMAL`) | 圧縮を無効化 (`NONE`) |
|-----------|-----------------------------|------------------------------|
| 法的契約書のアーカイブ | ❌ ピクセル忠実度が変わる可能性あり | ✅ 元の外観を保証 |
| 低解像度スキャンの大量バッチ | ✅ ストレージ節約 | ❌ 効果がないのにサイズ増大 |
| 細かいフォントでのOCR精度が必要 | ❌ 細部がぼやける | ✅ すべてのストロークを保持 |

要するに、**how to disable compression** はストレージと忠実度のトレードオフです。テキスト検索が主目的で、画像の再印刷が不要な多くの検索可能PDFワークフローでは、圧縮オフが安全な選択です。

## **Scanned Image PDF** を直接変換する方法

既にスキャン画像だけが含まれるPDF（「画像のみPDF」）を持っている場合、個別画像ではなくPDF全体をエンジンに渡すことで **convert scanned image pdf** できます。

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

同じ設定フラグ（`PDF_SEARCHABLE` と `PdfCompression.NONE`）が適用されるため、PDFコンテナから開始しても **pdf without compression** が得られます。

## よくある落とし穴と回避策

* **出力形式の設定忘れ** – エンジンはデフォルトでラスタPDFを生成し、検索不可になります。`recognizeToPdf()` の前に必ず `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` を呼び出してください。  
* **大規模バッチでメモリ不足** – ページをチャンク単位でロード・処理するか、SDK が提供するストリーミングAPIを利用してください。  
* **ファイルパスの誤り** – 絶対パスを使用するか、作業ディレクトリを正しく設定してください。さもなくば `pdf.save()` が `IOException` を投げます。  
* **ライセンス未認証** – 多くの商用OCR SDKは有効なライセンスが必要です。ライセンスがないとランタイム例外が発生します。  

---

## 結論

これで、スキャン画像から **how to create searchable PDF** ファイルを作成し、**convert scanned image PDF** し、**how to disable compression** して **pdf without compression** を生成する完全なソリューションが手に入りました。重要な手順は次の通りです。

1. 出力形式を `PDF_SEARCHABLE` に設定。  
2. `PdfCompression.NONE` でPDF圧縮をオフにする。  
3. OCRを実行し、`PdfDocument` を取得。  
4. ファイルとしてディスクに保存。

ここからはフォントを試したり、透かしを追加したり、フォルダ全体をバッチ処理したりできます。OCR言語パックの追加やマルチページTIFFの取り扱い、Webサービスへの統合に興味がある方は、次回の「JavaでのOCR言語選択」や「大規模文書セット向けストリーミングOCR」チュートリアルをご覧ください。

質問や問題があればコメントで教えてください。ハッピーコーディング、そして検索可能なPDFをお楽しみください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API機能の習得や代替実装アプローチの探求に役立ちます。

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}