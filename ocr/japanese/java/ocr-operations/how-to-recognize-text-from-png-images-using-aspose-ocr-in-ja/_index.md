---
category: general
date: 2026-09-25
description: JavaでAspose OCRを使用してPNG画像からテキストを認識する – 画像からテキストを抽出し、画像をテキストに変換するステップバイステップガイド
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from png
- extract text from image
- convert image to text
- load image for ocr
- read english text image
language: ja
lastmod: 2026-09-25
og_description: JavaでAspose OCRを使用してPNG画像からテキストを認識します。このガイドに従って画像からテキストを抽出し、画像をテキストに変換し、英語のテキスト画像を読み取ります。
og_image_alt: Screenshot showing recognized text output after processing a PNG with
  Aspose OCR
og_title: JavaでPNG画像からテキストを認識する – 完全なAspose OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  headline: How to recognize text from PNG images using Aspose OCR in Java
  type: TechArticle
- description: recognize text from PNG images with Aspose OCR in Java – a step‑by‑step
    guide to extract text from image and convert image to text.
  name: How to recognize text from PNG images using Aspose OCR in Java
  steps:
  - name: Why each line matters
    text: '| Line | Purpose | How it helps you **extract text from image** | |------|---------|---------------------------------------------|
      | `new OcrEngine()` | Instantiates the OCR processor. | Provides the engine
      that performs character analysis. | | `engine.setImage(...)` | Loads the PNG
      file into memory'
  - name: 4.1 Missing or corrupt PNG file
    text: 'If the file path is wrong, `ImageStream.fromFile` throws an `IOException`.
      Wrap the loading code in a `try‑catch` block to present a friendly message:'
  - name: 4.2 Non‑English languages
    text: 'Aspose OCR supports many languages. To recognize French, for example, replace
      the language line with:'
  - name: 4.3 Low‑resolution PNGs
    text: OCR accuracy drops when the source image is below 300 dpi. If you notice
      poor results, consider preprocessing the PNG (e.g., scaling up with `java.awt.Image`)
      before passing it to the engine.
  type: HowTo
tags:
- Aspose OCR
- Java
- Image processing
title: JavaでAspose OCRを使用してPNG画像からテキストを認識する方法
url: /ja/java/ocr-operations/how-to-recognize-text-from-png-images-using-aspose-ocr-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で Aspose OCR を使用して PNG 画像からテキストを認識する方法

Java アプリケーションで **PNG からテキストを認識** したい場合、このチュートリアルで手順をすべて解説します。ガイドの最後まで読むと、**画像からテキストを抽出** し、画像をプレーンテキストに変換して、コンソールに結果を表示できるようになります。

Aspose OCR ライブラリを使用します。このライブラリは画像の読み込み、言語の選択、認識文字の取得をシンプルな API で提供します。手順には **OCR 用に画像をロード** する安全な方法や、エンジンが失敗したときの対処法も含まれます。外部サービスは不要で、Java 8 以降のランタイムで動作します。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* Java 8 以上がインストール済み（JDK 8‑21 すべて対応）
* 依存関係管理に Maven または Gradle（ここでは Maven のスニペットを示します）
* `sample.png` という名前の画像ファイルを、コードから参照できるディレクトリに配置
* Java の構文と例外処理に関する基本的な知識

## 手順 1: Aspose OCR をプロジェクトに追加

Aspose OCR は Maven アーティファクトとして配布されています。`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version available -->
</dependency>
```

Gradle を使う場合は、同等の記述は次の通りです。

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

ライブラリを追加すると、`OcrEngine`、`ImageStream`、言語列挙型など、**画像をテキストに変換** するために必要なクラスが利用可能になります。

## 手順 2: Java クラスを作成し、必要なパッケージをインポート

`SampleDemo` という名前の新しいクラスを作成します。OCR クラスと、使用する標準 Java ユーティリティをインポートしてください。

```java
package com.example.ocrdemo;

import com.aspose.ocr.*;
import java.io.IOException;
```

`import com.aspose.ocr.*;` 行で OCR 操作に必要なすべてが取り込まれ、`java.io.IOException` はファイル関連エラーの処理に役立ちます。

## ## Aspose OCR で PNG からテキストを認識する

ソリューションの核心は `main` メソッドにあります。メソッド内の番号付き手順に従って、各部分がどのように機能するかを確認してください。

