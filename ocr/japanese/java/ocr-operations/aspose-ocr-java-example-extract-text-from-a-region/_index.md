---
category: general
date: 2026-05-03
description: Aspose OCR Java のサンプルは、画像を OCR 用に読み込み、数行のコードで領域からテキストを抽出する方法を示しています。
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: ja
og_description: Aspose OCR Java のサンプルは、画像を OCR 用に読み込み、特定の領域からテキストを抽出する方法を示し、請求書処理に最適です。
og_title: Aspose OCR Java の例 – 領域テキスト抽出
tags:
- Aspose OCR
- Java
- Image Processing
title: Aspose OCR Java の例：領域からテキストを抽出する
url: /ja/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java の例: 領域からテキストを抽出する

画像から必要な部分だけを取得できる **Aspose OCR Java example** をお探しですか？このガイドでは **loading an image for OCR** と **extracting text from a region** の手順を解説します。請求書番号やフォームフィールド、または大きな画像の中に隠れたデータの抽出に最適です。

OCR をページ全体ではなく矩形に限定する理由が気になるかもしれません。簡潔に言えば、速度と精度です。エンジンが定義されたスライスだけを見ることで、不要なノイズをスキップし、処理が速くなり、よりクリーンな結果が得られます。このチュートリアルの最後までに、まさにそれを実現する自己完結型の Java プログラムが手に入り、初心者が陥りやすい落とし穴を回避するためのヒントもいくつか得られます。

## 必要なもの

- **Java Development Kit (JDK) 11** 以上がインストールされていること。
- **Aspose.OCR for Java** ライブラリ（Maven Central リポジトリまたは Aspose ダウンロードポータルから最新の JAR を取得できます）。
- 読み取り対象のテキストを含む画像ファイル – デモでは `invoice.png` を使用します。この画像は右上付近に請求書番号が配置されています。
- お好みの IDE またはシンプルなテキストエディタとターミナル；任意のビルドツール（Maven、Gradle、またはプレーンな `javac`）で構いません。

それだけです。余計な OCR エンジンやネイティブバイナリは不要で、純粋に Java と Aspose だけです。

![Aspose OCR Java の例 スクリーンショット](/images/aspose-ocr-java-example.png "領域抽出を示す Aspose OCR Java の例")

## Aspose OCR Java の例 – OCR エンジンの初期化

任意の OCR ワークフローで最初に必要なのはエンジンインスタンスです。Aspose は画像の読み込みから言語選択までをすべて処理する軽量な `OcrEngine` クラスを提供しています。

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Why this matters:** エンジンを事前に作成しておくことで、設定すべきクリーンなオブジェクトが得られます。バッチ処理で複数画像を扱う場合、同じ `OcrEngine` を再利用できるため、メモリと初期化時間を節約できます。

## OCR 用画像の読み込み

次にエンジンにスキャン対象の画像を指示します。Aspose は低レベルな `FileInputStream` のボイラープレートを抽象化した `ImageStream.fromFile` ヘルパーを提供しています。

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tip:** `YOUR_DIRECTORY` を `invoice.png` を保存した絶対パスまたは相対パスに置き換えてください。ファイルが見つからない場合、Aspose は `IOException` をスローするため、実装時には try‑catch でラップすることを検討してください。

## 領域を定義してテキストを抽出する

ここが本題です。エンジンに「どこを見るか」を指示する矩形です。`java.awt.Rectangle` コンストラクタは `(x, y, width, height)` を受け取り、すべてピクセル単位で指定します。

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**How it works:** `setRegion` を呼び出すことで、左端から 120 ピクセル、上端から 250 ピクセルの位置に幅 300 ピクセルのスライスに OCR スキャンを限定します。自分のレイアウトに合わせて数値を調整してください。ピクセル座標を表示できる任意の画像エディタで確認すると簡単です。

## 言語を有効化して認識を実行する

Aspose OCR は多数の言語をサポートしていますが、請求書番号の抽出には英語だけで十分です。適切な言語だけを有効にすることで、誤検出を大幅に減らせます。

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Why enable English only?** OCR エンジンは有効化されたすべての言語セットから文字を照合しようとするため、単純な英数字だけの場合は混乱の原因になります。言語範囲を絞ることで速度と精度の両方が向上します。

### 期待される出力

すべてが正しく設定されていれば、次のような出力が得られます。

```
Extracted region text: INV-12345
```

矩形が数ピクセルずれていると、出力が乱れたり空になることがあります。簡単な動作確認として、プログラムを実行しコンソールを確認、画像に表示されているテキストと一致しているかを確かめてください。

## コードを実行して出力を確認する

Maven を使用している前提で、`pom.xml` に Aspose OCR の依存関係を追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

コンパイルして実行:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

あるいはプレーンな `javac` を使う場合:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

コンソールに **Extracted region text** 行が表示されるはずです。もし “OCR recognition failed” と表示されたら、ファイルパスを再確認し、矩形が実際に読み取り可能な文字を含んでいるか確認してください。

## エッジケースと一般的なバリエーション

| 状況 | 変更点 |
|-----------|----------------|
| **Multiple languages** (e.g., English + Spanish) | Call `ocrEngine.getLanguage().setSpanish(true);` alongside English. |
| **Region outside image bounds** | Aspose will silently clip the rectangle, but you’ll lose data. Use `ImageInfo` (`ocrEngine.getImage().getWidth()`) to verify dimensions before setting the region. |
| **Dynamic invoices** (different layouts) | Consider running a lightweight pre‑scan on the whole image to locate keywords like “Invoice #” and then compute the rectangle programmatically. |
| **Higher DPI images** | Increase `ocrEngine.getImage().setResolution(300);` for better accuracy on scanned documents. |
| **Performance tuning** | Disable unnecessary languages, keep the region as small as possible, and reuse a single `OcrEngine` instance across many files. |

## 現場からのプロティップス

- **Pro tip:** If you only need digits (common for invoice numbers), enable the numeric mode with `ocrEngine.getLanguage().setDigits(true);`. This eliminates alphabetic noise.
- **Watch out for:** Transparent PNGs. Aspose sometimes misinterprets the alpha channel; converting the image to a solid‑background JPEG first can solve odd blank outputs.
- **Remember:** The rectangle uses the image’s native coordinate system, not any UI scaling you might see on screen. Always test with the exact file you’ll process in production.

## 次にやることは？

これで領域ベース抽出のための堅実な **Aspose OCR Java example** が手に入りました。以下のような方向で拡張できます：

- **Batch processing:** Loop over a folder of invoices, reusing the same `OcrEngine` to improve throughput.
- **Data validation:** Pipe the extracted text through a regex like `INV-\\d{5}` to ensure you captured a valid invoice number.
- **Integration with PDF:** Use Aspose.PDF to overlay the extracted text back onto the original document for audit trails.
- **Cloud deployment:** Wrap the code in a lightweight REST service (Spring Boot) so other systems can call it on demand.

これらのステップはすべて同じコア概念—**load image for OCR**、**extract text from a region**、結果の処理—に基づいているため、移行はスムーズです。

---

*Happy coding! If you hit any snags, drop a comment below or check the Aspose forums where the community shares real‑world tweaks for tricky layouts.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}