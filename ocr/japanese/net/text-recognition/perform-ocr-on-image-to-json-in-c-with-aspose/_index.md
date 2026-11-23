---
category: general
date: 2026-04-08
description: Aspose OCR を使用して画像の OCR を実行し、C# で JSON ファイルを書き出す方法を学びましょう。この Aspose OCR
  C# チュートリアルでは、信頼度値を含む OCR 画像から JSON への変換を示します。
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: ja
og_description: 画像に対して OCR を実行し、結果を C# で JSON ファイルにエクスポートします。このチュートリアルでは、信頼度スコアを含む
  Aspose OCR C# のフルワークフローをカバーしています。
og_title: C#で画像のOCRを実行しJSONに変換 – Aspose OCRガイド
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose を使用して C# で画像の OCR を実行し、JSON に変換する
url: /ja/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose で画像を OCR して JSON に変換する

画像ファイルに対して **画像に対して OCR を実行する** が必要なのに、結果を構造化された形式で取得する方法が分からないことはありませんか？ あなた一人ではありません—開発者は常に「スキャンした画像を使えるデータに変換するにはどうすればいいのか？」と質問しています。 良いニュースは、Aspose.OCR を使えばこの作業は簡単で、**C# で JSON ファイルを書き込む**‑style で信頼度スコアを含めて書き出すこともできます。

このガイドでは、画像の読み込みから認識テキストを JSON としてエクスポートするまでを網羅した完全な **aspose OCR C# tutorial** を解説します。最後までに、**画像に対して OCR を実行する** コンソールアプリが完成し、出力を JSON（信頼度も含む）に変換して、1 行のコードで保存できるようになります。隠れた手順や外部スクリプトは一切なく、純粋な C# だけです。

## 前提条件

- .NET 6.0 SDK 以降（コードは .NET Core や .NET Framework でも動作します）
- Visual Studio 2022（またはお好みのエディタ）
- 有効な **Aspose.OCR for .NET** ライセンスまたは無料の一時ライセンス（無料トライアルでテスト可能です）
- 処理したい画像ファイル（`input.png`）（PNG、JPG、BMP など一般的な形式なら何でも構いません）

以上です。これらが揃っていない場合は今すぐ入手してください。以降のチュートリアルはすでに環境が整っていることを前提としています。

## 手順 1: Aspose.OCR NuGet パッケージをインストールする

まずはライブラリをプロジェクトに追加します。プロジェクトフォルダでターミナルを開き、以下を実行してください：

```bash
dotnet add package Aspose.OCR
```

これにより最新バージョン（2026年4月時点で 23.12）を取得し、必要な DLL が `bin` フォルダに追加されます。追加の設定は不要です。

## 手順 2: OCR エンジンを初期化する（画像に対して OCR を実行）

ここで `OcrEngine` インスタンスを作成し、使用する言語を指定します。英語（`"en"`）が最も一般的ですが、`"fr"`、`"de"`、またはサポートされている任意の言語に変更できます。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**ここで初期化する理由:** `OcrEngine` は認識プロセスに必要なすべての設定を保持します。言語を事前に設定することで、エンジンが正しい文字セットを使用し、精度が大幅に向上します。

## 手順 3: 画像を認識し信頼度を取得する

エンジンの準備ができたら、画像ファイルを渡します。`RecognizeImage` メソッドは `OcrResult` オブジェクトを返し、抽出されたテキストと各単語の信頼度スコアの両方を含みます。

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**内部で何が起きているか:** Aspose はニューラルネットワークベースの認識エンジンを使用し、各ピクセルブロックを解析して言語モデルと照合し、各単語に対して 0‑100 の信頼度値を付与します。

## 手順 4: 結果を JSON に変換する（OCR 画像から JSON へ）

Aspose は変換を簡単に行います。`includeConfidence: true` を指定すると、以下のような JSON ペイロードが得られます：

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

JSON 文字列を生成するコードは次のとおりです：

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**なぜ信頼度を含めるのか:** データを下流のプロセス（例: バリデーション、UI のハイライト）に渡す場合、どの単語が不確かかを把握することで、ユーザーに確認を求めるかどうか判断できます。

## 手順 5: JSON ファイルを C# スタイルで書き込む

ここで実際に **C# で JSON ファイルを書き込む** ことができます。`File.WriteAllText` メソッドは原子的でクロスプラットフォーム対応なので、コンソールアプリに最適です。

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

以上が全体のワークフローです。5 つの簡潔な手順で **画像に対して OCR を実行** し、出力を JSON に変換して永続化します。

## 完全な動作例

以下は `Program.cs` にコピー＆ペーストできる完全なプログラムです。`input.png` がコンパイルされたバイナリと同じフォルダにあることを確認するか、パスを適宜調整してください。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### 期待される出力

プログラムを実行すると（`dotnet run`）、以下のような出力が表示されます：

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

そして `output.json` には先ほど示した構造化された JSON が格納され、各単語の信頼度パーセンテージも含まれます。

## プロのコツとエッジケース

- **Missing file handling:** 動的なパスを想定する場合は、`RecognizeImage` 呼び出しを `FileNotFoundException` 用の `try/catch` でラップしてください。
- **Different languages:** フランス語の場合は `ocrEngine.Language = "fr"` を設定するか、`ocrEngine.LoadLanguage("custom.lang")` でカスタム言語パックをロードします。
- **Large documents:** 複数ページの PDF では、まず各ページを画像に変換（例: `Aspose.PDF` を使用）し、OCR 手順をループします。
- **Performance tuning:** 迅速な結果だけが必要な場合は `RecognitionMode.Fast` に切り替えます—精度は若干低下しますが速度が向上します。
- **JSON formatting:** 整形された JSON が欲しい場合は、Aspose の JSON 文字列をデシリアライズした後、Newtonsoft の `JsonConvert.SerializeObject` を `Formatting.Indented` と共に使用します。

## よくある質問

**Q: これは .NET Framework でも動作しますか？**  
A: はい、問題ありません。同じ NuGet パッケージは .NET Standard 2.0 を対象としているため、.NET Framework 4.6.1 以降から参照できます。

**Q: 単語ごとの信頼度ではなく、文書全体の信頼度が必要な場合はどうすればいいですか？**  
A: `OcrResult` には `OverallConfidence` も公開されており、JSON に手動で追加できます。

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: JSON を直接 Web API にストリーム送信できますか？**  
A: はい。`File.WriteAllText` を `HttpClient` の POST に置き換えて `jsonResult` を送信すれば可能です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}