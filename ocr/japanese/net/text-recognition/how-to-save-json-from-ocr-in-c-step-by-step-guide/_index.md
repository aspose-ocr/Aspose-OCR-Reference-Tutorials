---
category: general
date: 2026-02-19
description: C#でOCR出力からJSONを保存する方法 – 画像からテキストを抽出し、C#でJSONファイルを書き込み、Aspose OCRで画像をJSONに変換する方法を学ぶ。
draft: false
keywords:
- how to save json
- extract text from image
- write json file c#
- convert image to json
- c# ocr tutorial
language: ja
og_description: C#でOCR結果からJSONを保存する方法は簡単です。このチュートリアルに従って画像からテキストを抽出し、C#スタイルでJSONファイルを書き出しましょう。
og_title: C#でOCRからJSONを保存する方法 – 完全ガイド
tags:
- C#
- OCR
- JSON
title: C#でOCRからJSONを保存する方法 – ステップバイステップガイド
url: /ja/net/text-recognition/how-to-save-json-from-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR から JSON を保存する方法 – 完全チュートリアル

C# で OCR の結果から JSON を保存することは、スキャンした書類を構造化データに変換する際によくあるニーズです。このガイドでは、画像からテキストを抽出し、JSON に変換し、最後に C# スタイルで JSON ファイルを書き出す方法を正確に示します—余計な説明はなく、実用的なソリューションだけです。

スキャナーでレシートを読み取ろうとして、検索できないぼやけた画像になったことはありませんか？それが、画像からデータを抽出しようとする多くの開発者が直面する問題です。この記事の最後までに、画像を読み込み、Aspose OCR でテキストを取得し、下流のサービスに渡せるきれいな JSON ファイルを保存する小さなコンソールアプリが手に入ります。

ここでは、必要な NuGet パッケージ、完全で実行可能かつ詳細にコメントされたコード、よくある落とし穴、出力をすばやく検証する方法をすべてカバーします。OCR の事前知識は不要です—C# と .NET の基本的な理解さえあれば大丈夫です。

## 前提条件

- .NET 6 SDK 以降（コードは .NET 6 を対象としていますが、.NET 5+ でも動作します）
- Visual Studio 2022、VS Code、またはお好みのエディタ
- 処理したい画像ファイル（`input.png`）
- **Aspose.OCR** NuGet パッケージを取得できるインターネット接続

これらのいずれかが不足している場合は、今すぐ入手してください。そうしないと、後で時間を無駄にします。  

> **プロのコツ:** Aspose OCR には無料トライアルキーが用意されており、ライセンスなしで実験できます。

## ステップ 1: Aspose OCR NuGet パッケージをインストールする

まずは、重い処理を担うライブラリを追加します。プロジェクトフォルダでターミナルを開き、次のコマンドを実行してください：

```bash
dotnet add package Aspose.OCR
```

この単一コマンドで最新の Aspose OCR バイナリがダウンロードされ、`.csproj` に参照が追加されます。  

> **このステップが重要な理由:** パッケージが無いと `OcrEngine` クラスが存在せず、コンパイル時エラーが発生します。  

パッケージが準備できたら、コンソールアプリの骨格を作成しましょう。

## ステップ 2: プロジェクト構造を設定する

まだ作成していない場合は、新しいコンソールプロジェクトを作成します：

```bash
dotnet new console -n JsonExportOcr
cd JsonExportOcr
```

`Program.cs` のデフォルト内容を以下の完全なサンプルに置き換えてください。後で各行を解説しますが、ファイルが用意できていれば、波括弧を抜かす心配なくコピー＆ペーストできます。

## ステップ 3: OCR エンジンを初期化する（画像からテキストを抽出）

最初の実装行は OCR エンジンを作成し、英字文字を対象にするよう指示します。`Language.Spanish` など他のサポート言語に切り替えることも可能ですが、英語が最も一般的です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3.1: Create an OCR engine and set the language to English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Step 3.2: Recognize text from the input image
        // Replace the path with where your image actually lives
        string inputPath = @"YOUR_DIRECTORY/input.png";
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**何が起きているのか？**  
- `OcrEngine` は Aspose OCR のエントリーポイントです。  
- `Language` を設定すると、エンジンが言語固有のヒューリスティックを適用できるため精度が向上します。  
- `RecognizeImage` は認識された単語、信頼度スコア、バウンディングボックスを保持する `OcrResult` オブジェクトを返します。

画像が存在しない、または破損している場合、ガード句がフレンドリーなメッセージを出力して中止します—この小さなチェックで後々の NullReference エラーを防げます。

## ステップ 4: OCR 結果を JSON に変換する（画像を JSON に変換）

