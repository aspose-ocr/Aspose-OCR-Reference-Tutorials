---
date: 2026-06-19
description: Javaで画像をテキストに変換し、画像から段落を抽出し、Aspose OCR Javaライブラリを使用してテキスト領域の矩形を取得する方法を学びます。
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – 画像からテキストを認識し、テキスト領域の矩形を取得する
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – 画像をテキストに変換し、テキスト領域の矩形を取得する
url: /ja/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストへの変換 Java – 画像をテキストに変換しテキスト領域の矩形を取得

## はじめに

Java アプリケーションで **convert image to text** が必要な場合、Aspose.OCR for Java は高速で高精度なソリューションを提供します。このチュートリアルでは、画像から段落を抽出し、各テキスト領域のバウンディング矩形を取得し、コンソールに座標を出力するために必要な正確な手順を順に説明します。最後まで読むと、このアプローチがなぜ機能するのか、ライブラリの統合方法、そして独自のユースケースに拡張できる場所が理解できるようになります。

## クイック回答

`AreasType` はテキストセグメンテーションのレベル（単語、行、段落）を指定する列挙型です。

- **“recognize text from image” とは何ですか？** 画像内の視覚的文字を編集可能な文字列データに変換することを意味します。  
- **Java でこれを処理するライブラリはどれですか？** Aspose.OCR for Java。  
- **開発にライセンスは必要ですか？** テスト用の一時ライセンスが利用可能ですが、本番環境ではフルライセンスが必要です。  
- **単語ではなく段落を抽出できますか？** はい – `AreasType.PARAGRAPHS` を使用して段落レベルの矩形を取得します。  
- **コードは Java 11+ と互換性がありますか？** はい、API は Java 11 以降で動作します。

## Aspose.OCR における “convert image to text” とは何ですか？

`convert image to text` は、ビットマップを解析し OCR アルゴリズムを適用して、認識された文字を文字列として返すプロセスを指します。Aspose.OCR の `RecognizePage` メソッドは、この変換を実行し、検出された各テキストブロックの正確な `Rectangle` 座標をオプションで提供します。

## なぜこの **java ocr library** を使用するのですか？

Aspose.OCR は **30+ languages** をサポートし、画像サイズが **50 MB** までで、ファイル全体をメモリにロードせずに処理でき、典型的なサーバーハードウェア上でサブ秒応答時間を実現します。ライブラリはスレッドセーフで、単一の JAR だけで済み、出力形式も柔軟です – 生テキスト、HTML、正確なテキスト領域矩形などを提供し、高スループットのエンタープライズシナリオに最適です。

## 前提条件

- **Java Development Kit** (JDK 11 以上) がマシンにインストールされていること。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトから [here](https://releases.aspose.com/ocr/java/) でダウンロード。  
- JAR 依存関係を管理する IDE またはビルドツール (Maven/Gradle)。

## パッケージのインポート

Java プロジェクトで必要なクラスをインポートします。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## ステップバイステップガイド

### ステップ 1: プロジェクトのセットアップ
新しい Java プロジェクトを作成する（または既存プロジェクトに追加）し、Aspose.OCR JAR をクラスパスに配置します。Maven を使用する場合は、ダウンロードパッケージに記載の依存関係を追加してください。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### ステップ 2: ドキュメントディレクトリと画像パスの定義
サンプル画像が配置されている場所を指定します。

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### ステップ 3: AsposeOCR インスタンスの作成
`AsposeOCR` は OCR 機能を提供するメインクラスです。

OCR エンジンのインスタンス化:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### ステップ 4: 画像内のテキストを認識する
画像をロードし、`RecognizePage` を呼び出して画像をプレーンテキストに変換します。この単一メソッド呼び出しで画像前処理、文字セグメンテーション、言語固有の認識が一度に行われます。

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### ステップ 5: テキスト領域の矩形を取得する
各段落（または他のエリアタイプ）に対するバウンディング矩形を取得します。このステップは、検出されたテキストブロックを正確に囲む `Rectangle` オブジェクトのコレクションを返し、個別セクションのハイライトやさらに処理することが可能です。

CODE_BLOCK_PLACEHOLDER_5_END

## 一般的な問題とトラブルシューティング

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| `RecognizePage` の `IOException` | ファイルパスが間違っている、または読み取り権限がない | `imagePath` が既存の PNG/JPG を指しており、アプリにファイルシステムへのアクセス権があることを確認してください。 |
| 結果文字列が空 | 画像の品質が低い、またはサポート外の言語 | 画像を前処理（コントラスト上げ、二値化）するか、`api.setLanguage("eng")` で正しい言語を指定してください。 |
| 矩形が返されない | 間違った `AreasType` を使用している（例: 段落を期待しているのに `WORDS`） | 必要に応じて `AreasType.PARAGRAPHS` または `AreasType.LINES` に切り替えてください。 |

## よくある質問

**Q: Aspose.OCR は Java 11 と互換性がありますか？**  
A: はい、Aspose.OCR は Java 11 以降のバージョンで動作します。

**Q: Aspose.OCR を個人・商用プロジェクトの両方で使用できますか？**  
A: はい、あらゆるタイプのプロジェクトで使用可能です。ライセンスの詳細は [here](https://purchase.aspose.com/buy) をご覧ください。

**Q: 評価用の一時ライセンスはどのように取得できますか？**  
A: 一時ライセンスは [here](https://purchase.aspose.com/temporary-license/) から取得できます。

**Q: コミュニティサポートや公式サポートはどこで得られますか？**  
A: サポートやディスカッションは [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) をご利用ください。

**Q: Aspose.OCR はマルチスレッドに対応していますか？**  
A: はい、ライブラリはスレッドセーフで、同時実行環境でのパフォーマンス向上に利用できます。

## 結論

この **aspose ocr java tutorial** では、Aspose.OCR for Java を使用して **convert image to text** を行い、段落を抽出し、各テキストブロックを囲む正確な矩形を取得する方法を学びました。これらの機能により、検索可能な PDF の作成、UI オーバーレイでのテキストハイライト、または構造化データを下流プロセスに渡すことが可能になります。API をさらに調査して、言語設定のカスタマイズ、さまざまな画像形式の処理、またはクラウドストレージとの統合を行ってみてください。

---

**最終更新日:** 2026-06-19  
**テスト環境:** Aspose.OCR 23.10 for Java  
**作者:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 関連チュートリアル

- [画像からテキスト抽出 – Aspose.OCR for Java の OCR 基礎](/ocr/java/ocr-basics/)
- [Aspose.OCR Detect Areas モードを使用した Java での画像からテキスト抽出](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR BufferedImage を使用した Java での画像からテキストへの変換](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}