---
category: general
date: 2026-10-24
description: Aspose OCR と Java を使用して画像からテキストを抽出する方法を学びます。English、Ukrainian、Arabic
  に対応しています。OCR 用に画像を読み込み、画像上で OCR を実行するステップバイステップガイド。
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: Aspose OCR と Java を使用して画像からテキストを抽出する方法を学びます。English、Ukrainian、Arabic
  に対応しています。OCR 用に画像を読み込み、画像上で OCR を実行するステップバイステップガイド。
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: Aspose OCR と Java を使用した画像からテキストを抽出する方法
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: Aspose OCR と Java を使用した画像からテキストを抽出する方法
url: /ja/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する方法（Aspose OCR を使用、Java）

英語、ウクライナ語、アラビア語の文字が混在する画像ファイルから **extract text from image** が必要な場合、Aspose OCR を使えば簡単です。このチュートリアルでは、**load image for OCR** の方法、*multi‑language OCR* の有効化、そして最終的に **run OCR on image** してクリーンで読みやすいテキストを取得する、完全な実行可能サンプルを示します。手順は平易な言葉で説明されているので、*what* と *why* の両方が理解できます。

## クイック回答
- **最初のコード行は何ですか？** `OcrEngine engine = new OcrEngine();`
- **デフォルトでサポートされている言語は何ですか？** English (`en`)、Ukrainian (`uk`)、Arabic (`ar`) と 27 の追加言語。
- **テストにライセンスは必要ですか？** いいえ、無料トライアルで動作しますが、ライセンスを取得すると透かしが除去されます。
- **複数の画像を同時に処理できますか？** はい、`OcrInput` を使用して複数のファイルを追加し、`recognize` を呼び出す前に設定できます。
- **必要な Java バージョンは何ですか？** Java 8 以上。

## Aspose OCR を使用して Java で画像からテキストを抽出する方法

画像は `OcrInput` で読み込み、必要な言語用に `OcrEngine` を構成し、`engine.recognize(input)` を呼び出します。エンジンは自動的に言語ブロックを検出し、適切な OCR モデルを適用して、認識されたテキストを含む `OcrResult` を返します。このワンステップのフローは、最大 10 000 × 10 000 ピクセルの画像サイズでも動作し、30 以上の言語パックをサポートします。

## 学習内容

- Aspose OCR ライブラリを Java プロジェクトに追加する（Maven または Gradle）。  
- OCR エンジンを正しく初期化する。  
- エンジンを *multi‑language OCR* 用に構成し、オートデテクションを有効にする。  
- 混在したスクリプトを含む画像を読み込む。  
- 認識を実行し、**extract text from image** を行う。  
- 未サポートの言語やファイル欠如など、一般的な落とし穴に対処する。

最後までに、任意のプロジェクトに組み込める自己完結型の Java クラスが手に入り、すぐに画像処理を開始できます。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose OCR は Java 8+ を対象としています。 |
| Maven or Gradle (any build tool) | Aspose OCR JAR を自動的に取得します。 |
| An image file with mixed‑language text (e.g., `mixed_script.jpg`) | これが **load image for OCR** する対象です。 |
| A valid Aspose OCR license (optional) | ライセンスがない場合は透かしが付いた出力になりますが、コードは同様に動作します。 |

すべて揃いましたか？素晴らしい—さあ始めましょう。

## ステップ 1: Aspose OCR をプロジェクトに追加する

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Aspose OCR は 30 以上の言語パックをサポートし、画像全体をメモリに読み込まずに最大 10 000 × 10 000 ピクセルまで処理できるため、高解像度スキャンを効率的に扱えます。

依存関係を追加することは **how to use Aspose** の最初の具体的なステップです—このライブラリは後で必要になる `OcrEngine`、`OcrInput`、`OcrResult` クラスを提供します。

## ステップ 2: OCR エンジンを初期化する

`OcrEngine` クラスは Aspose OCR のコアコンポーネントで、認識プロセスを実行します。

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**Why this matters:** エンジンの初期化を省略すると、後で *run OCR on image* できるものがなくなり、`NullPointerException` が発生します。

## ステップ 3: マルチ言語サポートとオートデテクションを構成する

`OcrEngine` は `setRecognitionLanguages` メソッドでロードする言語モデルを指定し、`setAutoDetectLanguage` でテキストブロックごとの自動言語検出を有効にします。

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Explanation:**  
- `"en"` = English, `"uk"` = Ukrainian, `"ar"` = Arabic.  
- Auto‑detect を使用すると、Aspose が画像をスキャンし、各セグメントが属する言語を判断して適切な OCR モデルを適用します。これがないと、3 つの別々の認識を実行しなければならず、手間がかかりエラーが起きやすくなります。

## ステップ 4: OCR 用に画像を読み込む

