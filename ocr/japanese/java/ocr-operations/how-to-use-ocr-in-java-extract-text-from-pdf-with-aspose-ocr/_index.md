---
category: general
date: 2026-02-17
description: JavaでOCRを利用してPDFからテキストを抽出し、PDFを画像に変換し、Aspose.OCRでスキャンしたPDFファイルにOCRを実行する方法。
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: ja
og_description: JavaでOCRを使用してPDFファイルからテキストを抽出する方法。PDFを画像に変換し、Aspose.OCRでスキャンされたPDFを認識する方法を学びましょう。
og_title: JavaでOCRを使用する方法 – 完全ガイド
tags:
- OCR
- Java
- Aspose
title: JavaでOCRを使用する方法 – Aspose.OCRでPDFからテキストを抽出する
url: /ja/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で OCR を使用する方法 – Aspose.OCR で PDF からテキストを抽出

スキャンした PDF を検索可能なテキストに変換する **OCR の使い方** を知りたくありませんか？ あなたは一人ではありません。PDF が画像の集合として届くと、ほとんどの開発者が壁にぶつかります。通常のテキスト抽出ツールは何も返さないのです。朗報です！ 数行の Java と Aspose.OCR さえあれば、**PDF からテキストを抽出**、**PDF を画像に変換**、そして **スキャンした PDF を認識** するワークフローを、手間なく実現できます。

このチュートリアルでは、ライセンスの取得から最終結果の出力まで、必要なすべてを順を追って解説します。最後まで読めば、スキャンしたレポート、請求書、電子書籍など、あらゆる PDF からプレーンテキストを抽出できる実行可能なプログラムが手に入ります。外部サービスは不要、魔法も不要—すべて自分で管理できる純粋な Java コードだけです。

## 必要なもの

- **Java Development Kit (JDK) 8 以上** – 最近のバージョンであればどれでも可。
- **Aspose.OCR for Java** JAR（Aspose の公式サイトからダウンロード）。  
- **有効な Aspose.OCR ライセンスファイル**（`Aspose.OCR.lic`）。無料トライアルでも動作しますが、ライセンスを取得すると精度がフルに解放されます。
- **サンプルのスキャン PDF**（例：`scanned-report.pdf`）。  
- IDE もしくはシンプルなテキストエディタとターミナル。

以上です。Maven や Gradle、余分な依存関係は不要—クラスパスに Aspose.OCR JAR を置くだけです。

![OCR の使用例](image-placeholder.png "OCR の使用例")

## Step 1 – Aspose.OCR ライセンスをロードする（重要な理由）

エンジンがフルスピードで動作するためには、ライセンスファイルの場所を教える必要があります。このステップを省くと、ライブラリは評価モードになり、出力に透かしが入ったり精度が制限されたりします。

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**動作原理:** `License` クラスが `.lic` ファイルを読み込み、グローバルに登録します。これが設定されると、以後作成するすべての `OcrEngine` が自動的にライセンス機能を使用します。

## Step 2 – OCR エンジンを作成する（魔法の裏側）

`OcrEngine` インスタンスは画像をスキャンしテキストを出力する主役です。ピクセルパターンを解釈する脳と考えてください。

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**プロのコツ:** 言語や信頼度閾値、GPU 加速などをエンジンのプロパティで調整できます。英語の PDF がほとんどの場合、デフォルト設定で問題ありません。

## Step 3 – 入力を準備する：PDF を追加（内部で PDF を画像に変換）

Aspose.OCR は PDF の各ページを画像として扱います。`addPdf` を呼び出すと、ライブラリは各ページを静かにラスタライズし、**PDF を画像に変換** した状態で認識に備えます。

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**内部で起きていること:**  
- PDF が開かれます。  
- 各ページが 300 dpi（デフォルト）でレンダリングされ、文字のディテールが保持されます。  
- レンダリングされたビットマップオブジェクトが `OcrInput` コレクションに格納されます。

デバッグや独自前処理のために生画像が必要な場合は、このステップの後で `ocrInput.getPages()` を呼び出してください。

## Step 4 – OCR プロセスを実行（PDF 上で OCR を実行）

いよいよ本格的な処理が始まります。`recognize` メソッドはすべての画像を走査し、認識アルゴリズムを実行して結果を `OcrResult` に集約します。

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**注目すべき点:** `OcrResult` にはプレーンテキストだけでなく、信頼度スコア、バウンディングボックス、元画像への参照が含まれます。多くのユースケースでは `getText()` だけで十分です。

## Step 5 – 抽出したテキストを取得して表示

最後に、結果からプレーンテキスト文字列を取り出してコンソールに出力します。ファイルに書き出したり、検索インデックスに投入したり、下流の NLP パイプラインに流すことも可能です。

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### 期待される出力

`scanned-report.pdf` にシンプルな段落が含まれている場合、次のような出力が得られます。

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

元のレイアウトをできるだけ保持し、改行位置も可能な限り再現します。

## よくあるケースの対処法

### 1. マルチランゲージ PDF

文書にフランス語やスペイン語が混在している場合は、`recognize` を呼び出す前に言語を設定します。

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

配列で複数言語を指定すれば、エンジンが自動検出します。

### 2. 低解像度スキャン

150 dpi のスキャンを扱うときは、内部レンダリング DPI を上げます。

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

DPI を上げると文字の鮮明さが向上しますが、メモリ使用量も増加します。

### 3. 大容量 PDF（メモリ管理）

ページ数が多数ある PDF はバッチ処理で対応します。

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

この方法により、JVM ヒープが過度に膨らむのを防げます。

## 完全版・すぐに実行できるサンプル

以下はインポート文とライセンス処理を含むフルプログラムです。コピー＆ペーストしてすぐに実行できます。

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

実行コマンド:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

コンソールに抽出されたテキストが表示されるはずです。

## まとめ – 本チュートリアルで学んだこと

- Aspose.OCR を使った **Java での OCR の利用方法**。  
- **PDF からテキストを抽出** するワークフロー。  
- ライブラリは内部で **PDF を画像に変換** してから文字認識を行うこと。  
- 複数言語、低解像度スキャン、大容量文書に対する **OCR 実行のコツ**。  
- 任意の Java プロジェクトに組み込める、**完全な実行可能コードサンプル**。

## 次のステップと関連トピック

スキャン PDF を認識できるようになったら、以下の応用を検討してみてください。

- **検索可能 PDF の生成** – OCR テキストを元の PDF に重ね合わせ、検索可能な文書を作成。  
- **バッチ処理サービス** – コードを Spring Boot のマイクロサービス化し、REST 経由で PDF を受け取る。  
- **Elasticsearch との統合** – 抽出テキストをインデックス化し、ドキュメントリポジトリ全体の高速全文検索を実現。  
- **画像前処理** – OpenCV を使ってページの傾き補正やノイズ除去を行い、OCR 精度をさらに向上。

これらのテーマは本チュートリアルで学んだ基礎概念を土台にしています。ぜひ実験して、OCR エンジンに重い処理を任せてみてください。

---

*Happy coding! ライセンスエラーや予期せぬ null 結果などでつまずいたら、遠慮なくコメントを残してください。デバッグのお手伝いをします。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}