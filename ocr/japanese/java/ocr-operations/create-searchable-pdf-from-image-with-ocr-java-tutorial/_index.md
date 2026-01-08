---
category: general
date: 2026-01-07
description: Aspose OCR を使用して Java で画像から検索可能な PDF を作成します。画像を PDF に変換し、画像からテキストを認識し、JPG
  から PDF を生成する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: ja
og_description: Aspose OCR を使用して Java で画像から検索可能な PDF を作成します。画像を PDF に変換し、画像からテキストを認識し、JPG
  から PDF を生成するステップバイステップガイド。
og_title: 画像から検索可能なPDFを作成 – Java OCRガイド
tags:
- OCR
- Java
- PDF
- Aspose
title: 画像からOCRで検索可能なPDFを作成 – Javaチュートリアル
url: /ja/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から OCR で検索可能な PDF を作成 – Java チュートリアル

スキャンした画像から **検索可能な PDF** を作成したいけど、どこから手を付ければいいか分からないことはありませんか？同じ壁にぶつかる開発者は多いです。JPEG を実際に検索できる PDF に変換する最初の一歩は意外とハードルが高いものです。

このガイドでは、**画像を PDF に変換**、**画像からテキストを認識**、そして最終的に **JPG から PDF を生成** する完全な実行可能サンプルを紹介します。Aspose OCR for Java を使った具体的なコードをそのままコピーして、すぐに実行できます。

## 必要なもの

作業を始める前に、以下が環境に揃っていることを確認してください。

* **Java 17** 以上（API は最近の JDK であれば動作します）。  
* **Aspose.OCR for Java** ライブラリ – Maven Central もしくは Aspose の公式サイトから最新の JAR を取得してください。  
* サンプル画像（例: `sample.jpg`）を、参照できるフォルダーに配置しておく。  
* 好みの IDE もしくはテキストエディタ＋ターミナル。  

以上です。重いフレームワークや追加のネイティブ依存関係は不要です。さっそく始めましょう。

## Step 1 – 検索可能な PDF を作成: OCR エンジンの初期化

まず最初に `OcrEngine` インスタンスを生成し、対象画像を指定します。このオブジェクトが Aspose OCR の中心で、ビットマップの読み込みから認識結果の取得までを担います。

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **ポイント:** エンジンを正しく初期化しないと、ライブラリは指定された画像形式を読み込めません。パスが間違っていると `FileNotFoundException` が発生し、パイプライン全体が停止します。

## Step 2 – パフォーマンス向上: GPU、マルチコア CPU、スペル補正の有効化

OCR は特に大きな文書になると CPU に負荷がかかります。Aspose では処理速度と精度を高めるためのオプションが用意されています。

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **プロのコツ:** GPU が無いサーバーで実行する場合は `setUseGpu(false)` にしても問題ありません。その場合はマルチコア CPU にフォールバックします。

## Step 3 – 画像品質の改善: デスキューとデスペックル（任意だが推奨）

スキャン画像は完璧ではありません。わずかな傾きやノイズが認識精度を下げることがあります。`ImageProcessingOptions` クラスを使って、エンジンが画像を読む前に前処理を行いましょう。

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **エッジケース:** 元の画像がすでにきれいな場合はこのステップを省略しても構いません。処理時間に数ミリ秒程度のオーバーヘッドが加わるだけです。

## Step 4 – 画像からテキストを認識し PDF を生成

いよいよ本番です。`recognize()` を呼び出すと `OcrResult` が返ってきます。そこから PDF など好きな形式で保存できますが、検索可能な文書としては PDF が最も一般的です。

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **期待される結果:** `sample-output.pdf` には元画像が背景レイヤーとして配置され、認識されたテキストは透明なオーバーレイとして重なります。Adobe Reader で開き、テキスト選択を試してみてください。驚くはずです。

## Step 5 – 作成した検索可能 PDF の検証

ファイルを書き出したら、実際に PDF が検索可能かどうかを確認するのがベストプラクティスです。

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

PDF を開き **Ctrl F** で、画像中に確実に存在する単語を入力します。検索でヒットすれば、**検索可能な PDF の作成** に成功です！

## 実務での OCR 活用例（ボーナス）

* **バッチ処理:** フォルダー内の JPG をループで処理するコードに組み込みます。メモリ使用量を抑えるため、`OcrEngine` インスタンスはできるだけ再利用してください。  
* **言語サポート:** Aspose OCR は 60 以上の言語に対応しています。`ocrEngine.getEngineOptions().setLanguage(Language.English);` のように列挙型で指定できます（他の言語でも同様）。  
* **エラーハンドリング:** `OcrException` を捕捉して、破損したファイルなどの例外を穏やかに処理しましょう。  

これらの調整により、プロダクション向けパイプラインでも安定して利用できます。

## 完全版 Java サンプル – JPG から検索可能 PDF を作成

以下はそのままコンパイル・実行できる自己完結型プログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えて使用してください。

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**期待出力:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

生成された PDF を開くと、`sample.jpg` に含まれていた単語を検索できるはずです。テキストレイヤーが見えない場合は、画像パスや OCR エンジンが内部で例外を出していないか再確認してください。

## まとめ

今回は Aspose OCR for Java を使って、JPEG から **検索可能な PDF** を作成する手順をすべて解説しました。画像の読み込み、パフォーマンス設定の調整、画像前処理、テキスト認識、そして検索可能 PDF の保存まで、各ステップの「なぜ」と「どうやって」を具体例と共に示しました。

これで **画像を PDF に変換**、**画像からテキストを認識**、そして **JPG から PDF を生成** できるようになりました。次はフォルダー全体を一括処理したり、別言語に挑戦したり、出力 PDF にパスワード保護を付与したりしてみてください。可能性は無限です。

実装上の疑問やライセンス、パフォーマンスチューニングに関する質問があれば、ぜひコメントで教えてください。Happy coding!  

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "Create searchable PDF diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}