---
category: general
date: 2026-02-22
description: Aspose を使用して多言語 OCR を実行し、画像ファイルからテキストを抽出する方法—OCR 用に画像を読み込み、効率的に OCR を実行する方法を学びましょう。
draft: false
keywords:
- how to use aspose
- multi language ocr
- extract text from image
- load image for ocr
- run ocr on image
language: ja
og_description: Aspose を使用して複数言語の画像で OCR を実行する方法 – OCR 用に画像を読み込み、画像からテキストを抽出するステップバイステップガイド
og_title: JavaでAsposeを使用した多言語OCRの使い方
tags:
- Aspose
- OCR
- Java
title: Javaでの多言語OCRにAsposeを使用する方法
url: /ja/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaでのマルチランゲージ OCR に Aspose を使用する方法

画像に英語、ウクライナ語、アラビア語のテキストが同時に含まれている場合、**Aspose の使い方**を疑問に思ったことはありませんか？ あなたは一人ではありません—単一言語でない画像ファイルから*画像からテキストを抽出*する必要がある開発者は多く壁にぶつかります。  

このチュートリアルでは、**load image for OCR** の方法を示す完全な実行可能サンプルを順を追って解説し、*multi language OCR* を有効にし、最後に **run OCR on image** してクリーンで読みやすいテキストを取得するまでを紹介します。曖昧な説明はなく、具体的なコードと各行の理由付けだけです。

## 学べること

- Maven または Gradle で Java プロジェクトに Aspose OCR ライブラリを追加する方法
- OCR エンジンを正しく初期化する方法
- *multi language OCR* 用にエンジンを設定し、自動検出を有効にする方法
- 混在したスクリプトを含む画像をロードする方法
- 認識を実行し、**extract text from image** する方法
- 未対応言語やファイル欠損などの一般的な落とし穴への対処法

最後まで読めば、任意のプロジェクトにすぐに組み込める自己完結型の Java クラスが手に入り、画像処理を即座に開始できます。

---

## 前提条件

以下を事前に用意してください。

| 要件 | 重要な理由 |
|------|------------|
| Java 8 以上 | Aspose OCR は Java 8+ を対象としています。 |
| Maven または Gradle（任意のビルドツール） | Aspose OCR JAR を自動取得するために必要です。 |
| 混在言語テキストを含む画像ファイル（例: `mixed_script.jpg`） | これが **load image for OCR** の対象です。 |
| 有効な Aspose OCR ライセンス（任意） | ライセンスがない場合は透かし付き出力になりますが、コードは同じように動作します。 |

すべて揃いましたか？ それでは始めましょう。

---

## ステップ 1: Aspose OCR をプロジェクトに追加

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

> **プロのコツ:** バージョン番号に注意してください。新しいリリースでは言語パックやパフォーマンス改善が追加されています。

依存関係を追加することは **how to use Aspose** の最初の具体的なステップです。ライブラリは後で使用する `OcrEngine`、`OcrInput`、`OcrResult` クラスを提供します。

---

## ステップ 2: OCR エンジンを初期化

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**なぜ重要か:**  
`OcrEngine` は認識アルゴリズムをカプセル化します。このステップを省略すると、後で *run OCR on image* できず、`NullPointerException` が発生します。

---

## ステップ 3: マルチランゲージサポートと自動検出を設定

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**説明:**  
- `"en"` = English、`"uk"` = Ukrainian、`"ar"` = Arabic。  
- 自動検出を有効にすると、Aspose が画像をスキャンし、各セグメントの言語を判別して適切な OCR モデルを適用します。これがないと、3 回別々に認識を実行しなければならず、手間とエラーが増えます。

---

## ステップ 4: OCR 用に画像をロード

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **`OcrInput` を使用する理由:** 複数ページや複数画像を保持でき、後でバッチモードで *load image for OCR* する柔軟性が得られます。

ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローします。`if (!new File(path).exists())` のガードを入れるとデバッグ時間を短縮できます。

---

## ステップ 5: 画像で OCR を実行

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

この時点でエンジンは画像を解析し、言語ブロックを検出し、認識されたテキストを含む `OcrResult` オブジェクトを生成します。

---

## ステップ 6: 画像からテキストを抽出して表示

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**期待される出力:**  
`mixed_script.jpg` に “Hello мир مرحبا” が含まれている場合、コンソールには次のように表示されます。

```
=== Extracted Text ===
Hello мир مرحبا
```

これが **how to use Aspose** で *extract text from image* を多言語対応で実現する完全なソリューションです。

---

## エッジケースとよくある質問

### 言語が認識されない場合は？

Aspose は提供されている OCR モデルの言語しかサポートしません。たとえば日本語が必要な場合は `setRecognitionLanguages` に `"ja"` を追加します。モデルが存在しない場合、エンジンはデフォルト（通常は英語）にフォールバックし、文字化けが発生します。

### 低解像度画像の精度を上げるには？

- 画像を前処理（DPI を上げる、二値化を適用）する。  
- `engine.setResolution(300)` で期待 DPI をエンジンに伝える。  
- 回転したスキャン用に `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` を有効にする。

### フォルダ内の画像を一括処理できる？

もちろん可能です。`input.add()` 呼び出しをディレクトリ内の全ファイルを走査するループでラップすれば、同じ `engine.recognize(input)` が各ページのテキストを連結して返します。

---

## 完全動作サンプル（コピペ即実行）

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

このコードを `MultiLangOcrDemo.java` として保存し、`javac` でコンパイル、`java MultiLangOcrDemo` で実行してください。環境が正しく設定されていれば、認識されたテキストがコンソールに表示されます。

---

## 結論

**how to use Aspose** をエンドツーエンドでカバーしました：ライブラリの追加、*multi language OCR* の設定、**load image for OCR**、**run OCR on image**、そして最終的に **extract text from image** まで。アプローチはスケーラブルです—言語コードを増やすか、ファイルリストを渡すだけで、数分で堅牢な OCR パイプラインが構築できます。

次のステップは？

- **バッチ処理:** ディレクトリを走査し、各結果を個別の `.txt` ファイルに書き出す。  
- **後処理:** 正規表現や NLP ライブラリを使って出力をクリーンアップ（余分な改行除去、一般的な OCR エラーの修正）。  
- **統合:** OCR ステップを Spring Boot の REST エンドポイントに組み込み、他サービスが画像を送信して JSON 形式のテキストを受け取れるようにする。

ぜひ実験し、失敗し、修正してみてください—それが Aspose で OCR を真にマスターする方法です。問題があれば下のコメント欄で教えてください。ハッピーコーディング！

---

![Aspose OCR の使用例（スクリーンショット）](/images/aspose-ocr-demo.png){alt="Javaコードを示す Aspose OCR の使用例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}