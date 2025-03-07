---
title: OCR画像認識で結果をドキュメントとして保存
linktitle: OCR画像認識で結果をドキュメントとして保存
second_title: Aspose.OCR .NET API
description: Aspose.OCR for .NET の可能性を解き放ちます。画像内のテキストを簡単に認識し、結果をさまざまなドキュメント形式で保存します。
weight: 10
url: /ja/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR画像認識で結果をドキュメントとして保存

## 導入

Aspose.OCR for .NET を使用した光学式文字認識 (OCR) のエキサイティングな世界へようこそ!この包括的なチュートリアルでは、Aspose.OCR を使用して画像内のテキストを認識する複雑な方法を詳しく説明し、結果をさまざまなドキュメント形式で保存する方法を示します。

## 前提条件

この OCR の取り組みを開始する前に、次の前提条件が満たされていることを確認してください。

-  .NET 用の Aspose.OCR。 Aspose.OCR ライブラリがインストールされていることを確認してください。ダウンロードできます[ここ](https://releases.aspose.com/ocr/net/).

- ドキュメント ディレクトリ: ドキュメント用に指定されたディレクトリを用意し、`dataDir`それに応じて、提供されたコード内の変数を変更します。

## 名前空間のインポート

まず、必要な名前空間をインポートします。これらは、コードに OCR 機能を追加するための構成要素です。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

ここで、例を複数のステップに分けてみましょう。

## ステップ 1: Aspose.OCR を初期化する

```csharp
//ドキュメントディレクトリへのパス。
string dataDir = "Your Document Directory";

// AsposeOcr のインスタンスを初期化する
AsposeOcr api = new AsposeOcr();
```

このステップでは、Aspose.OCR API を初期化することで段階を設定します。

## ステップ 2: 画像を認識する

```csharp
//画像を認識する
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

ここでは、Aspose.OCR を使用して、指定された画像内のテキストを認識します (「sample.png」を画像ファイルに置き換えます)。

## ステップ 3: 結果をさまざまな形式で保存する

```csharp
//結果を好みの形式で保存します
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

ニーズに基づいてこのステップをカスタマイズします。 Aspose.OCR を使用すると、認識されたテキストを DOCX、TXT、PDF、XLSX などのさまざまなドキュメント形式で保存できます。

## ステップ 4: 成功メッセージを表示する

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

プロセスが問題なく完了したことを知らせる簡単な確認メッセージ。

これらの手順に従うことで、Aspose.OCR for .NET の機能を利用して、画像内のテキストを認識し、結果をさまざまなドキュメント形式で保存することができます。

## 結論

結論として、Aspose.OCR for .NET は画像内のテキスト認識の可能性の世界を開きます。データを抽出する場合でも、検索可能なドキュメントを作成する場合でも、Aspose.OCR は直感的な API を使用してプロセスを簡素化します。

## よくある質問

### Q1. Aspose.OCR はさまざまな画像形式と互換性がありますか?

A1: はい、Aspose.OCR は幅広い画像形式をサポートしており、OCR タスクの柔軟性を確保しています。

### Q2: 精度を高めるために認識設定をカスタマイズできますか?

A2：もちろんです！ Aspose.OCR は、特定の要件に応じて OCR プロセスを微調整するための認識設定を提供します。

### Q3: 無料トライアルはありますか?

 A3: はい、無料トライアルから始めることができます。[ここ](https://releases.aspose.com/).

### Q4: Aspose.OCR の一時ライセンスを取得するにはどうすればよいですか?

 A4: 仮免許は取得可能です[ここ](https://purchase.aspose.com/temporary-license/).

### Q5: どこに助けを求めたり、コミュニティに連絡したりできますか?

 A5: Aspose.OCR コミュニティに参加してください。[アスペス フォーラム](https://forum.aspose.com/c/ocr/16)サポートとディスカッションのため。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
