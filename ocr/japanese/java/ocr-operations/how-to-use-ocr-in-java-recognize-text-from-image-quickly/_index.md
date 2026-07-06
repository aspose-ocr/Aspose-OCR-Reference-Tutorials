---
category: general
date: 2026-02-17
description: JavaでOCRを使用して画像ファイルからテキストを認識し、PNGレシートからテキストを抽出し、Aspose OCRでレシートをJSONに変換する方法を学びましょう。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: ja
og_description: 画像からテキストを認識し、PNGレシートからテキストを抽出し、レシートをJSONに変換するためのJavaでのOCR使用方法のステップバイステップガイド。
og_title: JavaでOCRを使用する方法 – 画像からテキストを認識する
tags:
- OCR
- Java
- Aspose
- Image Processing
title: JavaでOCRを使用する方法 – 画像からテキストを素早く認識する
url: /ja/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で OCR を使う方法 – 画像からテキストをすばやく認識する

レシートの写真からテキストを抽出する **OCR の使い方** が気になったことはありませんか？いくつかのオンラインツールを試したものの、文字化けしたり解析できない形式になってしまった経験はありませんか。実は、数行の Java コードさえ書けば、画像ファイルから **テキストを認識** でき、PNG のレシートから **テキストを抽出** し、さらには **レシートを JSON に変換** して下流処理に回すことができます。

このチュートリアルでは、Aspose OCR ライブラリのライセンス取得から、データベースや機械学習モデルに投入できるクリーンな JSON ペイロードを得るまでの全工程を解説します。余計な説明は省き、IDE にコピペできる実用的なサンプルコードを提供します。最後まで読むと、`receipt.png` を入力として、すぐに使える JSON 文字列を出力する自己完結型プログラムが完成します。

## 必要なもの

- **Java Development Kit (JDK) 8+** – 最近のバージョンであれば問題ありません。  
- **Aspose OCR for Java** ライブラリ（Maven アーティファクトは `com.aspose:aspose-ocr`）。  
- **有効な Aspose OCR ライセンスファイル**（`Aspose.OCR.lic`）。無料トライアルでもテストは可能ですが、正式ライセンスを取得すれば評価版の制限が解除されます。  
- テキストを読み取りたい画像ファイル（PNG、JPEG など）— ここでは `receipt.png` と呼び、既知のフォルダーに配置します。  
- お好みの IDE（IntelliJ IDEA、Eclipse、VS Code など） – 好きなものを選んでください。

> **Pro tip:** ライセンスファイルはソースフォルダーの外に置き、絶対パスまたは相対パスで参照するようにすれば、バージョン管理にコミットしてしまうリスクを回避できます。

前提条件が整ったので、実際のコードに入りましょう。

## OCR の使い方 – 基本手順

以下は実行するアクションのハイレベルな概要です。

1. **Aspose OCR ライブラリをロード**し、ライセンスを適用する。  
2. **`OcrEngine` インスタンスを作成** – これが本格的な OCR 処理を行うエンジンです。  
3. **`OcrInput` オブジェクトを用意**し、処理対象の画像を指し示す。  
4. **`ResultFormat.JSON` で `recognize` を呼び出し**、抽出テキストの JSON 表現を取得する。  
5. **JSON 出力を処理** – コンソールに表示したり、ファイルに書き出したり、さらに解析したりします。

各ステップは以下のセクションで詳しく説明します。

## 手順 1 – Aspose OCR をインストールしライセンスを適用

Maven を使用している場合は、`pom.xml` に Aspose OCR の依存関係を追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

次に、Java コード内でライセンスをロードします。このステップは必須です。ライセンスがないと評価モードで動作し、出力に透かしが入る可能性があります。

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Why this matters:** `License` オブジェクトは OCR エンジンに対し、フル機能（高精度認識や JSON エクスポートを含む）を使用できる権限があることを通知します。このステップを省略すると **画像からテキストを認識** は可能ですが、結果が制限されたり品質が低下したりします。

## 手順 2 – OCR エンジンインスタンスを作成

`OcrEngine` クラスはすべての OCR 操作のエントリーポイントです。ピクセルを読み取り、どの文字に相当するかを判断する「脳」のようなものです。

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

