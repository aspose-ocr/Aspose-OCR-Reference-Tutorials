---
category: general
date: 2026-06-16
description: Java OCR を使用して画像からテキストを認識します。OCR 用に画像を読み込む方法、画像内の言語を検出する方法、そして数ステップで自動言語検出を有効にする方法を学びましょう。
draft: false
keywords:
- recognize text from image
- load image for OCR
- detect languages in image
- enable auto language detection
language: ja
og_description: 画像からテキストを素早く認識します。このチュートリアルでは、OCR用に画像を読み込む方法、画像内の言語を検出する方法、そしてJavaで自動言語検出を有効にする方法を示します。
og_title: Java OCRで画像からテキストを認識する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Java OCR. Learn how to load image for
    OCR, detect languages in image, and enable auto language detection in a few steps.
  headline: recognize text from image with Java OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Image Processing
- Multilingual OCR
title: Java OCRで画像からテキストを認識する – 完全ガイド
url: /ja/java/ocr-operations/recognize-text-from-image-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識する Java OCR – 完全ガイド

画像から **テキストを認識** したいことはありますか？しかし、どの Java API が混在言語の画像に対応できるか分からない…という方は多いです。開発者は、複数言語が混在したスキャン、レシート、看板など、単一言語設定では対応できないケースに頻繁に直面しています。

このチュートリアルでは、画像を OCR 用に読み込む方法、自動言語検出を有効にする方法、そして抽出されたテキストを結果から取得する手順を順を追って解説します。最後まで実行すれば、**画像内の言語を検出** し、認識された内容を出力する Java プログラムがすぐに動作するようになります—追加設定は不要です。

> **得られるもの:** 完全に自己完結した Java クラス、ステップバイステップの解説、低解像度スキャンや未対応スクリプトといったエッジケースへの対処法。

## 前提条件

- Java 8 以上がインストール済み（コードは JDK 11 でもコンパイル可能）。  
- 自動言語検出に対応した最新の OCR ライブラリ—ここでは **Aspose.OCR for Java** を使用しますが、同様の設定を提供するライブラリであればどれでも構いません。  
- 複数言語が混在した画像ファイル（`mixed_languages.png`）。  
- 依存関係管理に Maven または Gradle の基本的な知識（Maven のスニペットを示します）。

これらが初めてでも心配はいりません。以下の手順には正確な Maven 座標と最小限の `pom.xml` を記載しているので、コピー＆ペーストしてすぐに実行できます。

## プロジェクトのセットアップ

新規 Maven プロジェクトを作成するか、既存プロジェクトに OCR 依存関係を追加してください。

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```

`mvn clean compile` を実行してライブラリを取得します。これでコードを書く準備が整いました。

## 手順 1: 必要なクラスをインポート

まずは使用するクラスをインポートします。OCR エンジン、画像処理ユーティリティ、結果コンテナなどが対象です。

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;
```

> **プロのコツ:** インポートは整理しておきましょう—IDE のショートカット（IntelliJ の `Ctrl+Shift+O` など）で自動整列できます。

## 手順 2: OCR エンジンのインスタンスを作成

エンジンは処理の中心です。インスタンス化することで、言語検出などの設定にアクセスできるようになります。

```java
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

エンジン生成と画像読み込みを分ける理由は何でしょうか？画像ごとにエンジンを再生成すると、重いリソースの初期化が繰り返されます。エンジンを再利用すれば、バッチ処理時のパフォーマンスが向上します。

## 手順 3: OCR 用に画像を読み込む

いよいよ **画像を OCR 用に読み込み** ます。`ImageStream.fromFile` メソッドはファイルをストリームに変換し、エンジンが消費できる形にします。

```java
// Step 3: Load the image that contains mixed languages
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed_languages.png"));
```

`YOUR_DIRECTORY` をテスト画像が置かれている絶対パスまたは相対パスに置き換えてください。パスが間違っていると `FileNotFoundException` がスローされ、初心者がよく遭遇する落とし穴です。

> **画像のコツ:** ベストな結果を得るには PNG または TIFF 形式を使用しましょう。JPEG の圧縮はアーティファクトを生み、認識精度を下げることがあります。

## 手順 4: 自動言語検出を有効化

本チュートリアルの核心です: **自動言語検出を有効化** して、エンジンに画像内の言語を自動で判別させます。

```java
// Step 4: Turn on automatic language detection
engine.getRecognitionSettings().setAutoDetectLanguage(true);
```

このフラグが `true` の場合、OCR エンジンは画像をスキャンし、存在する言語を特定して内部で該当する言語パックをロードします。このステップを省くと、エンジンはデフォルトの主要言語（通常は英語）で動作し、他のスクリプトのテキストは認識されません。

## 手順 5: OCR 認識を実行

設定が完了したら、**画像からテキストを認識** し、検出された言語リストと抽出テキストの両方を取得します。

```java
// Step 5: Run the recognition process
OcrResult result = engine.recognize();

