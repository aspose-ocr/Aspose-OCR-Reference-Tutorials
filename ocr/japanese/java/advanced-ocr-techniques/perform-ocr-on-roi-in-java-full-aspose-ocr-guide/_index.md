---
category: general
date: 2026-06-19
description: Aspose OCR を使用して Java で ROI の OCR を実行します。ステップバイステップのコードとベストプラクティスで、領域内のテキスト認識方法を学びましょう。
draft: false
keywords:
- perform OCR on ROI
- recognize text in region
- Aspose OCR Java
- OCR region detection
- Java image processing
language: ja
og_description: Aspose OCR を使用して Java で ROI の OCR を実行します。このガイドでは、領域内のテキストを認識する方法、複数言語に対応する方法、そして一般的な落とし穴を回避する方法を示します。
og_title: JavaでROI上のOCRを実行 – 完全なAspose OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  headline: Perform OCR on ROI in Java – Full Aspose OCR Guide
  type: TechArticle
- description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  name: Perform OCR on ROI in Java – Full Aspose OCR Guide
  steps:
  - name: 1. License Path Errors
    text: If `setLicense` throws a `FileNotFoundException`, double‑check the absolute
      path or place the `.lic` file in the project’s resources folder and load it
      with `getResourceAsStream`.
  - name: 2. Overlapping or Out‑of‑Bounds ROIs
    text: Aspose does not automatically clip ROIs that extend beyond the image dimensions.
      Overlapping rectangles can cause duplicated text. Use `engine.getImageSize()`
      to verify bounds before creating rectangles.
  - name: 3. Unsupported Languages
    text: Attempting to set a language not bundled with the library will raise `UnsupportedOperationException`.
      Stick to the languages listed in Aspose’s documentation, or download the additional
      language packs.
  - name: 4. Low‑Resolution Images
    text: OCR accuracy drops dramatically below 100 dpi. If you have a low‑resolution
      scan, consider up‑scaling with a library like **Imgscalr** before feeding it
      to Aspose.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Recognition
title: JavaでROI上のOCRを実行する – 完全なAspose OCRガイド
url: /ja/java/advanced-ocr-techniques/perform-ocr-on-roi-in-java-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでROIに対してOCRを実行 – 完全な Aspose OCR チュートリアル

画像全体をスキャンせずに **ROI に対して OCR を実行** したいと思ったことはありませんか？開発者からは「請求書のテーブル部分だけを抽出したいが、画像全体をスキャンしたくない」という質問が頻繁に寄せられます。このガイドでは、Aspose OCR を使用して **ROI に対して OCR を実行** する方法をステップバイステップで解説し、さらに異なる言語が隣り合う場合の **領域内テキスト認識** の方法も紹介します。

ポイントは次のとおりです。特定の矩形（ROI）を対象にすると処理時間が短縮され、ノイズが減り、結果がクリーンになることが多いです。多言語のレシート、フォーム、スキャンした契約書などを扱う場合、ROI ベースの OCR をマスターすることは大きなアドバンテージになります。さっそく始めましょう。

## 必要なもの

開始する前に以下を用意してください。

- **Java 8+**（任意の最新 JDK で動作します）
- **Aspose.OCR for Java** ライブラリ（Aspose のサイトからダウンロードするか、Maven で追加）
- 有効な **Aspose OCR ライセンス** ファイル（`Aspose.OCR.lic`）– デモはライセンスなしでも動作しますが、透かしが入ります。
- 処理したい領域がはっきりした画像（例：ヘッダーとフランス語テーブルがある請求書）

以上だけです。余計なフレームワークや重い依存関係は不要です。IntelliJ IDEA や Eclipse といった基本的な IDE が使える環境であればすぐに始められます。

## Perform OCR on ROI – エンジンのセットアップ

まず OCR エンジンを初期化し、デフォルトで使用する言語を設定します。ここから **ROI に対して OCR を実行** するワークフローが本格的に始まります。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

> **プロのコツ:** ライセンス設定を忘れると Aspose は動作しますが、出力に「Evaluation」透かしが入ります。テストには問題ありませんが、本番環境では必ず設定してください。

## 認識したい領域を定義する

次に、画像の中で関心のある部分を表す矩形を作成します。各 `Rectangle` はエンジンに「ここを見て」と指示する **クロップボックス** と考えてください。

```java
        // Step 2: Create an OCR engine and set the default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Step 3: Define the regions (ROIs) you want to recognize
        // Header region (top part of the image)
        Rectangle header = new Rectangle(0, 0, 1200, 200);
        // Table body region (below the header)
        Rectangle table = new Rectangle(0, 210, 1200, 800);
```

**perform OCR on ROI** という用語は暗黙的に使用されています—各 `Rectangle` が ROI です。座標は自分の文書レイアウトに合わせて調整してください。`header` 矩形は上部バナーを、`table` 矩形は後で **領域内テキスト認識** を行う本文部分をキャプチャします。

## 領域を追加し、領域ごとの言語を設定する

Aspose OCR では領域ごとに言語を割り当てられるため、多言語文書に最適です。ここではヘッダーは英語、テーブルはフランス語に設定します。

```java
        // Step 4: Add the regions to the engine
        engine.addRegion(header);                     // uses default language (English)
        engine.addRegion(table, Language.French);    // optional per‑region language
```

