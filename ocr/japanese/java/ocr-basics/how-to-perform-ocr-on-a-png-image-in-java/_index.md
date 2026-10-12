---
category: general
date: 2026-10-11
description: JavaでPNG画像に対してOCRを実行し、画像からテキストを抽出し、シンプルなOcrEngineの例で画像をテキストに変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: ja
lastmod: 2026-10-11
og_description: JavaでPNG画像にOCRを実行し、画像からテキストを抽出してテキストに変換する、簡潔で即実行可能なサンプル。
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: JavaでPNG画像にOCRを実行する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: JavaでPNG画像のOCRを行う方法
url: /ja/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでPNG画像のOCRを実行する方法

画像ファイルに対して **OCR を実行** する必要がある場合、Javaで **OCR を実行** する方法を学ぶことは多くの自動化タスクで不可欠です。領収書のデジタル化、スキャンした文書のインデックス作成、検索可能な写真アーカイブの構築など、 **画像からテキストを抽出** できることで、膨大な手作業の時間を削減できます。

このチュートリアルでは、PNG を読み込み、OCR エンジンを実行し、 **PNG からテキストを認識** する完全な実行可能ソリューションを示します。また、 **画像をテキストに変換** する方法や、低解像度入力や非 ASCII 文字といった一般的な落とし穴への対処方法も解説します。

## 何ができるようになるか

このガイドを最後まで読むと、以下ができるようになります。

* ディスクから PNG を読み込む **load image java** コード
* 軽量な OCR エンジンの初期化
* **画像からテキストを抽出** し、コンソールに結果を出力
* 他の画像形式やバッチ処理への適用方法のカスタマイズ

外部サービスは不要です。オープンソースの OCR ライブラリ（Tess4J）と Java SE ランタイムだけで完結します。

---

## 前提条件

* Java 17 以上（コードは JDK 17 でコンパイル可能）
* 依存関係管理に Maven または Gradle
* コマンドラインとお好みの IDE の基本的な操作に慣れていること
* `tess4j` ライブラリ（Tesseract の Java ラッパー）。以下の Maven 依存を追加してください。

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Gradle を使用する場合は、同等の設定は次のとおりです。

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

また、Tesseract のデータファイル（`.traineddata`）が必要です。公式リポジトリから英語データパックをダウンロードし、プロジェクトルートに `tessdata` というフォルダを作成して配置してください。

---

## 手順 1: Java で画像を読み込む

標準の `ImageIO` クラスを使えば PNG の読み込みは簡単です。以下のコードは **load image java** を安全に、例外に配慮した形で実装した例です。

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**ポイント:** `ImageIO.read` は画像フォーマットを自動検出しますが、PNG が破損している場合に `null` が返ることを明示的にチェックして、サイレント失敗を防いでいます。このパターンは **load image java** を OCR に利用する際のベストプラクティスです。

---

## 手順 2: OCR エンジンの初期化

Tess4J はネイティブの Tesseract バイナリをラップし、シンプルな Java API を提供します。次のメソッドは `Tesseract` インスタンスを生成し、`tessdata` フォルダを指すように設定し、言語を英語に構成します。

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**理由:** エンジンを一度だけ初期化して複数画像で再利用することで、起動オーバーヘッドを削減できます。`setOcrEngineMode` の呼び出しはデフォルトモードを選択し、ほとんどの PNG でうまく機能します。ノイズが多いスキャンの場合は、他のモード（例: `OEM_LSTM_ONLY`）を試すことができます。

---

## 手順 3: OCR を実行し **PNG からテキストを認識**

ここで画像ローダーと OCR エンジンを組み合わせます。以下のメソッドは `BufferedImage` に対して OCR を実行し、抽出した文字列を返します。

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**完全な実行可能サンプル**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**期待される出力**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

コンソールには `sample.png` からエンジンが抽出した文字がそのまま表示されます。PNG に単語が1つだけ含まれている場合、出力はその単語と改行だけになります。

---

## 手順 4: よくあるバリエーションとエッジケース

### 4.1 低解像度 PNG の扱い方

Tesseract は最低でも 300 DPI の画像で最良の結果を出します。元の PNG が小さい場合は、OCR 前に拡大してください。

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

`extractText` を呼び出す前に `upscale(image, 2)` を適用すると精度が向上します。

### 4.2 非英語テキストの抽出

**画像からテキストを抽出** する対象が他言語の場合、該当する `.traineddata` をダウンロードし、言語コードを設定します。

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 複数 PNG のバッチ処理

フォルダ内の **PNG からテキストを認識** する必要がある場合は、ディレクトリを走査します。

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 OCR エラーへの対処

典型的な OCR の誤認識例として、`0`（ゼロ）を `O` と読んだり、`1` を `l` と読んだりします。正規表現を使った後処理で結果をクリーンアップできます。

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Java で信頼性の高い OCR を実現するプロのコツ

| コツ | 理由 |
|-----|------|
| **ロスレス PNG を使用** | JPEG の圧縮アーティファクトがエンジンを混乱させることがあります。 |
| **余白をトリミング** | 不要な白領域は処理時間を増やし、誤検出の原因になることがあります。 |
| **`tesseract.setPageSegMode(ITesseract.PSM_AUTO)` はレイアウトが不明なときだけ使用**; それ以外は特定モード（例: `PSM_SINGLE_BLOCK`）を選択 |
| **`ITesseract` インスタンスをキャッシュ** | 再利用でパフォーマンス向上 |

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Java で Aspose OCR を使用して画像からテキストを読み取る方法 – 完全ガイド](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Java で OCR を使用する方法 – 画像からテキストを素早く認識](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Java でバッチ画像 OCR – PNG ファイルからテキストを高速抽出](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}