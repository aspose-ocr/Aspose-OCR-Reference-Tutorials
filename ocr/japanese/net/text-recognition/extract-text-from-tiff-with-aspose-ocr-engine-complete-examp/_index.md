---
category: general
date: 2026-04-04
description: C# の OCR エンジンの例を使って、TIFF ファイルからテキストを抽出する方法を学びましょう。JSON および XML 出力付きのステップバイステップガイドです。
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: ja
og_description: C#でOCRエンジンを使用してTIFFファイルからテキストを抽出する例。詳細な手順、完全なコード、JSON/XML出力のためのヒント。
og_title: Aspose OCRエンジンでTIFFからテキストを抽出する – 完全ガイド
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Aspose OCRエンジンでTIFFからテキストを抽出 – 完全サンプル
url: /ja/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFFからテキストを抽出 – 完全なOCRエンジン例（C#）

Ever needed to **TIFFからテキストを抽出** images but weren’t sure which library could handle multi‑page files without a circus of workarounds? You’re not the only one. In many legacy systems, documents arrive as multi‑page TIFF scans, and pulling the raw text out is a must‑have feature for search, compliance, or data entry automation.

The good news? With Aspose OCR you can do it in a handful of lines—no fiddling with low‑level pixel buffers. This tutorial walks you through a **完全なOCRエンジン例** that loads a multi‑page TIFF, recognizes every page, and spits out both pretty‑printed JSON and optional XML. By the end you’ll have a ready‑to‑run C# console app that extracts text from TIFF files in seconds.

## 学べること

- .NETプロジェクトでAspose OCRエンジンをセットアップする方法。  
- マルチページ処理を含む、**TIFFからテキストを抽出**するために必要な正確なコード。  
- JSONとXMLの出力を選択する理由と、両方を生成する方法。  
- 一般的な落とし穴（例：画像のDPI、メモリ使用量）のトラブルシューティングのヒント。  

### 前提条件

- .NET 6.0 SDK 以上（コードは .NET Core と .NET Framework でも動作します）。  
- 有効な Aspose OCR ライセンス（または無料トライアルキー）。  
- Visual Studio 2022 またはお好みの C# エディタ。  
- サンプルのマルチページTIFFファイル（例では `multi-page.tiff` と命名）。

> **プロのコツ:** 予算が限られている場合でも、無料トライアルでは月最大100ページまでテキストを抽出できるので、テストに最適です。

---

## ステップ1 – OCRエンジンの初期化 (ocr engine example)

TIFFからテキストを抽出**する前に、OCRエンジンのインスタンスが必要です。このオブジェクトは、後で調整できるすべての設定（言語、解像度など）を保持します。

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*この点が重要な理由:* `OcrEngine` クラスは重い処理を抽象化します。一度インスタンス化して複数の画像で再利用する方が、ページごとに新しいエンジンを作成するよりもメモリ効率が良いです。

---

## ステップ2 – マルチページTIFFのロード (extract text from TIFF)

