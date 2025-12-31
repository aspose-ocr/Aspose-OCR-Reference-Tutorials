---
category: general
date: 2025-12-30
description: C# を使用して画像から OCR テキストを抽出する方法を学びましょう。このチュートリアルでは、画像ファイルからテキストを抽出する方法、PNG
  からテキストを読み取る方法、そして完全な C# OCR チュートリアルが含まれています。
draft: false
keywords:
- how to extract ocr
- extract text from image
- read text from png
- c# ocr tutorial
language: ja
og_description: C# を使用して画像から OCR テキストを抽出する方法。C# OCR チュートリアルに従って、PNG ファイルからテキストを読み取り、画像からテキストを簡単に抽出しましょう。
og_title: C#でOCRテキストを抽出する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRテキストを抽出する方法 – 完全ステップバイステップガイド
url: /ja/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRテキストを抽出する方法 – 完全ステップバイステップガイド

スキャンしたフォームから **OCR を抽出** する方法を、カスタムパーサーを書いて何時間も費やすことなく知りたくありませんか？ あなただけではありません。請求書処理、パスポートスキャン、古いアーカイブのデジタル化など、実際のプロジェクトでは画像ファイルからテキストを確実に取り出す手段が必要です。良いニュースは、Aspose.OCR を使えば C# の数行で実現できることです。

このチュートリアルでは、**c# ocr tutorial** として **画像からテキストを抽出** する方法（特に PNG）と、**png からテキストを読む** 方法を、文字単位のメタデータを保持したまま紹介します。最後まで読めば、Aspose が取得したすべての情報を含む整形済み JSON 文字列をコンソールに出力する、すぐに実行できるアプリが手に入ります。

> **前提条件**  
> • .NET 6.0 以降がインストール済み  
> • Visual Studio 2022（またはお好みの IDE）  
> • Aspose.OCR for .NET NuGet パッケージ（`Aspose.OCR`）  

これらが揃っていれば、さっそく始めましょう。

---

## C#で画像からOCRテキストを抽出する方法 – プロジェクトの設定

コードを書く前に、クリーンなプロジェクトと正しい依存関係が必要です。

```bash
# Create a new console app
dotnet new console -n OcrDemo
cd OcrDemo

# Add Aspose.OCR package
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio を使用している場合は、NuGet パッケージ マネージャー UI から「Aspose.OCR」を検索して追加できます。

パッケージをインストールしたら `Program.cs` を開きます。デフォルトの `Main` メソッドが表示され、ここにコードを記述していきます。

---

## 手順 1 – OCR エンジンの初期化（重要な理由）

OCR エンジンはプロセスの中心です。初期化することで、後で使用する言語モデルを Aspose に伝えます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance
            var ocrEngine = new OcrEngine();

            // The rest of the steps will follow here...
        }
    }
}
```

*なぜこの手順が必要か？*  
`OcrEngine` オブジェクトを作成すると、画像解析に必要なリソースが確保されます。これがなければ画像をエンジンに渡すことができず、ライブラリは高度なパターン認識アルゴリズムを適用できません。

---

## 手順 2 – 英語言語モデルのロード（画像からテキストを抽出）

Aspose には複数の言語パックが同梱されています。正しいモデルをロードすることで精度が大幅に向上します。

```csharp
// Step 2: Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

別の言語が含まれる **png からテキストを読む** 必要がある場合は、`LanguageModel.English` を適切な列挙値（例: `LanguageModel.French`）に置き換えるだけです。この柔軟性が、Aspose がグローバルアプリケーションで人気の理由です。

---

## 手順 3 – PNG ファイルからテキストを認識（PNG からテキストを読む）

いよいよエンジンに実際の画像を指示します。このデモでは、実行ファイルから相対パスで `YOUR_DIRECTORY` フォルダー内にある `form_image.png` を使用します。

```csharp
// Step 3: Perform OCR on the image
var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");
```

> **ファイルが見つからない場合は？**  
> `Recognize` メソッドは `FileNotFoundException` をスローします。実運用でのエラーハンドリングが必要な場合は、try‑catch でラップしてください。

---

## 手順 4 – 結果を整形された JSON に変換（なぜ JSON？）

Aspose は単なるテキストだけでなく、バウンディングボックス、信頼度スコア、行情報などを含むリッチな `RecognitionResult` オブジェクトを返します。JSON にシリアライズすれば、ログ保存や API 送信が簡単になります。

```csharp
// Step 4: Serialize the result to a nicely indented JSON string
string json = JsonResult.FromRecognitionResult(recognitionResult)
                        .ToString(prettyPrint: true);

