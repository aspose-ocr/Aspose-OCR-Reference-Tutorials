---
category: general
date: 2026-05-03
description: JavaでOCRを使用してPDFファイルからテキストを抽出する方法。PDFからテキストを認識し、PDFをテキストに変換し、OCRによるマルチページPDFを効率的に処理する方法を学びます。
draft: false
keywords:
- how to use ocr
- extract text from pdf
- recognize text from pdf
- convert pdf to text
- ocr multi page pdf
language: ja
og_description: JavaでOCRを使用してPDFファイルからテキストを抽出する方法。このガイドでは、PDFからテキストを認識し、PDFをテキストに変換し、OCRでマルチページPDFを処理する方法を示します。
og_title: JavaでOCRを使用する方法 – 複数ページPDFからテキストを抽出
tags:
- ocr
- java
- pdf
- aspose
title: JavaでOCRを使用する方法 – 複数ページのPDFからテキストを抽出する
url: /ja/python-java/general/how-to-use-ocr-in-java-extract-text-from-multi-page-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRを使用する方法 – マルチページPDFからテキストを抽出

**JavaプロジェクトでOCRを使用する** 方法は？ PDFの内部テキスト層に依存せずにテキストを抽出する必要がある場合は、ここが正解です。このチュートリアルでは、**PDFからテキストを認識**し、PDFをテキストに変換し、さらに **OCRマルチページPDF** をワンコールで処理できる、完全に実行可能なソリューションをステップバイステップで解説します。

たとえば、スキャンされた契約書 — 12ページのTIFFがPDFに埋め込まれているとします。インデックス作成のために検索可能なテキストが必要ですが、ファイルには文字情報が埋め込まれていません。問題ありません。手順通りにやってみましょう。

> **得られるもの:** Aspose.OCR を使用したすぐに実行できる Java スニペット、各行が重要な理由の解説、一般的な落とし穴への対策、そして即座に確認できるサンプル出力。

---

## 必要なもの

作業を始める前に、以下を用意してください。

* **Java 17**（または最近の JDK） – 古いバージョンでも動作しますが、17 が推奨です。  
* **Aspose OCR for Java** ライブラリ – Aspose のサイトから JAR をダウンロードするか、Maven/Gradle で追加してください。  
* 処理したい **マルチページ PDF**（または TIFF）。例では `contract_multipage.pdf` を `YOUR_DIRECTORY` フォルダーに配置します。  
* 有効な **Aspose OCR ライセンスファイル**（`Aspose.OCR.Java.lic`）。ライセンスがない場合は評価モードで動作し、透かしが入りますが、簡単なテストには問題ありません。

以上です—追加の OCR エンジンやネイティブバイナリは不要、JAR とライセンスだけで完結します。

---

