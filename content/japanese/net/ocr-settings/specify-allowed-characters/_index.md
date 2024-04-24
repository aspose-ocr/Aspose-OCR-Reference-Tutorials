---
title: OCR画像認識で使用できる文字を指定する
linktitle: OCR画像認識で使用できる文字を指定する
second_title: Aspose.OCR .NET API
description: Aspose.OCR を使用して、.NET で正確な OCR をロック解除します。画像からテキストを簡単に認識します。今すぐダウンロードして、革新的な開発エクスペリエンスを体験してください。
type: docs
weight: 13
url: /ja/net/ocr-settings/specify-allowed-characters/
---
## 導入

テクノロジーが進化し続ける中で、光学式文字認識 (OCR) が革新的なツールとして台頭し、機械が画像からテキストを理解できるようになりました。 Aspose.OCR for .NET は強力なソリューションとして際立っており、.NET アプリケーションで堅牢な OCR 機能を求める開発者にシームレスな統合を提供します。

## 前提条件

チュートリアルに入る前に、次の前提条件が満たされていることを確認してください。

- .NET 開発に関する実践的な知識。
-  .NET ライブラリの Aspose.OCR。ダウンロードできます[ここ](https://releases.aspose.com/ocr/net/).
- Visual Studio またはその他の推奨される .NET 開発環境に精通していること。

## 名前空間のインポート

.NET プロジェクトで、Aspose.OCR for .NET の機能を効果的に活用するために必要な名前空間をインポートします。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

ここで、チュートリアルを一連の包括的な手順に分割してみましょう。

## ステップ 1: OCR 画像認識で使用できる文字を指定する

まず、ドキュメント ディレクトリへのパスを設定します。

```csharp
string dataDir = "Your Document Directory";
```

## ステップ 2: 許可されたシンボルを使用して Aspose.OCR を初期化する

許可されるシンボルを指定して、AsposeOcr のインスタンスを作成します。この場合、数字 (0 ～ 9) を許可します。

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## ステップ 3: 画像を認識する

AsposeOcr インスタンスを利用して画像からテキストを認識します。

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## ステップ 4: 認識されたテキストを表示する

認識されたテキストをコンソールに出力します。

```csharp
Console.WriteLine(result);
```

## ステップ 5: 2 番目のケース - 特定の設定で画像を認識する

別の AsposeOcr インスタンスを、今回はより具体的な設定で初期化します。

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## ステップ 6: 2 番目の大文字と小文字が認識されたテキストを表示する

番目のケースで認識されたテキストをコンソールに出力します。

```csharp
Console.WriteLine(result2.RecognitionText);
```

## ステップ 7: 実行の成功

最後に、SpecifyAllowedCharacters チュートリアルが正常に実行されたことを確認します。

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

これらの手順に従うことで、Aspose.OCR for .NET を使用した OCR 画像認識で許可される文字を指定する機能のロックが解除されました。

## 結論

Aspose.OCR for .NET を使用すると、開発者は OCR 機能をアプリケーションにシームレスに統合でき、さまざまなドメインで革新的なソリューションへの扉が開きます。 OCR のパワーを活用し、正確なテキスト認識でプロジェクトを強化します。

## よくある質問

### Q1: Aspose.OCR for .NET は初心者と経験豊富な開発者の両方に適していますか?

A1: もちろんです！ Aspose.OCR for .NET は、あらゆるスキル レベルの開発者に対応し、シームレスな統合のための直感的な機能を提供します。

### Q2: 複数の言語の文字を認識するために Aspose.OCR for .NET を使用できますか?

A2: はい、Aspose.OCR はさまざまな言語での認識をサポートしているため、さまざまなアプリケーションに多用途に使用できます。

### Q3: Aspose.OCR for .NET はどのくらいの頻度で更新されますか?

 A3: 最新テクノロジーとの互換性を確保し、潜在的な問題に対処するために、アップデートが定期的にリリースされます。チェックしてください[ドキュメンテーション](https://reference.aspose.com/ocr/net/)最新情報については。

### Q4: Aspose.OCR for .NET の無料トライアルはありますか?

A4: はい、Aspose.OCR をダウンロードすると、その機能を調べることができます。[無料トライアル](https://releases.aspose.com/).

### Q5: どこで支援を求めたり、コミュニティに連絡してサポートを求めたりできますか?

 A5: にアクセスしてください。[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)コミュニティに参加し、専門家の支援を受けることができます。