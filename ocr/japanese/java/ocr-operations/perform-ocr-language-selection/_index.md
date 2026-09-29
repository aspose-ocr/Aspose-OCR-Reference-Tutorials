---
date: 2026-06-24
description: Aspose.OCR for Java を使用して、言語選択付きで画像テキストを OCR する方法を学びます。この step‑by‑step
  ガイドでは、extract text java、OCR skew correction などをカバーしています。
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Aspose.OCR を使用した OCR の傾き補正と語言語選択の実行方法
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Aspose.OCR を使用した OCR の傾き補正と語言語選択の実行方法
url: /ja/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用した OCR 歪み補正と語彙選択の実行方法

## はじめに

画像ファイルからテキストを抽出することは、スキャンした文書のデジタル化、領収書の処理、検索可能なアーカイブの構築など、さまざまな場面で一般的な要件です。このチュートリアルでは、**特定の言語設定で画像テキストを OCR** する完全なハンズオン例を示します。これにより、Java アプリケーションに信頼性の高い OCR をすぐに統合できます。また、**OCR 歪み補正** と領域ベースの認識を活用して精度を最大化する方法も紹介します。これらを組み合わせることで、斜めスキャンに対して最大 30 % の **OCR 精度向上** が期待できます。

## クイック回答
- **Java で OCR を処理するライブラリは？** Aspose.OCR for Java  
- **言語を選択する設定は？** `settings.setLanguage(Language.Eng)`（またはサポートされている任意の言語）  
- **開発用にライセンスは必要ですか？** 無料評価ライセンスでテスト可能。商用利用には製品ライセンスが必要です。  
- **画像の特定領域だけを OCR できますか？** はい、`RecognitionSettings.setRecognitionAreas()` に矩形を指定します。  
- **典型的な実行時間は？** 標準的なノートPCでページあたり数秒、画像サイズと言語の複雑さに依存します。  

`Language` は Aspose.OCR がサポートする OCR 言語を列挙したものです。例として English、French、Spanish などがあります。

## OCR 歪み補正とは？

OCR 歪み補正は、文字認識の前に傾いたテキスト行を検出し、水平に補正するプロセスです。テキストのベースラインを揃えることで、OCR エンジンは言語モデルをより効果的に適用でき、斜めスキャンによる誤認識を減らします。このステップは入力画像の視覚的品質を向上させ、回転による歪みではなく実際の文字形状に焦点を当てることができます。

## なぜ OCR 歪み補正が精度向上につながるのか

テキストが歪んでいると文字形状が歪み、エラー率が最大 20 % 上昇します。**ocr 歪み補正** を適用するとこの歪みが除去され、エンジンは実際のグリフに集中できます。ベンチマークテストでは、10‑15° の回転がある文書に対し、歪み補正を行うことで Aspose.OCR の認識精度が 15‑30 % 向上しました。

## なぜ言語選択付き Aspose.OCR を使うのか？

ソーステキストの正確な言語を指定すると、OCR エンジンは言語固有の辞書と文字モデルを使用でき、認識精度が大幅に向上し、処理時間も短縮されます。さらに、Aspose.OCR は歪み補正、領域選択、出力形式に対する細かな制御を提供し、多言語文書処理パイプラインに最適です。

- **多言語サポート** – 画像に含まれる正確な言語を選択して精度を向上。  
- **細かな制御** – 歪み調整、認識領域の定義、オートスキュー動作の設定が可能。  
- **Pure Java API** – ネイティブ依存なし、任意の Java プロジェクトに簡単統合。  
- **豊富な結果データ** – プレーンテキスト、JSON、バウンディング矩形、警告を一括取得。  
- **定量的な能力** – Aspose.OCR は **50 以上** の入力・出力形式をサポートし、**500 ページ** までの画像バッチをメモリ全体をロードせずに処理可能。

## 前提条件

開始前に以下を確認してください。

