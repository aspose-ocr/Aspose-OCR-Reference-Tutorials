---
category: general
date: 2026-03-26
description: C#でAspose OCRを使用してPNGからテキストを認識し、レシートデータを抽出します。画像をJSON‑Lに変換し、OCRでレシートを処理する完全な例です。
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: ja
og_description: PNGからテキストを認識し、領収書をJSON‑Lに変換する Aspose OCR を C# で使用。ステップバイステップのコードとヒントをフルで提供。
og_title: PNGからテキストを認識する – Aspose OCR C# ガイド
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: PNGからテキストを認識する – Aspose OCR C# JSON‑L チュートリアル
url: /ja/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from png – Full Aspose OCR C# Guide

PNG ファイルから **テキストを認識** したいけれど、どのライブラリが行単位できれいに結果を出してくれるか分からない、ということはありませんか？ 小規模ビジネスアプリでは、領収書が PNG 画像として保存されており、金額・日付・店舗名を抜き出すのが日々の課題です。

朗報です！数行の C# と **Aspose OCR** ライブラリさえあれば、**領収書からテキストを抽出** し、**画像を jsonl に変換** して下流の分析に活用できます。このチュートリアルでは、PNG の読み込み、OCR の実行、各行を JSON‑L ファイルに書き出すまでの全パイプラインを解説するので、すぐに **OCR で領収書を処理** できるようになります。

必要なものはすべて網羅しています：必須 NuGet パッケージ、実行可能な完全プログラム、各ステップの重要性の解説、領収書が乱雑になったときに役立つ実践的なコツ。外部ドキュメントは不要です。コピー＆ペーストして実行し、必要に応じてカスタマイズしてください。

---

## What You’ll Learn

- `Aspose.OCR` を使って **PNG からテキストを認識** する方法  
- 領収書の **テキストを行オブジェクトとして抽出** し、信頼度スコアを取得する方法  
- **画像を jsonl に変換** して、各 OCR 行を個別の JSON オブジェクトにする方法  
- **OCR で領収書をエンドツーエンドに処理** し、空画像や低信頼度行といったエッジケースに対応する方法  
- 一般的な OCR の問題点のトラブルシューティングと精度向上のコツ  

### Prerequisites

- .NET 6.0 以上（.NET Core や .NET Framework でも動作します）  
- Visual Studio 2022 もしくはお好みの IDE  
- 有効な Aspose OCR ライセンス（Aspose.com から無料の一時ライセンスを取得可能）  
- `receipt.png` として保存したサンプル領収書（任意のフォルダーに配置）  

---

## Step 1: Recognize text from png with Aspose OCR

最初に必要なのは初期化済みの `OcrEngine` です。このオブジェクトは OCR エンジンの設定（言語、検出モードなど）を保持します。デフォルトでは英語が使用され、ページレイアウトは自動検出されるため、ほとんどの領収書で問題なく動作します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Why this matters:**  
`OcrEngine` は重い処理を担うコンポーネントです。一度作成して複数画像で再利用すれば、メモリの消費を抑えられます。別言語（例：スペイン語の領収書）を扱う場合は、`ocrEngine.Language = OcrLanguage.Spanish;` を `Recognize` 呼び出し前に設定してください。

---

## Step 2: Extract text from receipt lines

`OcrResult` には `Lines` というコレクションがあり、各行は生テキストと信頼度スコア（0‑100）を保持します。これを取り出すことで、低信頼度の行を除外したり、手動レビューの対象にしたりと、細かい制御が可能になります。

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Why we escape JSON:**  
領収書のテキストには引用符（`"`）やバックスラッシュ（`\`）が含まれることがあり、これらをエスケープしないと JSON が壊れます。`EscapeJson` メソッドは有効な JSON 行を保証します。

**What the output looks like:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

各行が個別のレコードになるため、データレイクへのストリーミングや機械学習モデルへの入力に最適です。

---

## Step 3: Convert image to JSONL – handling edge cases

大量の領収書を処理する際、空画像・破損画像・極端に低い信頼度スコアの画像が混ざることがあります。パイプラインを少しだけ頑健にしましょう。

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Why filter:**  
薄く印刷された紙の領収書は、低信頼度のノイズ文字を多く生成します。80 % 未満の行を除外すれば、ノイズは減り、実用的なデータだけが残ります。

---

## Step 4: Process receipt with OCR – end‑to‑end example

すべてをまとめた **完全版・すぐに実行可能** なプログラムです。`YOUR_DIRECTORY` を PNG ファイルが入っているフォルダーに置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Running the code:**  
1. プロジェクトフォルダーでターミナルを開く。  
2. `dotnet add package Aspose.OCR` – ライブラリをインストール。  
3. `dotnet run` – 成功メッセージと `receipt.jsonl` が生成されます。

**Expected result:** 行単位で区切られた JSON ファイルで、各行が領収書の行に対応し、信頼度スコアも含まれます。このファイルを Power BI、Elastic、または JSON‑L を扱える任意の分析ツールにパイプできます。

---

## Common Pitfalls & Pro Tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | 画像パスが間違っている、またはファイルが PNG でない | パスを再確認し、`File.Exists(imagePath)` を使用 |
| **Garbage characters** | DPI が低すぎる、または過度に圧縮された PNG | 300 dpi 以上のスキャンを使用し、JPEG 圧縮は避ける |
| **Too many low‑confidence lines** | 熱紙で印刷された領収書が薄くなっている | `minConfidence` 閾値を上げるか、画像前処理（コントラスト/閾値）を実施 |
| **JSON parsing errors** | 領収書テキストにエスケープされていない引用符が含まれる | `EscapeJson` ヘルパーを残すか、`System.Text.Json` で安全にシリアライズ |

**Pro tip:** 特定フィールド（例：合計金額）を抽出したい場合は、JSON‑L ファイル生成後に各 `line.Text` に対してシンプルな正規表現を走らせると便利です。OCR とビジネスロジックを分離でき、デバッグが楽になります。

---

## Extending the Solution

- **バッチ処理:** `Main` のロジックをディレクトリ内のすべての PNG ファイルに対する `foreach` にラップする。  
- **多言語サポート:** `ocrEngine.Language = OcrLanguage.Spanish;`（またはサポートされている任意の言語）を `Recognize` 前に設定。  
- **構造化出力:** 行単位の JSON ではなく、`Date`、`Merchant`、`Total` プロパティを持つ `Receipt` オブジェクトを作成し、最後に一括シリアライズする。

これらのバリエーションでも **画像を jsonl に変換** するコアは変わらないので、下流のコンシューマだけを差し替えて OCR 部分はそのまま利用できます。

---

## Conclusion

Aspose OCR を使って **PNG からテキストを認識** し、**領収書からテキストを抽出**、さらに **画像を jsonl に変換** する方法をご紹介しました。完全な C# プログラムは、PNG の読み込み、エッジケース処理、クリーンな JSON‑L ファイル書き出しまでの全工程を実演していますので、すぐに自分のプロジェクトで **OCR で領収書を処理** できるようになります。

サンプル領収書で試し、信頼度閾値を調整すれば、ノイズだらけの画像スタックが構造化データに変わります。慣れたらバッチ処理や、費用カテゴリを自動分類する小さな機械学習モデルの組み込みにも挑戦してみてください。

質問や便利なカスタマイズがあれば、下のコメントでぜひ共有してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}