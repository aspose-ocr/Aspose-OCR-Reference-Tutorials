---
title: Aspose.OCR for Java で URL からの画像に対して OCR を実行する
linktitle: Aspose.OCR for Java で URL からの画像に対して OCR を実行する
second_title: Aspose.OCR Java API
description: Aspose.OCR を使用して、Java でのシームレスな画像テキスト抽出をロック解除します。簡単に統合できる高精度 OCR。
weight: 11
url: /ja/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR for Java で URL からの画像に対して OCR を実行する

## 導入

Aspose.OCR for Java を使用して URL の画像に対して光学式文字認識 (OCR) を実行するためのステップバイステップ ガイドへようこそ。このチュートリアルは、Aspose.OCR を Java アプリケーションにシームレスに統合し、画像からテキストを簡単に抽出できるようにすることを目的に設計されています。 Aspose.OCR は、さまざまな画像形式をサポートする強力な OCR ライブラリであり、テキスト抽出が必要なアプリケーションにとって貴重なツールになります。

## 前提条件

チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。

1. Java 開発環境: マシン上に動作する Java 開発環境がセットアップされていることを確認してください。

2.  Aspose.OCR ライブラリ: Java ライブラリ用の Aspose.OCR をダウンロードしてインストールします。ライブラリと関連ドキュメントは、[Aspose.OCR Web サイト](https://reference.aspose.com/ocr/java/).

## パッケージのインポート

Java プロジェクトで、Aspose.OCR に必要なパッケージをインポートします。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## ステップ 1: API インスタンスを作成する

AsposeOCR クラスのインスタンスを初期化します。

```java
AsposeOCR api = new AsposeOCR();
```

## ステップ 2: 画像 URL を定義する

OCR を実行する画像の URL を指定します。

```java
String uri = "https://www.example.com/your-image.png";
```

## ステップ 3: 認識オプションを設定する

自動スキューの無効化や認識領域の定義などの認識設定を構成します。

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

//長方形を使用して認識領域を定義する
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## ステップ 4: OCR を実行する

OCR 認識プロセスを呼び出します。

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## ステップ 5: 結果を印刷する

抽出されたテキスト、認識領域のテキスト、JSON 出力、警告などの認識結果を表示します。

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Aspose.OCR を Java アプリケーションに統合し、画像からテキストを正確に抽出するには、これらの手順を繰り返します。

## 結論

結論として、Aspose.OCR for Java を活用すると、OCR タスクに堅牢なソリューションが提供され、開発者が画像からテキストをシームレスに抽出できるようになります。ステップバイステップのガイドにより、スムーズな統合プロセスが保証され、あらゆるレベルの開発者がアクセスできるようになります。

## よくある質問

### Q1: Aspose.OCR は画像からテキストを認識する精度はどの程度ですか?

A1: Aspose.OCR は、特に正確な認識領域で構成されている場合に、高い精度のテキスト認識を実現します。

### Q2: Aspose.OCR は OCR 認識中に複数の言語を処理できますか?

A2: はい、Aspose.OCR は複数の言語でのテキストの認識をサポートしており、さまざまなアプリケーションに多用途性を提供します。

### Q3: 商用プロジェクトで Aspose.OCR を使用する場合、ライセンスに関する考慮事項はありますか?

A3: はい。商用利用の場合は、Aspose.OCR ライセンス条項に必ず準拠してください。参照する[購入.aspose.com](https://purchase.aspose.com/buy)ライセンスの詳細については、

### Q4: Aspose.OCR 関連の問題のサポートを受けるにはどうすればよいですか?

 A4: にアクセスしてください。[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)コミュニティのサポートとディスカッションのために。プレミアム サポートについては、次のサイトから一時ライセンスを取得することを検討してください。[仮免許](https://purchase.aspose.com/temporary-license/).

### Q5: Aspose.OCR for Java の無料トライアルはありますか?

 A5: はい、次の場所で利用できる無料トライアルで Aspose.OCR の機能を試してください。[releases.aspose.com](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
