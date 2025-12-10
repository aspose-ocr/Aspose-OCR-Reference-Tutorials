---
date: 2025-12-10
description: Aspose.OCR for Java を使用して画像からテキストを認識し、画像から段落を抽出する方法を学びます。コード例付きのステップバイステップガイド。
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: 画像からテキストを認識し、テキスト領域の矩形を取得する
url: /ja/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを認識し、テキスト領域の矩形を取得する

## はじめに

Java アプリケーションで **画像からテキストを認識** したい場合、Aspose.OCR for Java は高速かつ高精度な方法を提供します。このチュートリアルでは、画像から段落を抽出し、各テキスト領域のバウンディング矩形を取得してコンソールに出力する手順を詳しく解説します。最後まで読むと、このアプローチがなぜ有効か、ライブラリの統合方法、そして独自のユースケースに拡張できるポイントが理解できるようになります。

## クイック回答
- **「画像からテキストを認識」とは何ですか？** 画像内の視覚的文字を編集可能な文字列データに変換することです。  
- **Java でこれを扱うライブラリはどれですか？** Aspose.OCR for Java。  
- **開発用にライセンスは必要ですか？** テスト用の一時ライセンスが利用可能です。製品版では正式ライセンスが必要です。  
- **単語ではなく段落を抽出できますか？** はい。`AreasType.PARAGRAPHS` を使用すると段落レベルの矩形が取得できます。  
- **コードは Java 11+ と互換性がありますか？** 完全に対応しており、Java 11 以降で動作します。

## Aspose.OCR における「画像からテキストを認識」とは？
Aspose.OCR の `RecognizePage` メソッドはビットマップを解析し、OCR アルゴリズムを適用して認識された文字列を返します。テキスト領域を要求すると、ライブラリは各テキストブロックの正確な `Rectangle` 座標も計算し、後で特定のセクションをハイライトしたり処理したりするのが容易になります。

## なぜ Aspose.OCR for Java を選ぶのか？
- **高精度** – 複数言語や複雑なフォントに対応。  
- **簡単統合** – 1 つの JAR でフル OCR 機能が利用可能。  
- **柔軟な出力** – 生テキスト、フォーマット済み HTML、または正確なテキスト領域矩形を取得可能。  
- **スレッドセーフ** – 高スループットなサーバ環境でも安心して使用可能。

## 前提条件

- **Java Development Kit**（JDK 11 以上）がマシンにインストールされていること。  
- **Aspose.OCR for Java** ライブラリ – 公式サイトから [こちら](https://releases.aspose.com/ocr/java/) でダウンロード。  
- IDE またはビルドツール（Maven/Gradle）で JAR 依存関係を管理できる環境。

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

### 手順 1: プロジェクトのセットアップ
新規 Java プロジェクトを作成（または既存プロジェクトに追加）し、Aspose.OCR JAR をクラスパスに配置します。Maven を使用する場合は、ダウンロードパッケージに記載の依存情報を pom.xml に追加してください。

### 手順 2: ドキュメントディレクトリと画像パスの定義
サンプル画像が保存されている場所を指定します:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### 手順 3: Aspose.OCR インスタンスの作成
OCR エンジンをインスタンス化します:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### 手順 4: 画像内のテキストを認識
`RecognizePage` を呼び出して画像をプレーンテキストに変換します。このステップが **画像からテキストを認識** するコア機能です:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 手順 5: テキスト領域の矩形を取得
各段落（または他のエリアタイプ）のバウンディング矩形を取得します。ここで **画像から段落を抽出** し、座標を取得します:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## よくある問題とトラブルシューティング

| 症状 | 考えられる原因 | 対処方法 |
|------|----------------|----------|
| `IOException` が `RecognizePage` で発生 | ファイルパスが間違っている、または読み取り権限がない | `imagePath` が既存の PNG/JPG を指しているか確認し、アプリにファイルシステムアクセス権があるか確認 |
| 結果文字列が空 | 画像品質が低い、または未対応言語 | 画像を前処理（コントラスト上げ、二値化）するか、`api.setLanguage("eng")` などで正しい言語を指定 |
| 矩形が返ってこない | 誤った `AreasType` を使用（例: 段落を期待しているのに `WORDS`） | 必要に応じて `AreasType.PARAGRAPHS` または `AreasType.LINES` に切り替える |

## FAQ（よくある質問）

**Q: Aspose.OCR は Java 11 と互換性がありますか？**  
A: はい、Java 11 以降のバージョンで動作します。

**Q: 個人・商用プロジェクトのどちらでも使用できますか？**  
A: どちらのプロジェクトでも使用可能です。ライセンス詳細は [こちら](https://purchase.aspose.com/buy) をご覧ください。

**Q: 評価用の一時ライセンスはどこで取得できますか？**  
A: [こちら](https://purchase.aspose.com/temporary-license/) から取得できます。

**Q: コミュニティサポートや公式サポートはどこで受けられますか？**  
A: サポートやディスカッションは [Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16) で行われています。

**Q: Aspose.OCR はマルチスレッドに対応していますか？**  
A: はい、ライブラリはスレッドセーフで、同時実行環境でのパフォーマンス向上に利用できます。

## 結論

このチュートリアルでは、Aspose.OCR for Java を使って **画像からテキストを認識** し、段落を抽出し、各テキストブロックを囲む正確な矩形を取得する方法を学びました。これらの機能を活用すれば、検索可能な PDF の作成、UI オーバーレイでのテキストハイライト、あるいは構造化データへの変換といったさまざまなシナリオに応用できます。さらに API を探求し、言語設定のカスタマイズや異なる画像形式への対応、クラウドストレージとの統合などを試してみてください。

---

**最終更新日:** 2025-12-10  
**テスト環境:** Aspose.OCR 23.10 for Java  
**作成者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}