---
category: general
date: 2026-03-18
description: C# で Aspose OCR を使用して検索可能な PDF を作成します。画像を PDF に変換し、OCR テキスト層を追加し、数ステップで
  PDF バイトをファイルに書き込みます。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: ja
og_description: Aspose OCR を使用して C# で検索可能な PDF をすばやく作成します。画像を PDF に変換し、OCR テキストレイヤーを追加し、PDF
  バイト列をファイルに書き込む方法を学びましょう。
og_title: 画像から検索可能なPDFを作成 – 高速C# OCRガイド
tags:
- OCR
- PDF
- C#
- Aspose
title: OCRで画像から検索可能なPDFを作成 – C#ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からOCRで検索可能なPDFを作成 – C# ガイド

スキャンした画像から **検索可能なPDF** を作成したことがありますか？Aspose OCR を使えば、数行のコードで実現でき、重いライブラリは不要です。このチュートリアルでは **画像をPDFに変換**し、上に **OCRテキストレイヤー** を付与し、最後に **PDFバイト列をファイルに書き込む**ことで、ユーザーが実際に検索できる標準準拠の PDF/A‑2b ドキュメントを作成します。

検索可能なPDFを作る意味が分からない、単なる画像ファイルで十分では？と思うかもしれませんが、ユーザー体験を考えてみてください。検索可能なPDFはテキストのコピー、選択、インデックス作成が可能で、アーカイブや法務文書、後でテキスト抽出が必要なワークフローに最適です。さっそく始めましょう。

## 必要なもの

- .NET 6 以降（コードは .NET Framework 4.7 以上でも動作します）
- Aspose.OCR NuGet パッケージ（`Aspose.OCR` バージョン 23.10 以降）
- 検索可能なPDFに変換したいラスタ画像（`.png`、`.jpg` など）
- C# の基本的な知識（特別なスキルは不要）

以上です。外部ツールや追加コンバータは不要です。すべての重い処理は Aspose OCR エンジンが担当します。

## 検索可能なPDF作成 – 概要

コードに入る前に、プロセスを概観しましょう。

1. **Instantiate** OCR エンジン – このオブジェクトは画像からテキストを読み取る方法を知っています。  
2. **Load** ソース画像 – エンジンに `ImageStream` を渡します。  
3. **Configure** PDF/A‑2b 保存オプション – これにより Aspose が認識したテキストを隠しレイヤーとして埋め込みます。  
4. **Run** OCR と **capture** された PDF バイト列。  
5. **Write** それらのバイトをディスクに書き込み、最終的な検索可能な PDF ファイルを生成します。

これらのステップはそれぞれ C# の数行に対応しており、全体のワークフローは大規模なプロジェクトというよりも小さなスクリプトのように感じられます。

## ステップ 1: 画像をPDFに変換 – 画像の読み込み

まず最初に、OCR エンジンに読み取る対象を渡す必要があります。`ImageStream.FromFile` ヘルパーはファイルを Aspose が処理できるストリームに読み込みます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **プロのコツ:** 画像解像度は 300 dpi 以上に保ちましょう。低解像度のスキャンでは OCR の精度が大幅に低下します。

## ステップ 2: 画像からテキストを認識し OCR テキストレイヤーを追加

ここで OCR エンジンを作成し、テキスト認識を指示します。`IncludeTextLayer = true` が設定された `PdfSaveOptions` と認識結果を組み合わせると魔法が起きます。このフラグにより Aspose は抽出した文字を不可視のテキストレイヤーとして埋め込み、PDF を検索可能にします。

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

PDF/A‑2b を選ぶ理由は？ これは ISO 標準のアーカイブ形式で、長期保存を保証し、特に検索可能なテキストレイヤーを必ず含むように PDF に強制します。アーカイブ準拠が不要であれば `PdfCompliance` を省略できますが、残しておいてもコストはかかりません。

## ステップ 3: PDF バイト列を書き込む – 結果の保存

エンジンとオプションの準備ができたら、認識を実行し、すぐに Aspose に PDF を `byte[]` として取得させます。そのバイト列を `File.WriteAllBytes` でディスクに書き出します。シンプルながら強力です。

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

この `Console.WriteLine` 行は任意ですが、ターミナルからプログラムを実行した際に即座にフィードバックを得られます。

## 完全動作サンプル

すべてをまとめると、こちらが完全な実行可能プログラムです。新しいコンソールプロジェクトにコピー＆ペーストし、`YOUR_DIRECTORY` を実際のパスに置き換えて **F5** を押してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### 期待される出力

- 指定したフォルダーに `output.pdf` という名前のファイルが作成されます。  
- Adobe Acrobat Reader などの PDF ビューアで開き、テキスト選択を試みてください。文字をコピーできれば、**検索可能なPDFの作成に成功**です。  
- 適切なコンプライアンスフラグを使用したため、PDF/A‑2b 検証ツールも合格します。

## よくある質問とエッジケース

**画像が複数ページの場合はどうすれば？**  
各ページを個別の `ImageStream` にラップし、`OcrEngine` に順次渡します。Aspose が自動的にページを結合して単一の PDF にします。

**OCR の言語を変更できますか？**  
もちろんです。`Recognize` を呼び出す前に `ocrEngine.Language = Language.English;`（またはサポートされている任意の言語）を設定してください。

**巨大ファイルのメモリ使用量は？**  
ギガバイト規模のスキャンを処理する場合、`byte[]` 全体をメモリに保持する代わりに、結果を直接 `FileStream` にストリーミングすることを検討してください。

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**ライセンスは必要ですか？**  
Aspose は透かしなしの無料トライアルを提供しています。製品環境で使用する場合は、評価バナーを除去し、すべての機能を利用できるようにライセンスを購入してください。

## OCR 精度向上のヒント

- **Pre‑process** 画像: 歪み補正、ノイズ除去、コントラスト向上。  
- **Use lossless formats** PNG など; JPEG の圧縮アーティファクトはエンジンを混乱させる可能性があります。  
- **Avoid colored backgrounds**; 無地の白背景が最良の結果をもたらします。

## 次のステップ

検索可能な PDF を **作成できる**ようになったので、次のことを検討できます:

- `Directory.GetFiles` を使ってフォルダー内の画像を **バッチ処理**。  
- 後で `PdfDocument` API を使って **隠しテキストを抽出**し、インデックス作成に利用。  
- OCR とデジタル署名を組み合わせ、改ざん検知可能なアーカイブを作成。

これらはすべて、ここで説明した「ロード → 認識 → 設定 → 保存」の基本パターンに基づいています。

---

*スキャンしたアーカイブを検索可能な PDF に変換する準備はできましたか？コードを取得し、画像を指定して Aspose に重い処理を任せましょう。コーディングを楽しんでください！*

![検索可能なPDFの例](/images/create-searchable-pdf.png "画像から生成された検索可能なPDFのイラスト")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}