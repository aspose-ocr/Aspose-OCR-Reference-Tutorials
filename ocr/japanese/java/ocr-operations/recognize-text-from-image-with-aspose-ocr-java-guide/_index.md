---
category: general
date: 2026-06-19
description: Aspose OCR を使用して Java で画像からテキストを認識し、画像を docx に変換する方法、png からテキストを抽出する方法、スキャンした画像をスプレッドシートに変換する方法を学びます。
draft: false
keywords:
- recognize text from image
- convert image to docx
- extract text from png
- convert scanned image to spreadsheet
language: ja
og_description: Aspose OCR を使用して Java で画像からテキストを認識します。このステップバイステップのチュートリアルに従い、画像を
  docx に変換し、png からテキストを抽出し、スキャン画像をスプレッドシートに変換してください。
og_title: Aspose OCRで画像からテキストを認識する – Javaガイド
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in Java and learn to convert
    image to docx, extract text from png, and convert scanned image to spreadsheet.
  headline: recognize text from image with Aspose OCR – Java guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCRで画像からテキストを認識する – Javaガイド
url: /ja/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR – Java ガイドで画像からテキストを認識する

画像から **テキストを認識** したいけど、ドイツ語の PDF や PNG、さらにはスプレッドシートまで出力できるライブラリがどれか分からない、ということはありませんか？ あなたは一人ではありません。このチュートリアルでは、文字を抽出するだけでなく **画像を docx に変換**、**png からテキストを抽出**、さらには **スキャン画像をスプレッドシートに変換** までできる、数行のコードで完結する完全な Java サンプルを解説します。

Aspose.OCR はシンプルな API を備えた商用ライブラリです。ライセンスがなくても評価モードで動作しますが、一部機能（高解像度出力など）は制限されます。最終的に、レポートの PNG スクリーンショットを入力として、DOCX、XLSX、EPUB ファイルを自動的に生成できるプログラムが完成します。

## 前提条件

作業を始める前に以下を用意してください。

* **Java Development Kit (JDK) 17** 以上がインストールされていること。
* **Aspose.OCR for Java** の JAR（Aspose の公式サイトからダウンロード、または Maven で取得）。
* 評価版の透かしを除去したい場合は、オプションで **Aspose.OCR.lic** ファイル。
* サンプル画像（例: `report.png`）を、コードから参照できるフォルダーに配置。

Maven を使用している場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

準備が整ったら、さっそく実装に取り掛かりましょう。

## Step 1: recognize text from image – apply the license (optional)

まず最初に、Aspose にライセンスがあることを通知します。このステップを省略してもデモは動作しますが、出力ファイルに小さな “Evaluation” バナーが表示されます。

```java
import com.aspose.ocr.*;

public class ExportDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (optional for full functionality)
        License license = new License();
        try {
            license.setLicense("Aspose.OCR.lic");
            System.out.println("License loaded successfully.");
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
```

> **プロのコツ:** `.lic` ファイルはコンパイル済み JAR と同じディレクトリに置くか、絶対パスで指定してください。そうしないと `setLicense` 呼び出しで例外がスローされます。

## Step 2: recognize text from image – create and configure the OCR engine

次に OCR エンジンを起動し、期待する言語を設定します。この例ではドイツ語を扱いますが、Aspose は多数の言語を標準でサポートしています。

```java
        // Create an OCR engine and set the recognition language to German
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.German); // change to Language.English for English text
```

言語を設定する理由は何ですか？ エンジンは言語固有の辞書を利用して精度を向上させます。特に “ß” や “ü” といった文字に有効です。設定しなくても結果は得られますが、ノイズが増える可能性があります。

## Step 3: recognize text from image – feed the PNG and get raw results

デモの核心です。PNG ファイルへのパスをエンジンに渡し、重い処理を任せます。

```java
        // Recognize text from the input image
        String inputImagePath = "YOUR_DIRECTORY/report.png"; // <-- replace with your actual path
        OcrResult ocrResult = ocrEngine.recognizeImage(inputImagePath);
        System.out.println("OCR completed. Extracted " + ocrResult.getText().length() + " characters.");
```

`OcrResult` オブジェクトには生の Unicode 文字列と、レイアウト情報が含まれます。後でフォーマットを保持したい場合に利用できます。画像がスキャンした表であっても、エンジンはプレーンテキストを返すので、次の **スキャン画像をスプレッドシートに変換** ステップで活用できます。

## Step 4: convert image to docx – saving the result as a Word document

