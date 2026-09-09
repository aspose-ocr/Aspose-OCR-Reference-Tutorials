---
category: general
date: 2026-01-07
description: Javaで画像からテキストを読み取り、画像をテキストに変換する方法を学びましょう。このステップバイステップのJava OCRチュートリアルでは、画像からテキストを認識し、PNGに対してOCRを実行する方法も示しています。
draft: false
keywords:
- read text from image
- convert image to text
- recognize text from picture
- perform ocr on png
- java ocr tutorial
language: ja
og_description: JavaでAspose OCRを使用して画像からテキストを読み取ります。このガイドでは、画像をテキストに変換し、画像からテキストを認識し、PNGでOCRを実行する方法を順を追って説明します。
og_title: Javaで画像からテキストを読み取る – 完全なAspose OCRチュートリアル
tags:
- OCR
- Java
- Aspose
title: Javaで画像からテキストを読み取る – 完全なAspose OCRガイド
url: /ja/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを読み取る Java – 完全 Aspose OCR ガイド

画像から **テキストを読み取る** 必要があって、どこから始めればいいか分からないことはありませんか？開発者はよく「画像をテキストに変換したいけど、どうすればいいの？」と質問します。良いニュースは、Aspose OCR for Java を使えば数行のコードで実現できることです。この **java ocr tutorial** では、PNG ファイルの読み込みからクリーンでスペルチェックされた出力まで、全工程を解説します。

また、異なる画像フォーマットの取り扱いや速度重視のエンジン調整といった「もしも」シナリオもカバーします。最後まで読めば、**画像からテキストを認識** し、**PNG で OCR を実行** し、任意の Java プロジェクトに統合できるようになります。外部サービスは不要、単一の JAR と実行可能なサンプルだけです。

## 前提条件

始める前に以下を用意してください：

- Java 8 以上がインストールされていること（コードは標準の `java.io` と `java.nio` パッケージを使用）。  
- お好みの IDE またはテキストエディタ（IntelliJ IDEA、Eclipse、VS Code など）。  
- Aspose OCR for Java ライブラリ（Aspose のウェブサイトから最新の JAR をダウンロードするか、Maven/Gradle で追加）。  
- サンプル画像（例：`english-text.png`）を参照できるフォルダーに配置。

> **プロのコツ:** Maven を使用している場合は、依存関係 `<groupId>com.aspose</groupId><artifactId>aspose-ocr</artifactId>` に適切なバージョンを追加してください。JAR ファイルを手動で管理する手間が省けます。

## Java で画像からテキストを読み取る方法

以下は、**画像からテキストを読み取り**、修正済みの結果をコンソールに出力する完全な自己完結型プログラムです。`SpellCorrectTutorial` という新しいクラスにコピー＆ペーストして使用してください。

```java
import com.aspose.ocr.*;

public class SpellCorrectTutorial {

    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance and point it at your image file
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/english-text.png"));

        // Step 2: Turn on the built‑in spell‑correction feature (optional but handy)
        ocrEngine.getEngineOptions().setEnableSpellCorrection(true);

        // Step 3: Run the OCR process – this is where we actually **read text from image**
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 4: Output the corrected text; you now have **converted image to text**
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### コードの流れ（ステップごと）

| ステップ | 重要な理由 | キーポイント |
|------|----------------|--------------|
| **Create OcrEngine** | ラスターデータを解析できるコアエンジンをインスタンス化します。 | **画像からテキストを認識** する前にエンジンが必要です。 |
| **setImage** | PNG（またはサポートされている任意の形式）をメモリにロードします。 | ここで **PNG で OCR を実行** します。 |
| **Enable spell correction** | 英文の一般的なタイプミスを修正し、精度を向上させます。 | 任意ですが、**画像をテキストに変換** するときに結果がきれいになることが多いです。 |
| **recognize()** | 文字抽出の重いアルゴリズムを実行します。 | **java ocr tutorial** の核心で、実際に **画像からテキストを読み取る** 部分です。 |
| **Print result** | 最終文字列を `System.out` に出力します。 | プレーンテキストとして保存、検索、表示が可能になります。 |

> **よくある質問:** *画像が PNG でない場合は？*  
> Aspose OCR は JPEG、BMP、TIFF、さらにはマルチページ PDF もサポートしています。`fromFile(...)` の拡張子を変更すれば、エンジンが自動的に処理します。

## 画像をテキストに変換 – 高度なオプション

より細かい制御が必要な場合は、`EngineOptions` クラスでいくつかのパラメータを調整できます：

```java
ocrEngine.getEngineOptions().setLanguage(OcrLanguage.ENGLISH);
ocrEngine.getEngineOptions().setResolution(300); // DPI for better accuracy
ocrEngine.getEngineOptions().setDetectWhiteSpace(true);
```

これらの設定は、低解像度や多言語が混在する **画像からテキストを認識** する際に有用です。たとえば DPI を調整すると、スマートフォンのカメラで撮影した **PNG 画像で OCR を実行** したときに顕著な差が出ます。

## 出力の検証

プログラムを実行すると、次のような出力が得られるはずです：

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

出力が乱れている場合は、以下を再確認してください：

1. 画像パスが正しいか（`YOUR_DIRECTORY` は絶対パスまたは相対パス）。  
2. 画像が鮮明か（高コントラストで文字がはっきりしているほど OCR の品質が向上）。  
3. スペル補正が必要かどうか。場合によってはオフにした方が忠実な文字起こしになることがあります。

## よくあるバリエーション

### 1. PDF ページからテキストを読む

```java
ocrEngine.setImage(ImageStream.fromFile("sample.pdf"));
```

Aspose OCR は各ページを内部的に画像として扱うため、同じ **画像からテキストを読み取る** ロジックがそのまま使えます。

### 2. 複数ファイルからテキストを抽出

```java
String[] files = {"page1.png", "page2.png", "page3.png"};
for (String file : files) {
    ocrEngine.setImage(ImageStream.fromFile(file));
    OcrResult result = ocrEngine.recognize();
    System.out.println("File: " + file);
    System.out.println(result.getText());
}
```

ループ処理により、バッチモードで **画像をテキストに変換** できます。大量の文書デジタル化プロジェクトに便利です。

### 3. 結果をテキストファイルに保存

```java
java.nio.file.Files.write(
    java.nio.file.Paths.get("output.txt"),
    ocrResult.getText().getBytes(),
    java.nio.file.StandardOpenOption.CREATE);
