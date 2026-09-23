---
date: 2026-02-09
description: Aspose OCR Java ライブラリを使用して画像をテキストに変換し、テキスト領域の矩形を抽出する方法を学びましょう。コード例付きのステップバイステップガイド。
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 画像をテキストに変換 – 画像からテキストを認識し、テキスト領域の矩形を取得
url: /ja/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストへ変換 – 画像からテキストを認識しテキスト領域の矩形を取得する

## はじめに

Java アプリケーションで **convert image to text** と **recognize text from image** ファイルが必要な場合、Aspose.OCR for Java は高速で正確な方法を提供します。このチュートリアルでは、画像から段落を抽出し、各テキスト領域のバウンディング矩形を取得し、それらの座標をコンソールに出力するために必要な正確な手順を順に説明します。最後まで読むと、このアプローチがなぜ機能するのか、ライブラリの統合方法、そして独自のユースケースに拡張できる場所が理解できるようになります。

## クイック回答
- **What does “recognize text from image” mean?** 画像内の視覚的文字を編集可能な文字列データに変換することを意味します。  
- **Which library handles this in Java?** Aspose.OCR for Java。  
- **Do I need a license for development?** テスト用の一時ライセンスが利用可能です。製品版にはフルライセンスが必要です。  
- **Can I extract paragraphs instead of single words?** はい – `AreasType.PARAGRAPHS` を使用して段落レベルの矩形を取得できます。  
- **Is the code compatible with Java 11+?** もちろん、API は Java 11 以降で動作します。

## Aspose.OCR における “convert image to text” とは何ですか？

Aspose.OCR の `RecognizePage` メソッドはビットマップを解析し、OCR アルゴリズムを適用して認識された文字列を返します。テキスト領域を要求すると、ライブラリは各テキストブロックの正確な `Rectangle` 座標も計算し、後で特定のセクションをハイライトしたり処理したりするのが容易になります。

## なぜこの **java ocr library** を使用するのか？

- **High accuracy** – 複数の言語と複雑なフォントをサポートします。  
- **Easy integration** – 1 つの JAR でフル OCR 機能を追加できます。  
- **Flexible output** – 生テキスト、フォーマットされた HTML、または正確なテキスト領域の矩形を取得できます。  
- **Thread‑safe** – 高スループットのサーバー環境に適しています。

## 前提条件

- **Java Development Kit** (JDK 11 以上) がマシンにインストールされていること。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトからダウンロードしてください [here](https://releases.aspose.com/ocr/java/)。  
- JAR 依存関係を管理するための IDE またはビルドツール (Maven/Gradle)。

## パッケージのインポート

Java プロジェクトで必要なクラスをインポートします:

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

## 手順ガイド

### 手順 1: プロジェクトの設定
新しい Java プロジェクトを作成する（または既存のプロジェクトに追加する）し、Aspose.OCR JAR をクラスパスに配置します。Maven を使用する場合は、ダウンロードパッケージに記載された依存関係を追加してください。

### 手順 2: ドキュメントディレクトリと画像パスの定義
サンプル画像の所在場所を指定します:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 手順 3: Aspose.OCR インスタンスの作成
OCR エンジンのインスタンスを作成します:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### 手順 4: 画像内のテキストを認識する
`RecognizePage` を呼び出して画像をプレーンテキストに変換します。この手順はコアな **recognize text image java** 機能を示しています:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 手順 5: テキスト領域の矩形を取得する
次に、各段落（または他の領域タイプ）のバウンディング矩形を取得します。ここで **extract paragraphs from image** を行い、座標を取得します:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## よくある問題とトラブルシューティング

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| `RecognizePage` の `IOException` | ファイルパスが間違っている、または読み取り権限がない | `imagePath` が存在する PNG/JPG を指しており、アプリにファイルシステムへのアクセス権があることを確認してください。 |
| 結果文字列が空 | 画像の品質が低い、またはサポートされていない言語 | 画像を前処理（コントラスト増加、二値化）するか、`api.setLanguage("eng")` で正しい言語を指定してください。 |
| 矩形が返ってこない | 間違った `AreasType` を使用している（例: 段落を期待しているのに `WORDS`） | 必要に応じて `AreasType.PARAGRAPHS` または `AreasType.LINES` に切り替えてください。 |

## よくある質問

**Q: Aspose.OCR は Java 11 と互換性がありますか？**  
**A:** はい、Aspose.OCR は Java 11 以降のバージョンで動作します。

**Q: Aspose.OCR を個人プロジェクトと商用プロジェクトの両方で使用できますか？**  
**A:** はい、あらゆるタイプのプロジェクトで使用可能です。ライセンスの詳細は [here](https://purchase.aspose.com/buy) をご覧ください。

**Q: 評価用の一時ライセンスはどこで取得できますか？**  
**A:** 一時ライセンスは [here](https://purchase.aspose.com/temporary-license/) から取得できます。

**Q: コミュニティサポートや公式サポートはどこで得られますか？**  
**A:** サポートやディスカッションは [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) をご利用ください。

**Q: Aspose.OCR はマルチスレッドに対応していますか？**  
**A:** はい、ライブラリはスレッドセーフで、同時実行環境でのパフォーマンス向上に利用できます。

## 結論

この **aspose ocr java tutorial** では、Aspose.OCR for Java を使用して **convert image to text** を行い、段落を抽出し、各テキストブロックを囲む正確な矩形を取得する方法を学びました。これらの機能により、検索可能な PDF の作成、UI オーバーレイでのテキストハイライト、または構造化データを下流プロセスに供給することが可能になります。API をさらに調査して、言語設定のカスタマイズ、さまざまな画像形式の処理、またはクラウドストレージとの統合を行ってみてください。

---

**最終更新日:** 2026-02-09  
**テスト環境:** Aspose.OCR 23.10 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}