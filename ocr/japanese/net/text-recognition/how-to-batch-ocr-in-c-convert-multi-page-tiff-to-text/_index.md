---
category: general
date: 2026-03-28
description: C#でバッチOCRを行い、TIFFを簡単にテキストに変換する方法を学びましょう。このステップバイステップガイドでは、Aspose OCRを使用してTIFFファイルからテキストを抽出する方法を示しています。
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: ja
og_description: C#でバッチOCRを行う方法は？Aspose OCRを使用して、マルチページTIFFファイルを検索可能なテキストに変換する完全なチュートリアルをご覧ください。
og_title: C#でバッチOCRを行う方法 – マルチページTIFFをテキストに変換
tags:
- OCR
- C#
- Aspose
title: C#でバッチOCRを行う方法 – マルチページTIFFをテキストに変換
url: /ja/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でバッチOCRする方法 – マルチページTIFFをテキストに変換

スキャンしたページの山を **バッチで OCR** したいと思ったことはありませんか？同じように考えている人は多いです。請求書処理やアーカイブのデジタル化など、**TIFF をテキストに変換** する必要が毎日のように出てくるプロジェクトでは、1ページずつ処理するとすぐに悪夢のようになります。

良いニュースは、数行の C# と Aspose OCR さえあれば、マルチページTIFF全体をエンジンに渡すだけで、ページ番号と抽出文字列の辞書が手に入ります。このチュートリアルでは、**バッチOCRのやり方**、**TIFF からテキストを抽出する方法**、そしてこのアプローチが手作業の代替手段より優れている理由を示す、完全に実行可能なサンプルを順に解説します。

## 学べること

- .NET プロジェクトに Aspose OCR ライブラリを設定する方法。  
- `Image.FromMultiPageFile` を使ってマルチページTIFFファイルを読み込む方法。  
- `RecognizeBatch` を実行してページごとの `Dictionary<int,string>` を取得する方法。  
- 結果を見やすい形式で出力する方法。  

最後まで読めば、任意のマルチページTIFFをプレーンテキストに変換できるコンソールアプリがすぐに作れます—追加ツールは不要です。

### 前提条件

- .NET 6.0 SDK（またはそれ以降のバージョン）。  
- Visual Studio 2022 または VS Code—お好きな IDE で構いません。  
- 有効な Aspose OCR ライセンス、または無料評価キー（ライセンスなしでも API は動作しますが透かしが入ります）。  
- `multipage.tif` という名前のサンプルマルチページTIFFを、参照できるフォルダーに配置しておくこと。

> **プロのコツ:** Windows ではプロジェクトフォルダーが TIFF を置くのに便利です。Linux/macOS ではパスを適宜調整してください。

## 手順 1: Aspose OCR NuGet パッケージをインストール

コードを書く前に OCR ライブラリが必要です。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

これで最新の安定版（2026年3月時点の v23.9）が取得され、必要な DLL がプロジェクトに追加されます。シンプルなコンソールアプリの場合、追加の設定は不要です。

## 手順 2: コンソールアプリの雛形を作成

OCR エンジンを参照する最小限のプログラムを作ります。`using` ディレクティブは必須です—これがないとコンパイラが型不足でエラーになります。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **なぜ重要か:** `Image` クラスはサブネームスペースに属しており、`ImageProcessing` のインポートを忘れると「型または名前空間が見つかりません」エラーになり、デバッグに時間がかかります。

次に `Main` メソッドと、目的を簡潔に説明するコメントを追加します。

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## 手順 3: OCR エンジンを初期化

`OcrEngine` が実質的な作業ユニットです。インスタンスを一度作成し、すべてのページで再利用すればメモリ効率も高速性も確保できます。

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **内部で何が起きているか？** エンジンは言語モデルを読み込み、デフォルト設定（例: 英語、オートローテート）を事前構成します。後から調整可能ですが、デフォルトでほとんどの文書に対して十分です。

## 手順 4: マルチページ TIFF を読み込む

Aspose はマルチフレーム画像の読み込みを簡単にします。実行ファイルの作業ディレクトリからの相対パス、またはフルパスを指定してください。

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

ファイルが見つからない場合、`FromMultiPageFile` は `FileNotFoundException` をスローします。エラーハンドリングが必要なら `try/catch` でラップしてください—次の手順で例を示します。

## 手順 5: バッチ OCR を実行

本題の `RecognizeBatch` です。戻り値は `Dictionary<int,string>` で、キーがページインデックス（0 から開始）、値が認識されたテキストになります。

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **エッジケース:** 空白ページがある TIFF では、Aspose は空文字列を返します。不要な出力を除去したい場合は後でフィルタリングできます。

## 手順 6: 結果を表示

最後に辞書を走査し、各ページのテキストを出力します。文字列補間を使うとコードがすっきりします。

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

プログラムを実行すると、次のような出力が得られます。

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

文字化けが出た場合は、元の TIFF が破損していないか、テキストの言語がエンジンのデフォルト（英語）と合っているかを確認してください。非英語文書の場合は `ocrEngine.Language = OcrLanguage.Spanish;` などと設定できます。

## 完全動作サンプル

すべてをまとめたプログラムを以下に示します。`Program.cs` に貼り付けてそのままビルド・実行できます。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

保存してビルド、実行：

```bash
dotnet run
```

各ページの抽出内容がコンソールに表示されます。これが求めていた **c# ocr tutorial** の全容です。

## FAQ とエッジケース

### TIFF が何十ページもある場合は？

`RecognizeBatch` はすべてのフレームを一括で処理しますが、ページ数が増えるとメモリ使用量も比例して増えます。数百ページ規模の大文書の場合は、チャンクに分割して処理することを検討してください。

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### 抽出したテキストをコンソールに出す代わりにファイルへ保存したい？

もちろん可能です。`Console.WriteLine` 部分をファイル入出力に置き換えてください。

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

これで各ページが個別の `.txt` ファイルとして保存され、後続のインデックス作成に便利です。

### 出力言語やオートローテートを変更したい場合は？

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

これらの設定は **`RecognizeBatch` を呼び出す前** に適用する必要があります。

## まとめ

Aspose OCR と C# を使って、マルチページTIFFを **バッチで OCR** する方法を解説しました。画像を一度だけ読み込み、`RecognizeBatch` を呼び出し、得られた辞書を走査するだけで、**TIFF をテキストに変換** できるようになります。サンプルは **TIFF からテキストを抽出** し、エラーハンドリングやファイル出力のオプションも示しています—すべてがシンプルなコンソールアプリに収められています。

次のステップに進みませんか？この手法を PDF 生成ライブラリと組み合わせて検索可能な PDF を作成したり、データベースに結果を保存してアーカイブ検索を実装したりできます。また、`Image.FromMultiPageFile` を `Image.FromFile` に置き換えれば、PNG や JPEG など他の画像形式でも同様に処理可能です。

OCR、ライセンス、パフォーマンスチューニングに関する質問があれば下のコメント欄へどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}