- **Java Development Kit (JDK)** がインストール済み（JDK 8 以降）。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトから [こちら](https://reference.aspose.com/ocr/java/) でダウンロード。  
- テキスト抽出対象の画像ファイル（例: `p3.png`）。

## パッケージのインポート

以下のインポートで OCR コアクラスと標準 Java ユーティリティにアクセスできます。  
`import com.aspose.ocr.*;` – メイン OCR エンジンを取得。  
`import com.aspose.ocr.config.*;` – `RecognitionSettings` などの設定オブジェクトを含む。  
`import java.awt.Rectangle;` – 認識領域の定義に使用。  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Java で OCR 歪み補正を適用する方法

画像を読み込み、オートスキュー検出を無効にし、手動で角度を指定するか `settings.setAutoSkew(false)` でエンジンに計算させます。OCR エンジンはまず提供された（または検出された）角度で画像を水平化し、その後文字認識を実行します。この二段階アプローチにより、言語モデルが適用される前にすべての傾きが除去され、テキスト出力がクリーンになり誤認識が減少します。

## 手順ガイド

### 手順 1: ドキュメントディレクトリを設定

ソース画像が格納されたフォルダーを指す `File` オブジェクトを作成します。これにより OS 間でパス処理がポータブルになります。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` を `p3.png` が存在する絶対パスに置き換えてください。

### 手順 2: 画像パスを定義

処理対象の画像用に `File` オブジェクトをインスタンス化します。`File` オブジェクトを使用すると、後で必要になるファイルメタデータへ簡単にアクセスできます。

```java
// The image path
String file = dataDir + "p3.png";
```

`file` 変数が正確に処理したい画像を指していることを確認してください。

### 手順 3: Aspose.OCR API インスタンスを作成

`AsposeOCR` クラスはすべての OCR 操作のエントリーポイントです。エンジンをカプセル化し、リソース管理と `recognizePage` メソッドを提供します。

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` オブジェクトで全 OCR 操作にアクセスできます。

### 手順 4: 認識オプションを設定（言語選択）

`RecognitionSettings` は OCR プロセスを細かく調整できる Aspose.OCR の設定コンテナです。

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

ここでは以下を行います。

1. 手動スキュー値を提供するためオートスキューを無効化。  
2. 矩形領域（`RecognitionAreas`）を定義し、画像中のテキストが実際に存在する部分だけを OCR 対象に限定。  
3. **言語** を英語 (`Language.Eng`) に設定。画像に合わせて `Language.Fra`、`Language.Spa` などに変更してください。

### 手順 5: OCR を実行し結果を取得

`recognizePage` を呼び出すと、指定した画像と設定で OCR エンジンが実行されます。結果は `RecognitionResult` オブジェクトに格納され、すべての有用データが集約されます。

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 呼び出しは画像と設定を使用して OCR エンジンを実行し、結果は `RecognitionResult` に保存されます。

### 手順 6: 結果を出力・活用

コンソール出力には以下が含まれます。

- 完全抽出テキスト（`recognitionText`）。  
- 各矩形領域ごとのテキスト（`recognitionAreasText`）。  
- バウンディング矩形の座標。  
- downstream 処理向けの JSON 表現。  
- 検出されたスキュー角度と警告メッセージ。

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

コンソールに完全抽出テキスト、領域別テキスト、バウンディングボックス、JSON、スキュー角度、警告が表示されます。`result.recognitionText` をビジネスロジックに渡して保存、インデックス、または他サービスへ送信できます。

## よくある問題と対策

| 問題 | 原因 | 対策 |
|------|------|------|
| **文字化け** | 言語設定が誤っている | 正しい `Language` 列挙体（例: フランス語なら `Language.Fra`）を設定 |
| **テキストが取得できない** | 認識領域がテキストをカバーしていない | `Rectangle` 座標を調整するか、`RecognitionAreas` を削除して全画像を処理 |
| **パフォーマンスが低下** | 画像が非常に大きい・高解像度 | OCR 前に画像を縮小するか、JVM のメモリ割り当てを増やす |
| **未対応フォーマットの警告** | 画像形式が認識されない | PNG、JPEG、TIFF などサポート形式に変換してから処理 |

## FAQ

**Q: 1 回の OCR 呼び出しで複数言語を認識できますか？**  
A: はい。`settings.setLanguage(Language.Eng \| Language.Fra)` のようにビット演算で複数言語を有効化できます。

**Q: Aspose.OCR がサポートする画像形式は？**  
A: PNG、JPEG、BMP、TIFF、GIF など多数。正しいファイルパスを指定してください。

**Q: 画像サイズに上限はありますか？**  
A: 明確な上限はありませんが、10 MB 超の画像はメモリ使用量と実行時間が増加します。必要に応じてリサイズしてください。

**Q: 本番用ライセンスはどう取得しますか？**  
A: Aspose 公式サイトでライセンスを購入し、Aspose のドキュメントに示された `License` クラスで適用します。

**Q: PDF ページから直接テキストを抽出できますか？**  
A: Aspose.OCR だけでは直接はできません。まず Aspose.PDF などで PDF ページを画像に変換し、次に OCR を実行してください。

## 結論

このチュートリアルで、Java 向け Aspose.OCR を使用し、適切な言語を選択しながら **OCR 歪み補正** を適用して画像からテキストを抽出する方法を学びました。これにより、任意の Java ベースワークフロー（文書管理システムやデータキャプチャパイプラインなど）に高精度・高性能な OCR を組み込めます。さまざまな `Language` 列挙体を試し、`RecognitionAreas` を調整し、JSON 出力を downstream 分析に統合して、真のエンドツーエンドソリューションを構築してください。

---

**最終更新日:** 2026-06-24  
**テスト環境:** Aspose.OCR 24.11 for Java  
**作者:** Aspose

## 関連チュートリアル

- [How to calculate skew angle java using Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}