Aspose を使えば OCR の出力を DOCX ファイルに簡単にエクスポートできます。編集可能な Word 文書が必要な downstream 処理に便利です。

```java
        // Save the recognized text in DOCX format
        String outputDocxPath = "YOUR_DIRECTORY/report.docx";
        ocrResult.save(outputDocxPath, OutputFormat.Docx);
        System.out.println("Saved DOCX to " + outputDocxPath);
```

内部的には、抽出したテキストを 1 つの段落として含むシンプルな Word 文書が生成されます。見出しや表といったリッチなスタイリングが必要な場合は、後から Apache POI や Aspose.Words で DOCX を加工できます。

## Step 5: convert scanned image to spreadsheet – export to XLSX

スキャンした請求書や財務表は Excel で扱う方が楽なことがあります。同じ `OcrResult` を XLSX ファイルとして保存すれば、Aspose が表構造を検出した場合はセルに分割してくれます。

```java
        // Save the same result in additional formats (XLSX, EPUB)
        String outputXlsxPath = "YOUR_DIRECTORY/report.xlsx";
        ocrResult.save(outputXlsxPath, OutputFormat.Xlsx);
        System.out.println("Saved XLSX to " + outputXlsxPath);
```

元の PNG にきれいなグリッドがあれば、生成されたスプレッドシートは各列が別々のセルに配置されます。そうでない場合は改行で区切られた単一列になりますが、手動でコピー＆ペーストするよりは遥かに楽です。

## Step 6: extract text from png – also export to EPUB (optional)

最後に、EPUB 電子書籍を生成する方法を示します。これは Aspose の `save` メソッドの柔軟性を示すと同時に、**png からテキストを抽出** して出版物に活用する別の手段となります。

```java
        // Optional: export to EPUB for e‑reading devices
        String outputEpubPath = "YOUR_DIRECTORY/report.epub";
        ocrResult.save(outputEpubPath, OutputFormat.Epub);
        System.out.println("Saved EPUB to " + outputEpubPath);
    }
}
```

以上がプログラム全体です。`javac ExportDemo.java` でコンパイルし、`java ExportDemo` で実行してください。すべてが正しく設定されていれば、`YOUR_DIRECTORY` に `report.docx`、`report.xlsx`、`report.epub` の 3 ファイルが生成され、コンソールには抽出された文字数が表示されます。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| **License not found** | `Aspose.OCR.lic` のパスが間違っている、またはファイルが存在しない。 | ファイルを JAR と同じ場所に置くか、`setLicense` に絶対パスを指定する。 |
| **Garbage characters** | 言語設定が誤っている（例: ドイツ語テキストに英語を指定）。 | `ocrEngine.setLanguage(Language.German)` など、正しい言語 enum を呼び出す。 |
| **Empty output files** | 入力画像パスのタイプミス、または未対応フォーマット。 | パスを確認し、ファイルが存在すること、サポートされているラスタ形式（PNG、JPEG、BMP）であることを確認する。 |
| **Large file size** | 高解像度画像をそのまま使用している。 | OCR 前に画像を約 300 dpi にリサイズする。Aspose は `ocrEngine.setResolution(300)` で自動的にリサイズ可能。 |

## ソリューションの拡張

**画像からテキストを認識**し、**スキャン画像をスプレッドシートに変換**できるようになったら、次のような応用が考えられます。

* **バッチ処理** – フォルダー内の PNG をループで処理し、DOCX/XLSX の ZIP を生成。
* **後処理** – 正規表現で OCR ノイズ（余分な改行など）を除去。
* **統合** – Spring Boot の REST エンドポイントに組み込み、画像アップロードを受け取ってダウンロード可能な DOCX を返す。

これらのアイデアは、今回学んだコアステップをベースに実装できます。

## 結論

Aspose OCR for Java を使って **画像からテキストを認識** する方法、そして **画像を docx に変換**、**png からテキストを抽出**、**スキャン画像をスプレッドシートに変換** する手順を学びました。上記の完全なサンプルは、すべてのインポート文、設定、期待される出力を網羅しています。

次は言語を英語に変えてみたり、マルチページ TIFF を処理したり、DOCX 出力を Aspose.Words に渡して高度な書式設定を行ったりしてみてください。OCR と文書生成ライブラリを組み合わせれば、可能性は無限に広がります。

質問や問題があればコメントで教えてください。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、別の実装アプローチを検討したりする際に役立ちます。

- [JavaでAspose.OCR BufferedImageを使用して画像をテキストに変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR Detect Areas Modeで画像からテキストを抽出（Java）](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCRで言語を指定して画像テキストをOCRする方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}