---
category: general
date: 2026-02-17
description: 画像からテキストへの Java チュートリアル：Aspose OCR を使用して画像からウルドゥー語テキストを抽出する方法を学びます。完全な
  Java OCR のサンプルが含まれています。
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: ja
og_description: 画像からテキストへの Java チュートリアルでは、Aspose OCR を使用して画像からウルドゥー語テキストを抽出する方法を示します。ステップバイステップで完全な
  Java OCR の例を確認してください。
og_title: '画像からテキストへ Java: Aspose OCRでウルドゥー語テキストを抽出'
tags:
- OCR
- Java
- Aspose
title: '画像からテキストへ Java: Aspose OCRでウルドゥー語テキストを抽出'
url: /ja/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Aspose OCRでウルドゥー語テキストを抽出

ウルドゥー語の文書に対して **image to text java** 変換が必要な場合、ここが適切な場所です。手書きのメモやスキャンした新聞ページの画像から *テキストを抽出する方法* を考えたことはありませんか？このガイドでは、Aspose OCR を使用して画像からウルドゥー文字を直接抽出する **java ocr example** をステップバイステップで紹介します。

ライブラリのライセンス設定からコンソールへの結果出力まで、すべてをカバーします。最後まで読めば、**load image ocr** ファイルを読み込み、言語をウルドゥー語に設定し、余分なツールなしでクリーンな Unicode 出力を取得できるようになります。

## 必要なもの

- **Java Development Kit (JDK) 8+** – コードは最新の JDK で動作します。
- **Aspose.OCR for Java** JAR（Aspose のウェブサイトからダウンロード）。  
- 有効な **Aspose OCR license** ファイル（`Aspose.OCR.lic`）。  
- ウルドゥー語テキストを含む画像、例：`urdu-sample.png`。

これらの基本が揃っていれば、依存関係を探す手間なくすぐにコードに取り掛かれます。

## image to text java – Aspose OCR の設定

まず、Aspose にライセンスがあることを通知する必要があります。ライセンスがない場合、ライブラリは評価モードで動作し、出力に透かしが付加されます。

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Why this matters:**（この重要性） ライセンスを適用すると、5 秒の処理制限が解除され、2025‑Q3 に追加された完全なウルドゥー語パックが使用可能になります。この手順を省略すると OCR エンジンは動作しますが、結果に小さな “Evaluation” タグが表示されます。

## テキスト抽出方法 – OCR エンジンの初期化

ここでエンジンを作成し、ウルドゥー語に関心があることを明示的に指定します。`OcrLanguage.URDU` 定数は、適切な文字セットとセグメンテーション規則を有効にします。

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Pro tip:**（プロのコツ） 1 回の実行で複数言語を処理する必要がある場合は、カンマ区切りのリストを渡すことができます（例：`OcrLanguage.ENGLISH, OcrLanguage.URDU`）。エンジンは各領域を自動検出します。

## 画像 OCR のロード – 入力の準備

Aspose は、1 つまたは複数の画像を保持できる `OcrInput` オブジェクトを使用します。ここではローカルファイルから **load image ocr** データを読み込みます。

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Note:**（注意） `YOUR_DIRECTORY` を絶対パスまたはプロジェクトルートからの相対パスに置き換えてください。ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローします。`new File(path).exists()` で簡単に確認すれば、デバッグ時間を大幅に削減できます。

## テキスト認識 – OCR プロセスの実行

エンジンの設定と画像のロードが完了したら、最終的に `recognize` を呼び出します。このメソッドは抽出された文字列を保持する `OcrResult` を返します。

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**What’s happening under the hood?**（内部で何が起きているか） OCR エンジンは画像を行に分割し、さらに文字に分割して、ウルドゥー語固有の形状規則（結合形など）を適用します。そのため、言語設定を早めに行うことが重要です。設定しないと、ラテン文字のプレースホルダーが乱れた状態で出力されます。

## 認識されたウルドゥー語テキストの出力

最後のステップは結果を単に出力することです。ウルドゥー語は右から左へ書くスクリプトなので、コンソールが Unicode に対応していることを確認してください（ほとんどの最新ターミナルは対応しています）。

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Expected output (example):**（期待される出力（例））

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

もし疑問符や空文字列が表示された場合は、コンソールのエンコーディングが UTF‑8 に設定されているか再確認してください（Windows では `chcp 65001`、Java 実行時に `-Dfile.encoding=UTF-8` を付与）。

## 完全動作例 – すべての手順を一括で

以下に、コピー＆ペースト可能な完全なプログラムを示します。外部参照はなく、単一の Java ファイルだけです。

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

以下のコマンドで実行します：

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

JAR のバージョン（`23.10`）はダウンロードしたものに置き換えてください。コンソールには PNG から抽出されたウルドゥー語の文が表示されます。

## よくある落とし穴とエッジケース

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **出力が空** | 画像が暗すぎる、または解像度が低い。 | `BufferedImage` を使用して画像を前処理（コントラスト増加、二値化）し、Aspose に渡す前に実施してください。 |
| **文字化け** | 言語設定が間違っている（デフォルトは英語）。 | `recognize` を呼ぶ前に `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` が呼び出されていることを確認してください。 |
| **ライセンスが見つからない** | パスのタイプミスまたはファイルが存在しない。 | 絶対パスを使用するか、`.lic` ファイルをクラスパスに配置し、`license.setLicense("Aspose.OCR.lic");` を呼び出してください。 |
| **大きな画像でメモリ不足** | 大きな PNG がヒープを消費する。 | `ocrEngine.setMaxImageSize(2000);` を呼び出して内部で縮小するか、画像自体をリサイズしてください。 |

## デモの拡張

- **Batch processing:** フォルダーをループし、各ファイルを同じ `OcrInput` に追加して、結果を CSV に収集します。  
- **Different languages:** `OcrLanguage.URDU` を `OcrLanguage.ARABIC` に置き換えるか、複数言語を組み合わせます。  
- **Saving to file:** `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));` を使用します。  

これらすべてのアイデアは、先ほど作成した **java ocr example** を基にしており、実務プロジェクトに合わせてソリューションをカスタマイズできます。

## 結論

これで、Aspose OCR を使用して画像からウルドゥー語文字を抽出する堅実な **image to text java** ワークフローが手に入りました。このチュートリアルでは、ライセンス設定や言語選択から画像のロード、結果の出力までのすべての手順を網羅しているので、コードを任意の Java プロジェクトに貼り付けるだけで動作を確認できます。

次に、より大きな PDF や異なるスクリプトで実験したり、OCR ステップを Spring Boot の REST エンドポイントに統合してみてください。同じ原則—**how to extract text**、**load image o** 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}