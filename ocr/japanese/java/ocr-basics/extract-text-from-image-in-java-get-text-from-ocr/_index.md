---
category: general
date: 2026-05-25
description: JavaでOCRを使用して画像からテキストを抽出する。OCR用に画像を読み込む方法、写真からテキストを認識する方法、シンプルなコード例でOCRからテキストを取得する方法を学びましょう。
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: ja
og_description: Javaで画像からテキストを抽出するステップバイステップガイド。OCR用に画像を読み込む方法、写真からテキストを認識する方法、そしてOCRで効率的にテキストを取得する方法を学びましょう。
og_title: Javaで画像からテキストを抽出 – OCRでテキストを取得
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Javaで画像からテキストを抽出 – OCRでテキストを取得
url: /ja/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像からテキストを抽出 – OCRからテキストを取得

画像からテキストを**抽出**したいと思ったことはありませんか？どのJavaライブラリを選べば良いか分からないこともあるでしょう。領収書をデジタル化したり、製品写真からシリアル番号を取得したり、単に楽しいサイドプロジェクトで遊んだりする場合でも、画像を編集可能なテキストに変換するのは一般的なハードルです。

このチュートリアルでは、**load image for OCR** の方法、エンジンの設定、そして最終的に**recognize text from photo** する完全な実行可能サンプルを順に解説します。数行のコードだけで**get text from OCR** が可能です。曖昧な参照はありません—必要なものはすべてここにあります。

## 学べること

* Javaで軽量なOCRエンジンをセットアップする方法。  
* **load image for OCR** の正確な手順と、さまざまなファイルパスの扱い方。  
* 英語以外の**extract text from image** を行う際に、言語設定が重要になる理由。  
* 結果を安全に出力する方法と、エンジンが何も返さなかったときの対処法。  
* 最も一般的な落とし穴を回避するためのプロのコツ。

本ガイドの最後までに、ウクライナ語文字を含むJPEG（またはPNG）を読み取り、認識した文字列をコンソールに出力する自己完結型プログラムが手に入ります。言語や画像は自由に入れ替えて構いません—すべてがモジュール化されています。

---

![Java OCRエンジンを使用した画像からテキスト抽出プロセスのフローダイアグラム](/images/extract-text-from-image-java.png)

*Alt text: Javaでの画像からテキスト抽出プロセスのフローダイアグラム*

## 前提条件

* **Java Development Kit (JDK) 11+** – コードはモダンなモジュールシステムを使用していますが、古いバージョンでも軽微な調整で動作します。  
* **Maven または Gradle** – OCRライブラリを取得するために使用します（ここでは軽量で開発者向けに無料の **Asprise OCR** を使用します）。  
* プログラムが読み取れる場所に配置したサンプル画像ファイル（例: `ukrainian_sign.jpg`）。  
* Javaの `main` メソッドと例外処理に関する基本的な知識。

これらが揃っていればすぐに始められます。まだの場合は、Oracle または AdoptOpenJDK から JDK を入手し、シンプルな Maven プロジェクトをセットアップしてください—特別なことは必要ありません。

---

## ステップ 1: OCR 依存関係を追加

まず、ビルドツールに OCR エンジンを取得させます。Maven の場合は、`pom.xml` に以下を追加してください：

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Gradle を使用する場合は、同等の記述は次の通りです：

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

これらの座標は、`OcrEngine`、`OcrLanguage`、および使用するヘルパークラスを含むコンパクトな JAR を取得します。基本的なラテン文字とキリル文字のスクリプトには、追加のネイティブバイナリは不要です。

---

## ステップ 2: **Extract Text from Image** 用の Java クラスを作成

実際のプログラムを書きます。以下を `src/main/java/com/example/ocr/` 配下に `ExtractTextDemo.java` として保存してください。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### なぜこの構成が機能するのか

