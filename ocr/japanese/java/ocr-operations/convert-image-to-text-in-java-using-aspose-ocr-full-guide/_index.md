---
category: general
date: 2026-07-05
description: Aspose OCR を使用して Java で画像をテキストに変換します。スキャン画像、TIFF ファイル、ストリームからテキストを迅速かつ確実に抽出する方法を学びましょう。
draft: false
keywords:
- convert image to text
- extract text from scan
- extract text from tif
- recognize text from stream
- how to ocr stream
language: ja
og_description: JavaでAspose OCRを使用して画像をテキストに変換します。このガイドでは、スキャン画像、TIFFファイル、ストリームからテキストを抽出する方法を、セットアップから出力までのすべての手順を網羅して説明します。
og_title: Javaで画像をテキストに変換 – Aspose OCR 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Java using Aspose OCR. Learn how to extract
    text from scan, TIFF files, and streams quickly and reliably.
  headline: Convert Image to Text in Java Using Aspose OCR – Full Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
title: Aspose OCR を使用した Java での画像からテキストへの変換 – 完全ガイド
url: /ja/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでAspose OCRを使用して画像をテキストに変換 – 完全ガイド

低レベルの画像処理テクニックに苦戦せずに **convert image to text** できる方法を考えたことはありますか？ あなたは一人ではありません。多くの開発者は、スキャンファイルや大きな TIFF ドキュメントからテキストを抽出する必要があるとき、特にソースが単純なファイルパスではなくストリームから来る場合に壁にぶつかります。  

このチュートリアルでは、**extracts text from scan** 画像を処理し、**extract text from tif** ファイルに対応し、Aspose OCR ライブラリ for Java を使用して **how to ocr stream** データを正確に扱う実践的なエンドツーエンドソリューションを順を追って解説します。最後まで読むと、認識されたテキストをコンソールに直接出力する再利用可能なスニペットが手に入ります。

## 必要なもの

- **Java Development Kit (JDK) 8 or newer** – コードは最新の JDK で動作します。  
- **Maven or Gradle**（お好みのビルドツール） – Aspose OCR の依存関係を取得します。  
- 画像ファイル – できればテストしたいマルチページ **TIFF** (`large_image.tif`)。  
- ほどほどの忍耐力（冗談です – 手順はかなり速いです）。

これらに心当たりがなくても心配はいりません。最初のステップで Maven の設定を説明し、残りは純粋な Java です。

## ステップ 1: Aspose OCR をプロジェクトに追加

OCR エンジンをクラスパスに追加する最初のハードルです。Aspose はライブラリを Maven Central に公開しているので、依存関係を 1 つ追加するだけで済みます。

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest stable version -->
    </dependency>
</dependencies>
```

> **Pro tip:** Gradle を使用している場合は、同等は  
> `implementation 'com.aspose:aspose-ocr:23.9'`.  
> この小さな追加で `OcrEngine`、`RecognitionResult`、そして内部で行われるすべての重い処理にアクセスできます。

## ステップ 2: OCR エンジンの初期化

ライブラリの準備ができたので、`OcrEngine` のインスタンスを作成できます。エンジンは **recognize text from stream** データを認識する脳みそと考えてください。

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Initialize the OCR engine – this is where the magic starts.
OcrEngine engine = new OcrEngine();
```

なぜエンジンを一度だけインスタンス化するのでしょうか？ 同じ `OcrEngine` オブジェクトを複数の画像で再利用すると、オーバーヘッドが削減され、特にスキャンページのバッチ処理時にパフォーマンスが向上します。

## ステップ 3: 画像をストリームとして開く

実際のシナリオでは、ネットワーク上の場所、データベース、またはアップロードされたファイルから画像を読み取ることが多く、これらはすべてストリームとして表れます。ファイルシステムに直接触れずに **recognize text from stream** を行う方法は次のとおりです。

```java
import java.io.FileInputStream;
import java.io.InputStream;

// ...

// Step 3: Load the image (a TIFF in this case) as an InputStream.
try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {
    // The try‑with‑resources block ensures the stream closes automatically.
```

ソースが `ByteArrayInputStream` やサーブレットリクエストからの `InputStream` の場合は、`FileInputStream` コンストラクタを置き換えるだけで、残りのコードは同一です。

## ステップ 4: OCR を実行してテキストを抽出

ストリームが手に入ったら、`engine.recognizeImage` を呼び出します。このメソッドは抽出された文字列を保持する `RecognitionResult` オブジェクトを返します。

