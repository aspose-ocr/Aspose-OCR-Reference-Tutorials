---
category: general
date: 2026-04-06
description: Aspose OCR を使用して C# で画像のテキストを認識します。テキストの抽出方法、C# で画像ファイルを読み込む方法、C# で JSON
  を書き出す方法を、シンプルなステップバイステップの例で学びましょう。
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: ja
og_description: C#でAspose OCRを使用して画像のテキストを認識します。このガイドでは、テキストの抽出、画像ファイルの読み込み（C#）、およびJSONの書き出し（C#）を迅速に行う方法を示します。
og_title: C#で画像テキストを認識する – 完全ステップバイステップガイド
tags:
- OCR
- C#
- Aspose
title: C#で画像テキストを認識する – JSONエクスポート付き完全ガイド
url: /ja/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で画像テキストを認識する – 完全ステップバイステップガイド

スキャンしたレシートから **画像テキストを認識** したいと思ったことはありませんか？どのライブラリを選べば良いか分からないこともあるでしょう。実際のアプリ—経費トラッカー、請求書処理ツール、アクセシビリティ支援ツール—でも、画像から文字を抽出することが最初のハードルです。  

このチュートリアルでは、Aspose OCR ライブラリを使用して **画像テキストを認識** するハンズオンの解決策を順に解説し、**テキストの抽出方法** を示し、**C#で画像ファイルをロード** する正しい方法をデモし、最後に **C#でJSONを書き出す** 方法を紹介します。これにより、結果を保存または送信できます。最後まで読むと、任意の PNG を整然とした JSON ペイロードに変換する実行可能なコンソールアプリが手に入ります。

---

## 必要なもの

- **.NET 6+**（コードは .NET Framework 4.8 でも動作しますが、.NET 6 が最適です）。
- **Aspose.OCR for .NET** NuGet パッケージ。`dotnet add package Aspose.OCR` でインストールします。
- サンプル画像（`input.png`）を、アプリが読み取れる場所に配置します。  
- Visual Studio 2022 またはお好みのエディタ—特別な IDE のテクニックは不要です。

> プロのコツ: 画像ファイルはプロジェクト内の `Resources` フォルダーに入れておくと、パスが整理され「ファイルが見つからない」エラーを防げます。

---

## ステップ 1: 画像テキストを認識 – 画像ファイルのロード

OCR エンジンが動作する前に、**C#で画像ファイルをロード** する必要があります。`Image.FromFile` メソッドはパスが間違っているかサポート外の形式の場合に例外をスローするため、これを防止します。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*重要な理由*: `using` ブロック内で画像をロードすると、アンマネージドな GDI+ リソースが即座に解放され、長時間稼働するサービスでのメモリリークを防げます。

---

## ステップ 2: Aspose OCR でテキストを抽出する方法

ビットマップがメモリ上にあるので、**画像テキストを認識** エンジンに渡します。Aspose の `OcrEngine` はシンプルで、インスタンス化し、`Recognize` を呼び出すと、生テキスト、信頼度スコア、バウンディングボックスを含む `OcrResult` オブジェクトが取得できます。

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*説明*: `Recognize` メソッドは組み込みのニューラルネットワークを実行します。高コントラストで 300 DPI の画像で最適に動作します。ぼやけた写真を入力すると信頼度が低下するため、実運用コードでは前処理（傾き補正、二値化）を検討してください。

---

## ステップ 3: C#でJSONを書き出す – OCR 結果のエクスポート

多くの API は JSON を期待するため、Aspose の `JsonExport` を使って **C#でJSONを書き出す** 方法を示します。このライブラリは `OcrResult` 全体をシリアライズし、行情報と信頼度を保持します。

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### 期待される JSON 出力

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*なぜ JSON?* 言語に依存せず、デシリアライズが容易で、下流の検証に必要な詳細な OCR メタデータを保持します。

---

## ステップ 4: 完全な実行可能プログラム

各パーツを組み合わせた完全なコンソールアプリです。コピーして貼り付け、NuGet パッケージを復元し、**F5** を押すだけです。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

プログラムを実行し、`Resources/output.json` を開くと、エンジンが認識したすべてが整然とした JSON で表現されているはずです。

---

## 一般的なエッジケースの対処

| Situation | What to Do | Why |
|-----------|------------|-----|
| **画像が null または破損している** | `Image.FromFile` を try/catch でラップし、例外をログに記録する。 | アプリのクラッシュを防ぎ、明確なエラーメッセージを提供します。 |
| **信頼度が低い** | `ocrResult.Words[i].Confidence` を確認し、0.75 未満の場合は前処理（DPI の増加、シャープ化）を検討する。 | 金額抽出などの下流プロセスの信頼性が向上します。 |
| **大きなファイル（>10 MB）** | OCR 前に画像を縮小する（`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`）。 | メモリ負荷を減らし、認識速度を向上させます。 |
| **多言語ドキュメント** | `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` を設定する。 | エンジンが両言語の文字を検出できるようになります。 |

---

## ボーナス: OCR 結果の可視化（オプション）

各単語が画像上のどこに位置するかを確認したい場合、バウンディングボックスを描画できます：

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

生成された `annotated.png` には、認識されたすべての単語の周りに赤い矩形が表示されます—デバッグに便利です。

---

## 結論

C# で **画像テキストを認識** する一連の流れを実装しました：画像ファイルのロード、Aspose OCR を呼び出して **テキストの抽出方法**、そして最終的に **C#でJSONを書き出す** ことでデータを任意の場所へ転送できます。完全なサンプルはすぐに実行でき、追加のヒントによりぼやけたレシートや大容量ファイル、多言語スキャンにも対応できます。

次は何をすべきか？ Aspose を別のエンジン（Tesseract、Microsoft OCR）に置き換えて信頼度スコアを比較したり、JSON をデータベースに保存して経費報告に活用したりできます。また、コンソールアプリを ASP .NET Core Web API に拡張し、画像アップロードを受け取り即座に JSON を返すようにすることも可能です。

スケーリング、エラーハンドリング、Azure Functions との統合に関する質問がありますか？コメントを残すか、GitHub でメンションしてください。コーディングを楽しんで、OCR が常に鮮明でありますように！

---

![Screenshot of OCR JSON output – recognize image text example](https://example.com/ocr-example.png "recognize image text example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}