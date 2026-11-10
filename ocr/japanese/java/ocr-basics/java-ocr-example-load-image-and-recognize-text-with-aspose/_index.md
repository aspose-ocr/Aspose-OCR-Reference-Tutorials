---
category: general
date: 2026-06-16
description: 数行のコードで、JPG ファイルから画像を読み込み、テキストを認識し、Aspose を使用してテキストを抽出する Java OCR の例です。
draft: false
keywords:
- java ocr example
- load image ocr
- recognize text java
- recognize jpg text
- extract text aspose
language: ja
og_description: Java OCRのサンプルは、画像の読み込み、JPGテキストの認識、そしてAspose OCRライブラリを使用した抽出を示します。
og_title: Java OCRサンプル – 画像を読み込んでテキストを認識
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Java OCR example that shows how to load image OCR, recognize text Java,
    and extract text Aspose from a JPG file in just a few lines.
  headline: Java OCR Example – Load Image and Recognize Text with Aspose
  type: TechArticle
- questions:
  - answer: Absolutely. Just point `ImageStream.fromFile("image.png")` to the desired
      file; Aspose auto‑detects the format.
    question: Can I process PNG or TIFF files the same way?
  - answer: Check the image resolution (≥300 dpi is ideal) and consider enabling binarization.
      Also, verify that the correct language is set.
    question: What if the OCR returns garbled characters?
  - answer: 'Yes. `result.getWords()` returns a collection where each `OcrWord` has
      a `getConfidence()` method. ## Conclusion You now have a solid **java ocr example**
      that demonstrates how to **load image ocr**, **recognize text java**, and **extract
      text aspose** from a JPEG file. The snippet runs out‑of‑the‑b'
    question: Is there a way to get confidence scores for each word?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java OCRサンプル – 画像を読み込み、Asposeでテキストを認識
url: /ja/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR Example – 画像をロードしてテキストを認識する with Aspose

画像からテキストを抽出する簡単な方法を **java ocr example** で知りたくありませんか？ あなた一人ではありません—開発者は常にスキャンしたレシート、IDカード、あるいはスクリーンショットを編集可能な文字列に変換する必要があります。 良いニュースは、Aspose.OCR for Java を使えば、画像をロードし、OCR を実行し、数行のコードでクリーンなテキストを取得できることです。

このガイドでは、JPEG から **load image ocr** を行い、**recognize text java** を実行し、評価版を使用している場合でも **extract text aspose** の方法を示す、完全で実行可能なプログラムを順に解説します。最後まで読むと、任意のプロジェクトに組み込める堅実なテンプレートが手に入ります。

## 学べること

- Maven または Gradle プロジェクトに Aspose.OCR ライブラリを追加する方法。
- ディスク上のファイルから **recognize jpg text** を取得するために必要な正確なコード。
- 評価ビルドを検出し、透かし警告を処理する方法。
- サポートされていない画像形式や低解像度スキャンなど、一般的な落とし穴への対処法のヒント。

Aspose の事前経験は不要です。基本的な Java 環境とテスト用の画像ファイルがあれば始められます。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| JDK 17 以上（ライブラリは Java 8+ をサポートしていますが、最新の JDK の方がパフォーマンスが向上します） | 最新の Aspose バイナリとの互換性が保証されます。 |
| Maven 3.x または Gradle 7+（または JAR を手動で追加することも可能） | 依存関係の管理が簡素化されます。 |
| 処理したい JPEG 画像（`sample.jpg`） | 例では JPG を使用していますが、サポートされている形式であればどれでも動作します。 |
| Aspose.OCR for Java ライセンス（オプション） | ライセンスがない場合、評価用の透かしが表示されます。コードはそれをチェックします。 |

既にプロジェクトがある場合は、以下の依存関係を追加すれば準備完了です。

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro tip:** バージョン番号は常に最新に保ちましょう。Aspose は四半期ごとに改善をリリースしており、特に低コントラスト画像の精度が向上します。

## 手順 1: OCR エンジン インスタンスの作成

最初に必要なのは `OcrEngine` です。ピクセルを解析し文字に変換する脳のようなものと考えてください。

```java
// Step 1 – Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

なぜ別個のエンジンオブジェクトが必要かというと、同じ設定を複数の画像で再利用でき、メモリと起動時間を節約できるからです。

## 手順 2: OCR 用に画像をロードする

ここで実際にディスクから **load image ocr** データを取得します。Aspose は、生の `InputStream` の取り扱いを抽象化した便利な `ImageStream` ラッパーを提供しています。

```java
// Step 2 – Load the JPEG file you want to process
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

`YOUR_DIRECTORY` を `sample.jpg` が存在する絶対パスまたは相対パスに置き換えてください。このメソッドは PNG、BMP、TIFF、さらにはマルチページ PDF もサポートしているため、JPG に限定されません。

> **Common question:** *画像がバイト配列の場合はどうすればいいですか？*  
> その場合は `ImageStream.fromBytes(byteArray)` を使用してください。残りのフローは同じです。

## 手順 3: Java でテキストを認識する

