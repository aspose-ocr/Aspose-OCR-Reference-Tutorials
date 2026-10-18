---
category: general
date: 2026-03-04
description: 画像の傾きを補正し、コントラスト調整でOCR精度を向上させ、画像を強化してテキストを認識する方法を学びましょう。
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: ja
og_description: 画像の傾きを補正し、OCR結果を向上させる方法。コントラストの適用方法を学び、OCR精度を改善し、再利用可能なパイプラインで画像からテキストを認識します。
og_title: 画像の傾き補正方法 – 完全なC# OCRチュートリアル
tags:
- OCR
- C#
- image‑processing
title: OCR用画像の傾き補正方法 – ステップバイステップ C# ガイド
url: /ja/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像の傾き補正（Deskew）方法 – 完全な C# OCR チュートリアル

OCR エンジンが実際にテキストを読み取れるように **画像の傾き補正（deskew）** をしたことがありますか？ あなただけではありません。実際のプロジェクト—スキャンした領収書、撮影した契約書、スマートフォンで撮ったぼやけたレシート—では、画像が完全に水平でないことが多いです。ページが傾いていると文字認識器が混乱し、結果は意味不明な文字列になってしまいます。

朗報です！ 画像を **傾き補正** し、さらに **コントラスト** を調整すれば、 **OCR の精度を大幅に向上** させることができます。このチュートリアルでは、傾き補正フィルタとコントラスト強化を適用した後に **画像からテキストを認識** する完全な C# のサンプルを順を追って解説します。また、コントラストの正しい適用方法、エッジケースの取り扱い、どのプロジェクトにも組み込める再利用可能なパイプラインの作り方も紹介します。

## 本ガイドで得られるもの

- 傾き補正とコントラスト調整が OCR にとってなぜ重要かを分かりやすく解説  
- フィルタパイプラインを構築し、OCR エンジンに接続して複数画像を読み取る、すぐに実行できる C# コードサンプル  
- 同じパイプラインを多数のファイルで再利用する方法、失敗ケースの処理、精度向上の測定方法のヒント  
- 画像の二値化、ノイズ除去、多言語 OCR など、関連トピックへのリンク（ページ遷移なし）

**前提条件** – .NET 6+ 環境、フィルタパイプラインに対応した OCR ライブラリ（例：Tesseract‑.NET、IronOCR、または任意の商用 SDK）、サンプル PNG が数枚あれば OK。外部サービスは不要です。

---

## Step 1 – なぜ傾き補正が最初にすべきことなのか

スキャンしたページが数度だけでも回転していると、OCR エンジンは各行のベースラインを斜めに認識します。ほとんどの認識器は水平テキストを前提としているため、角度がずれると信頼度が下がり、置換エラーが増えます。

> **プロのコツ:** 可能であれば、平らな面と十分な照明で画像を撮影してください。ソフトウェアだけで完全に補正できるわけではありません。

コード上では、 “how to deskew image” は主に「支配的な文字行の向きを検出し、ビットマップを 0° に回転させる」ことを意味します。多くの OCR SDK はこの処理を自動で行う `DeskewFilter` を提供しています。

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

このフィルタは「ページのテキストが背景より多い」ことを前提に動作しますが、これはほとんどの文書で当てはまります。余白が多い写真の場合は代替アルゴリズムが必要になることがありますが、一般的なスキャン PDF ではデフォルトで問題ありません。

---

## Step 2 – コントラストを上げて文字を際立たせる

コントラストは最も暗いピクセルと最も明るいピクセルの差です。コントラストが低いスキャンは色あせて見え、OCR エンジンは文字の始点・終点を判別できません。コントラストを上げることで視覚的な分離が「シャープ」になり、 **OCR の精度が向上** します。

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

なぜ 1.2 なのか？ 実務では 10‑30 % 程度の控えめな増幅で十分です。やりすぎると細いフォントのディテールが失われます。自由に実験してみてください。後述のパイプラインでは、アプリ全体を再コンパイルせずにレベルを調整できます。

---

## Step 3 – 再利用可能なフィルタパイプラインの構築

ここで 2 つのフィルタを 1 つのパイプラインにまとめます。これにより、 **画像からテキストを認識** するたびに同じ前処理が適用され、結果が一貫します。

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**パイプラインが必要な理由**  
- **モジュール性:** フィルタの追加・削除が OCR 呼び出しに影響しない  
- **パフォーマンス:** ライブラリ側でバッチ処理が可能になり、メモリ消費が抑えられる  
- **再利用性:** 同じパイプラインを複数の `engine.Recognize` 呼び出しに共有できる  

