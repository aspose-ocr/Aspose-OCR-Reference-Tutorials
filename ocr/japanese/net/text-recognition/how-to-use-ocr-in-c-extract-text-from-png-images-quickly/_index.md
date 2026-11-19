---
category: general
date: 2026-03-29
description: Aspose を使用して OCR を行い、PNG ファイルからテキストを抽出し、画像をテキストに変換する方法。C# でステップバイステップの非同期
  OCR を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: ja
og_description: C#でAsposeを使用してPNGファイルからテキストを抽出するOCRの使い方。このガイドでは非同期OCR、コード、ヒントをご紹介します。
og_title: C#でOCRを使用する方法 – PNG画像からテキストを抽出
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – PNG画像からテキストを素早く抽出
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – PNG 画像からテキストを素早く抽出

PNG スクリーンショット数枚からテキストを抽出する **OCR の使い方** が気になったことはありませんか？スキャンした領収書や請求書、UI モックアップなどがあり、そのテキストを検索可能な形式にしたいときに便利です。良いニュースは、Aspose.OCR を使えば、非同期 C# コード数行で画像をテキストに変換できることです。

このチュートリアルでは、PNG ファイルからテキストを抽出する手順を正確に示し、各ステップの重要性を解説し、すべてのページの認識テキストを出力する実行可能なプログラムを提供します。最後まで読めば、ドキュメントを探し回ることなく **画像からテキストを抽出** できるようになります。

## 学べること

- Aspose.OCR NuGet パッケージをインストールし、参照する方法。  
- OCR エンジンを初期化し、言語を設定する方法（この例では英語）。  
- `RecognizeImagesAsync` に PNG ファイルの配列を渡して高速・ノンブロッキング処理を行う方法。  
- `OcrResult` オブジェクトをループし、抽出された文字列を出力する方法。  

外部サービス不要、複雑なコールバック不要—.NET 6+ で動作するクリーンな非同期 C# です。

---

## 前提条件

| 要件 | 理由 |
|------|------|
| .NET 6 SDK（またはそれ以降） | `async Main` などの最新言語機能 |
| Visual Studio 2022 または VS Code | コードをコンパイル・実行するための IDE |
| Aspose.OCR NuGet パッケージ（`Aspose.OCR`） | サンプルで使用される `OcrEngine` クラスを提供 |
| PNG 画像数枚（`page1.png`、`page2.png`、…） | OCR 処理の入力ファイル |

既に .NET プロジェクトがある場合は `dotnet add package Aspose.OCR` を実行してください。新規にコンソール アプリを作成する場合は `dotnet new console -n OcrDemo` で開始します。

---

## Step 1: Install Aspose.OCR and Set Up the Project

まず、OCR ライブラリをプロジェクトに追加します：

```bash
dotnet add package Aspose.OCR
```

**Why this matters:** Aspose.OCR はネイティブ OCR エンジン、言語パック、シンプルな API をバンドルしています。NuGet 経由で取得することでバージョン互換性と自動更新が保証されます。

---

## Step 2: Initialize the OCR Engine and Choose a Language

エンジンに認識させる言語を指定する必要があります。英語が最も一般的ですが、`Language.Spanish`、`Language.French` などに置き換えることも可能です。

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **プロのコツ:** 言語は必ず明示的に設定してください。デフォルトのままにすると精度が低下し、処理時間が増加することがあります。

---

## Step 3: Prepare the List of PNG Files

単一ファイルでも配列でも構いません。配列を渡すことでエンジンは非同期にバッチ処理でき、数ページ程度の処理に最適です。

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

画像がサブフォルダーにある場合は相対パス（例：`"images/page1.png"`）を付けるだけです。パスが間違っているとエンジンは明確な `FileNotFoundException` をスローするので、ファイル名は必ず確認してください。

---

## Step 4: Run Asynchronous OCR on All Images

`RecognizeImagesAsync` メソッドは `OcrResult` の配列を返します。非同期であるため、UI（またはコンソール）は OCR がバックグラウンドで実行されている間も応答し続けます。

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Why async?**  
Web API やデスクトップ アプリに OCR を組み込む場合、エンジンが各ピクセルを走査している間にスレッドがブロックされるのは望ましくありません。`await` によりスレッドはスレッドプールに戻り、スケーラビリティが向上します。

---

## Step 5: Display the Extracted Text for Each Page

結果が得られたら、各ページを走査して認識されたテキストを出力します。`Text` プロパティにはプレーンテキストが格納されており、データベース保存などの後続処理にすぐ利用できます。

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### 期待される出力

`page1.png` に「Invoice #12345」、`page2.png` に「Total: $89.99」が含まれていると仮定すると、次のように表示されます：

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

OCR がテキストを検出できなかった場合、`Text` プロパティは空文字列になります。実運用コードでは `string.IsNullOrWhiteSpace` でチェックして対処してください。

---

## 完全動作サンプル

以下は `Program.cs` に貼り付けてそのまま使用できる完全なプログラムです。using ディレクティブ、非同期 `Main`、各ステップを説明するコメントが含まれています。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

ファイルを保存し、PNG を実行ファイルと同じディレクトリに置く（またはパスを調整）ことで、次のコマンドを実行します：

```bash
dotnet run
```

コンソールに抽出されたテキストが表示され、**画像をテキストに変換** に成功したことが確認できます。

---

## よくあるエッジケースの対処

| 状況 | 対処方法 |
|------|----------|
| **低解像度 PNG** | 認識前に `ocrEngine.ImageProcessingOptions.Dpi` を上げる |
| **複数言語** | `ocrEngine.Language = Language.English \| Language.Spanish;`（ビット単位 OR） |
| **大量バッチ（数百ファイル）** | メモリスパイクを防ぐため、20 ファイルずつなどに分割して `RecognizeImagesAsync` を呼び出す |
| **信頼度スコアが必要** | `ocrResults[i].Confidence`（0〜1 の float）を使用して低品質結果を除外する |

これらの調整により、デモから本番環境へ移行しても OCR パイプラインの堅牢性が保たれます。

---

## ボーナス: 結果をテキスト ファイルに保存

コンソール出力ではなく永続的なコピーが欲しい場合は、次のヘルパーを追加してください：

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

これで **画像からテキストを抽出** した単一ファイルが作成され、インデックス作成、検索、あるいは言語モデルへの入力など、下流処理に最適です。

---

## 結論

Aspose を使って C# で **OCR を使用し、PNG 画像からテキストを抽出** し、**画像をテキストに変換** する方法を順を追って解説しました。非同期アプローチによりアプリケーションは応答性を保ち、シンプルな API によりコードは読みやすく保守しやすくなります。

ぜひ自分のドキュメントで試し、言語を変えてみたり、出力を検索インデックスや要約サービスに連結したりしてみてください。画像を確実に検索可能な文字列に変換できれば、可能性は無限です。

---

### 次のステップと関連トピック

- **他のフォーマット（JPEG、TIFF）から画像のテキストを抽出** – ファイル拡張子を変更するだけです。  
- **大量処理を Parallel.ForEach で実行** – 大規模ワークロード向け。  
- **OCR 後のクリーンアップ** – 正規表現で日付、金額、ID などを正規化。  
- **Azure Cognitive Services と統合** – 追加機能が必要なクラウドベース OCR。  

問題があればコメントで教えてください。また、この基本フローを拡張した事例もぜひ共有してください。ハッピーコーディング！   ![抽出されたテキストを示す OCR 結果のスクリーンショット](/images/ocr-result.png){.align-center alt="OCR の使用例出力"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}