```java
public class SampleDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image to be processed (load image for OCR)
        // Replace "YOUR_DIRECTORY" with the actual path to your PNG file.
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));

        // Step 3: (Optional) Specify the language for recognition.
        // The default language is English, but we set it explicitly to
        // demonstrate how to read english text image.
        engine.setLanguage(OcrLanguage.English);

        // Step 4: Execute the OCR process
        if (engine.process()) {
            // Step 5: Retrieve and display the recognized text
            String text = engine.getText();
            System.out.println("Recognized text: " + text);
        } else {
            System.err.println("OCR processing failed.");
        }
    }
}
```

### 各行が重要な理由

| 行 | 目的 | **画像からテキストを抽出** する際の役割 |
|------|---------|---------------------------------------------|
| `new OcrEngine()` | OCR プロセッサをインスタンス化します。 | 文字解析を実行するエンジンを提供します。 |
| `engine.setImage(...)` | PNG ファイルをメモリにロードします。 | これは **OCR 用に画像をロード** するステップで、エンジンが読む対象が無ければ処理できません。 |
| `engine.setLanguage(OcrLanguage.English)` | 使用する言語モデルを指定します。 | **英語テキスト画像を読む** シナリオで正確な認識を保証します。 |
| `engine.process()` | 認識アルゴリズムを実行します。 | **画像をテキストに変換** の核心で、ビットマップを走査して文字列を生成します。 |
| `engine.getText()` | 認識された文字を Java の `String` として返します。 | 最終的なプレーンテキスト結果を取得でき、保存・検索・表示が可能です。 |

## 手順 4: 一般的なエッジケースの処理

OCR フローが適切に書かれていても問題が発生することがあります。以下に実用的なヒントを示します。

### 4.1 PNG ファイルが欠損または破損している場合

ファイルパスが間違っていると `ImageStream.fromFile` が `IOException` をスローします。ロードコードを `try‑catch` で囲み、ユーザーフレンドリーなメッセージを表示しましょう。

```java
try {
    engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
} catch (IOException e) {
    System.err.println("Unable to load image: " + e.getMessage());
    return;
}
```

### 4.2 英語以外の言語

Aspose OCR は多数の言語に対応しています。たとえばフランス語を認識したい場合は、言語設定行を次のように置き換えます。

```java
engine.setLanguage(OcrLanguage.French);
```

中国語、アラビア語などでも同様に設定でき、スクリプトに関係なく **画像からテキストを抽出** できます。

### 4.3 低解像度 PNG

ソース画像が 300 dpi 未満だと OCR の精度が低下します。結果が悪い場合は、エンジンに渡す前に `java.awt.Image` で拡大するなど前処理を検討してください。

## 手順 5: 出力の確認

IDE もしくはコマンドラインからプログラムを実行します。

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.SampleDemo"
```

次のような出力が得られるはずです。

```
Recognized text: Hello, world! This is a sample PNG image.
```

コンソールに `OCR processing failed.` と表示されたら、ファイルパスを再確認し、画像が破損していないか確認してください。

## 本番環境での追加ヒント

* **バッチ処理** – PNG ファイルが格納されたディレクトリをループし、`OcrEngine` インスタンスを再利用してパフォーマンスを向上させます。  
* **メモリ管理** – 大きな画像を処理した後は `engine.dispose()` を呼び出し、ネイティブリソースを解放します。  
* **ロギング** – `System.out` の代わりにロギングフレームワーク（SLF4J、Log4j など）を統合し、スケーラブルなアプリケーションにします。  
* **エラーコード** – `engine.process()` が `false` を返す理由は多数あります。`engine.getErrorCode()` を使って具体的な失敗原因を診断しましょう。

## 結論

これで Java で Aspose OCR を使用して **PNG 画像からテキストを認識** する方法が分かりました。完全なワークフロー（**OCR 用に画像をロード**、必要に応じて **英語テキスト画像を読む** 設定、**処理**、**画像からテキストを抽出**）は、任意の Java プロジェクトに組み込む準備が整いました。ここからは、PDF やスキャン文書、リアルタイムカメラフィード向けに **画像をテキストに変換** する拡張も可能です。

## 次のステップ

* PDF や TIFF 形式向けの **画像をテキストに変換** API を探求する。  
* この OCR フローを Apache Tika と組み合わせ、抽出したテキストを検索エンジンにインデックスする。  
* `OcrLanguage.English` を他の言語列挙子に置き換えて多言語サポートを実験する。  
* ノイズの多い PNG に対する精度向上のため、`engine.setPreprocessOptions` など Aspose OCR の高度な設定を検討する。

コーディングを楽しみながら、画像を検索可能なテキストに変換してください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装を試したりするのに役立ちます。

- [Recognize Text from Image with Aspose OCR – Full Java Guide](/ocr/english/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)
- [recognize text image using Aspose OCR GPU – Java](/ocr/english/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}