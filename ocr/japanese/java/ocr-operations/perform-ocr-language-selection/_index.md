---
date: 2026-02-12
description: Aspose.OCR for Java を使用して、言語選択付きの画像テキスト OCR の方法を学びましょう。このステップバイステップガイドでは、Java
  でのテキスト抽出、OCR の歪み補正などを取り上げています。
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR を使用して言語別に画像テキストを OCR する方法
url: /ja/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 言語指定で画像テキストを OCR する方法（Aspose.OCR 使用）

## はじめに

画像ファイルからテキストを抽出することは、スキャンした文書のデジタル化、レシートの処理、検索可能なアーカイブの構築など、さまざまなシナリオで一般的な要件です。このチュートリアルでは、**画像テキストを OCR する**方法を、特定の言語設定とともに実装する完全なハンズオン例を紹介します。これにより、Java アプリケーションに信頼性の高い OCR をすぐに組み込めます。また、OCR の傾き補正や領域ベースの認識方法も併せて解説し、精度を最大化します。

## クイック回答
- **Java で OCR を扱うライブラリは？** Aspose.OCR for Java  
- **言語を選択する設定は？** `settings.setLanguage(Language.Eng)`（またはサポートされている任意の言語）  
- **開発時にライセンスは必要？** 無料評価ライセンスでテスト可能。商用利用には製品ライセンスが必要です。  
- **画像の一部だけを OCR したい？** はい、`RecognitionSettings.setRecognitionAreas()` に矩形を指定します。  
- **典型的な実行時間は？** 画像サイズや言語の複雑さにもよりますが、標準的なノートPCでページあたり数秒程度です。

## 言語選択で画像テキストを OCR する方法
このセクションでは、テキストの言語が分かっている場合の **画像 OCR のやり方** を解説します。正しい言語を指定すると、OCR エンジンが言語固有の辞書や文字モデルを利用できるため、認識精度が大幅に向上します。

### なぜ重要か
- **精度向上** – 言語固有モデルにより誤認識が減少します。  
- **パフォーマンス向上** – 不要な言語チェックをスキップできるため高速化します。  
- **アクセント文字の正確な処理** – フランス語、スペイン語、ドイツ語など、該当する `Language` 列挙体を使用すれば正しく認識されます。

## 「画像からテキストを抽出する」とは？
画像からテキスト（OCR）を抽出するとは、文字のビジュアル表現を機械が読み取れる文字列に変換することです。これにより、検索、分析、データ抽出といったワークフローを手作業の文字起こしなしで実現できます。

## Aspose.OCR を言語選択付きで使うメリット
- **多言語対応** – 画像に含まれる正確な言語を指定して精度を向上させられます。  
- **細かな制御** – 傾き補正、認識領域の指定、オートスキュー動作の設定が可能です。  
- **純粋な Java API** – ネイティブ依存がなく、任意の Java プロジェクトに簡単に統合できます。  
- **豊富な結果データ** – プレーンテキスト、JSON、バウンディング矩形、警告情報を一度の呼び出しで取得できます。

## 前提条件

開始する前に以下を用意してください。

- **Java Development Kit (JDK)** がインストール済み（JDK 8 以上）。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトから[こちら](https://reference.aspose.com/ocr/java/)でダウンロード。  
- テキスト抽出対象の画像ファイル（例: `p3.png`）。

## パッケージのインポート

Java ソースファイルで必要な Aspose.OCR クラスと標準 Java ユーティリティをインポートします。

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

## 手順ガイド

### 手順 1: ドキュメントディレクトリを設定

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` を `p3.png` が格納されている絶対パスに置き換えてください。

### 手順 2: 画像パスを定義

```java
// The image path
String file = dataDir + "p3.png";
```

`file` 変数が処理したい画像を正しく指していることを確認します。

### 手順 3: Aspose.OCR API インスタンスを作成

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` オブジェクトを通じてすべての OCR 操作にアクセスできます。

### 手順 4: 認識オプションを設定（言語選択）

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

ここで行っていること：

1. 手動で傾き値を指定するため、オートスキューを無効化。  
2. 矩形領域（`RecognitionAreas`）を定義し、テキストが実際に存在する部分だけを OCR 対象に限定。  
3. **言語** を英語（`Language.Eng`）に設定。画像に合わせて `Language.Fra`、`Language.Spa` などに変更してください。

### 手順 5: OCR を実行し結果を取得

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 呼び出しにより、画像と設定に基づいて OCR エンジンが実行されます。結果は `RecognitionResult` オブジェクトに格納されます。

### 手順 6: 結果を出力・活用

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

コンソール出力例：

- 完全抽出テキスト（`recognitionText`）。  
- 各矩形領域ごとのテキスト（`recognitionAreasText`）。  
- バウンディング矩形の座標。  
- 後続処理がしやすい JSON 表現。  
- 検出された傾き角度と警告情報。

取得した `result.recognitionText` をビジネスロジックに組み込んで、保存・インデックス化・他サービスへの送信などに活用できます。

## よくある問題と対策

| 問題 | 原因 | 対策 |
|------|------|------|
| **文字化け** | 言語設定が誤っている | 正しい `Language` 列挙体（例: フランス語は `Language.Fra`）を設定 |
| **テキストが取得できない** | 認識領域がテキストをカバーしていない | `Rectangle` の座標を調整するか、`RecognitionAreas` を削除して画像全体を処理 |
| **処理が遅い** | 画像が非常に大きい・高解像度 | OCR 前に画像を縮小するか、JVM のメモリ割り当てを増やす |
| **未対応フォーマットの警告** | 画像形式が認識できない | PNG、JPEG、TIFF などサポート形式に変換してから処理 |

## FAQ

**Q: 1 回の OCR 呼び出しで複数言語を認識できますか？**  
A: はい。`settings.setLanguage(Language.Eng | Language.Fra)` のようにビット演算で複数言語を指定してマルチリンガル認識が可能です。

**Q: Aspose.OCR がサポートする画像形式は？**  
A: PNG、JPEG、BMP、TIFF、GIF など多数。正しいファイルパスを指定すれば自動で判別します。

**Q: 画像サイズに上限はありますか？**  
A: 明確な上限はありませんが、非常に大きな画像はメモリ使用量と処理時間が増大します。必要に応じてリサイズしてください。

**Q: 本番環境用のライセンスはどう取得しますか？**  
A: Aspose の公式サイトでライセンスを購入し、Aspose のドキュメントに示された通り `License` クラスで適用します。

**Q: PDF ページから直接テキストを抽出できますか？**  
A: Aspose.OCR だけでは直接はできません。まず Aspose.PDF などで PDF ページを画像に変換し、その画像を OCR にかけてください。

## 結論

本稿で、Aspose.OCR for Java を用いて **画像からテキストを抽出** し、適切な言語を選択しつつ認識領域を限定する方法を学びました。この手法により、高精度・高性能な OCR を任意の Java ベースワークフローに組み込めます。次のステップとして、言語列挙体を変更したり、認識領域を調整したりして実験し、結果を自アプリケーションのロジックに統合してみてください。

---

**最終更新日:** 2026-02-12  
**テスト環境:** Aspose.OCR 24.11 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}