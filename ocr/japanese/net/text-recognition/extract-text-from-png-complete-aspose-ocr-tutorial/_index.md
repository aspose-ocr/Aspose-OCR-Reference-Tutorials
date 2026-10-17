---
category: general
date: 2026-01-09
description: Aspose OCRでPNGからテキストを迅速に抽出しましょう。画像のテキストの読み取り方法、OCR精度の向上、そしてC#でクリーンな結果を得る方法を学びます。
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: ja
og_description: Aspose OCRでPNGからテキストを迅速に抽出。画像の文字を読み取る方法、OCR精度の向上、そしてC#でクリーンな結果を得る方法を学びましょう。
og_title: PNGからテキストを抽出する – 完全なAspose OCRチュートリアル
tags:
- Aspose OCR
- C#
- Image Processing
title: PNGからテキストを抽出 – 完全なAspose OCRチュートリアル
url: /ja/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGからテキストを抽出 – 完全な Aspose OCR チュートリアル

PNGファイルから **PNGからテキストを抽出** したことがありますか？しかし結果が意味不明な文字だらけだったことはありませんか？あなたは一人ではありません。実務のプロジェクト—請求書、領収書、スキャンしたフォーム—では、OCR の出力品質が自動化パイプラインの成否を左右します。  

このガイドでは、Aspose OCR を使用して画像テキストを読み取る **step‑by‑step** の方法を示し、**OCR の精度を向上** させるカスタム辞書を追加し、ノイズを除去し、最終的に整った文字列を出力します。最後まで読めば、PNG 画像から確実にテキストを抽出できる C# コンソール アプリがすぐに実行可能になります。

> **学べること**  
> * 完全で実行可能なコードサンプル  
> * カスタム辞書が重要になる理由の理解  
> * 低コントラストのスキャンなどのエッジケースへの対処法  

## 前提条件

- .NET 6 SDK 以降（コードは .NET 6 を対象としていますが、.NET 5 でも動作します）。  
- Visual Studio 2022 またはお好みのエディタ。  
- 処理したい **PNG** 画像（例：`invoice.png`）。  
- **Aspose.OCR** NuGet パッケージ（`dotnet add package Aspose.OCR`）。  

追加の設定ファイルは不要です。すべては単一の `.cs` ファイルに収められます。

## Step 1 – Aspose OCR のインストールと参照

まず、ライブラリをプロジェクトに追加します。ソリューション フォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

この一行で最新の安定版（2026 年 1 月時点でバージョン 23.9）を取得します。パッケージにはチュートリアル全体で使用する `OcrEngine` クラスが含まれています。

## Step 2 – OCR エンジンの初期化

`OcrEngine` インスタンスを作成することが基礎となります。ピクセルを解釈できるスキャナをオンにするイメージです。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Pro tip:** 多数の画像をループで処理する場合は、同じ `OcrEngine` インスタンスを再利用してください。内部リソースがキャッシュされ、以降の呼び出しが高速化されます。

## Step 3 – カスタム辞書で精度を向上

標準の OCR は優秀ですが、 “Aspose” や “OCR”、 “SDK” といったドメイン固有語に苦戦することがあります。これらの語句を **custom dictionary** に追加すると、エンジンはそれらの文字列を有効とみなし、誤認識が減少します。

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### カスタム辞書が有効な理由

- OCR の背後にある **Statistical models** は一般的な言語パターンに重みを置きます。珍しい語は確率が低く、似た形の文字に置き換えられやすくなります。  
- 明示的に列挙することで、モデルの推測を上書きできます。  
- 製品コード、略語、ブランド名が含まれる **read image text** に特に便利です。

## Step 4 – PNG ファイルからテキストを認識

次に、エンジンに画像パスを渡します。`RecognizeImage` メソッドは、生の文字列を返しますが、エンジンがマッピングできなかった未知のトークン（例: “#@!”）が残ります。

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Edge case:** ファイルが見つからない場合、`RecognizeImage` は `FileNotFoundException` をスローします。実装時は try‑catch でラップしてください。

## Step 5 – `CleanText` で結果をクリーンアップ

Aspose OCR には「未知」とフラグ付けされた文字を除去するヘルパーが同梱されています。このステップは、下流のパーサが英数字と基本的な句読点のみを期待する **extract text from image** プロジェクトで特に重要です。

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText` メソッドは改行コードも正規化し、データベースへの保存や他サービスへの受け渡しが安全になるよう出力を整えます。

## Step 6 – クリーンテキストの出力

最後に結果を表示または保存します。コンソール アプリでは `Console.WriteLine` が手軽です。

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

プログラムを実行すると、`invoice.png` の内容を鏡写しした整ったテキストブロックが表示されます。画像に “Aspose” が含まれていれば、カスタム辞書のおかげで正しく表示され、 “A5p0se” のような誤認識は起きません。

## 完全な動作例

すべてをまとめると、以下の `Program.cs` を新しいコンソール プロジェクトにコピーペーストすれば完了です。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**期待される出力**（PNG にシンプルな請求書が含まれていると仮定）:

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

余計な記号が出た場合は、画像品質を再確認するか、カスタム辞書にさらに語句を追加してください。

## ボーナス: 低品質スキャンへの対処

PNG が 72 dpi でスキャンされていたり、圧縮アーティファクトが多い場合があります。C# を離れずに **OCR の精度を向上** させるための簡単なテクニックをいくつか紹介します。

1. `SixLabors.ImageSharp` などのライブラリで **Pre‑process the image** – コントラストを上げ、グレースケールに変換、または軽いブラーをかけてノイズを減らす。  
2. `OcrEngine` の `Resolution` プロパティを設定（例: `ocrEngine.Resolution = 300;`）し、エンジンに高解像度として扱わせる。  
3. 非英語テキストを扱う場合は **Enable language packs**（例: `ocrEngine.Language = Language.English;`）。

これらの手法はすべて `RecognizeImage` 呼び出しの前に追加できます。

## Frequently Asked Questions

- **Does this work with other image formats?**  
  Yes. `RecognizeImage` は JPEG、BMP、TIFF、さらには PDF（画像コンテナとして）も受け付けます。同じ手順が適用できます。

- **Can I extract text from multiple PNGs in a folder?**  
  Absolutely. コアロジックを `foreach (var file in Directory.GetFiles(folder, "*.png"))` ループで囲み、各結果をリストに格納するか別ファイルに書き出してください。

- **What if I need the text coordinates?**  
  Aspose OCR はバウンディング ボックスを含む `OcrResult` オブジェクトも提供します。高度なシナリオでは `ocrEngine.RecognizeImageToResult(imagePath)` を使用してください。

## Conclusion

本稿では、Aspose OCR を用いて **complete, end‑to‑end** に **PNG からテキストを抽出** するソリューションを紹介しました。エンジンの初期化、**custom dictionary** の投入、生データのクリーンアップ、そして一般的な落とし穴への対処を行うことで、C# アプリケーション内で確実に **read image text** し、**OCR の精度を向上** させることができます。

次のステップに進む準備はできましたか？PNG をスキャンした領収書に差し替えてみたり、辞書にさらにドメイン固有語を追加したり、出力をデータベースに連携して自動請求書処理を実装したりしてみてください。Aspose OCR と .NET の豊かなエコシステムを組み合わせれば、可能性は無限です。

Happy coding, and may your OCR always be spot‑on!  

![Extract text from png example](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}