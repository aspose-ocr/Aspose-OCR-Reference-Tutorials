---
category: general
date: 2026-02-22
description: JavaでAspose OCRを使用して、スキャンされたPDFから検索可能なPDFを作成します。スキャンPDFの変換、PDF画像の圧縮、そしてPDF
  OCRの効率的な認識方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: ja
og_description: JavaでAspose OCRを使用して、スキャンしたPDFから検索可能なPDFを作成します。このステップバイステップのチュートリアルでは、スキャンPDFの変換、PDF画像の圧縮、PDFのOCR認識方法を示します。
og_title: 検索可能なPDFを作成 – スキャンしたPDFを変換するJavaガイド
tags:
- Java
- OCR
- PDF
- Aspose
title: 検索可能PDFの作成 – スキャンしたPDFを変換するJavaガイド
url: /ja/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 検索可能な PDF を作成 – スキャンした PDF を変換する Java ガイド

スキャンした文書の山から **検索可能な PDF を作成** したことがありますか？ これはよくある悩みです—PDF は見た目は問題ないのに、*Ctrl + F* で検索できません。 良いニュースは、数行の Java と Aspose OCR を使えば、画像だけの PDF を完全に検索可能なファイルに変換でき、**スキャンした PDF をテキストに変換** でき、さらに **PDF 画像の圧縮** でサイズを縮小できることです。

このチュートリアルでは、完全に実行可能な例を順に解説し、各設定がなぜ重要かを説明し、マルチページのスキャンや低解像度画像といったエッジケースに合わせてプロセスを調整する方法を示します。最後まで読むと、**recognize pdf ocr** を確実に行い、きれいな検索可能ドキュメントを生成する、堅牢で本番環境向けのコードスニペットが手に入ります。

---

## 必要なもの

- **Java 17**（または最近の JDK；API は JDK 非依存）  
- **Aspose.OCR for Java** ライブラリ – Maven Central から取得できます（`com.aspose:aspose-ocr`）  
- 検索可能にしたいスキャン済み PDF（画像のみ）  
- お好みの IDE またはテキストエディタ（IntelliJ、VS Code、Eclipse など）

重いフレームワークや外部サービスは不要です—純粋な Java と単一のサードパーティ JAR だけです。

![検索可能な PDF の作成例](placeholder-image.png "スキャンした文書から作成された検索可能な PDF のイラスト")

*画像の代替テキスト:* **create searchable pdf** のイラストで、スキャンした PDF が検索可能なテキストに変換された前後を示しています。

---

## ステップ 1 – OCR エンジンの初期化  

最初に行うべきことは `OcrEngine` インスタンスを作成することです。これは PDF 内の各ビットマップを解析し、Unicode 文字を出力する脳のようなものです。  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **プロのコツ:** 連続して多数の PDF を処理する場合は、毎回新しい `OcrEngine` を作成するのではなく、同じインスタンスを再利用してください。数ミリ秒の時間を節約し、メモリの churn を減らせます。

---

## ステップ 2 – PDF 固有の OCR オプションを設定  

Aspose は出力 PDF の構築方法を細かく調整できます。以下の 3 つの設定は、検索可能性を保ちつつ **compress pdf images** に最も効果的です。  

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi がちょうど良いバランスです。低い値にすると速度は上がりますが、小さなフォントが抜け落ちる可能性があります。  
- **CompressImages** – 背後でロスレス PNG 圧縮を有効にします。検索可能な PDF は鮮明さを保ちつつ軽量化されます。  
- **EmbedOriginalImages** – このフラグが無いとエンジンは元のラスタ画像を破棄し、見えないテキストだけが残ります。画像を保持することで、PDF がスキャンと全く同じ外観になるため、コンプライアンスチームの要求を満たします。

---

## ステップ 3 – スキャンした PDF を `OcrInput` にロード  

Aspose は `OcrInput` ラッパーを介してソースファイルを読み取ります。複数のファイルを追加できますが、このデモでは単一の **image PDF** に焦点を当てます。  

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **なぜ `File` を直接渡さないのか？** `OcrInput` を使用すると、OCR 前に複数の PDF を連結したり、画像ファイル（PNG、JPEG）を混在させたりする柔軟性が得られます。複数のソースに分割された **convert scanned pdf** を処理する際に推奨されるパターンです。

