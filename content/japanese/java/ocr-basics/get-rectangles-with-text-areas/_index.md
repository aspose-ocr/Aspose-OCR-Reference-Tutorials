---
title: Aspose.OCR でテキスト領域を含む四角形を取得する
linktitle: Aspose.OCR でテキスト領域を含む四角形を取得する
second_title: Aspose.OCR Java API
description: Aspose.OCR for Java の機能を解放します。このステップバイステップのガイドで、画像からテキストをシームレスに抽出する方法を学びましょう。効率的なテキスト認識のために今すぐダウンロードしてください。
type: docs
weight: 12
url: /ja/java/ocr-basics/get-rectangles-with-text-areas/
---
## 導入

強力な光学式文字認識 (OCR) 機能を Java アプリケーションに統合したいと考えていますか? Aspose.OCR for Java は、画像から正確かつ効率的にテキストを抽出するための頼りになるソリューションです。このチュートリアルでは、Aspose.OCR を使用してテキスト領域を含む四角形を取得するプロセスを説明し、この Java OCR ライブラリの可能性を最大限に活用するのに役立ちます。

## 前提条件

チュートリアルに入る前に、次の前提条件が満たされていることを確認してください。

- Java 開発環境: システムに Java がインストールされていることを確認してください。
-  Aspose.OCR for Java ライブラリ: Aspose.OCR ライブラリをダウンロードしてセットアップします。ダウンロードリンクが見つかります[ここ](https://releases.aspose.com/ocr/java/).

## パッケージのインポート

Java プロジェクトで、Aspose.OCR の機能を利用するために必要なパッケージをインポートします。

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

## ステップ 1: プロジェクトをセットアップする

Java プロジェクトの準備ができており、Aspose.OCR ライブラリが統合されていることを確認してください。

## ステップ 2: ドキュメント ディレクトリと画像パスを定義する

```java
//ドキュメントディレクトリへのパス。
String dataDir = "Your Document Directory";

//画像のパス
String imagePath = dataDir + "p3.png";
```

## ステップ 3: Aspose.OCR インスタンスを作成する

```java
// Aspose.OCR インスタンスの作成
AsposeOCR api = new AsposeOCR();
```

## ステップ 4: 画像内のテキストを認識する

```java
try {
    //ファイルへのフルパスでページを認識します
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## ステップ 5: テキスト領域のある四角形を取得する

```java
//画像内のテキスト領域を含む長方形を取得します。
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

//各テキスト領域の四角形を印刷します
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## 結論

このチュートリアルでは、Aspose.OCR for Java をプロジェクトに統合して画像からテキストを効率的に抽出する方法を学習しました。 Aspose.OCR は OCR タスクを簡素化し、正確な結果を提供してシームレスなユーザー エクスペリエンスを実現します。

## よくある質問

### Q1: Aspose.OCR は Java 11 と互換性がありますか?

A1: はい、Aspose.OCR は Java 11 以降のバージョンと互換性があります。

### Q2: Aspose.OCR は個人プロジェクトと商用プロジェクトの両方に使用できますか?

 A2: はい、Aspose.OCR は個人プロジェクトと商用プロジェクトの両方に使用できます。ライセンスの詳細については、次のサイトを参照してください。[ここ](https://purchase.aspose.com/buy).

### Q3: Aspose.OCR の一時ライセンスを取得するにはどうすればよいですか?

 A3: 仮免許は取得できます。[ここ](https://purchase.aspose.com/temporary-license/).

### Q4: Aspose.OCR のサポートはどこで見つけられますか?

 A4: サポートとディスカッションについては、次のサイトにアクセスしてください。[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16).

### Q5: Aspose.OCR はマルチスレッドをサポートしていますか?

A5: はい、Aspose.OCR は同時環境でのパフォーマンスを向上させるためにマルチスレッドをサポートしています。