単一言語だけで良い場合は第2引数を省略できます。エンジンは事前に設定したデフォルト言語に自動的にフォールバックします。

## Perform OCR on ROI を実行し、結合テキストを取得する

最後に画像全体に対して OCR を実行しますが、処理されるのは定義した ROI のみです。結果は領域を追加した順にテキストが連結されるため、後処理がシンプルになります。

```java
        // Step 5: Perform OCR on the image and retrieve the combined text
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");
        System.out.println(result.getText()); // text from all defined regions in order
    }
}
```

**期待される出力**（簡略表示）:

```
Invoice #12345
Date: 2026‑06‑01
...
Produit   Quantité   Prix
Café      2          5,00 €
...
```

最初のブロックは英語のヘッダー、2番目はフランス語のテーブルから取得されたものです。**領域内テキスト認識** が混在言語で正しく機能している典型例です。

## よくある落とし穴の対処法

シンプルな **perform OCR on ROI** フローでも、隠れた問題に引っかかることがあります。以下に最も頻出する問題と回避策をまとめました。

### 1. ライセンスパスエラー

`setLicense` が `FileNotFoundException` を投げた場合は、絶対パスを再確認するか、`.lic` ファイルをプロジェクトの `resources` フォルダに置き、`getResourceAsStream` で読み込んでください。

```java
License license = new License();
license.setLicense(RoiDemo.class.getResourceAsStream("/Aspose.OCR.lic"));
```

### 2. 重複または画像範囲外の ROI

Aspose は画像サイズを超える ROI を自動でクリップしません。重複した矩形はテキストの重複抽出につながります。矩形を作成する前に `engine.getImageSize()` で画像サイズを取得し、範囲内か確認しましょう。

```java
Size imgSize = engine.getImageSize("YOUR_DIRECTORY/invoice.png");
if (header.getRight() > imgSize.getWidth()) {
    // Adjust width to stay inside the image
    header.setWidth(imgSize.getWidth() - header.getX());
}
```

### 3. 未対応言語

ライブラリに同梱されていない言語を設定しようとすると `UnsupportedOperationException` が発生します。Aspose のドキュメントに記載された言語のみ使用するか、追加の言語パックをダウンロードしてください。

### 4. 低解像度画像

解像度が 100 dpi 未満になると OCR 精度が大幅に低下します。低解像度のスキャン画像は、**Imgscalr** などのライブラリで拡大してから Aspose に渡すことを検討してください。

```java
BufferedImage src = ImageIO.read(new File("invoice.png"));
BufferedImage highRes = Scalr.resize(src, Scalr.Method.QUALITY, 300);
ImageIO.write(highRes, "png", new File("invoice_high.png"));
```

その後、`recognizeImage` の引数を `invoice_high.png` に変更します。

## 応用例：複数 ROI と動的検出

デモは静的な矩形を使用していますが、実務ではテーブルを自動検出したいことが多いでしょう。Aspose OCR とシンプルな **画像処理** ライブラリ（例：OpenCV）を組み合わせて輪郭を検出し、その境界を `engine.addRegion` に渡すことで、静的な **perform OCR on ROI** スクリプトを動的パイプラインに変換できます。

```java
// Pseudo‑code: Detect contours → create Rectangle objects → addRegion()
List<Rect> detected = OpenCVHelper.findTables("invoice.png");
for (Rect r : detected) {
    engine.addRegion(new Rectangle(r.x, r.y, r.width, r.height), Language.French);
}
```

これでピクセル値をハードコーディングせずに **領域内テキスト認識** が可能になり、バッチ処理に最適です。

## 完全動作サンプル（コピー＆ペースト用）

以下はそのまま実行できる完全版プログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えてください。

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply license (optional for evaluation)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Initialize engine with default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Define ROIs
        Rectangle header = new Rectangle(0, 0, 1200, 200);   // top banner
        Rectangle table  = new Rectangle(0, 210, 1200, 800); // body table

        // Add regions – per‑region language optional
        engine.addRegion(header);                     // English (default)
        engine.addRegion(table, Language.French);    // French for table

        // Run OCR on the image – only the defined ROIs are processed
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");

        // Output combined text
        System.out.println("--- OCR Result ---");
        System.out.println(result.getText());
    }
}
```

`javac RoiDemo.java && java RoiDemo` を実行します。すべて正しく設定されていれば、両領域から結合されたテキストがコンソールに表示されます。

## まとめ

本稿では Aspose OCR を使って **Java で ROI に対して OCR を実行** する方法を解説し、**領域内テキスト認識** を単一言語・多言語シナリオの両方で実現する手順を紹介しました。画像を論理的な矩形に分割することで、

1. 処理時間を短縮
2. 誤検出を削減
3. 言語選択を細かく制御

というメリットが得られます。ここからは動的 ROI 検出を試したり、結果をデータベースに保存したり、検索可能な PDF を生成したりと、応用の幅は無限です。ROI 座標の検証、ライセンスパスの管理、適切な言語パックの選択を忘れずに。

レイアウトが複雑でお困りですか？コメントやプルリクエストで改善案を共有してください。Happy coding、そして OCR が常に正確でありますように！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを踏まえてさらに深く学べる関連トピックです。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能や代替実装アプローチを自分のプロジェクトに取り入れる際に役立ちます。

- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}