---

## ステップ 4 – OCR を実行し、検索可能な PDF をバイト配列として取得  

ここで魔法が起きます。エンジンは各ページを解析し、OCR エンジンを実行し、元の画像と隠しテキスト層の両方を含む新しい PDF を構築します。  

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

他の目的（例：インデックス作成）のために生テキストが必要な場合は、`ocrEngine.recognize(ocrInput)` を呼び出すと `String` が返ります。ただし **create searchable pdf** が目的の場合は、バイト配列をディスクに書き込むことになります。

---

## ステップ 5 – 検索可能な PDF をディスクに保存  

最後に、バイト配列をファイルに書き込みます。Java の NIO を使えばワンライナーで実現できます。  

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

`searchable_output.pdf` を Adobe Acrobat や最新のビューアで開くと、テキストを選択・コピー・検索できるようになっていることに気付くでしょう—これは **image pdf to text** 変換が約束する通りです。

---

## OCR でスキャンした PDF をテキストに変換（オプション）

場合によっては新しい PDF が不要で、抽出したプレーンテキストだけが必要なことがあります。同じエンジンを再利用できます。  

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

このスニペットは、検索インデックスへの投入や自然言語解析など、下流処理のために **recognize pdf ocr** を行うのがいかに簡単かを示しています。

---

## PDF 画像を圧縮してファイルサイズを小さくする  

元のスキャンが大きい（例：600 dpi のカラー スキャン）場合、生成された検索可能な PDF もまだ容量が大きくなることがあります。`setCompressImages(true)` フラグに加えて、OCR 前に手動でダウンサンプリングすることもできます。  

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

DPI を下げるとファイルサイズは概ね半分になりますが、可読性をテストしてください—150 dpi 以下ではフォントが読めなくなることがあります。**compress pdf images** と OCR 精度のトレードオフは、ストレージ制約に応じて判断してください。

---

## PDF OCR 設定の解説  

| 設定 | 出力への影響 | 主な使用ケース |
|---|---|---|
| `setOutputDpi(int)` | OCR 出力のラスタ解像度を制御 | 高品質アーカイブ（300 dpi）と軽量ウェブ PDF（150 dpi）の比較 |
| `setCompressImages` | PNG 圧縮を有効化 | PDF をメールで送信したりクラウドに保存したりする必要がある場合 |
| `setEmbedOriginalImages` | 元のスキャン画像を保持 | 元の外観を保持しなければならない法的・コンプライアンス文書 |
| `setLanguage` (optional) | 言語モデルを強制指定（例: "eng"） | デフォルトの自動検出が失敗しやすい多言語コーパス |

これらの設定を理解することで、**recognize pdf ocr** をより賢く行い、「ぼやけたテキスト」罠を回避できます。

---

## 画像 PDF をテキストに変換する際の一般的な落とし穴と回避策  

1. **低解像度スキャン** – 150 dpi 未満では OCR 精度が急激に低下します。Aspose に渡す前にソースをアップサンプリングするか、スキャナに高 DPI を要求してください。  
2. **回転したページ** – ページが横向きにスキャンされている場合、オートローテートを有効にします：`pdfOcrOptions.setAutoRotate(true);`。  
3. **暗号化された PDF** – エンジンはパスワードで保護されたファイルを読み取れません。まず Aspose.PDF の `PdfDocument` を使って復号してください。  
4. **ラスタとテキストが混在** – 既に隠しテキスト層を持つ PDF もあります。再度 OCR を実行するとテキストが重複する可能性があります。元の層を保持するには `PdfOcrOptions.setSkipExistingText(true);` を使用してください。

これらの問題に対処することで、**create searchable pdf** パイプラインが実務の文書コレクションでも堅牢に動作します。

---

## 完全な動作例（すべてのステップを 1 ファイルにまとめたもの）

以下は IDE にコピー＆ペーストできる完全な Java クラスです。`YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}