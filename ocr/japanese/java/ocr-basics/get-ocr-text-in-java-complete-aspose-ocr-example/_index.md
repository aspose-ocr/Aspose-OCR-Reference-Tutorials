---
category: general
date: 2026-01-07
description: Aspose OCR Java を使用して画像から OCR テキストを取得します。テキスト画像の抽出方法、画像 OCR のロード方法、数分で
  Java OCR のサンプルを実行する方法を学びましょう。
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: ja
og_description: Aspose OCR Java を使用して画像から OCR テキストを取得します。このガイドでは、Java の OCR の例、テキスト画像の抽出方法、そして画像
  OCR を効率的にロードする方法を示します。
og_title: JavaでOCRテキストを取得 – 完全なAspose OCRチュートリアル
tags:
- OCR
- Java
- Aspose
- Image Processing
title: JavaでOCRテキストを取得 – 完全なAspose OCR例
url: /ja/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRテキストを取得 – 完全なAspose OCR例

スキャンしたドキュメントから **OCRテキストを取得** したいと思ったことはありませんか？どのライブラリを選べばいいか分からないこともありますよね。実際のプロジェクトでは、請求書の自動化、レシート処理、または多言語フォームのデジタル化など、画像からテキストを抽出することが自動化への第一歩です。  

このチュートリアルでは、Aspose OCR for Java ライブラリを使用した **java OCR example** を順に解説します。最後まで読むと、**load image OCR** の方法、エンジンの実行、そして **extract text image** データを数行のコードで取得する方法が分かります。余計な説明は省き、実際にプロジェクトにコピペできる実用的な解決策を提供します。

## 学べること

- Aspose OCR for Java のセットアップ方法（Maven の座標を含む）。  
- **load image OCR** を実行し、言語を指定する正確な手順。  
- **get OCR text** をプレーン文字列として取得し、コンソールに出力する方法。  
- 多言語画像の取り扱いと自動言語検出のコツ。  

*前提条件*: Java 8 以降、Maven 対応 IDE（IntelliJ IDEA、Eclipse、または VS Code）、有効な Aspose OCR for Java ライセンス（評価用の無料トライアルで可）。

---

![Flowchart showing how to get OCR text from an image using Aspose OCR Java](https://example.com/ocr-flowchart.png "Get OCR text flow diagram")

## ステップ 1 – Aspose OCR 依存関係の追加 (Load Image OCR)

まず、Maven に Aspose OCR ライブラリを取得させます。`pom.xml` を開き、`<dependencies>` 内に以下の `<dependency>` ブロックを挿入してください。

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro tip**: Gradle を使用している場合は、同等の記述は `implementation 'com.aspose:aspose-ocr:23.9'` です。依存関係を追加するだけで、プロジェクトに **load image OCR** 機能を最も手軽に組み込めます。

## ステップ 2 – OCR エンジンを作成し画像をロード

次に、`OcrEngine` インスタンスを作成し、画像ファイルを指し示し、認識させる言語を指定する小さな Java クラスを書きます。言語は ISO‑639‑2 コードで識別されます（例: タミル語は `"tam"`）。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### なぜ言語を明示的に設定するのか？

言語を指定すると誤認識が減り、認識速度が向上します。多言語 PDF の場合は言語コードの配列をループさせるか、便利な自動検出を有効にできます。

## ステップ 3 – OCR プロセスを実行し **OCRテキストを取得**

エンジンの設定が完了したら、次の行で実際に認識が行われます。結果オブジェクトには抽出された文字列と追加メタデータが含まれます。

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

`LanguageExample` を実行すると、以下のような出力が得られるはずです。

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

`setAutoDetectLanguage(true)` を使用した場合、エンジンは言語を自動的に推測します。未知の文書を扱う際に便利です。

## ステップ 4 – 一般的なエッジケースの処理 (Extract Text Image Variations)

### 低解像度画像への対処

300 dpi 未満では OCR の精度が急激に低下します。元画像が低解像度の場合は、まずアップサンプリングを検討してください。

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### 背景ノイズの除去

スキャンしたフォームに小さな点があるとエンジンが混乱することがあります。前処理を有効にすると改善できます。

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### 特定領域からのテキスト抽出

特定の矩形領域（例: テーブルセル）だけのテキストが必要な場合は、`recognize()` を呼び出す前に `Rectangle` を設定します。

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

これらの調整により、**java OCR example** は本番環境でも十分に頑健になります。

## ステップ 5 – 出力の検証 (期待される結果は？)

正常に実行されると、画像のプレーンテキスト版がコンソールに出力されます。多言語画像の場合、混在したスクリプトが表示されることがあります。

```
Hello World
こんにちは世界
مرحبا بالعالم
```

出力が空だったり文字化けしている場合は、次を再確認してください。

1. `setImage` のファイルパスが正しいか（正しいかどうか）。  
2. 言語コードが画像内のスクリプトと一致しているか。  
3. 画像の品質（コントラスト、DPI）が十分か。

## 完全動作例 (コピー＆ペースト可能)

以下に、コンパイルして実行できる全ファイルを示します。`YOUR_DIRECTORY/multilingual.png` を実際のテスト画像パスに置き換えてください。

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

コンパイルと実行:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

コンソールに抽出された内容が表示されるはずです。

---

## 結論

今回は Aspose OCR for Java を使用して画像から **OCRテキストを取得** する方法を示しました。この **java OCR example** に従えば、**extract text image** データの取得、**load image OCR** の実装、さらには多言語やノイズが多い入力に対するエンジンの微調整まで行えます。  

ここからは次のような活用が考えられます。

- OCR ステップをより大きなワークフローに組み込み（例: テキストをデータベースに保存）。  
- 翻訳 API と組み合わせて、多言語スキャンを単一言語に変換。  
- PDF 変換やバーコード検出など、他の Aspose OCR 機能を試す。

ぜひ試してみて、いくつかの設定を変えてみてください。設定を調整し続けることで、出力が完璧になるはずです。コーディングを楽しんで、OCR が常にクリアに動作しますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}