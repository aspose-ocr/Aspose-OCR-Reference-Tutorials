---
category: general
date: 2026-04-26
description: JavaでAspose OCRを使用して画像から検索可能なPDFを作成します。画像をPDFに変換し、OCRでPDF化し、画像からテキストを迅速に抽出する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: ja
og_description: Aspose OCR を使用して画像から検索可能な PDF を作成します。このガイドでは、画像を PDF に変換する方法、画像を OCR
  して PDF にする方法、そして画像からテキストを抽出する方法を示します。
og_title: Java OCRで画像から検索可能なPDFを作成
tags:
- Java
- OCR
- PDF
title: Java OCRで画像から検索可能なPDFを作成する
url: /ja/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から Java OCR で検索可能な PDF を作成する

スキャンした請求書から **検索可能な PDF** を作成したいけど、どこから始めればいいかわからないことはありませんか？ 同じ壁にぶつかる開発者は多いです。朗報です！ Aspose OCR for Java を使えば、**画像を PDF に変換**し、リアルタイムで OCR を実行し、数行のコードだけで整った検索可能なファイルを作成できます。

このチュートリアルでは、画像の読み込み、エンジンに期待する言語の設定、OCR の実行、そして最終的に **検索可能な PDF** を保存するまでの全工程を解説します。最後には **画像からテキストを抽出** する方法や言語設定の調整、一般的なエッジケースの対処法も学べます。外部サービスやマイナーなコマンドラインツールは不要、純粋な Java だけです。

## 必要なもの

- Java 17 以上（API は古いバージョンでも動作しますが、17 が推奨です）。  
- Aspose OCR for Java ライブラリ – Maven Central から最新の JAR を取得できます（`com.aspose:aspose-ocr:23.10`）。  
- 読み取り可能なテキストを含む画像ファイル（PNG、JPG、TIFF が利用可能）。  
- ちょっとした IDE の忍耐力 – IntelliJ IDEA か VS Code があれば OK。

これらがすでに揃っていれば完璧です。まだの場合は、以下の Maven スニペットで環境を整えてください。

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

準備ができたら、コードに入りましょう。

## 手順 1: OCR エンジンの初期化 – **検索可能な PDF を作成** の中心

変換を始める前に `OcrEngine` インスタンスを作成します。これはピクセルを文字に変換する「脳」のようなものです。

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*ポイント:* エンジンは認識設定（言語、精度モードなど）を保持します。エンジンを一度だけインスタンス化し、複数の画像で再利用する方が、ファイルごとに新しいエンジンを作るより効率的です。

## 手順 2: **言語の設定方法** – フランス語、ドイツ語、その他のスクリプトの精度向上

元文書の言語が分かっている場合は OCR エンジンに伝えてください。処理速度が上がり、誤認識が減ります。

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

`OcrLanguage.FRENCH` を `ENGLISH`、`SPANISH`、`GERMAN` などに置き換えられます。言語が不明な場合はこの行を省略して Aspose に自動判定させても構いませんが、精度が若干低下する可能性があります。

## 手順 3: **画像を PDF に変換** したい画像を読み込む

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

`setImage` メソッドはファイルパス、`InputStream`、あるいは `java.awt.Image` オブジェクトを受け取ります。バイト配列（例: Web アップロード）からの場合は `ByteArrayInputStream` にラップして直接渡せます。

## 手順 4: OCR を実行し **画像を PDF に OCR** で一括変換

Aspose ではこのステップがシンプルです。`recognizeToPdf` が認識エンジンを走らせ、検索可能な PDF を一度に書き出します。

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

内部的には、元画像に合わせた見えないテキストレイヤーが作成されます。Adobe Reader で結果のファイルを開くと、検索ボックスに単語を入力するだけで該当箇所へ瞬時にジャンプできます。

## 手順 5: 結果を確認 – 出力はどうなる？

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

プログラムを実行し、`french_invoice_searchable.pdf` を開きます。請求書に確実に存在する単語（例: “Total”）で検索してみてください。ハイライトが正しい位置に表示されれば **検索可能な PDF を作成** できています。  

![検索可能なPDFの例](example.png)<!-- alt text includes primary keyword -->

### 期待される出力

```
Searchable PDF generated.
```

そして `YOUR_DIRECTORY` に PDF ファイルが生成されます。これを共有、インデックス、またはアーカイブに利用できます。

## 手順 6: 画像から生テキストを抽出（オプション）

場合によっては、PDF を作らずにプレーンテキストだけが必要になることがあります。データベースに保存したり感情分析に回したりする際に便利です。Aspose は認識テキストを直接取得できる機能を提供しています。

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

このスニペットは **画像からテキストを抽出** する例で、PDF を作成せずに内容だけを取得したいときに役立ちます。

## 複数ページまたは複数画像の取り扱い

ソースがマルチページ TIFF や JPEG フォルダの場合は、ファイルをループして各画像に `recognizeToPdf` を呼び出し、最後に Aspose PDF などで PDF を結合できます。簡易パターンは次の通りです。

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**プロのコツ:** 結合後は一時的に作成した PDF を削除して、作業領域をすっきり保ちましょう。

## よくある落とし穴と回避策

- **低解像度画像:** 150 dpi 未満では OCR 精度が大幅に低下します。可能であれば解像度を上げるか、スキャン時に高解像度を要求してください。  
- **傾いたページ:** 回転した画像はエンジンを混乱させます。`ocrEngine.getImagePreprocessingSettings().setDeskew(true)` で軽度の傾きは自動補正できます。  
- **未対応言語:** 設定した言語が Aspose OCR ライセンスに含まれているか確認してください。含まれていない場合、エンジンは英語にフォールバックします。  
- **大容量ファイル:** 30 MB の TIFF はメモリを大量に消費します。小さなチャンクに分割するか、JVM ヒープを増やす（例: `-Xmx2g`）ことを検討してください。

## 次のステップ – さらに進めるには

**検索可能な PDF を作成** の基本をマスターしたら、以下の拡張も検討できます。

- **バッチ変換:** マルチページパターンとスケジューラを組み合わせ、毎晩スキャンを自動処理。  
- **メタデータ注入:** Aspose PDF を使ってタイトル、作者、カスタムタグなどを検索可能 PDF に追加。  
- **デジタル署名:** OCR 後に証明書で PDF に署名し、法的文書のコンプライアンスを確保。

これらすべては、OCR エンジンの初期化、言語設定（任意）、画像の読み込み、`recognizeToPdf` の呼び出しというコア概念に基づいています。

---

### TL;DR

画像から Aspose OCR for Java を使って **検索可能な PDF を作成** する完全な実装例を紹介しました。手順はエンジンの初期化、言語設定（「言語の設定方法」）、画像の読み込み、OCR の実行、検索可能な PDF の保存、そしてオプションでプレーンテキスト抽出です。また、複数ページの処理、一般的な落とし穴、さらなる自動化のアイデアもカバーしました。

自分の領収書、契約書、手書きメモなどで試してみてください。静止画像を数秒でフル検索可能な文書に変換できます。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}