```java
import com.aspose.ocr.RecognitionResult;

// ...

    // Step 4: Recognize text from the image stream
    RecognitionResult ocrResult = engine.recognizeImage(imageStream);

    // Step 5: Print the extracted text to the console
    System.out.println("=== OCR Output ===");
    System.out.println(ocrResult.getText());
}
```

`recognizeImage` の呼び出しがすべての重い処理を行うことに注目してください：TIFF をデコードし、OCR エンジンを実行し、プレーンテキストを返します。これが **convert image to text** 機能の核心です。

## ステップ 5: マルチページ TIFF の処理（オプション）

TIFF に複数ページが含まれている場合、Aspose OCR は各ページのテキストを自動的に連結します。ただし、可読性のためにページを分割したいこともあるでしょう。簡単な調整は次のとおりです。

```java
String fullText = ocrResult.getText();
String[] pages = fullText.split("\\f"); // Form feed character denotes page break

for (int i = 0; i < pages.length; i++) {
    System.out.println("--- Page " + (i + 1) + " ---");
    System.out.println(pages[i].trim());
}
```

このスニペットは **extracts text from scan** ドキュメントをページ単位で抽出し、出力に対する細かな制御を可能にします。

## 完全な動作例

すべてをまとめると、IDE にコピーできる完全な実行可能クラスは以下の通りです。

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import java.io.FileInputStream;
import java.io.InputStream;

public class StreamOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Open the image file as a stream
        try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {

            // Step 3: Recognize text from the image stream
            RecognitionResult ocrResult = engine.recognizeImage(imageStream);

            // Step 4: Print the extracted text
            System.out.println("=== OCR Output ===");
            System.out.println(ocrResult.getText());

            // Optional: Separate pages if it's a multi‑page TIFF
            String[] pages = ocrResult.getText().split("\\f");
            for (int i = 0; i < pages.length; i++) {
                System.out.println("--- Page " + (i + 1) + " ---");
                System.out.println(pages[i].trim());
            }
        }
    }
}
```

**Expected output** (truncated for brevity):

```
=== OCR Output ===
This is the first line of the scanned document.
Another line follows...
--- Page 1 ---
This is the first line of the scanned document.
...
```

画像がぼやけている、または言語が英語でない場合は、`engine.setLanguage` を調整したり前処理オプションを変更したりできますが、基本的なフローは変わりません。

## よくある落とし穴と回避策

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `NullPointerException` on `ocrResult.getText()` | Engine not initialized or image stream closed prematurely | Ensure the `OcrEngine` is created **before** opening the stream and keep the stream open until after `recognizeImage` returns. |
| Garbled characters | Image DPI too low (below 300) | Use a higher‑resolution source or enable Aspose’s image enhancement (`engine.getImagePreprocessingOptions().setDpi(300)`). |
| No output for multi‑page TIFF | Result not split correctly | Use `\\f` (form feed) as shown above to separate pages. |
| `OutOfMemoryError` on huge files | Loading the entire file into memory | Process the TIFF page‑by‑page using `engine.recognizeImage(pageStream)` inside a loop. |

## ボーナス: 結果をテキストファイルに変換

**convert image to text** を行い、後で使用できるように保存したい場合は、数行追加するだけです。

```java
import java.nio.file.Files;
import java.nio.file.Paths;

// ...

String outputPath = "output.txt";
Files.write(Paths.get(outputPath), ocrResult.getText().getBytes());
System.out.println("Text saved to " + outputPath);
```

これで OCR 出力の永続的なコピーが得られ、下流処理やインデックス作成に最適です。

## 結論

Java で Aspose OCR を使用して **convert image to text** を行う方法を学びました。**extract text from scan** ファイルから **extract text from tif** 画像まで網羅し、**recognize text from stream** 技術をマスターしました。完全な例は今日すぐに実行できる手順を示し、オプションのスニペットはマルチページ文書の処理や結果のディスク保存方法を示しています。

次は何をすべきでしょうか？ OCR エンジンに PDF を入力したり、言語設定を試したり、出力を検索インデックスに統合したりしてみてください。同じパターンは **how to ocr stream** データがウェブアップロード、クラウドストレージ、あるいはメッセージキューから来る場合にも機能します。

質問や、なかなか認識してくれない画像があれば下のコメント欄にどうぞ。 happy coding!

![画像ファイル → InputStream → OcrEngine → テキスト出力 のフローを示す図 – convert image to text](https://example.com/convert-image-to-text-diagram.png "画像をテキストに変換するフローダイアグラム")


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Java 用 Aspose.OCR で TIFF からテキストを抽出する方法](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose.OCR BufferedImage を使用した Java での画像からテキストへの変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR を使用した言語別画像テキスト OCR の方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}