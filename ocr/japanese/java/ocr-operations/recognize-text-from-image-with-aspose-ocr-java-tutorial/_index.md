---
category: general
date: 2026-02-17
description: Aspose OCR Java ライブラリを使用して画像からテキストを認識し、OCR 用に画像を読み込む方法を学びます。スペル補正機能付きのステップバイステップガイド。
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: ja
og_description: Aspose OCR Java を使用して画像からテキストを認識します。このチュートリアルでは、OCR 用に画像をロードし、スペル補正を有効にして、クリーンなテキストを出力する方法を示します。
og_title: 画像からテキストを認識する – 完全な Aspose OCR Java ガイド
tags:
- Java
- OCR
- Aspose
title: Aspose OCRで画像からテキストを認識する – Javaチュートリアル
url: /ja/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からのテキスト認識 – Java チュートリアル

画像からテキストを **recognize text from image** したいと思ったことはありませんか？どのライブラリを選べば良いか迷うことも多いですよね。実際のプロジェクトでは、請求書のスキャンや手書きメモのデジタル化、スクリーンショットからのキャプション抽出など、正確な OCR 結果が重要です。  

このガイドでは、OCR 用の画像の読み込み、Aspose OCR の組み込みスペル補正機能の有効化、そして最終的にクリーンアップされたテキストを出力する手順を解説します。最後まで読むと、数行のコードだけで **recognize text from image** ができる、すぐに実行可能な Java プログラムが手に入ります。

## このチュートリアルでカバーする内容

- Aspose OCR ライセンスの適用方法（デモが透かしなしで実行できるように）  
- `OcrEngine` インスタンスの作成と認識言語として English を選択  
- **Load image for OCR** を `OcrInput` で実行し、誤字が含まれる PNG を指定  
- スペル補正機能の有効化、必要に応じてカスタム辞書を指定  
- 認識を実行し、補正結果を出力  

外部サービスや隠し設定ファイルは不要です—純粋な Java と Aspose OCR JAR だけです。

> **Pro tip:** Aspose を初めて使う方は、Aspose のウェブサイトから 30 日間の無料トライアルライセンスを取得し、コードから参照できるフォルダーに `.lic` ファイルを配置してください。

## 前提条件

- Java 8 以上（コードは JDK 11 でもコンパイル可能）  
- クラスパスに Aspose.OCR for Java JAR があること  
- 有効な `Aspose.OCR.lic` ファイル（評価モードでも動作しますが、デモには透かしが入ります）  
- 意図的に綴りミスが含まれるテキストを持つ画像ファイル（`misspelled.png`）—スペル補正機能の動作確認に最適  

すべて揃いましたか？それでは、始めましょう。

## Step 1: Aspose OCR ライセンスの適用

エンジンが本格的な処理を行う前に、ライセンスが適用されていることを知らせる必要があります。そうでないと、出力に「Trial version」のバナーが表示されます。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Why this matters:* ライセンスを適用すると、試用版の透かしが無効になり、フルスペル補正辞書が使用可能になります。この手順を省略すると動作はしますが、出力に “Aspose OCR Demo” のテキストが混ざります。

## Step 2: OCR エンジンの作成と設定

ここでエンジンを起動し、使用する言語を指定します。English が最も一般的ですが、Aspose は数十言語をサポートしています。

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Why we set the language:* 言語モデルは文字セットを決定し、スペル補正の提案に影響します。誤った言語を設定すると、精度が大幅に低下します。

## Step 3: スペル補正の有効化と（オプションで）カスタム辞書の指定

Aspose OCR には組み込みの英語辞書が付属していますが、医療用語や製品コードなど、ドメイン固有の用語がある場合は独自の辞書を提供できます。

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*What the corrector does:* OCR エンジンが辞書にない単語を検出すると、最も近い一致語に置き換えようとします。これにより、デモでは “recieve” が自動的に “receive” に変換されます。

## Step 4: OCR 用画像の読み込み

ここでは **load image for OCR** に直接対応する部分です。`OcrInput` オブジェクトを作成し、PNG ファイルを追加します。

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Why we use `OcrInput`:* ファイル読み込みロジックを抽象化し、後でマルチページ PDF や画像セットを処理する場合に複数ページを追加できるようにします。

## Step 5: 認識を実行し、補正テキストを取得

エンジンが本格的な処理を行います—文字認識、言語モデルの適用、そして最終的なスペル補正です。

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Expected output:* `misspelled.png` に “Ths is a smple test” というフレーズが含まれていると仮定すると、コンソールには次のように出力されます。

```
Corrected text:
This is a simple test
```

誤字（`Ths`、`smple`）が自動的に修正されていることに注目してください。

## 完全な実行可能サンプル

以下にプログラム全体を一つのブロックで示します。コピーして貼り付け、パスを調整し、**Run** を実行してください。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tip:** PNG の代わりに JPEG や BMP を処理したい場合は、ファイル拡張子を変更するだけです—Aspose OCR はすべての一般的なラスタ形式をサポートしています。

## よくある質問とエッジケース

- **What if my image is low‑resolution?**  
  `java.awt.Image` などのライブラリでリスケールし、Aspose に渡す前に DPI を上げます。DPI が高いほどエンジンが扱えるピクセル数が増え、通常は精度が向上します。

- **Can I recognize multiple languages in the same image?**  
  はい。`engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` を呼び出し、必要に応じて `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);` で言語リストを追加できます。

- **My custom dictionary isn’t being used—why?**  
  フォルダーに 1 行 1 単語のプレーンテキストファイルが入っていること、パスが絶対パスまたは作業ディレクトリから正しく相対指定されていることを確認してください。

- **How do I extract confidence scores?**  
  `result.getConfidence()` はページ全体の信頼度を 0 から 1 の float で返します。文字単位の信頼度を取得するには `result.getWordList()` を調べてください。

## 結論

これで、Aspose OCR for Java を使用して **recognize text from image** を行う方法、**load image for OCR** の方法、そしてスペル補正機能を有効にして一般的なタイプミスを修正する方法が分かりました。上記の完全なサンプルは任意の Maven または Gradle プロジェクトにすぐに組み込め、少し調整すればフォルダーのバッチ処理や Web サービスへの組み込み、ドキュメント管理システムへの統合などに拡張できます。

次のステップに進む準備はできましたか？マルチページ PDF を入力したり、業界固有の用語向けにカスタム辞書を試したり、出力を翻訳 API に連結したりしてみてください。可能性は無限に広がりますが、基本パターンは変わりません—ライセンス → エンジン → 言語 → スペル補正 → 入力 → 認識 → 出力。

コーディングを楽しんで、OCR の結果が常に的確でありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}