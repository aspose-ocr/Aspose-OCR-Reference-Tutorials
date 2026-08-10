---
category: general
date: 2026-05-06
description: JavaでOCRを使用して画像からテキストを抽出する方法。OCRによる画像からテキストへの変換を学び、OCRエラーを修正し、Aspose
  OCRで画像をOCR用に読み込む。
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: ja
og_description: Aspose OCR を使用して、Java で画像からテキストを抽出し、OCR エラーを修正し、OCR 用に画像を読み込む方法。
og_title: JavaでOCRを使用する方法 – 完全ガイド
tags:
- OCR
- Java
- Aspose
title: JavaでOCRを使用する方法 – 画像からテキストを抽出し、スペル補正を行う
url: /ja/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRを使用する方法 – 画像からテキストを抽出し、スペル補正を行う

ぼやけたレシートの写真をきれいで検索可能なテキストに変換する **OCRの使い方** を疑問に思ったことはありませんか？ あなただけではありません。経費管理アプリ、請求書デジタル化パイプライン、あるいは簡単なメモ取りスクリプトなど、多くのプロジェクトで画像から信頼できるテキストを取得することが最初のハードルです。

このチュートリアルでは、JavaでOCRを使用する方法をステップバイステップで解説します。画像の読み込みからOCRエラーの修正まで、結果が人が入力したかのように自然になるまでをカバーします。最後まで読むと、**画像からテキストを抽出** し、**OCR画像からテキストへの変換** を実行し、一般的な認識ミスを自動的に修正できるようになります。

## 作成するもの

以下の小さなJavaコンソールプログラムを作成します。

1. PNG（またはサポートされている任意の形式）を Aspose OCR エンジンに読み込む。  
2. 組み込みのスペル補正機能を有効にして **OCRエラーを修正** する。  
3. 認識処理を実行し、クリーンアップされたテキストを出力する。  

外部サービスや重厚なフレームワークは不要です。単一のJARと数行のコードだけで完結します。

### 前提条件

- Java Development Kit (JDK) 8 以上。  
- Maven（または任意のビルドツール）で Aspose OCR ライブラリを取得。  
- 解析したい画像ファイル（例：`receipt.png`）。

Aspose OCR JAR が無い場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **プロのコツ:** 無料評価版はテストに利用できますが、ライセンスを取得すれば評価用の透かしが除去されます。

## Step 1 – OCRエンジンの初期化 (Primary Keyword in Action)

最初に行うべきことは `OcrEngine` のインスタンスを作成することです。ピクセルを読み取り文字に変換する脳のようなものと考えてください。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*なぜ重要か:* エンジンを初期化することで内部リソース（言語モデル、辞書など）が設定されます。このステップを省略すると、画像を読み込もうとした際に `NullPointerException` が発生します。

## Step 2 – OCR用画像の読み込み

ここで実際に **OCR用画像を読み込み** ます。Aspose は便利な `ImageStream.fromFile` ヘルパーを提供していますが、好みで `byte[]` を渡すことも可能です。

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*よくある落とし穴:* ファイルパスは絶対パスまたは作業ディレクトリからの相対パスである必要があります。画像が見つからない場合、エンジンは `IOException` をスローします。特に IDE から実行する場合とパッケージ化された JAR から実行する場合でパスを再確認してください。

## Step 3 – スペル補正を有効にして **OCRエラーを修正**

標準の OCR はノイズが多く、例えば “l0ve” が “love” になったり、“0” が “O” になったりします。スペル補正を有効にすると、エンジンは典型的なミスを修正するポストプロセスを実行します。

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*なぜ必要か:* スペル補正が無いと、出力を手動でクリーンアップしなければならず、Automation の目的が失われます。組み込み辞書は英語や他のいくつかの言語でうまく機能します。

## Step 4 – 認識を実行 (**OCR画像からテキストへ**)

画像が読み込まれ、スペル補正が有効になったので、いよいよエンジンにテキスト認識を指示できます。

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*エッジケース:* 画像が低コントラストまたは大きく傾いている場合、結果に意味不明な文字列が残ることがあります。エンジンに渡す前に前処理（例：二値化、デスキュー）を検討してください。

## Step 5 – クリーンアップされたテキストの出力

最後のステップは結果を単に出力することです。実際のアプリケーションではデータベースやファイルに書き込むこともありますが、このデモでは `System.out` で十分です。

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### 期待される出力

`receipt.png` に項目のリストがはっきり写っていると仮定すると、以下のような出力が得られます。

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

元のスキャンで「Qy」のような誤字があっても、“Qty” と “Price” が正しく綴られていることに注目してください。

## 完全な動作例

以下は `SpellCorrectDemo.java` というファイル名でコピー＆ペーストできる完全なプログラムです。Aspose OCR JAR がクラスパスに含まれていることを確認してください。

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

以下のコマンドで実行します:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

コンソールにクリーンアップされたテキストが表示されるはずです。

## ボーナス: 精度向上のための設定調整

デフォルト設定はほとんどの印刷文書で機能しますが、特定のシナリオではいくつかのパラメータを調整する必要があるかもしれません。

| Setting | 機能 | 変更すべきタイミング |
|---------|------|----------------------|
| `setLanguage(OcrLanguage.English)` | 英語辞書を強制（誤検出を減らす） | 画像が英語のみの場合。 |
| `setResolution(300)` | ソース画像の DPI をエンジンに伝える | 高解像度スキャンの場合。 |
| `setEnableAutoSkewCorrection(true)` | わずかに傾いたページを自動回転 | スマートフォンで撮影した画像の場合。 |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## よくある質問

**Q: PDFでも動作しますか？**  
A: はい。各 PDF ページを画像に変換（例：Aspose PDF を使用）し、その画像を OCR エンジンに渡します。

**Q: 画像が BMP 形式の場合は？**  
A: `ImageStream.fromFile` は PNG、JPEG、BMP、TIFF、GIF を標準でサポートしています。拡張子を変更するだけです。

**Q: スペル補正を無効にできますか？**  
A: もちろんです。下流処理で生の OCR 出力が必要な場合は `setEnableSpellCorrection(false)` を設定してください。

## 結論

これで Java で **OCR を使用する方法**、**画像からテキストを抽出**、自動的に **OCR エラーを修正**、そして Aspose OCR を使った正しい **OCR用画像の読み込み** が分かりました。初期化、読み込み、スペル補正の有効化、認識、出力という5ステップのフローは、日常的な OCR 作業の大部分をカバーします。

ここからは、このロジックをデータベースへの書き戻し、REST エンドポイント、またはバッチプロセッサと組み合わせて、数十枚のレシートを一括処理することを検討してください。上記の設定表を試して、精度を最大限に引き出しましょう。

コーディングを楽しんでください。そして、OCR の結果がコーヒーで汚れたレシートよりも常にクリアでありますように！

![OCRの使用方法を示す図：画像 → OCRエンジン → 補正されたテキストのフロー]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}