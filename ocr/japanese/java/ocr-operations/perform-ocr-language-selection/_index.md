---
date: 2025-12-13
description: 言語選択を使用して、Aspose.OCR for Javaで画像からテキストを抽出する方法を学びましょう。このステップバイステップのAspose
  OCR Javaチュートリアルでは、正確なOCR設定を示します。
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR を使用した言語選択付き画像からのテキスト抽出方法
url: /ja/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR を使用した言語選択付き画像からテキストを抽出する方法

## Introduction

画像ファイルからテキストを抽出することは、スキャンした文書のデジタル化、レシートの処理、検索可能なアーカイブの構築など、さまざまな場面で一般的な要件です。Aspose.OCR for Java を使用すれば、この作業はシンプルになり、言語選択、傾き補正、認識領域の細かい制御が可能です。このチュートリアルでは、**画像からテキストを抽出する**方法を、特定の言語設定を使用した完全なハンズオン例で解説します。これにより、Java アプリケーションに信頼性の高い OCR をすぐに組み込めます。

## Quick Answers
- **Java で OCR を処理するライブラリは何ですか？** Aspose.OCR for Java  
- **どの設定で言語を選択しますか？** `settings.setLanguage(Language.Eng)`（またはサポートされている任意の言語）  
- **開発にライセンスは必要ですか？** 無料の評価ライセンスでテストは可能ですが、商用利用には商用ライセンスが必要です。  
- **画像の特定領域に OCR を限定できますか？** はい、`RecognitionSettings.setRecognitionAreas()` に矩形を指定します。  
- **典型的な実行時間はどれくらいですか？** 標準的なノートパソコンでページあたり数秒、画像サイズや言語の複雑さに依存します。

## What is “extract text from image”?
画像からテキストを抽出する（OCR）とは、文字の視覚的表現を機械が読める文字列に変換することです。これにより、検索、分析、データ抽出のワークフローが実現し、手作業での文字起こしが不要になります。

## Why use Aspose.OCR with language selection?
- **多言語サポート** – 画像に含まれる正確な言語を選択することで精度が向上します。  
- **細かな制御** – 傾きの調整、認識領域の定義、auto‑skew 動作の設定が可能です。  
- **純粋な Java API** – ネイティブ依存がなく、任意の Java プロジェクトに簡単に統合できます。  
- **豊富な結果データ** – 1 回の呼び出しでプレーンテキスト、JSON、バウンディング矩形、警告情報が取得できます。  

## Prerequisites

開始する前に、以下が揃っていることを確認してください：

- **Java Development Kit (JDK)** がインストールされていること（JDK 8 以上）。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトからダウンロードしてください [here](https://reference.aspose.com/ocr/java/)。  
- 抽出したいテキストを含む画像ファイル（例: `p3.png`）。

## Import Packages

In your Java source file, include the required Aspose.OCR classes and standard Java utilities:

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

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

「Your Document Directory」を、`p3.png` が存在する絶対パスに置き換えてください。

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

`file` 変数が処理したい画像を正確に指していることを確認してください。

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` オブジェクトは、すべての OCR 操作にアクセスするためのインスタンスです。

### Step 4: Set Recognition Options (Language Selection)

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

ここでは次の設定を行います：

1. 手動で傾き値を指定するため、auto‑skew を無効にします。  
2. 矩形領域（`RecognitionAreas`）を定義し、実際にテキストが含まれる画像部分に OCR を限定します。  
3. **言語** を英語（`Language.Eng`）に設定します。画像の言語に応じて `Language.Fra`、`Language.Spa` などに変更してください。

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 呼び出しは、指定した画像と設定で OCR エンジンを実行します。結果は `RecognitionResult` オブジェクトに格納されます。

### Step 6: Print and Utilize Results

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

コンソール出力には以下が表示されます：

- 完全な抽出テキスト（`recognitionText`）。  
- 各矩形領域ごとのテキスト（`recognitionAreasText`）。  
- バウンディング矩形の座標。  
- 後続処理が容易な JSON 表現。  
- 検出された傾き角度と警告情報。

これで `result.recognitionText` をビジネスロジックに組み込めます — 保存、インデックス作成、または他のサービスへの渡しなどが可能です。

## Common Issues and Solutions

| 問題 | 原因 | 対策 |
|-------|-------|-----|
| **文字化け** | 言語が誤って選択されている | 正しい `Language` 列挙体を設定する（例: フランス語は `Language.Fra`）。 |
| **テキストが返らない** | 認識領域がテキストをカバーしていない | `Rectangle` の座標を調整するか、`RecognitionAreas` を削除して画像全体を処理する。 |
| **パフォーマンスが遅い** | 画像が非常に大きい、または解像度が高い | OCR 前に画像を縮小するか、JVM のメモリ割り当てを増やす。 |
| **未対応フォーマットの警告** | 画像フォーマットが認識されない | 処理前に画像を PNG、JPEG、または TIFF に変換する。 |

## Frequently Asked Questions

**Q: 1回の OCR 呼び出しで複数言語を認識できますか？**  
A: はい。`settings.setLanguage(Language.Eng | Language.Fra)` のように設定して多言語認識を有効にします。

**Q: Aspose.OCR がサポートする画像フォーマットは何ですか？**  
A: PNG、JPEG、BMP、TIFF、GIF など多数。正しいファイルパスを指定すれば利用できます。

**Q: 画像サイズに制限はありますか？**  
A: 明確な上限はありませんが、非常に大きな画像はメモリ使用量と処理時間が増加します。大きなファイルはリサイズすることを検討してください。

**Q: 本番用ライセンスはどう取得しますか？**  
A: Aspose のウェブサイトでライセンスを購入し、Aspose のドキュメントに示されているように `License` クラスで適用します。

**Q: PDF ページから直接テキストを抽出できますか？**  
A: Aspose.OCR だけでは直接はできません。まず PDF ページを画像に変換（例: Aspose.PDF を使用）し、その後 OCR を実行してください。

## Conclusion

これで、Aspose.OCR for Java を使用し、適切な言語を選択しつつ特定領域に限定して **画像からテキストを抽出する**方法が理解できました。この手法は、高精度・高性能な OCR を提供し、ドキュメント管理システムからデータキャプチャパイプラインまで、あらゆる Java ベースのワークフローに組み込むことが可能です。

---

**最終更新日:** 2025-12-13  
**テスト環境:** Aspose.OCR 24.11 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}