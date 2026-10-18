---
category: general
date: 2026-02-22
description: Aspose OCR for Java を使用して OCR を迅速に実行する方法。画像からテキストを認識し、PNG からテキストを抽出し、数分で画像をテキストに変換する方法を学びます。
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from png
- how to read text
- convert image to text
language: ja
og_description: Aspose OCR for Java を使用した OCR の実行方法。このガイドでは、画像からテキストを認識し、PNG からテキストを抽出し、画像を効率的にテキストに変換する方法を示します。
og_title: JavaでOCRを実行する方法 – ステップバイステップ Aspose ガイド
tags:
- OCR
- Java
- Aspose
title: JavaでOCRを実行する方法 – 完全なAspose OCRチュートリアル
url: /ja/java/ocr-operations/how-to-perform-ocr-in-java-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでOCRを実行する方法 – 完全なAspose OCRチュートリアル

低レベルの画像処理に悩むことなく、PNGファイルで **OCRの実行方法** を疑問に思ったことはありませんか？ あなただけではありません。多くのプロジェクト—請求書のスキャン、レシートのデジタル化、または単にスクリーンショットからテキストを抽出するだけ—で、開発者は **画像からテキストを認識** する信頼できる方法を必要としています。良いニュースは？ Aspose OCR for Java を使用すれば、数行のコードで **画像をテキストに変換** できます。

このチュートリアルでは、必要なすべての手順を解説します：ライセンスの適用、画像の読み込み、テキストの抽出、そして一般的な落とし穴のいくつかへの対処です。最後まで読むと、**PNGファイルからテキストを抽出** できるようになり、他のサポートされている形式でも同様に、コードをクリーンで本番環境向けに保つことができます。

## 前提条件

始める前に、以下が揃っていることを確認してください：

* Java 11 以上がインストールされていること（ライブラリは Java 8+ でも動作しますが、11+ が推奨されます）。
* Aspose OCR for Java のライセンスファイル（`Aspose.OCR.Java.lic`）。Aspose のウェブサイトから無料トライアルを取得できます。
* 依存関係管理のための Maven または Gradle（Maven のスニペットを示します）。
* プロジェクトが読み取れる場所に配置したサンプル画像（`sample.png`）。

他のサードパーティ OCR エンジンは不要です—Aspose が内部で重い処理を行います。

---

## ステップ 1: Aspose OCR の依存関係を追加

まず、`pom.xml` に Aspose OCR ライブラリを追加します。この1行で Maven Central から最新の安定版が取得されます。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the newest version -->
</dependency>
```

> **プロのコツ:** Gradle を使用している場合、同等は  
> `implementation 'com.aspose:aspose-ocr:23.10'`.

依存関係を追加することで、余分な設定なしに **画像からテキストを認識** できるようになります。

## ステップ 2: Aspose OCR ライセンスを適用

有効なライセンスがない場合、エンジンは評価モードで動作し、透かしが追加され、処理できるページ数が制限されます。ライセンスの適用は簡単で、ディスク上の `.lic` ファイルを指すだけです。

```java
import com.aspose.ocr.*;

public class LicenseDemo {
    public static void main(String[] args) throws Exception {

        // 👉 Step 2.1: Apply the Aspose OCR license (replace with your actual path)
        AsposeLicense.apply("C:/licenses/Aspose.OCR.Java.lic");

        // Continue with OCR operations...
    }
}
```

> **重要な理由:** ライセンスを適用すると “Evaluation” バナーが削除され、完全な精度が解放されます。これは、下流処理のためにクリーンな **png からテキストを抽出** 結果が必要な場合に不可欠です。

## ステップ 3: OcrEngine を初期化

ライセンスが有効になったので、`OcrEngine` インスタンスを作成します。このオブジェクトが実際の認識を行う中心的な要素です。

```java
        // 👉 Step 3.1: Create a fully‑licensed OcrEngine
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak language or DPI settings here if needed
        ocrEngine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setResolution(300); // higher DPI can improve accuracy
```

> **エッジケース:** 画像に英語以外の文字が含まれる場合は、`OcrLanguage` を適切に切り替えてください（例: `OcrLanguage.FRENCH`）。エンジンは標準で30以上の言語をサポートしています。

## ステップ 4: 画像を読み込みテキストを認識

エンジンの準備ができたら、処理したい画像を指定します。Aspose OCR は PNG、JPEG、BMP、TIFF など複数のフォーマットを読み取れます。

```java
        // 👉 Step 4.1: Load the image file
        String imagePath = "C:/images/sample.png";
        OcrResult result = ocrEngine.recognizeImage(imagePath);

        // 👉 Step 4.2: Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
```

プログラムを実行すると、以下のような出力が表示されます：

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑12‑01
Total: $256.78
Thank you for your business!
```

