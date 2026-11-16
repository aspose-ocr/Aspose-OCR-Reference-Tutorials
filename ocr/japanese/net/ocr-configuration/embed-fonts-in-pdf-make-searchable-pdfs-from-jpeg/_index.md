---
category: general
date: 2026-03-05
description: Aspose OCR を使用して JPEG を検索可能な PDF に変換する際に、PDF にフォントを埋め込みます。JPEG からテキストを認識し、PDF/A‑2b
  準拠のためにフォントを埋め込む方法を学びましょう。
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: ja
og_description: JPEGを検索可能なPDFに変換しながら、PDFにフォントを埋め込む。このステップバイステップガイドでは、JPEGからテキストを認識し、PDF/A‑2b準拠のファイルを作成する方法を示します。
og_title: PDFにフォントを埋め込む – JPEGから検索可能なPDFを作成
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: PDFにフォントを埋め込む – JPEGから検索可能なPDFを作成
url: /ja/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFにフォントを埋め込む – JPEGから検索可能なPDFを作成

スキャン画像から生成された **PDF にフォントを埋め込む** 必要があったことはありませんか？ あなただけではありません。多くの開発者が、生成された PDF は自分のマシンでは問題なく表示されても、他の環境で開くとフォントが埋め込まれていないために文字が欠けているという問題に直面します。  

良いニュースです。Aspose OCR を使用すれば、**JPEG からテキストを認識** し、必要なフォントを埋め込み、数行の C# コードで完全に検索可能な PDF/A‑2b ドキュメントを出力できます。このチュートリアルでは、各設定がなぜ重要か、一般的な落とし穴を回避する方法、最終的な PDF の見た目についてステップバイステップで解説します。

本ガイドを終える頃には、**画像を検索可能な PDF に変換** し、フォントを正しく埋め込み、プログラムから **画像ファイルに対して OCR を実行** する方法が理解できるようになります。

---

## 必要なもの

