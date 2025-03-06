---
title: OCR画像認識におけるフォルダーのOCRO操作
linktitle: OCR画像認識におけるフォルダーのOCRO操作
second_title: Aspose.OCR .NET API
description: Aspose.OCR を使用して、.NET での OCR 画像認識の能力を解放します。画像からテキストを簡単に抽出します。
weight: 11
url: /ja/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR画像認識におけるフォルダーのOCRO操作

## 導入

Aspose.OCR for .NET を使用した光学式文字認識 (OCR) の世界へようこそ! .NET アプリケーション内で画像からテキストをシームレスに抽出したい場合は、ここが正しい場所です。このチュートリアルでは、Aspose.OCR の強力な機能を活用して、フォルダーを使用した OCR 画像認識のプロセスを説明します。

## 前提条件

チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。

- C# および .NET 開発の実践的な知識。
- Visual Studio がマシンにインストールされていること。
-  Aspose.OCR for .NET ライブラリ (ダウンロード可能)[ここ](https://releases.aspose.com/ocr/net/).
- OCR の概念の基本的な理解。

## 名前空間のインポート

C# コードでは、Aspose.OCR を使用するために必要な名前空間を必ずインポートしてください。スクリプトの先頭に次の内容を含めます。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ステップ 1: ドキュメント ディレクトリを設定する

```csharp
//例開始:1
//ドキュメントディレクトリへのパス。
string dataDir = "Your Document Directory";
```

「Your Document Directory」を画像が保存されている実際のパスに置き換えてください。

## ステップ 2: Aspose.OCR を初期化する

```csharp
// AsposeOcr のインスタンスを初期化する
AsposeOcr api = new AsposeOcr();
```

AsposeOcr クラスのインスタンスを作成して、その機能を利用します。

## ステップ 3: 画像パスを指定する

```csharp
//画像パス
string fullPath = dataDir + "OCR";
```

ドキュメント ディレクトリ パスと画像を含む特定のフォルダーを連結します。

## ステップ 4: 画像を認識する

```csharp
//画像を認識する
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //デフォルトまたはカスタム
});
```

RecognizeMultipleImages メソッドを使用して、指定したフォルダー内の複数の画像に対して OCR を実行します。

## ステップ 5: 結果を印刷する

```csharp
//印刷結果
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

結果をループし、各画像の認識されたテキストを印刷します。

## ステップ 6: 結論

```csharp
//拡張終了:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

フォルダーに対する OCR 操作の実行が成功したことを示す、スクリプトの結論に達していることを確認します。

## 結論

おめでとう！ Aspose.OCR for .NET を使用してフォルダーに対する OCR 画像認識を実装する方法を学習しました。この強力なツールを使用すると、.NET アプリケーションの画像からテキストを抽出するための無数の可能性が開かれます。

## よくある質問

### Q1: Aspose.OCR for .NET を商用プロジェクトで使用できますか?

 A1: はい、Aspose.OCR for .NET は商用製品です。ライセンス情報については、次のサイトを参照してください。[ここ](https://purchase.aspose.com/buy).

### Q2:。無料トライアルはありますか?

 A2: はい、無料トライアルを試すことができます[ここ](https://releases.aspose.com/).

### Q3: ドキュメントはどこで入手できますか?

 A3: ドキュメントは入手可能です[ここ](https://reference.aspose.com/ocr/net/).

### Q4: 一時ライセンスを取得するにはどうすればよいですか?

 A4: 仮免許は取得可能です[ここ](https://purchase.aspose.com/temporary-license/).

### Q5: サポートが必要ですか? 質問がありますか?

 A5: にアクセスしてください。[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)コミュニティサポートのために。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
