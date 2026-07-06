---
category: general
date: 2026-03-13
description: Aspose OCR を使用して任意の画像から検索可能な PDF を作成します。画像を EPUB に変換し、検索可能なテキストを追加して、C#
  で検索可能な PDF を生成する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: ja
og_description: Aspose OCR を使用して任意の画像から検索可能な PDF を作成します。このガイドでは、画像を EPUB に変換し、検索可能なテキストを追加し、C#
  で検索可能な PDF を生成する方法を示します。
og_title: 検索可能なPDFを作成 – 画像をEPUBに変換してテキストを追加
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: 検索可能なPDFを作成 – 画像をEPUBに変換してテキストを追加
url: /ja/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Searchable PDF を作成 – 画像を EPUB に変換しテキストを追加

スキャンした領収書や任意の画像から **検索可能な PDF** を作成したいですか？このチュートリアルでは、Aspose OCR を使用して検索可能な PDF を作成し、さらに **画像を EPUB に変換** して **検索可能なテキスト層** を追加する方法を、単一の C# プロジェクトで実演します。

見た目は綺麗なのに検索できない PDF に悩んだことがあるなら、あなたは一人ではありません。隠しテキスト層を追加すれば、フラットな画像が完全に検索可能なドキュメントに変わります。Aspose がその作業をほぼ手間なく実現してくれます。

## 学べること

* Aspose OCR エンジンの初期化と言語設定の方法。  
* **画像を EPUB に変換** して電子書籍として配布する正確な手順。  
* PDF ライターを設定し、出力に隠し検索可能テキスト層を含める方法。  
* 複数ページの領収書や非英語言語など、エッジケースの取り扱いに関するヒント。  

事前に必要なのは .NET 開発環境（Visual Studio 2022 以降）と Aspose OCR NuGet パッケージだけです。外部サービスや特殊な設定ファイルは不要で、コピー＆ペーストしてすぐに実行できるシンプルな C# コードです。

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| .NET 6.0+ | Aspose OCR は .NET Standard 2.0+ を対象としているため、.NET 6 で最新のランタイム改善を利用できます。 |
| Aspose.OCR NuGet パッケージ | コードで使用する `OcrEngine`、`EpubWriter`、`PdfWriter` クラスを提供します。 |
| 画像ファイル（例: `receipt.jpg`） | OCR を実行する元画像です。PNG、JPEG、BMP などのラスタ画像なら何でも構いません。 |
| 基本的な C# 知識 | スニペットを読んで調整する程度で、言語をゼロから学ぶ必要はありません。 |

パッケージは次のコマンドでインストールできます。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio の NuGet パッケージ マネージャ UI でも同様にインストールできます。検索ボックスに “Aspose.OCR” と入力してください。

## 手順 1 – Aspose OCR で検索可能 PDF を作成

まず最初に、認識すべき言語を指定した `OcrEngine` インスタンスを作成します。デフォルトは英語ですが、`ocrEngine.Language` に設定すればフランス語やドイツ語などに切り替えられます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

エンジンを最初に初期化する理由は何ですか？エンジンは認識モデルをメモリに保持するため、1 回作成して複数画像で再利用すれば CPU と RAM の両方を節約できます。大量バッチ処理の場合は、実行全体で同じインスタンスを使い続けるのがベストです。

## 手順 2 – 画像を読み込み OCR を実行

次に、処理したいファイルをエンジンに渡します。`ImageStream.FromFile` は画像を OCR エンジンが理解できる形式に読み込みます。

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **画像が複数ページの場合は？**  
> Aspose OCR はマルチページ TIFF をそのまま扱えます。TIFF ファイルへのパスを渡すだけで、エンジンが自動的に各ページを順に処理します。

## 手順 3 – 画像を EPUB に変換

スキャンした文書の電子書籍版も必要な場合、Aspose ならワンライナーで実現できます。`EpubWriter` は同じ `OcrEngine` インスタンスを利用するため、OCR 結果を再処理せずにそのまま使用できます。

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

なぜ EPUB にエクスポートするのか？EPUB はリフロー可能なフォーマットで、モバイルリーダーに最適です。OCR で取得したテキストは選択可能になり、元画像は背景として残るため、スキャン元の外観が保たれます。

## 手順 4 – PDF に検索可能テキスト層を追加

ここが **検索可能 PDF を実際に作成** するステップです。`AddSearchableTextLayer` を有効にすると、PDF ライターは OCR 出力に合わせた見えないテキスト層を埋め込みます。ユーザーは検索、コピー、ハイライトがネイティブ PDF と同様に行えます。

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **よくある落とし穴:** `AddSearchableTextLayer` を設定し忘れると、見た目は同じでも検索できない PDF が生成されます。検索可能な文書が必要なときは必ずこのフラグを確認してください。

## 手順 5 – 完全動作サンプル

すべてを統合した、すぐに新しい .NET プロジェクトに貼り付けて実行できるコンソール アプリの例です。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### 期待される出力

* `receipt.epub` – Calibre、Apple Books、その他の e‑リーダーで開ける EPUB ファイル。  
* `receipt_searchable.pdf` – **Ctrl + F** で元画像に含まれる任意の単語を検索できる PDF。

Adobe Acrobat で PDF を開き、**ファイル → プロパティ → 説明** を確認すると、**フォント** タブに隠しテキスト ストリームが表示され、検索可能層が存在することが分かります。

## よくある質問とエッジケース

**Q: 非英語言語でも動作しますか？**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}