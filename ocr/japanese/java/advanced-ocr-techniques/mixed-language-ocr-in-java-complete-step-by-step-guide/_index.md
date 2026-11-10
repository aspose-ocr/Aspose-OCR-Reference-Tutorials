---
category: general
date: 2026-07-05
description: Java開発者向けの多言語OCRチュートリアル。マルチ言語OCRの例を使って、画像からテキストへのOCR文字取得方法を学び、Javaプロジェクトに活用しましょう。
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: ja
og_description: Javaでの混合言語OCRの解説。今日すぐにコピー＆ペーストできる多言語OCRの例を使って、画像からOCRテキストを取得しましょう。
og_title: Javaでの混合言語OCR – 完全プログラミングウォークスルー
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Javaでの混合言語OCR – 完全ステップバイステップガイド
url: /ja/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java における混合言語 OCR – 完全ステップバイステップガイド

英語とマラヤーラム語が混在した古文書をデジタル化したい、あるいは複数のスクリプトに対応したスキャナーアプリを作りたい…そんなときに **mixed language OCR** が必要になることがありますよね。このチュートリアルでは、**image to text Java** ワークフローを使って、両言語が含まれるビットマップから **OCR テキスト** を取得する方法をステップバイステップで解説します。

動作可能な **java OCR example** を実際に動かしながら、各行の意味を説明し、**multi language OCR** の落とし穴を回避するコツも紹介します。最後には、抽出したテキストをコンソールに出力するプログラムが完成します – 謎のライブラリは一切残りません。

## 必要なもの

作業を始める前に、以下がインストールされていることを確認してください。

* **Java Development Kit (JDK) 17** 以上 – コードはモジュールシステムを使用していますが、JDK 11+ でも動作します。  
* **Maven**（または Gradle） – OCR ライブラリを自動取得するために使用します。  
* 複数言語に対応した OCR エンジン – 本ガイドでは **Aspose.OCR for Java** を使用します。英語とマラヤーラム語が標準でサポートされています。（Tesseract を使う場合はインポート文を差し替えるだけで同様の手順です）  
* プロジェクト内の `resources` フォルダーに配置したサンプル画像 `mixed_english_malayalam.png`  
* 多少の好奇心 – あとは以下でカバーします。

> **Pro tip:** Windows 環境の場合、コマンドプロンプトで `mvn -v` を実行して Maven が PATH に通っているか確認してください。

## プロジェクトのセットアップ

### 1. Maven プロジェクトを作成

ターミナルで次のコマンドを実行します。

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

これで標準的な `src/main/java` レイアウトを持つ基本的な Java プロジェクトが作成されます。

### 2. Aspose.OCR 依存関係を追加

生成された `pom.xml` を開き、`<dependencies>` ブロック内に以下を挿入します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

`mvn clean install` を実行して JAR をダウンロードします。Maven がすべてを処理してくれるので、ネイティブ DLL を自分で探す必要はありません。

## 混合言語 OCR コードの作成

`src/main/java/com/example/ocr/` 配下に新しいクラス `MixedLanguageOcrDemo.java` を作成し、以下のコードを貼り付けます。各行にコメントを入れているので、**なぜ** そのように書くのかがすぐに分かります。

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### 動作概要

| ステップ | 何が起こるか | なぜ重要か |
|------|--------------|----------------|
| **1** | `OcrEngine` オブジェクトを作成。 | エンジンがすべての OCR 機能をカプセル化しており、これがなければメソッドを呼び出せません。 |
| **2** | `setRecognitionLanguage` に `ENGLISH` と `MALAYALAM` を渡す。 | 両言語を指定することで **multi language OCR** が有効になり、エンジンがリアルタイムでスクリプトの切り替えを検出します。 |
| **3** | 画像パスを定義。 | パスを相対パスにしておくことで、絶対パスをハードコーディングせずに **java OCR example** を再利用可能にします。 |
| **4** | `recognizeImage` がビットマップを処理。 | ここで本格的な処理が行われ、エンジンがピクセルを解析しニューラルネットを走らせて `RecognitionResult` を返します。 |
| **5** | `getText()` がプレーン文字列を抽出。 | これが **get OCR text** を取得し、データベース保存などの後続処理に渡すために必要なメソッドです。 |
| **6** | `System.out.println` が文字列を出力。 | 即座に視覚的フィードバックが得られ、**image to text Java** パイプラインが正しく機能しているか確認できます。 |