この出力は、PNG ファイルから **テキストを読み取る方法** を示しており、保存、検索、または他のシステムに渡すことができるプレーンテキスト文字列に変換します。

## ステップ 5: 一般的な落とし穴への対処

### 5.1 低品質画像への対処

OCR の結果が乱れている場合は、以下を試してください：

* 解像度を上げる（`ocrEngine.setResolution(400)`）。
* エンジンに渡す前に画像をグレースケールに変換する。
* `ocrEngine.getPreProcessingOptions().setAutoDeskew(true)` を使用して、傾いたテキストを補正する。

### 5.2 構造化データの抽出

テキストの塊以上のものが必要になることがあります—テーブルや行項目、キー/バリューのペアなどです。**画像をテキストに変換** した後、正規表現で後処理できます：

```java
        String raw = result.getText();
        Pattern invoicePattern = Pattern.compile("Invoice #(\\d+)");
        Matcher m = invoicePattern.matcher(raw);
        if (m.find()) {
            System.out.println("Found invoice number: " + m.group(1));
        }
```

### 5.3 複数ファイルのバッチ処理

レシートが多数入ったフォルダーがある場合、OCR 呼び出しをループでラップします：

```java
        File folder = new File("C:/images/receipts");
        for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".png"))) {
            OcrResult batchResult = ocrEngine.recognizeImage(file.getAbsolutePath());
            // Save or index batchResult.getText() as needed
        }
```

このパターンにより、**PNG ファイルからテキストを一括抽出** でき、夜間の ETL ジョブに便利です。

## ステップ 6: 完全な動作例

すべてをまとめると、IDE にコピー＆ペーストしてすぐに実行できる単一の Java クラスがこちらです（ライセンスと画像のパスを置き換えるだけです）。

```java
import com.aspose.ocr.*;

public class AsposeOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply license – mandatory for full functionality
        AsposeLicense.apply("C:/licenses/Aspose.OCR.Java.lic");

        // 2️⃣ Create engine (now fully licensed)
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Optional tweaks – language, DPI, preprocessing
        ocrEngine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setResolution(300);
        ocrEngine.getPreProcessingOptions().setAutoDeskew(true);

        // 4️⃣ Recognize a PNG image
        String imgPath = "C:/images/sample.png";
        OcrResult result = ocrEngine.recognizeImage(imgPath);

        // 5️⃣ Output the text – this is the core “convert image to text” step
        System.out.println("=== OCR Output ===");
        System.out.println(result.getText());

        // 6️⃣ Simple post‑processing example (extract invoice number)
        java.util.regex.Pattern p = java.util.regex.Pattern.compile("Invoice #(\\d+)");
        java.util.regex.Matcher m = p.matcher(result.getText());
        if (m.find()) {
            System.out.println("Detected invoice #: " + m.group(1));
        }
    }
}
```

プログラムを実行すると、抽出されたテキストがコンソールに表示され、その後に検出された請求書番号が続きます。これが、開始から完了までの完全な **OCR の実行方法** ワークフローです。

---

## よくある質問 (FAQ)

**Q: Aspose OCR は PDF ファイルで動作しますか？**  
A: はい。`ocrEngine.recognizePdf("file.pdf", pageNumber)` を使用して PDF ページを画像として渡すことができます。API は同じ `OcrResult` オブジェクトを返します。

**Q: ファイルではなく **画像からテキストを認識** ストリームが必要な場合はどうすればよいですか？**  
A: `ocrEngine.recognizeImage(InputStream)` を使用します—ウェブアップロードやクラウドストレージのブロブに最適です。

**Q: これを Android で実行できますか？**  
A: このライブラリは Java のみで、Android では公式にサポートされていませんが、モバイルサポートが必要な場合は Xamarin で .NET バージョンを使用できます。

**Q: エンジンの精度はオープンソースの代替品と比べてどうですか？**  
A: Aspose OCR はクリーンな印刷文書で常に 95 % 以上のスコアを出し、ノイズの多いスキャンでも多くの無料ツールより優れています。特に前処理を有効にすると効果的です。

---

## 結論

本稿では、Aspose OCR を使用した Java での **OCR の実行方法** を、ライセンスの適用から PNG ファイルからのクリーンなテキスト抽出までカバーしました。これで、**画像からテキストを認識**、**png からテキストを抽出**、プログラムで **テキストを読み取る方法**、そして下流処理のために **画像をテキストに変換** する方法が分かります。  

さまざまな言語、DPI 設定、バッチ処理を試してみてください—これらの調整が不安定なプロトタイプと本番レベルのソリューションの違いを生むことが多いです。このガイドが役立ったなら、**OCR 用画像前処理** と **OCR 結果を Elasticsearch と統合** して検索可能なドキュメントアーカイブを作るチュートリアルもご覧ください。

コーディングを楽しんで、OCR の結果が常にクリアでありますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}