```

これで **画像からテキストを読み取る** だけでなく、後で分析できるように永続化も完了です。

## 完全動作サンプル（全ステップ統合）

以下は、オプションの調整、バッチ処理、ファイル出力をすべて含んだ完成プログラムです。任意の Java プロジェクトに貼り付けてすぐに実行できます。

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class FullOcrDemo {

    public static void main(String[] args) throws Exception {
        // Configure engine once
        OcrEngine engine = new OcrEngine();
        engine.getEngineOptions().setEnableSpellCorrection(true);
        engine.getEngineOptions().setLanguage(OcrLanguage.ENGLISH);
        engine.getEngineOptions().setResolution(300);

        // Files to process – you can add as many as you like
        String[] imageFiles = {
            "YOUR_DIRECTORY/english-text.png",
            "YOUR_DIRECTORY/second-image.png"
        };

        StringBuilder allText = new StringBuilder();

        for (String imgPath : imageFiles) {
            engine.setImage(ImageStream.fromFile(imgPath));
            OcrResult result = engine.recognize();

            System.out.println("=== Result for " + imgPath + " ===");
            System.out.println(result.getText());
            System.out.println();

            allText.append(result.getText()).append(System.lineSeparator());
        }

        // Save combined output
        Path outPath = Paths.get("YOUR_DIRECTORY/ocr-output.txt");
        Files.write(outPath, allText.toString().getBytes(),
                    StandardOpenOption.CREATE, StandardOpenOption.TRUNCATE_EXISTING);

        System.out.println("All OCR results saved to " + outPath.toAbsolutePath());
    }
}
```

実行すると **画像からテキストを認識** し、**画像をテキストに変換**、さらに **PNG（またはサポートされている任意の形式）で OCR を実行** した結果が `ocr-output.txt` に書き込まれます。

![Aspose OCR を使用した画像からテキストを読み取る](https://example.com/placeholder-image.png "Aspose OCR を使用した画像からテキストを読み取る")

*上の画像は、画像からテキストを抽出するイメージを示すだけで、実際の OCR 処理はコード内で行われます。*

## 結論

本稿では、Aspose OCR を使って Java で **画像からテキストを読み取る** 方法をすべて解説しました。基本的な単一ファイル例からバッチ処理、ファイル出力まで、あらゆるプロジェクトに適用できる堅実な **java ocr tutorial** が手に入りました。

覚えておくべきポイント：

- 最高の精度を得るには、適切な解像度と使用言語を選択すること。  
- スペル補正は任意ですが、**画像をテキストに変換** する際に結果がきれいになることが多いです。  
- 同じワークフローは JPEG、BMP、TIFF、PDF でも機能します—拡張子を差し替えるだけです。

次のステップは？ OCR の出力を検索インデックスや翻訳 API、自然言語分類器に渡してみましょう。可能性は無限大です。これで基盤は整いました。

質問やエッジケース、共有したいヒントがあればコメントで教えてください—会話を続けましょう。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}