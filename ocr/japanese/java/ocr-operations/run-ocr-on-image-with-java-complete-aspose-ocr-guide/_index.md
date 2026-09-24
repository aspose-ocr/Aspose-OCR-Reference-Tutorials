---
category: general
date: 2026-02-09
description: JavaでAspose OCRを使用して画像のOCRを実行する – PNGからテキストを抽出し、数ステップで自動言語検出OCRを有効にする方法を学びましょう。
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: ja
og_description: 画像のOCRを即座に実行します。このガイドでは、PNGファイルからテキストを抽出し、Aspose OCR for Java を使用して自動言語検出
  OCR を有効にする方法を示します。
og_title: Javaで画像のOCRを実行 – 完全なAspose OCRチュートリアル
tags:
- OCR
- Java
- Aspose
title: Javaで画像のOCRを実行する – 完全なAspose OCRガイド
url: /ja/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image with Java – Complete Aspose OCR Guide

画像ファイルに対して **OCR を実行** したいが、どこから始めればよいかわからないことはありませんか？たとえば、ヒンディー語のテキストが含まれた PNG スクリーンショットが数枚あり、Java だけで大規模な機械学習環境を構築せずに文字を抽出できないかと考えているかもしれません。良いニュースは、可能であり、Aspose OCR を使えば意外と簡単に実現できるということです。

このチュートリアルでは、**PNG からテキストを抽出** する実践的な例を通して、**自動言語検出 OCR** を有効にする方法と、すぐに実行できる Java プログラムを紹介します。最後まで読めば、ヒンディー文字をコンソールに出力する動作サンプルが手に入り、各行が何のためにあるかも理解できるようになります。

## What You’ll Need

- **Java Development Kit (JDK) 8** 以上 – どの最近のバージョンでもコンパイル可能です。  
- **Aspose.OCR for Java** ライブラリ – Aspose の公式サイトまたは Maven Central から最新の JAR を取得してください。  
- デーヴァナーガリー文字が含まれるサンプル画像 (`hindi_sample.png`) – 任意のスクリーンショットツールで作成できます。  
- IDE またはシンプルなテキストエディタ – 私は IntelliJ IDEA を使用していますが、`javac` でも問題ありません。

外部サービスやクラウド API キーは不要です。ローカルの JAR と画像だけで完結します。シンプルですね。

## Step 1: Add Aspose OCR to Your Project

まず、Aspose OCR の JAR がクラスパスに含まれていることを確認します。Maven を使う場合は、次の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

手動で設定したい場合は、`aspose-ocr-23.10.jar` をダウンロードし、`libs/` フォルダに配置したうえで次のようにコンパイルします。

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro tip:** ソースファイルの冒頭に JAR のバージョン番号をコメントで残しておくと、将来どの API を対象にしたか思い出しやすくなります。

## Step 2: Create the OCR Engine Instance

次に、重い処理をすべて担うコアオブジェクトを生成します。`OcrEngine` はこの操作の「脳」に相当します。

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

なぜここでインスタンス化するかというと、エンジンは言語設定などの構成情報や再利用可能なリソースを保持しているため、アプリケーションごとに一度だけ作成すればオーバーヘッドを削減できるからです。

## Step 3: Configure Language Settings (and Enable Auto‑Detect)

事前に言語が分かっている場合（例: ヒンディー語）には、エンジンにデーヴァナーガリーに集中させるよう指示できます。これにより精度が向上し、処理速度も速くなります。

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

`setAutoDetectLanguage(true)` 行が **自動言語検出 OCR** のスイッチです。混在した言語の画像を渡すと、エンジンは各スクリプトを自動的に判別しようとします。ファイルごとに手動でタグ付けできないバッチ処理に便利です。

## Step 4: Run OCR on the PNG Image

ここで実際に **画像に対して OCR を実行** します。`recognize` メソッドはファイルパスを受け取り、ビットマップを読み込んで `RecognitionResult` を返します。

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

`YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。ファイルが見つからない場合は、Aspose が明確な例外をスローするので、後で原因を推測する必要はありません。

## Step 5: Retrieve and Display the Extracted Text

最後に、結果オブジェクトから認識された文字列を取得し、コンソールに出力します。ヒンディー語の場合、端末が UTF‑8 に対応していれば Unicode 文字が正しく表示されます。

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**期待される出力**（サンプル画像に「नमस्ते दुनिया」と書かれていると仮定）:

```
Hindi text:
नमस्ते दुनिया
```

自動検出を有効にしていて画像に英語も含まれていれば、両方のスクリプトが混在した形で出力されます。

## Full Working Example

以下が完全に動作するプログラムです。`LanguageExample.java` にコピペし、画像パスを調整すればすぐに実行できます。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** IDE を使用している場合は、プロジェクトのビルドパスに Aspose OCR JAR が含まれていることを確認してください。IntelliJ なら *File → Project Structure → Libraries* から JAR を追加します。

## Common Questions & Edge Cases

### What if my PNG is low‑resolution?

OCR の精度は 150 dpi 未満になると急激に低下します。ImageMagick などのツールで画像を拡大（例: `convert input.png -resize 200% output.png`）してからエンジンに渡すと良いでしょう。`auto detect language OCR` フラグは引き続き機能しますが、誤認識は減少しません。

### Can I process multiple images in a loop?

もちろん可能です。`recognize` 呼び出しを `for` ループで囲み、同じ `OcrEngine` インスタンスを再利用してください。エンジンを再利用することで、各イテレーションで言語モデルを再ロードする必要がなくなり、メモリと CPU の両方を節約できます。

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### How do I handle non‑Unicode consoles?

端末に文字化けが出る場合は、Java 起動時にファイルエンコーディングを UTF‑8 に設定します。

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### Is there a way to get confidence scores?

あります。`RecognitionResult` には `getConfidence()` があり、認識された各行に対して 0 から 1 の浮動小数点数を返します。`result.getLines()` を走査してスコアを取得すれば、信頼度の低い結果を除外するなどのフィルタリングが可能です。

## Pro Tips for Production Use

- **Cache language models**: 数千枚の画像を処理する場合は、バッチ全体でエンジンを保持すると効果的です。  
- **Parallel processing**: 各画像を `Callable` にラップしてスレッドプールに投入します。ただしエンジンはスレッドセーフではないため、スレッドごとにインスタンスを作成してください。  
- **Logging**: 大規模ジョブでは `System.out.println` の代わりに適切なロガー（SLF4J など）を使用しましょう。  
- **Memory management**: 終了時に `ocrEngine.dispose()` を呼び出してネイティブリソースを解放します。

## Visual Overview

![Run OCR on image example diagram](ocr_flow.png "Run OCR on image example diagram")

上図はフローを示しています：**画像に対して OCR を実行 → 言語設定 → 自動言語検出 OCR（オプション） → PNG からテキスト抽出**。

## Conclusion

本稿では、Aspose OCR for Java を使用して **画像に対して OCR を実行** し、**PNG からテキストを抽出** する方法、そして柔軟な多言語シナリオ向けに **自動言語検出 OCR** を切り替える手順を示しました。完全なコードサンプルはそのままコピー、コンパイル、実行でき、外部サービスや隠れた手順は一切ありません。

次のステップに挑戦したいですか？`Language.HINDI` を `Language.AUTO` に置き換えて混在スクリプトのドキュメントを処理したり、PDF 入力に挑戦したりしてみてください（Aspose OCR は PDF もサポートしています）。さらに、このスニペットを Spring Boot の REST エンドポイントに組み込んで OCR を Web サービスとして提供することも可能です。

Happy coding, and may your images always be readable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}