`OcrInput` は Aspose OCR のコンテナで、処理対象の画像ストリームを 1 つまたは複数保持します。

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Why we use `OcrInput`:** 複数のページや画像を保持できるため、後でバッチモードで **load image for OCR** する柔軟性が得られます。ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローします。簡単なガード (`if (!new File(path).exists())`) を入れるとデバッグ時間が節約できます。

## ステップ 5: 画像で OCR を実行する

`recognize` メソッドは画像を解析し、言語ブロックを検出して、認識されたテキストを含む `OcrResult` オブジェクトを生成します。

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## ステップ 6: 画像からテキストを抽出して表示する

`OcrResult` は最終的なテキスト出力をカプセル化し、改行や信頼度スコアを含みます。

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**What you’ll see:** `mixed_script.jpg` に “Hello мир مرحبا” が含まれている場合、コンソール出力は次のようになります:

```
=== Extracted Text ===
Hello мир مرحبا
```

これは、複数言語で **how to use Aspose** と **extract text from image** を行うための完全なソリューションです。

## エッジケースとよくある質問

### 言語が認識されない場合は？

Aspose は OCR モデルが提供されている言語のみをサポートします。日本語を追加するには、`setRecognitionLanguages` に `"ja"` を含めます。モデルが存在しない場合、エンジンはデフォルト（英語）にフォールバックし、文字化けした文字が出力されます。

### 低解像度画像の精度を向上させるには？

`setResolution` はエンジンが入力画像に対して想定する DPI 値を設定し、低解像度スキャンの精度向上に役立ちます。  
`setPreprocessOptions` は OCR 前の自動回転などの前処理アクションを選択します。

- 画像を前処理する（DPI を上げ、二値化を適用）。  
- `engine.setResolution(300)` を使用してエンジンに期待する DPI を伝える。  
- 回転したスキャン用に `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` を有効にする。

### フォルダー内の画像を処理できますか？

もちろんです。`input.add()` 呼び出しをディレクトリ内のすべてのファイルを反復するループでラップします。同じ `engine.recognize(input)` 呼び出しで各ページのテキストが連結して返されます。

## 完全な動作例（コピー＆ペースト可能）

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

`MultiLangOcrDemo.java` として保存し、`javac` でコンパイル、`java MultiLangOcrDemo` で実行します。すべて正しく設定されていれば、認識されたテキストがコンソールに出力されます。

## よくある質問

**Q: 各言語パックごとに別々のライセンスが必要ですか？**  
A: いいえ、単一の Aspose OCR ライセンスでバンドルされたすべての言語パックがカバーされます。

**Q: `OcrInput` に追加できる画像数に制限はありますか？**  
A: 実質的な制限はメモリだけです。Aspose は各画像を順次処理するため、数百のファイルを問題なく追加できます。

**Q: オートデテクションは同一行内の混在スクリプトをどのように処理しますか？**  
A: エンジンは各テキストブロックを独立して解析するため、行中で言語を切り替えても正確な結果を出せます。

**Q: 各認識単語の信頼度スコアを取得できますか？**  
A: はい、`OcrResult` は詳細な品質指標のための `getConfidence()` メソッドを提供します。

**Q: サポートされている Java バージョンは何ですか？**  
A: Aspose OCR は Java 8 から Java 21（LTS リリース含む）まで対応しています。

## 結論

ここまでで、**how to use Aspose** をエンドツーエンドでカバーしました：ライブラリの追加から *multi‑language OCR* の構成、**load image for OCR**、**run OCR on image**、そして最終的に **extract text from image** まで。アプローチはスケーラブルで、言語コードを追加したりファイルリストを渡すだけで、数分で堅牢な OCR パイプラインが構築できます。

次は何をすべきか？以下のアイデアを試してみてください：

- **バッチ処理:** ディレクトリをループし、各結果を別々の `.txt` ファイルに書き出す。  
- **ポストプロセッシング:** 正規表現や NLP ライブラリを使って出力をクリーンアップ（余分な改行の除去、一般的な OCR エラーの修正）。  
- **統合:** OCR ステップを Spring Boot の REST エンドポイントとして公開し、他のサービスが画像を送信して JSON 形式のテキストを受け取れるようにする。

自由に実験し、問題を起こしてから修正してください—それが Aspose で OCR を真にマスターする方法です。問題が発生したら下にコメントを残してください。ハッピーコーディング！

---

![Aspose OCR の使用例スクリーンショット](/images/aspose-ocr-demo.png){alt="Java コードを示す Aspose OCR の使用例"}

[Aspose OCR の使用例スクリーンショット](/images/aspose-ocr-demo.png)

**最終更新日：** 2026-10-24  
**テスト環境：** Aspose OCR 24.11 for Java  
**作者：** Aspose

## 関連チュートリアル

- [Java で OCR 用に画像を読み込むステップバイステップガイド](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [Java OCR における自動言語検出ステップバイステップガイド](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [Java で OCR 用 GPU を有効にして画像からテキストを抽出する方法](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}