// Optional: Write the JSON to a file for later inspection
System.IO.File.WriteAllText("ocr_output.json", json);
```

`prettyPrint: true` フラグを付けると改行とインデントが追加され、デバッグに最適です。生テキストだけが必要な場合は、`recognitionResult.Text` を使用すれば済みます。

---

## 手順 5 – JSON 出力をコンソールに表示（結果の確認）

最後に、JSON をコンソールに出力してすべてが正しく動作したか確認します。

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine(json);
```

プログラムを実行すると、以下のような（省略された）出力が得られます。

```json
{
  "Text": "John Doe\n123 Main St\nAnytown, USA",
  "Characters": [
    {
      "Value": "J",
      "Confidence": 0.99,
      "Bounds": { "X": 12, "Y": 8, "Width": 10, "Height": 14 }
    },
    // ... more character objects ...
  ],
  "Lines": [
    { "Text": "John Doe", "Confidence": 0.98 },
    { "Text": "123 Main St", "Confidence": 0.97 },
    { "Text": "Anytown, USA", "Confidence": 0.96 }
  ]
}
```

文字単位のメタデータに注目してください。これは多くの無料 OCR ライブラリにはない、Aspose の付加価値です。低信頼度の文字を除外したり、元画像上にハイライト表示したりすることが可能です。

---

## 完全動作サンプル（すべての手順を一括で）

以下はコピー＆ペーストだけで動く完全版プログラムです。欠けている部分はありません。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Load the English language model
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Recognize text from the PNG image
            var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");

            // Step 4: Convert the result to pretty‑printed JSON
            string json = JsonResult.FromRecognitionResult(recognitionResult)
                                    .ToString(prettyPrint: true);

            // Optional: Save JSON to a file
            System.IO.File.WriteAllText("ocr_output.json", json);

            // Step 5: Display the JSON output
            Console.WriteLine(json);
        }
    }
}
```

`Program.cs` として保存し、PNG を配置して `dotnet run` を実行すれば、JSON がコンソールに表示されます。

---

## よくある質問とエッジケース（“もしも” に答える）

### 画像が PNG ではなく JPEG だったら？

`Recognize` メソッドは Aspose がサポートする任意の形式（JPEG、BMP、TIFF など）を受け付けます。パスの拡張子を変更するだけで OK です。

### 低解像度スキャンの精度を上げるには？

1. **画像前処理** – コントラストを上げる、グレースケールに変換、シャープフィルタを適用。  
2. **高解像度の元画像を使用** – OCR エンジンは通常、300 dpi 以上を推奨します。  
3. **自動回転を有効化** – 認識前に `ocrEngine.AutoRotate = true;` を設定。

### JSON ではなくプレーンテキストだけが欲しい場合は？

`Recognize` 後に `recognitionResult.Text` を取得すれば OK です。

```csharp
Console.WriteLine(recognitionResult.Text);
```

### 複数ページの PDF からテキストを抽出できるか？

Aspose.OCR は画像向けですが、Aspose.PDF と組み合わせて各 PDF ページを画像にラスタライズし、ループで OCR エンジンに渡すことができます。

---

## 堅牢な C# OCR チュートリアルのプロTips

- **エンジンの破棄**: 多数の画像を処理する場合は `using` ブロックで `OcrEngine` を囲み、ネイティブリソースを速やかに解放しましょう。  
- **バッチ処理**: 大量フォルダーでは `Directory.GetFiles` でファイル列挙し、各ファイルを try‑catch で処理して、1 つの不良ファイルが全体を止めないようにします。  
- **ロギング**: 信頼度スコアを保存しておくと、低品質結果を手動レビューに回す際に非常に役立ちます。  
- **スレッド安全性**: `OcrEngine` インスタンスは **スレッドセーフではありません**。並列処理する場合はスレッドごとに別インスタンスを作成してください。

---

## 結論

C# で画像から OCR テキストを抽出する方法を習得しました。OCR エンジンの初期化、適切な言語モデルのロード、PNG の認識、結果の整形 JSON へのシリアライズという流れで、あらゆる文書デジタル化プロジェクトの基盤ができました。この **c# ocr tutorial** では **画像からテキストを抽出**、**png からテキストを読む** 方法と、よくある落とし穴への対処法も網羅しています。

次のステップは？ スキャンした請求書のバッチを同じパイプラインに流し込んだり、別言語パックで実験したり、JSON 出力を検索可能なデータベースに統合したりしてみてください。可能性は無限大です。このコードがその出発点です。

このガイドが役立ったら、チームと共有したり、リポジトリにスターを付けたり、OCR 成功体験をコメントで教えてください。Happy coding!

![OCR抽出例](https://example.com/ocr-demo.png "OCR抽出例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}