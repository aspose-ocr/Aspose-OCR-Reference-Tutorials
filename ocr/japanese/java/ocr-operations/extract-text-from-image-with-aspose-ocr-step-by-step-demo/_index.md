---
category: general
date: 2026-02-14
description: Aspose OCR を使用して画像からテキストを抽出します。OCR 用に画像をロードする方法、矩形領域からテキストを読み取る方法を学び、数分でこの
  Aspose OCR チュートリアルに従ってください。
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: ja
og_description: 画像からテキストを瞬時に抽出します。このガイドでは、OCR用に画像を読み込む方法、矩形領域からテキストを読み取る方法、そして Aspose
  OCR チュートリアルを完了する手順を示します。
og_title: Aspose OCRで画像からテキストを抽出 – クイックガイド
tags:
- Aspose
- OCR
- Java
title: Aspose OCRで画像からテキストを抽出 – ステップバイステップデモ
url: /ja/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR で画像からテキストを抽出 – ステップバイステップ デモ

画像から **テキストを抽出** したいことはありませんか？でも、どこから始めればいいか分からない…という方は多いです。レシートのスキャンや身分証明書の確認に初めて取り組むときに、壁にぶつかることがよくあります。良いニュースは、Aspose OCR を使えば画像を読み込み、テキストが存在する正確な領域を指定し、数行のコードで文字を取り出すことができるということです。

この **aspose ocr tutorial** では、OCR 用に画像をロードし、エンジンに検索させる矩形領域を設定し、抽出したテキストを読み取るまでの手順をすべて解説します。最後には、ROI（Region of Interest）テキストをコンソールに出力する実行可能な Java プログラムが完成します。謎はなく、明確で動作するソリューションです。

## 必要なもの

本格的に取り組む前に、以下の環境が整っていることを確認してください。

| 前提条件 | 必要な理由 |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR は Java ライブラリとして提供されており、最新の JDK があれば動作します。 |
| **Aspose.OCR for Java**（Aspose のウェブサイトからダウンロードするか Maven で追加） | `OcrEngine`、`ImageStream` などのクラスを提供します。 |
| **画像ファイル**（例: `receipt.jpg`）で、印字可能なテキストが含まれているもの | エンジンがこのファイル内の矩形領域を対象に処理します。 |
| **IDE またはエディタ**（IntelliJ、Eclipse、VS Code など） | サンプルをすぐにコンパイル・実行できるようにします。 |

Maven を使用している場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **プロのコツ:** 上記のバージョン番号は 2026 年 2 月時点の最新です。最新リリースに更新すると、バグ修正やパフォーマンス向上が得られます。

## Step 1 – OCR エンジンの初期化

まず最初に `OcrEngine` のインスタンスが必要です。これはピクセルを解析する「脳」のようなものです。

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

なぜこのように作成するのか？Aspose はエンジン（設定を保持）と画像データを分離しているため、同じエンジンを複数の画像で再利用できる柔軟性があります。

## Step 2 – OCR 用に画像をロード

次に **load image for OCR** を実行します。`ImageStream.fromFile` ヘルパーは、Aspose が理解できるストリームにファイルを読み込みます。

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

ファイルが見つからない場合は例外がスローされるので、実運用コードでは try‑catch でラップすることを推奨します。このデモでは例外をそのまま上位へ伝播させ、サンプルをシンプルに保っています。

## Step 3 – 矩形領域の定義（Read Text from Rectangle）

ここが **read text from rectangle** のポイントです。エンジンに「ここを見て」と正確に指示することで、処理速度が上がり誤認識が減ります。

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **なぜ矩形か？**  
> 多くの文書はレイアウトが決まっており、たとえばレシートでは金額が必ず下部に表示されます。その領域だけに注目すれば、不要な画像情報を無視でき、認識精度が向上します。

**エッジケース:** 矩形が画像の範囲を超えると、Aspose は自動的にクランプしますが、データが失われます。事前にチェックすることで回避できます。

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Step 4 – 画像の処理

すべての設定が完了したら、エンジンに処理を実行させます。

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

`process()` 呼び出しは `OcrResult` オブジェクトを返し、抽出されたテキストや信頼度スコア、必要に応じて各単語のバウンディングボックスも保持します。

## Step 5 – 抽出テキストの出力

最後に結果をコンソールに出力します。実際のアプリではデータベースに保存したり、別サービスに渡したりすることもありますが、このチュートリアルではコンソール出力で十分です。

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**期待される出力**（レシートの合計金額を矩形で捕捉した場合）:

```
ROI text:
$12.34
```

ROI が空だったり画像がぼやけていると、空文字列や文字化けが出力されます。その場合は矩形を調整するか、画像品質を向上させるか、Aspose の前処理オプション（例: `setAutoSkewCorrection(true)`）を有効にしてください。

## 完全動作サンプル

以下が実行可能な完全プログラムです。`RoiDemo.java` という名前で保存し、画像パスを調整したうえで `javac RoiDemo.java && java RoiDemo` を実行してください。

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **結果の検証:** 実行後、コンソール出力が矩形領域内の実際のテキストと一致すれば、Aspose OCR を使って **extract text from image** に成功したことになります。

## よくある質問とヒント

### 同じ画像で複数の ROI を処理したい場合は？
各領域ごとに新しい `Rectangle` を作成し、`setRegionOfInterest` を再度呼び出してから `process()` を実行します。画像データは再利用されるため、パフォーマンスは高いままです。

### 異なる言語やフォントに対応するには？
`ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` で言語モデルを切り替えられます。ラテン文字以外の場合は、Aspose のダウンロードページから該当言語パックを取得してロードしてください。

### PDF 入力はサポートされていますか？
はい。Aspose OCR は PDF ストリームを直接受け取れます。`ImageStream.fromFile` を `ImageStream.fromPdfFile("doc.pdf")` に置き換え、必要に応じてページ番号を指定してください。

### 低品質スキャンの精度を上げるには？
前処理を有効にします。

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

これらのオプションはノイズ除去や文字の整列を行い、認識前に画像をクリーンアップします。

## 結論

本稿では **aspose ocr tutorial** として、Java で **extract text from image**、**load image for OCR**、**read text from rectangle** を実現する手順をすべて解説しました。重要なステップはエンジンの初期化、画像の投入、関心領域の設定、処理の実行、結果の出力です。

ここからさらに進められるアイデア:

* **バッチ処理** – フォルダ内のレシートをループで走査し、各合計金額をデータベースに保存。  
* **動的 ROI 検出** – OpenCV などの画像処理ライブラリを使ってテキストブロックを自動検出。  
* **後処理** – 正規表現やファジーマッチングで OCR のゆらぎを補正。

ぜひこれらのアイデアを試し、矩形を自分の文書に合わせて調整し、堅牢なテキスト抽出パイプラインをすぐに構築してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}