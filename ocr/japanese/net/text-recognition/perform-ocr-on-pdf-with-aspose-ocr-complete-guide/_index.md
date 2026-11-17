---
category: general
date: 2026-05-06
description: C#でAspose OCRを使用してPDFファイルのOCRを実行する方法を学びます。このチュートリアルでは、PDFからテキストを抽出し、OCR用にPDFを読み込む方法も示しています。
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: ja
og_description: Aspose OCR を使用して C# で PDF の OCR を実行する方法を紹介します。ステップバイステップのコード、解説、そして
  PDF からテキストを効率的に抽出するためのヒントをご提供します。
og_title: Aspose OCRでPDFのOCRを実行する – 完全ガイド
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCRでPDFのOCRを実行する – 完全ガイド
url: /ja/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR で PDF の OCR を実行する – 完全ガイド

スキャンした **PDF に OCR を実行** したいけど、どこから始めればいいかわからないことはありませんか？同じ悩みを持つ人は多いです。実務では、請求書の自動処理やアーカイブされたレポートのデジタル化など、スキャンされた PDF からテキストを抽出できることが必須です。  

このチュートリアルでは、Aspose OCR ライブラリを使って **PDF に OCR を実行** するだけでなく、**PDF からテキストを抽出**、**OCR 用に PDF をロード**、さらには多言語ドキュメントの処理方法も紹介します。最後まで読めば、スキャンされた PDF を検索可能で編集可能なテキストに変換する C# プログラムがすぐに実行できるようになります。

## 学べること

- .NET プロジェクトに Aspose OCR を設定する方法。  
- **OCR 用に PDF をロード** してエンジンに渡す正確な手順。  
- PDF が英語・フランス語・ドイツ語など混在している場合に、ページごとに言語をマッピングする方法。  
- 出力結果の検証方法と、よくある落とし穴のトラブルシューティング。  

> **プロのコツ:** 大容量の PDF を扱う場合は、ページを並列処理して実行時間を数分短縮できます。後ほどその方法に触れます。

## 前提条件

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）。  
- 有効な Aspose OCR ライセンス、または一時的な評価キー。  
- `multilang.pdf` という名前のスキャン PDF を、コードから参照できるフォルダーに配置しておくこと。  

その他のサードパーティ パッケージは不要です。

---

## Step 1 – Aspose OCR をインストールしてエンジンを作成

まず、プロジェクトに Aspose.OCR NuGet パッケージを追加します。

```bash
dotnet add package Aspose.OCR
```

パッケージがインストールできたら、OCR エンジンのインスタンスを作成します。このオブジェクトが処理の中心で、画像や PDF を読み取りテキストに変換する役割を担います。

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **なぜ重要か:** エンジンを一度初期化してページ間で再利用すれば、メモリ使用量が抑えられ処理速度も向上します。

---

## Step 2 – OCR 用に PDF ドキュメントをロード

エンジンは PDF を直接開くことができますが、対象ファイルを指定する必要があります。これが多くの開発者が見落としがちな **OCR 用に PDF をロード** のステップです。

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

`YOUR_DIRECTORY` を実際のパスに置き換えてください。PDF がリソースとして埋め込まれている場合は、ストリームからロードすることも可能です。

> **エッジケース:** PDF がパスワード保護されている場合は、`ocrEngine.LoadPdf(path, password)` を呼び出して復号パスワードを渡します。

---

## Step 3 – 言語をページにマッピング（オプションだが強力）

スキャン PDF が複数言語で構成されていることは珍しくありません。デフォルトでは Aspose OCR は英語を想定しているため、フランス語やドイツ語のページでは精度が低下します。ここでは、ページごとに使用言語を指定するシンプルな辞書を作成します。

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **こうする理由:** 正しい言語を指定すると、特にアクセント文字や言語固有の句読点の認識精度が大幅に向上します。

---

## Step 4 – OCR を実行し結果を取得

いよいよ本番です。`Recognize()` を呼び出すと、先ほど設定した言語マップに従って *すべて* のページが処理されます。

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

`recognitionResult` オブジェクトの `Text` プロパティには、各ページで認識されたテキストが結合された形で格納されます。

---

## Step 5 – 抽出したテキストを出力

最後に、結合されたテキストをコンソールに書き出すだけです。もちろん、ファイルやデータベース、他のシステムへ出力することも可能です。

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

ファイルに書き出す場合は次のようにします。

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **検証のコツ:** 生成された `extracted_text.txt` を開き、各言語の既知の単語を検索してみてください。フランス語のアクセントが文字化けしている場合は、言語マップを再確認しましょう。

---

## 完全動作サンプル

すべてを組み合わせた、すぐに実行できる完全版プログラムです。新しいコンソールプロジェクトに貼り付けて **F5** を押すだけです。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**期待される出力**（抜粋）:

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## 大容量 PDF の処理とパフォーマンス調整

PDF が数百ページに及ぶ場合は、次の調整を検討してください。

1. **チャンク処理** – 50 ページずつ処理し、途中結果をディスクに書き出す。  
2. **並列処理** – `Parallel.ForEach` と個別の `OcrEngine` インスタンスを組み合わせて実行（各エンジンは初期化後スレッドセーフ）。  
3. **メモリ管理** – 各チャンク処理後に `ocrEngine.Dispose()` を呼び出し、ネイティブリソースを解放する。

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## よくある落とし穴と対処法

| 症状 | 想定原因 | 対処法 |
|------|----------|--------|
| フランス語ページで文字化け | 言語設定が間違っている | 該当ページで `PageLanguageProvider` が `OcrLanguage.French` を返すように確認 |
| 出力ファイルが空 | PDF がロードされていない（パスが誤り） | パスを再確認し、他プロセスがファイルをロックしていないか確認 |
| 巨大 PDF でメモリ不足例外 | エンジンが PDF 全体を一度に読み込んでいる | `LoadPdf` の単ページオーバーロードを使用するか、チャンク処理に分割 |
| 処理が遅い（100 ページで 5 分超） | シングルスレッド実行 | 前述の並列処理を有効化 |

---

## 次のステップ – 基本 OCR を超えて

**PDF に OCR を実行**し、**PDF からテキストを抽出**できるようになったら、次のような拡張も検討できます。

- **検索可能 PDF の作成** – Aspose.PDF を使って OCR テキストを元の PDF に埋め込み、検索可能にする。  
- **データ抽出** – 正規表現で請求書番号、日付、合計金額などを抽出。  
- **AI 連携** – OCR 出力を Azure OpenAI などの言語モデルに渡し、要約や分類を実施。  

これらの拡張もすべて **OCR 用に PDF をロード** できることが前提なので、基礎はすでに完成しています。

---

## まとめ

本稿では、Aspose OCR を使用して C# で **PDF に OCR を実行** し、**PDF からテキストを抽出** するために必要な手順をすべて網羅しました。ライブラリのインストール、PDF のロード、ページ単位の言語設定、認識エンジンの実行、そして最終的なテキスト保存まで、実務でそのまま使える生産性の高いソリューションをご紹介しました。  

並列処理や言語コンビネーションの実験、他の文書処理ライブラリとの組み合わせなど、自由にカスタマイズしてみてください。問題が発生したら上記のトラブルシューティング表を参照するか、コメントで質問を残してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}