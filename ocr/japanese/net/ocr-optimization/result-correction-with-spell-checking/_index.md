---
title: OCR画像認識におけるスペルチェックによる結果修正
linktitle: OCR画像認識におけるスペルチェックによる結果修正
second_title: Aspose.OCR .NET API
description: Aspose.OCR for .NET を使用して OCR の精度を向上させます。スペルを修正し、辞書をカスタマイズし、エラーのないテキスト認識を簡単に実現します。
type: docs
weight: 13
url: /ja/net/ocr-optimization/result-correction-with-spell-checking/
---
## 導入

光学式文字認識 (OCR) の分野では、画像から意味のある情報を抽出するには、正確な結果を達成することが重要です。よくある課題の 1 つは、認識プロセスでのスペルミスのある単語への対処です。幸いなことに、Aspose.OCR for .NET は、スペル チェックを通じて OCR 結果を強化する強力なソリューションを提供します。

このチュートリアルでは、Aspose.OCR for .NET を使用したスペル チェックによる結果修正のプロセスについて説明します。最終的には、OCR で生成されたテキストの精度を向上させ、より洗練されたエラーのない出力を保証できるようになります。

## 前提条件

スペルチェックの魔法に入る前に、次の前提条件が整っていることを確認してください。

-  Aspose.OCR for .NET ライブラリ: Aspose.OCR ライブラリを次の場所からダウンロードしてインストールします。[リリースページ](https://releases.aspose.com/ocr/net/).

- ドキュメント ディレクトリ: ドキュメント用に指定されたディレクトリがあることを確認します。コード スニペット内の「Your Document Directory」を実際のパスに置き換えます。

## 名前空間のインポート

まず、.NET プロジェクトに必要な名前空間をインポートします。

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## ステップ 1: Aspose.OCR を初期化する

Aspose.OCR のインスタンスを初期化して、OCR プロセスを開始します。

```csharp
//ドキュメントディレクトリへのパス。
string dataDir = "Your Document Directory";

// AsposeOcr のインスタンスを初期化する
AsposeOcr api = new AsposeOcr();
```

## ステップ 2: 画像を認識する

次に、Aspose.OCR を使用して画像内のテキストを認識します。このプロセスを示すスニペットは次のとおりです。

```csharp
//画像を認識する
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## ステップ 3: 修正前

修正前の OCR 結果を取得して、修正後のバージョンと比較します。

```csharp
//結果を取得する
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## ステップ 4: 修正後

スペルチェックを適用して、正しい結果を取得します。次のコード スニペットは、この手順を示しています。

```csharp
//修正結果を取得する
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## ステップ 5: 単語のスペルミスと提案

次のコードを使用して、スペルミスのある単語のリストと修正案を取得します。

```csharp
//スペルミスのある単語のリストを候補とともに取得します
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## ステップ 6: ユーザーテキストを修正する

Aspose.OCR ライブラリを使用して、特定のユーザー提供テキストを修正します。

```csharp
//正しいユーザーテキスト
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## ステップ7：ユーザー辞書による修正

カスタム ユーザー辞書を組み込むことで、修正がさらに強化されます。

```csharp
//ユーザー辞書による修正結果の取得
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## 結論

おめでとう！ Aspose.OCR for .NET のスペルチェック機能を正常に操作できました。この機能を使用すると、OCR 結果を調整して精度を確保し、エラーを排除できます。

## よくある質問

### Q1: 英語以外の言語でも Aspose.OCR を使用できますか?

A1: はい、Aspose.OCR は複数の言語をサポートしています。それに応じて言語設定を調整します。

### Q2: Aspose.OCR を .NET プロジェクトに統合するにはどうすればよいですか?

 A2: を参照してください。[ドキュメンテーション](https://reference.aspose.com/ocr/net/)詳細な統合手順については、

### Q3: Aspose.OCR の試用版はありますか?

 A3: はい、次の機能を使用して機能を探索できます。[無料試用版](https://releases.aspose.com/).

### Q4: スペルチェック用にカスタム辞書をアップロードできますか?

A4：もちろんです！このチュートリアルでは、ユーザーが提供する辞書を使用して補正を強化する方法を示します。

### Q5: Aspose.OCR のサポートはどこに問い合わせればよいですか?

 A5: にアクセスしてください。[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)コミュニティのサポートと指導のために。