エンジンは後からカスタマイズ（言語設定やデスクュー有効化など）できます。レシートがラテン文字以外を含む場合や、斜めにスキャンされている場合に便利です。米国の一般的なレシートであれば、デフォルト設定で十分です。

## 手順 3 – 処理対象画像をロード

ここでは OCR エンジンにレシート画像のパスを渡します。`OcrInput` クラスは複数画像を受け取れますが、このチュートリアルではシンプルに単一の PNG に限定します。

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

大量に **PNG からテキストを抽出** したい場合は、`input.add()` を繰り返すか、ファイルパスのリストを渡すだけです。

## 手順 4 – テキストを認識しレシートを JSON に変換

チュートリアルの核心です。エンジンにテキスト認識を指示し、結果を JSON 形式で取得します。`ResultFormat.JSON` フラグがすべての重い処理を代行してくれます。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON ペイロードには、認識された各行、バウンディングボックス、信頼度スコア、そして生テキストが含まれます。この構造により **レシートを JSON に変換** して、任意の下流 API に簡単に渡すことができます。

## 手順 5 – すべてをまとめてプログラムを実行

以下は、上記手順をすべて組み合わせた完成形の Java クラスです。`JsonExportDemo.java`（好きな名前でも可）として保存し、IDE またはコマンドラインから実行してください。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### 期待される出力

プログラムを実行すると、以下のような JSON 文字列がコンソールに出力されます（内容はレシートによって異なります）。

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

この JSON をデータベース、REST エンドポイント、あるいはデータ分析パイプラインに流し込めます。**レシートを JSON に変換** する作業はすでに完了しています。

## よくある質問とエッジケース

### 画像が回転している場合は？

Aspose OCR は軽度の回転を自動で検出・補正します。大きく歪んだ画像の場合は、認識前に `engine.getImagePreprocessingOptions().setDeskew(true)` を呼び出してください。

### 複数言語に対応させるには？

`engine.getLanguage()` で目的の言語を設定します。例: `engine.setLanguage(Language.FRENCH)`。多言語レシートから **画像からテキストを認識** したいときに便利です。

### JSON ではなくプレーンテキストが欲しい場合は？

もちろん可能です。`ResultFormat.JSON` を `ResultFormat.TEXT` に置き換え、`result.getText()` を呼び出してください。

### 特定領域だけを OCR したい場合は？

`ocrInput.add(imagePath, new Rectangle(x, y, width, height))` を使ってレシートの対象エリアだけを指定できます。これにより速度と精度が向上します。

## 本番環境向け OCR のプロ Tips

- **ライセンスオブジェクトをキャッシュ** することで、ループ内で多数のファイルを処理する際のオーバーヘッドを削減できます。  
- **バッチ処理**：すべてのレシートパスを単一の `OcrInput` にロードし、`recognize` を一度だけ呼び出すと、ページごとの配列を含む JSON が返ります。  
- **JSON の検証**：取得した文字列は Jackson などのライブラリでパースし、保存前に正しい形式か確認してください。  
- **信頼度の監視**：JSON には各行に `confidence` フィールドが含まれます。0.85 未満の行は除外するなど、品質管理に活用しましょう。  
- **ライセンスの保護**：`Aspose.OCR.lic` は安全なボールトや環境変数に格納し、特にクラウド環境では漏洩を防いでください。

## 結論

Java で **OCR を使う方法** を学び、**画像からテキストを認識**、**PNG からテキストを抽出**、そして **レシートを JSON に変換** する手順をエンドツーエンドで実装しました。手順はシンプルでコードはそのまま実行可能、JSON 出力はあらゆる下流システムで利用できる構造化データです。

次のステップとしては、JSON を Apache Kafka に流してリアルタイム処理を行ったり、正規表現で項目合計を抽出したり、クラウド OCR サービスと組み合わせてスケーラビリティを高めたりできます。どのシナリオを選んでも、ここで学んだ基礎は変わりません。

質問や実装中に問題が発生した場合は、下のコメント欄に書き込んでください。一緒にトラブルシュートしましょう。コーディングを楽しみながら、乱雑なレシート画像をクリーンで検索可能なデータに変換してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}