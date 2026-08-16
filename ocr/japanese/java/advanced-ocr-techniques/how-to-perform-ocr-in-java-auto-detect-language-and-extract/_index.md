---
category: general
date: 2026-04-26
description: Aspose OCR を使用して OCR を実行し、画像からテキストを抽出する方法を学びます。このガイドでは、OCR 用に画像を読み込む方法、自動言語検出を有効にする方法、そして言語を自動検出する
  OCR の使い方を示します。
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: ja
og_description: Aspose OCR を使用した Java での OCR の実行方法。OCR 用に画像を読み込む方法、自動言語検出を有効にする方法、画像からテキストを抽出する方法を学びます。
og_title: JavaでOCRを実行する方法 – 自動言語検出
tags:
- OCR
- Java
- Aspose
title: JavaでOCRを実行する方法 – 言語を自動検出してテキストを抽出
url: /ja/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRを実行する方法 – 自動言語検出とテキスト抽出

英語、スペイン語、そして場合によっては日本語文字が混在した写真で **how to perform OCR** が必要になったことはありませんか？ あなたは一人ではありません—開発者は、スキャンした文書、レシート、または多言語のサインからテキストを読み取る必要があるときに、常にこの壁にぶつかります。  

良いニュースです。数行のJavaコードとAspose OCRを使えば、**load image for OCR** を行い、**enable automatic language detection** を有効にし、言語を推測することなくすぐに **extract text from image** ができます。このチュートリアルでは、完全な実行可能サンプルを順に解説し、各ステップの重要性を説明し、**auto detect language OCR** の結果を検証する方法を示します。

> **得られるもの**  
> * 混合言語のPNGを読み取る動作するJavaプログラム。  
> * 言語検出を簡単にする主要なOCR設定に関する知識。  
> * 欠損ファイル、未対応言語、パフォーマンス調整の取り扱いに関するヒント。  

---

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 (or newer) | Aspose OCRは最新のJVMを対象としており、古いバージョンではAPI機能が欠落する可能性があります。 |
| Aspose OCR for Java library (latest version) | `OcrEngine` と language‑auto‑detect 機能を提供します。 |
| An image file (`mixed_lang.png`) containing text in at least two languages | **auto detect language OCR** 機能を示します。 |
| A Java IDE or simple command‑line setup | サンプルコードをコンパイルおよび実行するためです。 |

まだAspose OCR JARを取得していない場合は、公式Mavenリポジトリから取得してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

---

## 手順 1: OCRエンジンインスタンスの作成 – How to Perform OCR

**perform OCR** を実行したいときに最初に行うことはエンジンをインスタンス化することです。`OcrEngine` を、ビットマップを解析しピクセルを文字に変換する脳と考えてください。

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** 多くの画像で同じ `OcrEngine` を再利用すると、エンジンが内部で言語モデルをキャッシュするため、パフォーマンスが向上します。

---

## 手順 2: 自動言語検出の有効化 – Enable Automatic Language Detection

デフォルトではAspose OCRは英語を想定しています。多言語の画像では、テキストブロックごとに言語を「推測」させる必要があります。これが **enable automatic language detection** フラグの役割です。

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

エンジンは画像の各セグメントを検査し、最も可能性の高い言語を選択して適切な文字セットを適用します。これが無いと、英語以外の部分で文字化けした出力になります。

---

## 手順 3: OCR用画像の読み込み – Load Image for OCR

ここで実際に **load image for OCR** を行います。パスは絶対でも相対でも構いませんが、ファイルが存在することを確認してください。存在しない場合は `FileNotFoundException` が発生します。

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Edge case:** 画像がMavenプロジェクトのresourcesフォルダーにある場合は、ハードコーディングされたパスを避けるために `getClass().getResource("/mixed_lang.png")` を使用してください。

---

## 手順 4: 認識を実行し画像からテキストを抽出 – Extract Text from Image

エンジンの設定と画像の読み込みが完了したら、実際に **perform OCR** を行う時です。`recognize()` 呼び出しが重い処理を行い、`getText()` がシンプルな `String` を返します。

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

この時点でライブラリは各ブロックに対してすでに **auto detect language OCR** を実行しているため、`recognizedText` 変数にはクリーンで言語情報を考慮した文字起こしが格納されています。

---

## 手順 5: 結果の表示 – Verify Auto‑Detect Language OCR Output

最後に、結果をコンソールに出力します。実際のアプリでは、ファイルやデータベースに書き込んだり、翻訳サービスに渡したりすることもあります。

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### 期待される出力

`mixed_lang.png` に “Hello”（英語） と “¡Hola!”（スペイン語）が含まれていると仮定すると、以下のような出力が得られます。

```
Auto‑detected language output:
Hello
¡Hola!
```

設定で `setShowLanguage(true)` を有効にすると、エンジンは各行の先頭に言語コードを付加し、例として `[en] Hello` や `[es] ¡Hola!` のように表示されます。

---

## よくある質問と落とし穴

### 画像パスが間違っている場合は？

エンジンは `FileNotFoundException` をスローします。呼び出しを try‑catch ブロックで囲み、ユーザーに分かりやすいメッセージを提供してください：

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### 言語を限定して検出速度を上げられますか？

はい。`AUTO_DETECT` の代わりにリストで言語を指定できます。

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

これにより検索範囲が縮小し、大量バッチでのパフォーマンスが向上します。

### **auto detect language OCR** は手書きテキストをどのように扱いますか？

Aspose OCRは印刷テキストに焦点を当てています。手書き文字は通常別のエンジン（例: Aspose OCR for Handwriting）が必要です。検出を強制すると結果は芳しくありません。

---

## 完全動作例（コピー＆ペースト可能）

以下はコンパイルと実行が可能な完全なプログラムです。`YOUR_DIRECTORY` を `mixed_lang.png` が格納されている実際のフォルダーに置き換えてください。

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

以下のコマンドで実行します：

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

先ほど説明したコンソール出力が表示されるはずです。

---

## ソリューションの拡張

**how to perform OCR** が分かったので、次のステップを検討してください：

* **Batch processing** – 画像フォルダーをループし、同じ `OcrEngine` インスタンスを再利用して高速化します。  
* **Saving results** – 抽出したテキストを `.txt` ファイルに書き込むか、データベースに保存します。  
* **Post‑processing** – 正規表現を使用して改行を整理したり、不要な文字を除去したりします。  
* **Integration** – 出力を翻訳API（Google Translate、Azure Translator）に渡して多言語アプリケーションに活用します。  

これらの拡張はすべて、画像の読み込み、言語検出の有効化、テキスト抽出という基本概念に依存しています。

---

## 結論

ここでは、Javaで **how to perform OCR** を実行しながら自動的に言語を検出する完全なエンドツーエンドの例を示しました。エンジンの作成、自動言語検出の有効化、画像の読み込み、認識の実行、結果の表示という5つの手順に従うことで、複数の文字体系を含む **extract text from image** ファイルを確実に取得できます。  

スムーズな **auto detect language OCR** の鍵は、エンジンにブロックごとに言語を判断させることです。単一言語を強制すると文字化けしやすくなります。画像品質や言語リスト、パフォーマンス調整を試して、特定のユースケースに合わせて最適化してください。  

ここで取り上げていないシナリオがありますか？ コメントを残してください。一緒にトラブルシューティングしましょう。コーディングを楽しんで！  

![how to perform OCR example](/images/ocr-demo.png "Screenshot showing how to perform OCR with Aspose OCR in Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}