---
category: general
date: 2026-02-20
description: C#で画像からテキストを抽出し、JSONに変換して領収書を読み取る方法を学びます。Aspose OCRを使用したステップバイステップのコード。
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: ja
og_description: C#で画像ファイルを読み込み、Aspose OCRでテキストを抽出し、結果をJSONに変換してレシートを読み取る方法をご紹介します。完全なコード例です。
og_title: C#で領収書を読み取る方法 – テキスト抽出、JSONへ変換
tags:
- C#
- OCR
- Image Processing
- JSON
title: C#で領収書を読み取る方法 – 画像からテキストを抽出する完全ガイド
url: /ja/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

shortcodes.

Then heading "# How to Read Receipt in C# – Complete Guide" translate to Japanese: "# C#でレシートを読み取る方法 – 完全ガイド". Keep same heading level.

Then paragraph.

We need to translate natural Japanese.

Proceed.

Be careful to keep markdown formatting.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でレシートを読み取る方法 – 完全ガイド

レシート画像をプログラムで **読み取る方法** を考えたことはありませんか？たとえば、家計簿アプリを作っていて、レシートの写真から項目ごとの金額を抽出したいときなどです。実際に経験した中で最大の痛点は、ぼやけた JPEG を実際に使える構造化データに変換することです。朗報です！C# と Aspose OCR を数行書くだけで **画像からテキストを抽出** し、**画像を JSON に変換** でき、ほぼ魔法のように感じられます。

このチュートリアルを終えると、**画像ファイルを C# で読み込む**、OCR を実行する、そして詳細な JSON ペイロードを出力する、すぐに実行可能なソリューションが手に入ります。外部サービスや面倒な REST 呼び出しは不要です。純粋な .NET コードだけで、コンソール アプリでも ASP.NET プロジェクトでもそのまま組み込めます。最後まで読めば、各ステップの重要性、一般的なエッジケース（非標準サイズのレシートなど）の対処法、そして JSON 出力の実際の形が理解できるようになります。

## 必要なもの

- **.NET 6.0 以降** – コードは `System.Drawing.Common` を使用します。Windows、Linux、macOS でサポートされています。
- **Aspose.OCR for .NET** – 無料トライアルの NuGet パッケージ (`Aspose.OCR`) を取得するか、ライセンス版を使用してください。
- アプリが読み取れる場所に置いた **サンプルレシート画像** (`receipt.jpg`)。
- お好きな IDE（Visual Studio、Rider、VS Code など）。

以上です。追加設定や API キーは不要です。

---

## Step 1 – Load the Image File C# (Primary Keyword in Action)

OCR エンジンが魔法をかける前に、画像をメモリに読み込む必要があります。これは多くの開発者が見落としがちな、いわゆる “load image file C#” ステップです。

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**重要ポイント:**  
`Image.FromFile` はファイルを **一度だけ** 読み込みハンドルを保持します。大量のレシートをループで処理する場合は、ファイルロックを回避するために `Image.FromStream` の使用を検討してください。

> **プロのコツ:** `FileNotFoundException` が発生したら、パスを再確認し、画像が実際に存在するか確認しましょう。相対パス (`"./receipt.jpg"`) でも動作しますが、本番環境では絶対パスの方が安全です。

---

## Step 2 – Create and Configure the OCR Engine

Aspose OCR にはすぐに使える `OcrEngine` が同梱されています。モデルを自前で学習させる必要はありません。ライブラリは印刷されたテキストの読み取りに対応しており、ほとんどのレシートで使用できるフォントです。

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**このオプション設定の理由:**  
`DetectOrientation` は、レシートが逆さまにスキャンされていた場合に自動で画像を回転させます。言語を設定すると文字セットが絞り込まれ、特に英数字のみが必要な場合に精度が向上します。

---

## Step 3 – Recognize the Image and Convert to JSON