![how to use ocr example](https://example.com/ocr-demo.png "JavaでOCRを使用する方法 – 処理フローのビジュアル概要")

*画像代替テキスト: JavaでOCRを使用する方法 – 読み込み、認識、テキスト出力のビジュアル概要。*

---

## 手順 1: OCR エンジンのセットアップ – **OCR の正しい使い方**

最初に行うべきことは OCR エンジンのインスタンスを作成し、ライセンスを適用することです。ライセンスがない場合でもエンジンは動作しますが、出力に試用版の透かしが表示されます。

```java
// Import the Aspose OCR package
import com.aspose.ocr.*;

public class OcrPdfDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Apply your license – replace the path with your actual .lic file
        ocrEngine.setLicense(new License().setLicense("Aspose.OCR.Java.lic"));
```

**重要な理由:**  
`OcrEngine` は画像解析、言語検出、テキスト抽出を統括するコアオブジェクトです。ライセンスを早期に設定しておくことで、後から試用モードにフォールバックすることを防ぎ、精度に影響が出るのを回避できます。

---

## 手順 2: ドキュメントの読み込み – **PDF からテキストを効率的に抽出**

Aspose OCR は PDF と TIFF の両方のコンテナを直接読み取れます。ここではスキャン画像が格納されたマルチページ PDF をロードします。

```java
        // 3️⃣ Load a multi‑page PDF (or TIFF) from disk
        PdfDocument pdfDoc = PdfDocument.fromFile("YOUR_DIRECTORY/contract_multipage.pdf");
```

**重要な理由:**  
`PdfDocument.fromFile` はコンテナを解析し、各ページを画像として取得できるようにします。この抽象化により、元のフォーマットに関係なく OCR エンジンがすべてのページを同一に扱えます。

**ヒント:** ソースファイルが TIFF の場合も同じ呼び出しで動作します—Aspose が自動でフォーマットを検出するため、追加コードは不要です。

---

## 手順 3: すべてのページを一括で認識 – **PDF からテキストをシームレスに認識**

自分でページをループする代わりに、エンジンに対してドキュメント全体を一度の呼び出しで処理させられます。これは **OCR マルチページ PDF** を扱う際の **PDF からテキストへの変換** に最も効率的な方法です。

```java
        // 4️⃣ Recognize text on all pages with a single method call
        List<OcrPageResult> recognizedPages = ocrEngine.recognizeDocument(pdfDoc);
```

**重要な理由:**  
`recognizeDocument` を一回だけ呼び出すことで、エンジンの初期化に伴うオーバーヘッドが削減されます。また、ページ間で言語設定が一貫するため、フォントが混在しがちな法的文書で特に重要です。

---

## 手順 4: 認識結果の出力 – **インデックス作成用に PDF をテキストに変換**

すべてのページが処理されたら、結果をイテレートして抽出された文字列を出力します。ファイルやデータベースへの書き込み、検索インデックスへの投入も同様に行えます。

```java
        // 5️⃣ Loop through each page's result and print the text
        for (int i = 0; i < recognizedPages.size(); i++) {
            OcrPageResult pageResult = recognizedPages.get(i);
            System.out.println("--- Page " + (i + 1) + " ---");
            System.out.println(pageResult.getText());
        }
    }
}
```

**期待される出力（抜粋）:**

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
...
```

PDF が 12 ページの場合、`--- Page X ---` セクションが 12 個出力され、それぞれに OCR で抽出されたテキストが続きます。

---

## **OCR マルチページ PDF** の高度なヒント

### 1. 言語設定を調整

デフォルトでは Aspose が自動検出しますが、明示的に指定すると処理が高速化します。

```java
ocrEngine.getLanguage().setLanguage(Language.ENGLISH);
```

### 2. 画像前処理を制御

スキャンした契約書はノイズが多いことがあります。デスキューや二値化を有効にしましょう。

```java
ocrEngine.getImageProcessingOptions()
        .setDeskew(true)
        .setBinarization(true);
```

### 3. 大容量ファイルをうまく扱う

100 MB を超える PDF を処理する場合は、ドキュメント全体を一度にロードせずにページ単位でストリーミングすることを検討してください。

```java
for (int pageNum = 1; pageNum <= pdfDoc.getPageCount(); pageNum++) {
    OcrPageResult result = ocrEngine.recognizePage(pdfDoc.getPage(pageNum));
    // process result...
}
```

このパターンはメモリ使用量を抑え、バッチジョブに最適です。

### 4. 構造化フォーマットへのエクスポート

プレーンテキスト以外にも、JSON や XML にエクスポートして下流処理に利用できます。

```java
String json = pageResult.toJson();
System.out.println(json);
```

---

## よくある落とし穴と回避策

| 落とし穴 | 発生原因 | 対策 |
|---------|----------|------|
| **空の出力** | ライセンス未適用またはファイルパスが間違っている | `setLicense` のパスを確認し、ファイルが存在することを検証 |
| **文字化け** | 言語設定が誤っている、または解像度が低い | 正しい `Language` を設定し、画像解像度を ≥300 dpi に確保 |
| **メモリ不足エラー** | PDF を一括で読み込んでいる | 前述のストリーミング方式を使用 |
| **ページの一部だけ認識** | PDF にラスタとベクタが混在している | OCR 前に `pdfDoc.flatten();` でフラット化 |

---

## まとめ – 本チュートリアルで学んだこと

* Aspose を使った **Java での OCR の使い方**  
* **PDF（または TIFF）からテキストを一括で抽出** する方法  
* 手動ループ不要で **PDF 全ページのテキスト認識** を実現  
* **PDF をテキストに変換** してクリーンに出力  
* **OCR マルチページ PDF** の取り扱いに関する言語設定やメモリ対策などの実践的ヒント

これで、任意の Java プロジェクトに貼り付けられる完成度の高いコードが手に入りました。画像処理オプションを調整したり、出力先を変更したり、検索インデックスに統合したりして自由にカスタマイズしてください。

---

## 次のステップ

* **Aspose OCR の高度機能**（手書き認識や PDF/A 準拠など）を探求  
* **OCR と PDF 操作の組み合わせ**（例: PDF に検索可能な隠しテキスト層を再埋め込む）  
* **バッチ処理の自動化**（フォルダー内の PDF を読み込み、対応する `.txt` ファイルへ書き出す）

問題が発生した場合は、Aspose フォーラムで質問すると良いでしょう。また、API リファレンスは本チュートリアルで使用したすべてのメソッドの詳細情報を提供しています。

コーディングを楽しみながら、頑固なスキャン画像を検索可能なテキストへ変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}