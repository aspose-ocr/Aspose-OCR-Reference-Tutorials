---
category: general
date: 2026-06-16
description: Java の OCR バウンディングボックスチュートリアルでは、画像からテキストを抽出し、画像のテキストを読み取り、JPG ファイルの OCR
  信頼度スコアを取得する方法を示しています。
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: ja
og_description: Java の OCR バウンディングボックスを使えば、JPG ファイルからテキストを認識し、画像からテキストを抽出し、OCR の信頼度スコアを確認できます—すべてシンプルなコード例で。
og_title: JavaでOCRバウンディングボックス – 画像からテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: JavaにおけるOCRバウンディングボックス – 画像からテキストを抽出
url: /ja/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で OCR バウンディングボックス – 画像からテキストを抽出する

Java の画像内のテキストそれぞれに対して **ocr bounding box** を取得したいと思ったことはありませんか？このチュートリアルでは、**画像からテキストを抽出** する方法、**画像からテキストを読む** 方法、そして **jpg ファイルからテキストを認識** する際に **ocr confidence スコア** を確認する方法を紹介します。簡単に言えば？最新の OCR ライブラリを数行のコードで使い、各呼び出しが何のためにあるかを少し解説すれば完了です。

以下に、実行可能な完全なサンプル、ステップバイステップの解説、そしてすぐに自分のプロジェクトにコピペできる実用的なヒントをまとめました。最後まで読めば、次のような出力が得られるようになります。

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## 必要な環境

- **Java 11** 以上（下のコードは簡潔さのために `var` キーワードを使用していますが、古い JDK では省略可能です）。  
- Java API を提供する OCR ライブラリ – 本ガイドでは、人気の Tesseract エンジンの薄いラッパーである **[Tesseract4J](https://github.com/nguyenq/tess4j)** を使用します。  
- 明瞭な印刷文字が含まれる JPEG 画像（`.jpg`）。  
- お好きな IDE（IntelliJ IDEA、Eclipse、VS Code など） – どれでも構いません。

ライブラリがまだ無い場合は、次の Maven 依存関係を追加してください。

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

それでは始めましょう。

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR バウンディングボックス: エンジンの設定

最初に行うべきことは OCR エンジンのインスタンスを作成することです。これは、後でピクセルを読み取るスキャナーをオンにするイメージです。

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**なぜ重要か:**  
`datapath` を設定しないと、Tesseract は言語パックの場所が分からず「Failed loading language」という暗号的なエラーが発生します。`setLanguage` の呼び出しはデフォルトの英語パックだけを使用する場合は省略可能ですが、明示的に書くことで将来の読者にとってコードが分かりやすくなります。

## 処理したい画像をロードする

次に、エンジンに解析させたい JPEG を渡します。ライブラリは `File` または `BufferedImage` を受け取りますが、ここではシンプルさのために `File` を使用します。

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**プロチップ:**  
画像がリソース内（例: JAR 内）にある場合は `getResourceAsStream` を使い、`ImageIO.read` でラップしてください。これにより、ローカルでもパッケージ化されたアプリでもチュートリアルが動作します。

## OCR 認識を実行する

いよいよエンジンに画像を読ませます。結果はプレーンテキストの文字列ですが、同時に **ocr confidence スコア** と各行の **ocr バウンディングボックス** も取得したいです。

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**`doOCR` ではなく `getWords` を使う理由:**  
`doOCR` は文字列だけを返し、空間情報を捨ててしまいます。`RIL_WORD`（または行レベルのボックスが欲しい場合は `RIL_TEXTLINE`）と共に `getWords` を呼び出すことで、テキスト・信頼度・バウンディング矩形を保持した `Word` オブジェクトのリストが取得できます。これが **ocr バウンディングボックス** 機能の核心です。

## 出力の理解

上記スニペットをクリーンな JPEG に対して実行すると、以下のような出力が得られます。

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – 認識された文字列。  
- **Confidence** – 0 から 1 の浮動小数点値。数値が高いほどエンジンの確信度が高いことを示します。  
- **Box** – ピクセル座標 (x, y, width, height) で表された、単語を囲む矩形。  

これで **画像からテキストを読む** と同時に、各スニペットがキャンバス上のどこにあるか正確に把握できるようになり、ハイライトやクロップ、下流の NLP パイプラインへの入力として最適です。

## エッジケースとよくある落とし穴

| 状況 | 注意点 | 対策・回避策 |
|-----------|-------------------|-------------------|
| 画像がぼやけている、またはコントラストが低い | 信頼度スコアが大幅に低下（多くの場合 0.6 未満）する。 | OpenCV で前処理：コントラストを上げ、閾値処理を適用。 |
| JPEG に回転したテキストが含まれる | バウンディングボックスが歪むか欠落する。 | `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` を使用し、Tesseract に自動で向きを検出させる。 |
| 大きな画像で OutOfMemoryError が発生 | 大画像を読み込むと Java ヒープが不足する。 | OCR 前に画像を縮小（`ImageIO.read` → `BufferedImage.getScaledInstance`）。 |
| 単語レベルではなく行レベルのボックスが必要 | `RIL_WORD` は単語単位のボックスを返す。 | `ITesseract.PageIteratorLevel.RIL_TEXTLINE` に切り替える。 |
| 非英語文字が � と表示される | 言語データがロードされていない。 | 該当する `.traineddata` をダウンロードし、`setDatapath` をそのフォルダに指す。 |

これらの問題に早めに対処すれば、後々のデバッグに費やす時間を大幅に削減できます。

## 完全動作サンプル（すべての手順を 1 ファイルにまとめた例）

以下は `src/main/java` フォルダに貼り付けて `mvn exec:java` で実行できる、自己完結型の Java クラスです。ここまで説明したすべてをまとめています。

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}