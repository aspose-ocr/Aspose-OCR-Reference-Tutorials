---
category: general
date: 2026-02-09
description: C# のオフライン OCR を使用して画像からテキストを抽出します。完全な C# OCR のサンプルは、OCR 用に画像を読み込む方法、キリル文字テキストを認識する方法、そしてパスポートからテキストを抽出する方法を示しています。
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: ja
og_description: C# のオフライン OCR で画像からテキストを抽出。OCR 用に画像を読み込み、キリル文字を認識し、パスポートからテキストを抽出するステップバイステップの
  C# OCR 例を学びましょう。
og_title: C#で画像からテキストを抽出する – オフラインOCRガイド
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを抽出 – オフラインOCRの例
url: /ja/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを抽出 – オフライン OCR の例

画像からテキストを抽出**（extract text from image）**する必要があったが、ネットワーク依存の API に行き詰まったことはありませんか？ あなたは一人ではありません。特に制限された環境では、OCR サービスが実行時に言語パックをダウンロードしようとして壁にぶつかる開発者が多数います。

このガイドでは、完全にオフラインで実行され、OCR 用に画像を読み込み、パスポートからキリル文字テキストを認識する **c# ocr example** を順に解説します。最後までに、任意のサポート対象画像のプレーンテキスト内容をコンソールに直接出力する、すぐに実行できるプログラムが手に入ります。

## 学べること

- Aspose.OCR をオフライン処理用に設定する方法。  
- ディスクから **load image for OCR** する正確なコード。  
- エンジンを **recognize cyrillic text** に設定する方法。  
- パスポート形式の写真からテキストを抽出する、完全なコピー＆ペースト可能な **c# ocr example**。  

Aspose の事前経験は不要です。.NET 6（またはそれ以降）の SDK と Visual Studio 2022（または VS Code）さえあれば十分です。

---

![Aspose OCR を使用してパスポート写真からテキストを抽出](/images/ocr-passport.jpg "画像からテキストを抽出")

## 手順 1: 画像からテキストを抽出するプロジェクトの設定

コードを書く前に、Aspose.OCR NuGet パッケージがプロジェクトに追加されていることを確認してください：

```bash
dotnet add package Aspose.OCR
```

> ※ **Pro tip:** `--version` フラグを使用して最新の安定版リリース（例: `13.9.0`）に固定してください。これにより .NET 6 との互換性が保証されます。

新しいコンソールアプリを作成するのは次のように簡単です。

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

これでインターネットに一切触れずに **画像からテキストを抽出** できるクリーンな状態が整いました。

## 手順 2: OCR 用に画像を読み込む – パスポート写真の読み取り

OCR エンジンが最初に必要とするのは、画像を表すビットマップまたはストリームです。今回のシナリオでは、ローカルファイル `cyrillic_passport.jpg` から **画像を OCR 用に読み込む** ことにします。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> ※ **Why this matters:** 生の `Bitmap` ではなくストリームを提供することで、Aspose が内部でフォーマット検出を行い、ボイラープレートや潜在的なバグを減らすことができます。

## 手順 3: オフラインモードを設定し、キリル文字言語を選択

Aspose.OCR はオンザフライで言語モデルをダウンロードできますが、オフラインソリューションの目的に反します。ネットワーク呼び出しを無効にし、エンジンに使用する言語を明示的に指定しましょう。

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> ※ **Edge case:** 後で同じ文書内でラテン文字を認識する必要がある場合は、配列に `OcrLanguage.English` を追加するだけです。エンジンは自動的にマルチ言語検出を処理します。

## 手順 4: OCR エンジンを実行し、キリル文字テキストを認識

これで実際に **パスポート形式の画像からテキストを認識** します。`Recognize` メソッドは、プレーンテキスト、信頼度スコア、バウンディングボックスを含むリッチな結果オブジェクトを返します。

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### 期待されるコンソール出力

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

結果が文字化けしている場合は、元画像が鮮明であること、そして `OfflineMode` 用のキリル文字言語パックが Aspose のインストールフォルダー（通常は `\\Aspose.OCR\\resources\\languages`）に存在することを再確認してください。

## 完全な C# OCR 例 – 完全ソースコード

以下は **c# ocr example** の全体です。`Program.cs` にコピー＆ペーストして `dotnet run` を実行してください。**画像からテキストを抽出** するために必要なものはすべてここにあります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### 実行例

```bash
dotnet run
```

コンソールにキリル文字のパスポート情報が表示されるはずです。これが **画像からテキストを抽出** パイプラインが機能していることを確認できる瞬間です。

## よくある落とし穴と対処法

| 症状 | 考えられる原因 | 対策 |
|---------|--------------|-----|
| Empty `PlainText` | 言語モデルが間違っている、または画像が暗すぎる | `OfflineMode` 言語に `Cyrillic` が含まれていることを確認し、画像のコントラストを上げてください |
| `System.DllNotFoundException` | ネイティブ Aspose OCR バイナリが欠如 | NuGet パッケージを再インストールするか、`Aspose.OCR.Native.dll` を出力フォルダーにコピーしてください |
| 大きな画像での低速 | エンジンがフル解像度で処理 | `ImageStream` に渡す前に画像を幅 ≤ 1500 px に縮小してください |
| 文字化け | 画像が正しく回転していない | ストリーム作成前に `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` を使用してください |

## 次のステップ – オフライン OCR ワークフローの拡張

- `MemoryStream` から **Load image for OCR** を行い、ASP.NET Core でアップロードされたファイルを処理する。  
- フォルダー内のパスポートスキャンをループして、バッチモードで **recognize text from passport** に切り替える。  
- 結果を **regular expressions** と組み合わせて、パスポート番号や生年月日などのフィールドを抽出する。  
- `ocrEngine.Configuration.UseParallelProcessing = true` を試して、マルチコアでの高速化を実現する。

---

### 結論

ここでは、完全にオフラインの C# OCR パイプラインを使用して **画像からテキストを抽出** する方法を示しました。短く自己完結型の **c# ocr example** は画像を読み込み、エンジンを **recognize cyrillic text** に設定し、抽出したパスポートデータを出力します—ネットワーク要求は一切発生しません。

コードを自由に調整したり、言語を追加したり、出力をデータベースに接続したりしてください。画像を OCR 用に読み込む基本と、パスポート形式の写真からテキストを認識する方法をマスターすれば、可能性は無限です。

質問がある、または独自の調整を共有したい方は、下にコメントを残してください。コーディングをお楽しみください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}