- **Aspose.OCR for .NET** (最新バージョン、例: 23.10) – 重い処理を担うライブラリです。
- 有効な **Aspose OCR ライセンス ファイル** (`Aspose.OCR.lic`). 無料トライアルでも動作しますが、ライセンス版にすると評価用の透かしが除去されます。
- 印刷されたテキストまたは手書きテキストを含む JPEG 画像 (`input.jpg`)。
- .NET 開発環境 (Visual Studio、Rider、または C# 拡張機能付き VS Code)。

追加の NuGet パッケージは不要です。OCR エンジンには PDF 生成ユーティリティが同梱されています。

---

## ステップ 1: OCR エンジンの設定とライセンスの適用 *(PDF にフォントを埋め込む)*

認識を実行する前に、`OcrEngine` インスタンスを作成し、使用するライセンスを指定する必要があります。ライセンスの設定を省略すると、エンジンは評価モードで動作し、各ページに「Powered by Aspose」のオーバーレイが追加されます。

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**この設定が重要な理由:** ライセンスは透かしを除去するだけでなく、後でフォント埋め込みに必要となる PDF/A 準拠オプションも有効にします。

---

## ステップ 2: 処理したい JPEG 画像をロード *(JPEG からテキストを認識)*

OCR エンジンは `Image` プロパティで `ImageStream` を受け取ります。変換したい JPEG を指定してください。

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**ヒント:** 画像がストリーム上にある場合 (例: API 経由でアップロードされた場合) は、`FromFile` の代わりに `ImageStream.FromStream(yourStream)` を使用できます。

---

## ステップ 3: 検索可能な PDF のための PDF 保存オプションを設定

これが “PDF にフォントを埋め込む” 要件の核心です。`PdfSaveOptions` を使用して以下を行います:

1. **PDF/A‑2b** を対象とする（広く受け入れられているアーカイブ標準）。
2. 使用したすべてのフォントを **埋め込む** ことで、PDF がどこでも同じように表示されるようにする。
3. **ロスレス Flate 圧縮** を適用して、ファイルサイズを適切に保つ。
4. 元の JPEG を背景レイヤーとして保持し、視覚的忠実度を保つ。

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**これらの設定の理由**  
- **PdfAStandard.PdfA2b** は長期保存を保証し、フォントの埋め込みを強制します。  
- **EmbedFonts = true** は、主要なキーワード目標であるフォント埋め込みを満たす明示的なフラグです。  
- **Compression.Flate** は品質を損なうことなくサイズを削減します。  
- **RenderOriginalImage** は、スキャンページの視覚的外観を保持しつつ、隠れた OCR レイヤーが検索可能なテキストを提供します。

---

## ステップ 4: 画像で OCR 認識を実行 *(画像に対して OCR を実行)*

すべての準備が整ったら、認識を開始します。エンジンは JPEG を解析し、文字を抽出し、内部でテキストレイヤーを作成します。

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**よくある質問:** *言語や辞書を指定する必要がありますか？*  
ドキュメントが英語でない場合は、`Recognize()` を呼び出す前に `ocrEngine.Language = OcrLanguage.French;`（またはサポートされている任意の言語）を設定してください。デフォルトは英語です。

---

## ステップ 5: フォントが埋め込まれた検索可能な PDF として出力を保存

最後に、結果をディスクに書き込みます。`Save` メソッドは、保存先パスと先ほど定義した `PdfSaveOptions` を受け取ります。

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

`output.pdf` を Adobe Acrobat や任意の PDF ビューアで開くと、以下が可能になります:

- 元の JPEG に含まれていた任意の単語を **検索** できる。
- **フォントが欠けている警告が表示されない**（`EmbedFonts = true` のおかげです）。
- ファイルが **PDF/A‑2b** に準拠していることを確認できる（File → Properties → PDF/A）。

---

## 完全な動作例

以下は、完全な実行可能プログラムです。新しいコンソールアプリプロジェクトにコピー＆ペーストし、ファイルパスを調整して **F5** を押してください。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**期待される出力:**  
コンソールに成功メッセージが表示され、`output.pdf` が対象フォルダーに作成されます。PDF を開き、ビューアの検索ボックスを使用すると、`input.jpg` に含まれていた任意の単語が見つかるはずです。

---

## よくある質問とエッジケース

### 1. “JPEG がマルチページ TIFF の場合は？”

Aspose OCR は各ページを個別に扱います。TIFF を JPEG のシリーズに変換する（または各ページで `ImageStream.FromFile` を使用）ことで、OCR 処理をループし、同じ `OcrEngine` インスタンスを再利用して各結果を同一 PDF に追加します。

### 2. “DPI や画像前処理を制御できますか？”

はい。`Recognize()` を呼び出す前に、画像解像度を調整できます:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

特に小さなフォントの場合、DPI を上げることで認識精度が向上することが多いです。

### 3. “Adobe Reader でまだフォントが欠けていると表示される—何が問題？”

**PDF/A‑2b** を対象にし、`EmbedFonts` が `true` に設定されていることを確認してください。`PdfAStandard` を手動で `None` に変更した場合、PDF/A 検証ステップがスキップされ、一部のフォントが埋め込まれない可能性があります。

### 4. “モバイルデバイスでも OCR レイヤーは検索可能ですか？”

もちろんです。隠れたテキストレイヤーは PDF 仕様の一部なので、テキスト抽出に対応した PDF ビューア（iOS Files、Android PDF Viewer など）であれば検索が可能です。

### 5. “アラビア語など右から左への言語はどう扱う？”

認識前に言語を設定してください:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Aspose OCR は、`EmbedFonts` が true の場合、テキスト方向を自動的に切り替え、適切なフォントを埋め込みます。

---

## プロのコツと一般的な落とし穴

- **プロのコツ:** ソース画像がカラー写真の場合、まずグレースケールに変換することを検討してください（`ocrEngine.Image.ConvertToGrayscale();`）。これにより、OCR の精度を損なうことなくファイルサイズが削減されます。
- **注意点:** 大きな画像で無料トライアルライセンスを使用すると、エンジンが OCR テキストを切り詰めることがあります。本番環境ではフルライセンスにアップグレードしてください。
- **パフォーマンスのコツ:** 複数の画像で同じ `OcrEngine` インスタンスを再利用すると、OCR DLL のロードオーバーヘッドを回避できます。
- **セキュリティ上の注意:** PDF/A‑2b ファイルは設計上 **読み取り専用** であり、誤ってスクリプトが埋め込まれることを防止します。コンプライアンスが重視される環境にとっては大きな利点です。

---

## 結論

このチュートリアルでは、**PDF にフォントを埋め込む** と同時に **JPEG からテキストを認識** し、PDF/A‑2b 標準に準拠した **検索可能な PDF** を生成する全工程を解説しました。プロセスは以下の通りです:

1. `OcrEngine` を初期化し、ライセンスを適用する。  
2. JPEG 画像をロードする。  
3. `PdfSaveOptions` を設定する（フォント埋め込み、PDF/A‑2b、圧縮）。  
4. `Recognize()` を実行する。  
5. 設定したオプションで保存する。

これで、画像をリアルタイムで **検索可能な PDF に変換** する必要がある Web サービス、デスクトップユーティリティ、バッチジョブにこのフローを組み込むことができます。次は、マルチページ PDF や生成された PDF から **検索可能な PDF を作成** する方法を探求してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}