* **Separate numbered blocks** はフローを追いやすくし、特に **load image for OCR** や **recognize text from photo** の位置を探す際に便利です。  
* 画像の読み込みと認識を囲む `try/catch` により、プログラムが優雅に失敗します—ファイルパスが間違っている場合や OCR エンジンが言語データを見つけられない場合に有用です。  
* 言語設定を早めに行う（ステップ 2）ことで、英語以外のスクリプトの精度が大幅に向上します。後で他の言語の **java image to text** が必要になった場合は、`OcrLanguage.UKRAINIAN` を `OcrLanguage.ENGLISH`、`FRENCH` などに置き換えるだけです。

---

## ステップ 3: プログラムのビルドと実行

プロジェクトのルートから以下を実行します：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Gradle を使用している場合は：

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

`ukrainian_sign.jpg` にテキスト *«Ласкаво просимо»*（ウクライナ語で「ようこそ」）が含まれていると仮定すると、次のような出力が得られるはずです：

```
=== OCR Result ===
Ласкаво просимо
```

この出力は、**extract text from image** と **get text from OCR** を単一の実行で成功させたことを確認します。

---

## ステップ 4: ワークフローの調整 – 実際のプロジェクトで **Java Image to Text** を行う

デモは最小限ですが、実際のアプリケーションではもう少し手が必要になることが多いです：

| シナリオ | 調整内容 | 理由 |
|----------|----------------|--------|
| **バッチ処理** | `List<Path>` をループし、各結果をデータベースに保存する。 | 数百枚の写真がある場合の手作業を削減する。 |
| **異なる画像フォーマット** | `ImageIO.read(new File(path))` で前処理し、`BufferedImage` を `ocrEngine.getImage().loadFromBufferedImage(bufImg)` に渡す。 | PNG、BMP、または変換後の PDF も処理できる。 |
| **パフォーマンス調整** | 若干精度が低下しても構わない場合は `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` を呼び出す。 | 低スペックハードウェアでの認識速度を向上させる。 |
| **ポストプロセッシング** | 空白をトリムし、一般的な OCR 誤認識（`0` → `O`、`1` → `I`）を置換する。 | 下流データの品質を向上させる。 |

これらのバリエーションは、コアコンセプトである **recognize text from photo** を維持しつつ、実運用のワークロードに柔軟性を提供します。

---

## よくある落とし穴とプロのコツ

1. 言語設定の誤り – ステップ 2 を忘れると、エンジンはデフォルトで英語になり、キリル文字が意味不明な文字列になります。言語コードは必ず再確認してください。  
2. 画像品質が重要 – 低解像度やぼやけた写真は精度を低下させます。必要に応じてコントラスト強調や二値化で前処理してください。  
3. ファイルパスの注意点 – Windows ではバックスラッシュをエスケープする必要があります（`C:\\images\\file.jpg`）。`java.nio.file` の `Path.of(...)` を使用すればこの問題を回避できます。  
4. メモリリーク – `OcrEngine` はネイティブリソースを保持します。特に長時間稼働するサービスでは、使用後に `ocrEngine.dispose()` を呼び出してください。  
5. スレッド安全性 – エンジンはデフォルトでスレッドセーフではありません。スレッドごとに別インスタンスを作成するか、アクセスを同期してください。

---

## 完全動作例（オールインワン）

以下は、任意の IDE にコピー＆ペーストできる単一ファイルです。`dispose()` 呼び出しと、コードを少しすっきりさせる小さなヘルパーメソッドが含まれています。

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

このプログラムを実行すると、先ほど示したのと同じコンソール出力が得られます。`OcrLanguage.UKRAINIAN` を `OcrLanguage.ENGLISH` や他のサポートされている言語に置き換えて、エンジンの挙動を確認しても構いません。

---

## 結論

Java を使用して **extract text from image** するために必要なすべての手順を解説しました：OCR 依存関係の追加から **load image for OCR** まで、 

## 関連チュートリアル

- [Aspose OCR を使用したテキスト画像認識 – 完全な Java OCR チュートリアル](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR を使用した言語別画像テキスト OCR の方法](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR BufferedImage を使用した Java での画像からテキストへの変換](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}