> **Note:** `java.lang.UnsatisfiedLinkError` が発生した場合は、ネイティブライブラリフォルダーが `java.library.path` に含まれているか確認してください。Aspose は Windows、macOS、Linux 用のバイナリを同梱しています。

## デモの実行

Maven でコンパイル＆実行します。

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

期待される出力例は次のとおりです。

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

1 行目が英語、2 行目がマラヤーラム語となり、**mixed language OCR** が成功したことが確認できます。

## よくあるエッジケースの対処

### 低品質画像

画像がぼやけていたりコントラストが低いと OCR 精度は大幅に低下します。以下の対策を検討してください。

* **前処理** に OpenCV などのライブラリを使用し、グレースケール変換、適応的二値化、300 DPI 以上への拡大を行う。  
* `ocrEngine.setAutoSkewCorrection(true)` を有効にして、回転したテキストを自動で補正させる。  
* 必要に応じて `ocrEngine.setConfidenceThreshold(0.6f)` を上げ、信頼度の高い結果だけを取得する。

### 未サポート言語

Aspose は現在 70 以上のスクリプトをサポートしていますが、マラヤーラム語は言語パックが必要な場合があります。`RecognitionLanguage.MALAYALAM` が例外を投げたら、Aspose ポータルから追加言語データをダウンロードし、`resources/ocr-data` に配置してください。

### 大容量 PDF

マルチページ PDF を処理する場合は、各ページを別々の画像として渡すか、`OcrEngine.recognizePdf` を使用します。`setRecognitionLanguage` の呼び出しはすべてのページに共通なので、ドキュメント全体でシームレスな **multi language OCR** 体験が得られます。

## 例の拡張：コンソールから Web サービスへ

この機能を REST エンドポイントとして公開したい場合は、Spring Boot を追加します。

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

これでクライアントは画像を `POST` し、**get OCR text** の結果をプレーン JSON で受け取れます。この小さな拡張により、同じ **java OCR example** が単一ファイルのデモから本番レベルのサービスへとスケールします。

## 完全なソースツリーのスナップショット

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

記事内にプロジェクト全体の構成を示すことで、読者は IDE にコピーしてすぐに実行できます。

![mixed language OCR example output](https://example.com/assets/mixed-ocr-output.png "mixed language OCR example output")

*画像の代替テキスト:* mixed language OCR example output – 同一画像から抽出された英語とマラヤーラム語のテキストを示す。

## まとめと次のステップ

Java における **mixed language OCR** パイプラインを最初から最後まで解説しました。

* Maven プロジェクトを作成し、Aspose OCR 依存関係を追加。  
* 英語 + マラヤーラム語用にエンジンを設定し、認識を実行して **OCR テキスト** を取得。  
* 画像品質、言語パック、コンソールアプリから Web サービスへの拡張方法を紹介。

さらに踏み込むなら、以下のアイデアを試してみてください。

* Aspose を **Tesseract** に置き換えて、オープンソースエンジンでの **multi language OCR** の挙動を比較。  
* ヒンディー語やタミル語など、追加の言語を `setRecognitionLanguage` に加えて実験。  
* 抽出結果を検索インデックス（例: Elasticsearch）に統合し、スキャンしたアーカイブ全体で **image to text Java** による検索を実現。

何かうまくいかない点や独自の工夫があればコメントで教えてください。コーディングを楽しみながら、スキャンが常にクリアになることを願っています！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれているので、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}