Aspose OCR には `JsonResultWriter` というヘルパーが同梱されています。これにより `OcrResult` を REST API で期待される構造に合わせたきれいな JSON 文字列にシリアライズできます。

```csharp
        // Step 4: Convert the OCR result to a JSON string
        string jsonResult = JsonResultWriter.Write(ocrResult);
```

**なぜ `JsonResultWriter` を使うのか？**  
- ネストした `Word` コレクションなどの複雑なオブジェクトを自動的に処理します。  
- 独自のシリアライザを書かずに済むため、信頼度パーセンテージなど微細なフィールドを見落とすリスクが減ります。

この時点で `jsonResult` は概ね以下のようになります（可読性のために整形しています）：

```json
{
  "PageCount": 1,
  "Pages": [
    {
      "PageNumber": 1,
      "Words": [
        {
          "Text": "Hello",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 50, "Height": 15 }
        },
        // … more words …
      ]
    }
  ]
}
```

このスニペットを JSON ビューアに貼り付けて構造を確認できます。  

> **エッジケース:** 画像に複数ページが含まれる場合、JSON には `Pages` 配列が追加されます—下流のコンシューマが対応できることを確認してください。

## ステップ 5: JSON をディスクに書き込む（JSON の保存方法）

ここがチュートリアルの核心です: **JSON をディスクに保存する** 方法です。.NET の `File` クラスでワンライナーで実装できますが、堅牢性のために少しだけエラーハンドリングを加えます。

```csharp
        // Step 5: Write the JSON string to an output file
        string outputPath = @"YOUR_DIRECTORY/output.json";
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
```

これで「JSON をどうやって保存するか」という質問についに答えられました—ファイルは作成され、既に存在すれば上書きされ、成功を示す明確なコンソールメッセージが表示されます。

## ステップ 6: 結果を検証する

プログラムが終了したら、`output.json` を任意のエディタ（VS Code、Notepad++、あるいはブラウザ）で開きます。OCR 出力の整形された JSON 表現が表示されるはずです。もし空の `"Words": []` 配列が見つかったら、画像の品質を再確認してください—低コントラストやノイズが多いと OCR の精度が落ちます。

コマンドラインから簡単なサニティチェックを実行することもできます：

```bash
dotnet run
```

期待される出力は次のとおりです：

```
JSON saved to YOUR_DIRECTORY/output.json
```

エラーが出た場合、コンソールは入力ファイルが見つからないか書き込みに失敗したかを教えてくれます。

## 完全動作例

以下は **完全** なプログラムです。`Program.cs` にそのままコピー＆ペーストしてください。`YOUR_DIRECTORY` を `input.png` があるフォルダに置き換えます。他のファイルは不要です。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;
using System;
using System.IO;

class JsonExport
{
    static void Main()
    {
        // Step 3: Initialize OCR engine (extract text from image)
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };

        // Define file paths
        string inputPath = @"YOUR_DIRECTORY/input.png";
        string outputPath = @"YOUR_DIRECTORY/output.json";

        // Validate input image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        // Recognize text
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Convert OCR result to JSON (convert image to json)
        string jsonResult = JsonResultWriter.Write(ocrResult);

        // Write JSON to disk (how to save json)
        try
        {
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"JSON saved to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to write JSON: {ex.Message}");
        }
    }
}
```

プログラムを実行し、生成されたファイルを開けば、画像から **JSON を保存する方法** を示す **C# OCR チュートリアル** が無事完了したことになります。

## よくある落とし穴とヒント（C# で JSON ファイルを書き込む）

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **`Words` 配列が空** | 画像が暗すぎる、または解像度が低い | 画像を前処理する（コントラストを上げる、DPI を高くする） |
| **`File.WriteAllText` が UnauthorizedAccessException をスロー** | 読み取り専用フォルダに書き込もうとしている | 書き込み可能なディレクトリを選択（例: `%TEMP%` またはプロジェクトフォルダ） |
| **NuGet パッケージが欠如** | `dotnet add package Aspose.OCR` を忘れた | コマンドを再実行し、再ビルド |
| **JSON が単一行** | `WriteAllText` がフォーマットなしで生文字列を書き込む | オーバーロードがあれば `JsonResultWriter.Write(ocrResult, true)` を使用するか、`JsonSerializer` の `WriteIndented = true` オプションで整形する |

これらのチェックで **C# で JSON ファイルを書き込む** ワークフローがスムーズになり、「何も起きなかった」瞬間を防げます。

## 次のステップ（画像からテキスト抽出など）

Now that you know **how to save json**, you might want to:

- **Store the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}