---
category: general
date: 2026-02-14
description: JavaでAspose OCRを使用して画像のOCRを実行し、画像からテキストを抽出する方法を学びます。OCR用の画像の読み込み、カスタム辞書、スペル補正が含まれます。
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: ja
og_description: Aspose OCR を使用して Java で画像の OCR を実行します。このガイドでは、OCR 用に画像を読み込む方法、画像からテキストを抽出する方法、スペル補正を有効にする方法を示します。
og_title: 画像のOCRを実行する – 完全なJavaチュートリアル
tags:
- OCR
- Java
- Aspose
title: Aspose OCRで画像のOCRを実行する – Javaステップバイステップガイド
url: /ja/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像で OCR を実行する – 完全な Java チュートリアル

画像ファイルで **perform OCR on image** が必要だったことはありますか、でもどこから始めればいいか分からなかったことはありませんか？ あなたは一人ではありません。多くの開発者が画像データからテキストを抽出しようとしたときに同じ壁にぶつかります。良いニュースは、Aspose OCR for Java を使えば、数行のコードだけで信頼できる結果が得られ、さらにカスタム辞書とスペルチェックで精度を向上させられることです。

このガイドでは、必要なすべてのことを順に説明します：OCR 用に画像をロードすることから、スペル補正を有効にすること、そして最終的にクリーンアップされたテキストを出力することまで。最後まで読むと、独自の Java プロジェクトで **perform OCR on image** 資産を実行できるようになり、**extract text from image** ファイルをノイズの多いスキャンでも機能する方法で抽出できるようになります。

## 必要なもの

- **Java Development Kit (JDK) 8+** – コードは標準の Java API を使用します。
- **Aspose OCR for Java** ライブラリ（最新の JAR は Aspose のウェブサイトまたは Maven Central から取得できます）。
- 処理したい画像ファイル（例: `invoice.png`）。
- （オプション）ドメイン固有の単語を1行ずつ含むプレーンテキストファイル `custom_dict.txt`。

以上です—重厚なフレームワークも外部サービスも不要です。純粋な Java と Aspose OCR JAR だけです。

## 手順 1: プロジェクトのセットアップと依存関係のインポート

まず、新しい Maven（または Gradle）プロジェクトを作成し、Aspose OCR の依存関係を追加します。Maven を使用している場合、`pom.xml` に以下を含める必要があります：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

手動で JAR をダウンロードしたい場合は、`libs` フォルダーに配置し、クラスパスに追加してください。

> **Pro tip:** 記述時点のバージョン番号を必ず確認してください。新しいリリースでは言語パックなどの追加機能が導入されている場合があります。

## 手順 2: OCR 用に画像をロードする

最初の実際のコードステップは、解析したい画像を OCR エンジンに指定することです。Aspose OCR は `ImageStream` ラッパーを使用し、ファイル、バイト配列、あるいは URL から読み取ることができます。

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**load image for OCR** を単一のメソッド呼び出しで行っていることに注目してください—面倒な `BufferedImage` の操作は不要です。画像がリソース内にある場合は、パスを `getClass().getResourceAsStream(...)` に置き換えるだけです。

## 手順 3: スペル補正を有効にする（オプションだが強力）

Aspose OCR は一般的な OCR の誤り（例: “l” と “1” の混同）を自動的に修正できます。この機能を有効にするのはフラグを切り替えるだけで簡単です：

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

なぜやるのか？フォントが小さく、スキャナーが細かなノイズを入れてしまう印刷された請求書をスキャンしたと想像してください。スペル補正は “Inv0ice” を自動的に “Invoice” に戻すことが多く、追加の作業は不要です。

## 手順 4: カスタム辞書を提供する（エンジンを調整）

業界固有の用語（医療コード、法的用語、製品 SKU など）を扱う場合、カスタム辞書は精度を劇的に向上させます。辞書は1行に1単語のテキストファイルです。

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

ファイルは UTF‑8 エンコーディングを使用していることを確認してください。そうでないと、ASCII 以外の単語が文字化けする可能性があります。

## 手順 5: OCR プロセスを実行する

いよいよエンジンに処理を任せます。`process()` 呼び出しは、認識されたテキスト、信頼度スコア、必要に応じてレイアウトも含む `OcrResult` オブジェクトを返します。

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

エンジンが例外を投げたかどうか気になる場合は、この呼び出しを try‑catch ブロックでラップし、詳細は `ocrResult.getErrorMessage()` を確認してください。

## 手順 6: 認識（および修正）されたテキストを出力する

最後のステップは、抽出した文字列を表示（または保存）することです。簡単なデモとしてコンソールに出力します：

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

プログラムを実行すると、次のような出力が得られるはずです：

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

余計な文字が表示された場合は、カスタム辞書を再確認し、画像品質（例: エンジンに渡す前にコントラストを上げる）を調整してください。

### 完全な動作例

すべてをまとめると、以下が完全な実行可能クラスです：

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

このファイルを `SpellCorrectDemo.java` として保存し、パスを調整し、`javac` でコンパイル、`java SpellCorrectDemo` で実行してください。これで **perform OCR on image** ファイルが実行でき、抽出されたテキストが出力されます。

## よくある質問とエッジケース

### 画像が別の形式（PDF、TIFF など）の場合は？

Aspose OCR は多くのラスタ形式をそのまま処理できます。PDF の場合は、まず各ページを画像として抽出する必要があります—Aspose PDF for Java がそれをうまく行います。`BufferedImage` またはバイトストリームがあれば、同じ `setImage` 呼び出しが機能します。

### マルチページ文書を処理するには？

各ページ画像をループし、OCR 手順を実行して結果を連結します。独立したスペルチェックコンテキストが必要な場合は、各ページごとに `OcrEngine` をリセットまたは新規作成することを忘れないでください。

### 言語や文字セットを制限できますか？

はい。`ocrEngine.getEngineOptions().setLanguage(Language.English);`（または他のサポートされている言語）を使用して、誤検出を減らし、処理速度を向上させます。

### 大量バッチのパフォーマンスは？

Aspose OCR は読み取り専用操作に対してスレッドセーフです。スレッドプールを作成して画像を並行処理できます—ただし同じ `OcrEngine` インスタンスをスレッド間で共有しないでください。

## 精度向上のためのヒント

- **Pre‑process the image**: コントラストを上げ、背景ノイズを除去、またはグレースケールに変換します。
- **Use a high‑resolution scan**（300 dpi 以上）を使用してください。低解像度では文字化けが起きやすくなります。
- **Keep the custom dictionary lean**: 関連性の低い単語が多すぎるとスペルチェッカーが混乱します。
- **Validate the output**: 期待される形式（例: 日付、数値）が分かっている場合は、正規表現で後処理し異常を検出します。

## 次のステップ

これで Aspose OCR を使って **perform OCR on image** ファイルと **extract text from image** ができるようになったので、以下を検討してみてください：

- **Saving the OCR output to a PDF**: 検索可能なテキストレイヤー付きの PDF に OCR 出力を保存する。
- **Integrating with a database**: 抽出した請求書データを自動的にデータベースに保存する。
- **Applying machine‑learning post‑processing**: 手書きメモの精度をさらに向上させる機械学習による後処理を適用する。
- **Using the `load image for OCR` flag**: ユーザーがアップロードした画像を受け付ける Web サービスで `load image for OCR` フラグを使用する。

これらのトピックはすべて、ここで説明した基本手順に基づいているため、移行はスムーズに行えるでしょう。

---

*Happy coding! 問題が発生した場合は遠慮なくコメントを残してください。実際の例から学ぶことに勝るものはありません。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}