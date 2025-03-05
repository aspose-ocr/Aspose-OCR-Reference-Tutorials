---
title: Aspose.OCR で言語を選択して OCR を実行する
linktitle: Aspose.OCR で言語を選択して OCR を実行する
second_title: Aspose.OCR Java API
description: Aspose.OCR for Java を使用して、画像からの正確なテキスト抽出をロック解除します。言語を選択して正確な OCR を行うには、ステップバイステップのガイドに従ってください。
type: docs
weight: 11
url: /ja/java/ocr-operations/perform-ocr-language-selection/
---
## 導入

進化し続けるテクノロジーの状況において、光学式文字認識 (OCR) は、画像から意味のある情報を抽出する上で極めて重要な役割を果たしています。 Aspose.OCR for Java は、開発者が OCR 機能を Java アプリケーションにシームレスに統合できるようにする強力なツールとして際立っています。このステップバイステップ ガイドでは、Aspose.OCR を使用して言語を選択して OCR を実行し、多様なコンテンツを正確に処理する可能性を解き放つ方法を説明します。

## 前提条件

チュートリアルに入る前に、次の前提条件が満たされていることを確認してください。

- Java 開発環境: システムに Java がインストールされており、開発環境がセットアップされていることを確認してください。

-  Aspose.OCR ライブラリ: Java 用の Aspose.OCR ライブラリをダウンロードしてインストールします。ライブラリと関連ドキュメントを見つけることができます[ここ](https://reference.aspose.com/ocr/java/).

- 画像ファイル：抽出したいテキストを含む画像ファイルを用意します。たとえば、「p3.png」という名前のファイルを使用してみましょう。

## パッケージのインポート

Java プロジェクトで、Aspose.OCR 機能を利用するために必要なパッケージをインポートします。 Java ファイルの先頭に次の行を追加します。

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

## ステップ 1: ドキュメント ディレクトリを設定する

```java
//ドキュメントディレクトリへのパス。
String dataDir = "Your Document Directory";
```

「Your Document Directory」を、画像ファイルが置かれているディレクトリへの実際のパスに置き換えます。

## ステップ 2: 画像パスを定義する

```java
//画像のパス
String file = dataDir + "p3.png";
```

特定の画像ファイルを指すようにファイル変数を調整します。

## ステップ 3: Aspose.OCR API インスタンスを作成する

```java
//APIインスタンスの作成
AsposeOCR api = new AsposeOCR();
```

AsposeOCR オブジェクトを初期化して、その機能にアクセスします。

## ステップ 4: 認識オプションを設定する

```java
//認識オプションを設定する
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

要件に基づいて認識設定をカスタマイズします。スキュー、言語、認識領域などのパラメータを調整します。

## ステップ 5: OCR を実行して結果を取得する

```java
//結果オブジェクトの取得
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

指定した画像ファイルと設定を使用して OCR 操作を実行します。結果を RecognitionResult オブジェクトにキャプチャします。

## ステップ 6: 結果を印刷して利用する

```java
//印刷結果
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

抽出されたテキスト、認識領域、JSON 表現、スキュー角度、および警告を出力します。アプリケーションで必要に応じて結果を使用します。

## 結論

このチュートリアルでは、言語を選択して OCR を実行するための Aspose.OCR for Java のシームレスな統合について詳しく説明しました。この強力なライブラリは、画像からテキストを正確に抽出することを目指す開発者に可能性の世界を開きます。

## よくある質問

### Q1: 単一の認識プロセスで複数の言語に Aspose.OCR を使用できますか?

A1: はい、RecognitionSettings で複数の言語を設定して、多言語コンテンツの認識精度を高めることができます。

### Q2: Aspose.OCR でさまざまな画像形式を処理するにはどうすればよいですか?

A2: Aspose.OCR は、PNG、JPEG、TIFF などのさまざまな画像形式をサポートしています。画像パス変数に正しいファイル パスを指定するだけです。

### Q3: Aspose.OCR が処理できる画像のサイズに制限はありますか?

A3: Aspose.OCR はさまざまなサイズの画像を処理できますが、画像が大きいほど、より多くの処理時間とリソースが必要になる場合があります。

### Q4: 画像内の特定の領域の認識設定を微調整できますか?

A4: もちろんです。 RecognitionAreas 機能を利用して、対象を絞った認識のために画像内の特定の四角形を定義します。

### Q5: Aspose.OCR は個人プロジェクトと商業プロジェクトの両方に適していますか?

A5: はい、Aspose.OCR は柔軟なライセンス オプションを提供しており、個人使用と商用使用の両方に適しています。