ここでエンジンにソースファイルを指定します。`ImageStream.FromFile` は TIFF、JPEG、PNG など多数をサポートしていますが、このチュートリアルでは TIFF に焦点を当てます。

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **注意:** `YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。  
> **ヒント:** TIFF の DPI が低い（150 未満）場合は、OCR精度向上のために事前処理を検討してください。

---

## ステップ3 – すべてのページを認識

`Recognize()` を呼び出すと、TIFF の **すべてのページ** に対して OCR アルゴリズムが実行されます。結果オブジェクトには生テキスト、信頼度スコア、ページ単位のセグメンテーションが含まれます。

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*取得できる情報:* `ocrResult` は `PageResult` オブジェクトのコレクションを保持します。各ページのテキストは `ocrResult.Pages[i].Text` で取得できます。エンジンは信頼度レベルも提供し、品質チェックに役立ちます。

---

## ステップ4 – 結果をJSONとして保存（オプションでXMLも）

最新のパイプラインの多くはJSONを好みますが、レガシーシステムは依然としてXMLを使用します。ここでは、整形された両方の形式を生成する方法を示します。

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### サンプルJSON出力（省略）

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON は人間が読みやすく、デバッグが容易です。必要に応じて XML も同じ構造で出力されます。

---

## ステップ5 – 抽出結果の検証 (extract text from TIFF)

ファイルを書き出した後、簡単なサニティチェックで問題がないか確認します。

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

スニペットが表示されれば、**TIFFからテキストを抽出**し、永続化に成功したことになります。ここから JSON を検索インデックスやデータベース、その他の下流サービスに渡すことができます。

---

## なぜ Aspose OCR を使って TIFF からテキストを抽出するのか？

- **マルチページサポートが標準** – TIFF を手動で分割する必要はありません。  
- **高精度** – 独自のニューラルネットワークモデルによるものです。  
- **クロスプラットフォーム** – Windows、Linux、macOS の .NET ランタイムで動作します。  
- **豊富な出力形式**（JSON、XML、プレーンテキスト）で、モダンとレガシーの両スタックに対応します。  

まだ迷っている場合は、サンプルドキュメントで無料トライアルを試してみてください。オープンソースの代替品がしばしば追加の画像前処理を必要とするのに比べ、速度とシンプルさが際立ちます。

---

## よくある落とし穴と回避策

| Issue | Symptom | Fix |
|-------|---------|-----|
| Low‑resolution TIFF | Missing characters, low confidence | Upscale the image to ≥150 DPI before OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Wrong language | Garbled words, especially for non‑English text | Set `ocrEngine.Language = Language.Spanish` (or appropriate) before `Recognize()` |
| Out‑of‑memory on huge files | `OutOfMemoryException` | Process pages in batches: loop through `ocrEngine.Image.Pages` and call `RecognizePage(i)` |
| License not applied | Watermark “Evaluation” in output | Register your license: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

| Issue | Symptom | Fix |
|-------|---------|-----|
| 低解像度TIFF | 文字が欠ける、信頼度が低い | OCR 前に画像を ≥150 DPI に拡大する (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| 言語設定ミス | 文字化け、特に英語以外のテキストで | `Recognize()` の前に `ocrEngine.Language = Language.Spanish`（または適切な言語）を設定する |
| 巨大ファイルでメモリ不足 | `OutOfMemoryException` | ページをバッチ処理する：`ocrEngine.Image.Pages` をループし `RecognizePage(i)` を呼び出す |
| ライセンス未適用 | 出力に “Evaluation” の透かしが表示 | ライセンスを登録する: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## 完全動作例（コピー＆ペースト可能）

以下は新しいコンソールプロジェクトに貼り付けられる完全なプログラムです。初期化、ロード、認識、保存のすべての要素が含まれています。

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すると、コンソールに JSON と XML の保存先が表示されます。これで、TIFF からテキストを抽出する **OCRエンジン例** が完了しました。

---

## 次のステップと関連トピック

- **バッチ処理:** 上記ロジックを `foreach` ループでラップし、数十の TIFF ファイルを自動的に処理します。  
- **検索統合:** JSON を Elasticsearch や Azure Cognitive Search にプッシュして、スキャン文書の全文検索を実現します。  
- **画像前処理:** Aspose の `ImageProcessing` API を調査し、OCR 前に傾き補正、ノイズ除去、コントラスト調整などを行います。  
- **代替出力:** メタデータが不要で生文字列だけが必要な場合は `ocrResult.ToPlainText()` を使用します。  

他の画像形式に興味がある場合も、同じパターンが PDF（ソースファイルを変更するだけ）や PNG でも機能します。重要なポイントは、エンジンを設定すれば残りは繰り返し可能なパイプラインになることです。

---

## 結論

ここでは、Aspose OCR を使用して **TIFF からテキストを抽出** できる **完全な OCR エンジン例** を解説し、クリーンな JSON とオプションの XML を下流のワークフロー向けに出力しました。コードは単体で完結しており、各ステップの「なぜ」も説明しています。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}