いよいよ楽しいパートです。**画像からテキストを抽出** し、**画像を JSON に変換** する処理を一括で実行します。

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

`RecognizeToJson` メソッドは以下のようなリッチな JSON 構造を返します。

- `Text`: 連結されたプレーンテキスト。
- `Lines`: 座標情報を含む行オブジェクトの配列。
- `Words`: 各単語と信頼度スコア。
- `Regions`: 検出されたテキストブロックのバウンディングボックス。

型安全に扱いたい場合は、この JSON を C# のオブジェクトにデシリアライズできますが、多くのシナリオではそのまま生の JSON を出力するだけで十分です。

---

## Step 4 – Output the JSON (or Store It)

出力結果を確認し、次に何をすべきか考えてみましょう。

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### サンプル出力

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**次のステップは？**  
`Lines` 配列を解析して `Total` 金額を抽出したり、JSON を下流サービスに渡して費用項目を保存したりできます。結果がすでに JSON 形式なので、NoSQL データベース、Azure Function、Power Automate フローなど、好きな場所にそのまま流し込めます。

---

## Step 5 – Handling Common Edge Cases

どんなに優秀な OCR エンジンでも、いくつかのケースでつまずきます。以下は **レシート画像を読み取る方法** を学んでいるときに遭遇しやすいシナリオと対策です。

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **低解像度レシート（≤ 150 dpi）** | `Bitmap` と `Graphics`（`InterpolationMode.HighQualityBicubic`）で先に拡大してください。 |
| **回転または歪んだレシート** | `DetectOrientation = true` を維持します。大幅な歪みがある場合は `Image.RotateFlip` や OpenCV などのサードパーティライブラリで前処理を行います。 |
| **背景がカラー（例：テーブル上のレシート）** | グレースケールに変換し、コントラストを上げてから OCR を実行します（`ImageAttributes` を使用）。 |
| **1枚の写真に複数レシートが写っている** | 各レシート領域を手動で切り取るか、`ocrEngine.Config.RecognizeMultipleRegions = true` を利用します。 |
| **ファイルが大きくて OutOfMemory が発生** | `using` ステートメントで `Image` オブジェクトを速やかに破棄するか、チャンク単位で処理します。 |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Step 6 – Full Working Example (Copy‑Paste Ready)

以下は今すぐコンパイルできる **完全版プログラム** です。すべてのステップ、必要な `using` ディレクティブ、エラーハンドリングが含まれています。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**実行方法:**  
プロジェクトフォルダーで `dotnet run` を実行してください。環境が正しく設定されていれば、コンソールに JSON が表示され、レシート画像と同じフォルダーに保存されます。

---

## Conclusion

ここまでで **C# でレシート画像を読み取る方法** を最初から最後まで網羅しました。画像を読み込み、Aspose OCR を設定し、`RecognizeToJson` を呼び出すだけで、**画像からテキストを抽出** し、**画像を JSON に変換** でき、ほぼボイラープレートは不要です。この手法は、単一レシートのデモから、毎晩数百枚のレシートを処理するバッチプロセッサまでスケールします。

次に試したいこと:

- **JSON を解析** して日付、合計、明細行を抽出（`System.Text.Json` または `Newtonsoft.Json` を使用）。
- **データベースと統合**（SQL、Cosmos DB など）して費用レコードを自動保存。
- **UI を追加**（WinForms、WPF、Blazor）し、ユーザーがレシートをドラッグ＆ドロップできるように。
- **Aspose OCR を別エンジンに置き換え**（Tesseract、Microsoft Azure OCR など）してライセンスコストを調整。ただし、同じ “load image file C#” パターンは維持してください。

ぜひ実験し、失敗し、そしてここに戻ってリフレッシュしてください。問題が発生したら、コミュニティ（および Aspose フォーラム）で質問すると良いでしょう。コーディングを楽しみながら、紙のレシートをクリーンで検索可能なデータに変換しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}