// Display detected languages and the extracted text
System.out.println("Detected languages: " + result.getDetectedLanguages());
System.out.println("Extracted text:\n" + result.getText());
```

`getDetectedLanguages()` メソッドは `[en, fr, de]` のようなコレクションを返し、エンジンが正しく多言語コンテンツを判別したかを確認できます。

## 完全動作サンプル

以下が実行可能な完全な Java クラスです。`src/main/java/com/example/OcrDemo.java` に貼り付け、画像パスを調整したうえで `mvn exec:java -Dexec.mainClass="com.example.OcrDemo"` を実行してください。

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ImageStream;
import com.aspose.ocr.OcrResult;

/**
 * Demo program that recognises text from an image,
 * automatically detects languages present, and prints the result.
 */
public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load image for OCR – change the path as needed
        String imagePath = "YOUR_DIRECTORY/mixed_languages.png";
        engine.setImage(ImageStream.fromFile(imagePath));

        // 3️⃣ Enable auto language detection so we can detect languages in image
        engine.getRecognitionSettings().setAutoDetectLanguage(true);

        // 4️⃣ Perform the recognition
        OcrResult result = engine.recognize();

        // 5️⃣ Output the findings
        System.out.println("Detected languages: " + result.getDetectedLanguages());
        System.out.println("Extracted text:\n" + result.getText());
    }
}
```

**期待される出力**（実際の言語は画像次第です）:

```
Detected languages: [en, es, fr]
Extracted text:
Hello World!
¡Hola Mundo!
Bonjour le monde!
```

画像に英語だけが含まれている場合、リストは `[en]` となり、テキストも単一言語で出力されます。

## よくあるエッジケースの対処法

| 状況 | なぜ重要か | 簡単な対策 |
|-----------|----------------|-----------|
| 低解像度画像 | 文字が誤認識され、出力が文字化けしやすい。 | DPI を上げる、二値化処理を施すなど、事前に画像を前処理してから OCR に渡す。 |
| 未対応スクリプト（例: ベンガル文字） | 自動検出が未知のスクリプトをスキップし、その部分のテキストが空になる。 | ライブラリが対応していれば言語パックを手動で追加するか、別の OCR エンジンに切り替える。 |
| 大量バッチ処理 | エンジンを毎回生成するとオーバーヘッドが増大。 | `OcrEngine` インスタンスを1つだけ作成し、画像ごとに `setImage` を呼び出すだけにする。 |
| メモリ制約環境 | 高解像度画像を多数読み込むとヒープが枯渇する可能性。 | `ImageStream.fromFile` のストリーミングオプションを利用するか、リアルタイムで画像をダウンサンプルする。 |

## プロのコツ & ベストプラクティス

- **言語パックをキャッシュ**: 一部の OCR ライブラリは言語データの事前ロードをサポートしています。事前にキャッシュしておくと多数ファイル処理時のレイテンシが削減されます。  
- **検出言語をログに残す**: 言語リストを抽出テキストと共に保存すれば、後続の分析（例: 言語別感情分析）に活用できます。  
- **出力を検証**: 期待する文字種に対する正規表現チェックを入れるだけで、パイプライン内で OCR 失敗を早期に検知できます。  

## 次のステップ

**画像からテキストを認識** し、自動言語検出ができるようになったので、以下のように機能を拡張してみましょう。

- **PDF へエクスポート**: iText や Apache PDFBox を使って抽出テキストを検索可能な PDF に変換。  
- **データベース統合**: 画像パス、検出言語、OCR テキストを保存し、後から検索できるようにする。  
- **GUI の追加**: 軽量な Swing または JavaFX のフロントエンドを作り、非技術者でも画像をドロップして即座に結果を得られるようにする。  

これらのトピックはすべて、**load image for OCR**、**detect languages in image**、**enable auto language detection** という二次キーワードと密接に関連しており、同じ基盤の上に構築できます。

---

*Happy coding! If you hit a snag, drop a comment below and we’ll troubleshoot together.*

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を踏まえてさらに深く学べる関連トピックです。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や別実装アプローチの検証に役立ちます。

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}