---

## Step 4 – パイプラインを OCR エンジンに接続

多くの OCR エンジンは `Filters` プロパティまたは `SetFilters` メソッドを持っています。ここでパイプラインを設定すれば、以降のすべての画像は文字解析に入る前に **傾き補正 + コントラスト** が自動的に適用されます。

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

言語モデル（例：English → Spanish）を変更したい場合は、フィルタを接続する **前** に行ってください。前処理段階では順序は影響しません。

---

## Step 5 – 最初の画像でテキストを認識

パイプラインを実際に動かしてみましょう。PNG を読み込み、OCR を実行し、結果を出力します。同じ `engine` インスタンスを使い回すので、フィルタを再構築する必要はありません。

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**期待される結果:** 生のスキャンに比べて文字がきれいに整列し、乱れた文字が大幅に減少したテキストが出力されます。まだエラーが目立つ場合は、コントラスト処理の後に `BinarizeFilter`（白黒二値化）を追加すると効果的です。

---

## Step 6 – 追加ファイルでも同じパイプラインを再利用

フィルタパイプラインの最大の利点は、数十・数百のファイルに対して追加コストなしで使い回せる点です。

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

スキャンした PDF が大量にある場合は、`Directory.GetFiles(...)` で列挙しつつ `engine.Recognize` を呼び出すだけです。傾き補正とコントラストのステップが一定であることが、 **バッチ処理での OCR 用画像強化** の鍵になります。

---

## 完全動作サンプル – すべてをひとつにまとめる

以下は完結したコンソールアプリの全コードです。新規コンソールプロジェクトに貼り付け、使用している OCR SDK の NuGet パッケージを追加して実行してください。2 枚のサンプル画像に対する認識結果がコンソールに出力されます。

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### 期待出力例

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

フィルタパイプラインを **使用しない** バージョンと比較すると、文字欠損や数字のずれ、完全に乱れた行が目に見えて減少しているはずです。これが **画像の傾き補正（how to deskew image）** と **コントラスト適用（how to apply contrast）** を正しく行ったときの測定可能な効果です。

---

## よくある質問 & エッジケース

| 質問 | 回答 |
|----------|--------|
| *画像がすでに正立している場合は？* | `DeskewFilter` は 0° 回転を検出すると元のビットマップをそのまま返すので、オーバーヘッドはほぼありません。 |
| *PDF にも使える？* | はい。多くの OCR SDK は PDF ページを `ImageInfo` として読み込めます。ビットマップ処理は同一なのでパイプラインはそのまま機能します。 |
| *文書にカラー文字があるが、コントラストで色が崩れないか？* | コントラストフィルタは輝度に対して作用するため、色は保持されつつ見やすくなります。純粋な白黒が必要な場合は、コントラスト後に `BinarizeFilter` を追加してください。 |
| *精度向上をどう測る？* | フィルタ適用前後でテストセットに対する OCR を実行し、文字誤り率（CER）や単語誤り率（WER）を算出します。通常、エラーは 10‑30 % 程度減少します。 |
| *パフォーマンスへの影響は？* | 傾き補正はページあたり < 100 ms 程度の CPU コストです。コントラストはピクセル単位の単純演算なので、全体的な影響は OCR 本体に比べてごくわずかです。 |

---

## 次のステップ – OCR をさらに高める

**画像の傾き補正（how to deskew image）**、**コントラスト適用（how to apply contrast）**、そして **画像からテキストを認識（recognize text from image）** できる再利用可能パイプラインが手に入ったので、以下のトピックにも挑戦してみましょう。

- **ノイズ除去** – `MedianFilter` を傾き補正の前に追加して斑点を除去  
- **二値化** – 複雑なスクリプト言語向けに純粋な白黒変換を実施  
- **マルチページ処理** – PDF の各ページをループし、検索可能インデックスに保存  
- **言語モデル切替** – `OcrLanguage.English` と `OcrLanguage.French` を動的に切り替え  
- **ポストプロセッシング** – スペルチェックや正規表現で典型的な OCR 誤認（例: “0” と “O”）を修正  

これらすべてを同じ `FilterBuilder` チェーンに組み込めば、 **OCR 用画像強化（enhance image for OCR）** を実現するモジュール化・保守性の高いソリューションが完成します。

---

## 結論

本稿では **画像の傾き補正（how to deskew image）** の重要性、コントラスト調整が **OCR 精度向上（improve OCR accuracy）** に与える効果、そして **画像からテキストを認識（recognize text from image）** するためのクリーンで再利用可能なパイプライン構築方法を網羅的に解説しました。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}