画像がメモリ上にある状態で、Aspose に重い処理を任せます。`recognize()` 呼び出しは OCR アルゴリズムを実行し、`OcrResult` オブジェクトを返します。

```java
// Step 3 – Perform OCR and get the result object
OcrResult result = engine.recognize();
```

ライブラリは言語、向き、さらには基本的なノイズ除去も自動で検出します。特定の言語（例: フランス語）を強制したい場合は、`recognize()` を呼び出す前に `engine.getLanguage().setLanguage(Language.French);` と設定できます。

## 手順 4: 評価版の警告を処理する

無料の評価ビルドを実行している場合、結果に微細な透かしが含まれることがあります。`isEvaluation()` フラグを使ってユーザーに警告したり、状態をログに記録したりできます。

```java
// Step 4 – Check for evaluation mode
if (result.isEvaluation()) {
    System.out.println("[EVALUATION] Result may contain a watermark.");
}
```

後でライセンスを購入し、`License license = new License(); license.setLicense("Aspose.Total.Java.lic");` で適用すれば、このブロックは決して実行されません。

## 手順 5: Aspose でテキストを抽出し、表示する

最後に、結果から認識された文字列を取得して表示します。ここが **extract text aspose** の部分です。

```java
// Step 5 – Output the recognized text
System.out.println(result.getText());
```

返される文字列は改行を保持するため、元のレイアウトにかなり忠実な表現が得られます。

### 期待される出力

`sample.jpg` に “Hello, Aspose OCR!” という文が含まれていると仮定すると、以下のような出力が得られます。

```
[EVALUATION] Result may contain a watermark.
Hello, Aspose OCR!
```

画像がぼやけている、または低解像度の場合、余分なスペースや文字の誤認識が発生することがあります—これは次で説明する一般的な OCR の特性です。

## 手順 6: 精度向上のヒント（オプションの拡張）

| Tip | How it helps |
|-----|--------------|
| **DPI を上げる** – `engine` に渡す前に画像を 300 dpi にスケールする | 高解像度にすることでエンジンが扱える詳細が増え、精度が向上します。 |
| **二値化で前処理** – `engine.getImageProcessingOptions().setBinarization(true);` を使用して白黒に変換する | 文字検出を混乱させる背景ノイズを除去します。 |
| **言語を指定** – `engine.getLanguage().setLanguage(Language.English);` | OCR エンジンを誘導し、類似文字の誤検出を減らします。 |
| **バッチ処理** – 複数ファイルで同じ `OcrEngine` インスタンスを再利用する | オブジェクト生成のオーバーヘッドを削減します。 |

これらの調整は、低品質の JPEG で提供されるスキャンレシートや名刺から **recognize jpg text** を行う場合に特に有効です。

## 完全な動作例

以下は、IDE にコピー＆ペーストできる完全な単体 Java クラスです。上記のオプション拡張が含まれていますが、最小限の例が好みの場合はコメントアウトできます。

```java
import com.aspose.ocr.*;

public class JavaOcrExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // OPTIONAL: Improve accuracy for low‑resolution JPEGs
        // engine.getImageProcessingOptions().setBinarization(true);
        // engine.getLanguage().setLanguage(Language.English);

        // Load the image (replace the path with your own)
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Perform OCR
        OcrResult result = engine.recognize();

        // Detect evaluation mode
        if (result.isEvaluation()) {
            System.out.println("[EVALUATION] Result may contain a watermark.");
        }

        // Print the extracted text
        System.out.println(result.getText());
    }
}
```

> **Note:** ライセンスなしで実行すると、出力に評価用の通知が含まれます。有効なライセンスファイルを追加すれば、通知は消え、クリーンなテキストが得られます。

## よくある質問

**Q: PNG や TIFF ファイルも同様に処理できますか？**  
A: もちろんです。目的のファイルに対して `ImageStream.fromFile("image.png")` を指定すれば、Aspose が自動で形式を検出します。

**Q: OCR の結果が文字化けした場合は？**  
A: 画像解像度（理想は ≥300 dpi）を確認し、二値化の有効化を検討してください。また、正しい言語が設定されているかも確認しましょう。

**Q: 各単語の信頼度スコアを取得する方法はありますか？**  
A: はい。`result.getWords()` はコレクションを返し、各 `OcrWord` に `getConfidence()` メソッドがあります。

## 結論

これで、JPEG ファイルから **load image ocr**、**recognize text java**、**extract text aspose** を実演する堅実な **java ocr example** が手に入りました。このスニペットはすぐに動作し、評価版の警告に対応し、難しい画像の精度向上への明確な道筋を提供します。

次のステップは？ エンジンに請求書のバッチを投入したり、異なる言語設定を試したり、出力をデータベースに連携して検索可能なアーカイブを作成したりしてみてください。Aspose OCR ライブラリは、シンプルなデスクトップユーティリティから大規模な文書処理パイプラインまで、あらゆる用途に柔軟に対応できます。

質問がある、またはクールなユースケースを共有したい方は、下にコメントを残してください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose OCR で画像テキストを認識 – 完全な Java OCR チュートリアル](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR Detect Areas モードで画像からテキストを抽出（Java）](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR BufferedImage を使用して Java で画像をテキストに変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}