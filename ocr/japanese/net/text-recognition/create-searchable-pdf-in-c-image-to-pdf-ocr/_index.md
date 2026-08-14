---
category: general
date: 2026-02-28
description: C#でマルチページTIFFから検索可能なPDFを作成する。このガイドでは、画像から検索可能なPDFへの変換方法と、完全なC# OCR例を示します。
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: ja
og_description: Aspose.OCR を使用して TIFF から検索可能な PDF を作成します。このステップバイステップの C# OCR 例に従って、画像を検索可能な
  PDF に変換しましょう。
og_title: C#で検索可能なPDFを作成 – 画像からPDFへのOCR
tags:
- OCR
- PDF
- C#
- Aspose
title: C#で検索可能なPDFを作成 – 画像からPDFへのOCR
url: /ja/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で検索可能なPDFを作成 – 画像からPDFへのOCR

スキャンした文書から **検索可能なPDFを作成** する必要があったが、どこから始めればよいかわからなかったことはありませんか？ あなただけではありません。多くのオフィスワークフローでは、検索可能なPDFが、行き止まりのファイルと検索可能なアーカイブの違いを生みます。

このチュートリアルでは、マルチページTIFFを検索可能なPDFに変換する完全な **c# ocr example** を Aspose.OCR を使って解説します。最後まで読むと、**画像から検索可能なPDFへ** の方法、**TIFFをPDFへ変換** の方法が正確に分かり、任意の .NET プロジェクトに貼り付けてすぐに実行できるコードスニペットを手に入れられます。

## 学べること

* C# プロジェクトで Aspose.OCR をインストールし、参照する方法。  
* `RecognizeToPdf` を呼び出すために TIFF をロードし、言語を設定する正確な手順。  
* 各ステップが重要な理由 – メモリ管理から言語選択まで。  
* 大容量ドキュメントの処理、一般的な OCR の落とし穴のトラブルシューティング、他の画像フォーマットへの拡張に関するヒント。  

**Prerequisites** – 最近の .NET SDK（4.6 以上または .NET Core 3.1 以上）、Visual Studio（またはお好みの IDE）、そして Aspose.OCR ライセンス（無料トライアルでテスト可能）。他の外部ライブラリは不要です。

---

## 検索可能なPDFの作成 – 概要

全体的な流れは以下の通りです：

1. **Initialize** `OcrEngine`。  
2. **Load** ソース画像（この例では TIFF）をロードします。  
3. **Configure** 正確性向上のために言語設定を構成します。  
4. **Run** OCR を実行し、**save** 結果を直接検索可能な PDF として保存します。  

以上です。Aspose API が重い処理をすべて行うので、別々の OCR ライブラリと PDF ライブラリを組み合わせる必要はありません。

---

## 手順 1: Aspose.OCR のインストールとプロジェクト設定

まず、Aspose.OCR の NuGet パッケージを追加します：

```bash
dotnet add package Aspose.OCR
```

または、Visual Studio のパッケージ マネージャ コンソールを使用したい場合は：

```powershell
Install-Package Aspose.OCR
```

パッケージが復元されたら、プロジェクト ファイルを開き、参照が正しいことを確認します：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** バグ修正や最新の言語パックを取得するため、最新の安定版（Aspose のウェブサイトで確認）を使用してください。

---

## 手順 2: TIFF を PDF に変換 – 画像の読み込み

ここでは、検索可能にしたい TIFF を読み込みます。Aspose の `Image.Load` メソッドはマルチページ TIFF をそのままサポートしています。

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Why this matters:** `using` ブロック内で画像をロードすることで、アンマネージド リソースが速やかに解放されます。大容量ドキュメントを処理する際に重要です。

---

## 手順 3: 画像から検索可能なPDFへ – OCR エンジンの設定

OCR を実行する前に、エンジンに期待する言語を指定します。英語は多くの場合で機能しますが、任意の `OcrLanguage` 列挙値に置き換えることができます。

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Expert note:** 正しい言語を選択することで、誤認識が大幅に減少します。複数言語が混在する場合は、`|` 演算子で組み合わせられます。例: `OcrLanguage.English | OcrLanguage.French`。

---

## 手順 4: C# OCR 例 – 認識して保存

エンジンの準備ができたら `RecognizeToPdf` を呼び出します。このメソッドは検索可能な PDF を直接ディスクに書き込み、元の画像の背後に不可視のテキスト層を埋め込みます。

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

この行が実行されると、`output.pdf` には元の TIFF ページに加えて、任意の PDF リーダーで検索可能な隠しテキスト オーバーレイが含まれます。

---

## 手順 5: C# 画像から PDF へ – 結果の検証

すべてが正しく動作したか確認しましょう。生成された PDF を Adobe Reader（または任意のビューア）で開き、元の TIFF に含まれることが分かっている単語で検索してみてください。

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

検索でヒットが得られれば、画像から **検索可能なPDFを作成** に成功したことになります。ヒットしない場合は、言語設定や元の TIFF の品質を再確認してください。

---

## 完全な動作例

すべての要素を組み合わせた、コンパイルして実行できる自己完結型コンソール アプリがこちらです：

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output**（コンソール出力）:

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

`output.pdf` を開くと、元の TIFF の任意の単語をビューアの検索ボックスに入力でき、該当箇所がハイライト表示されます。

---

![検索可能なPDFの例](placeholder-image.png){: .align-center alt="検索可能なPDFの例"}

*上のスクリーンショットは、隠しテキスト層が有効になった状態でビューアで開かれた検索可能な PDF を示しています。*

---

## よくある質問とエッジケース

### TIFF が非常に大きい（数百ページ）場合はどうすべきですか？

Aspose.OCR はページを1つずつストリーミングしますが、メモリ制限に達する可能性があります。TIFF をバッチ処理することを検討してください：

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

その後、ページごとの PDF を PDF ライブラリ（例: Aspose.PDF）で結合します。

### 検索可能な DOCX など、別の形式で出力できますか？

はい。`RecognizeToPdf` の代わりに `RecognizeToDocument` を使用します。API は PDF メソッドと同様で、対象ファイルの拡張子を変更するだけです。

### 英語以外の言語を扱うには？

`OcrLanguage.English` を適切な列挙値に置き換えます。例: `OcrLanguage.Spanish`。複数言語を組み合わせることも可能です：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### パスワード保護された PDF はどうですか？

OCR ステップの後、生成された PDF を Aspose.PDF で開き、暗号化を適用できます：

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## まとめ

C# を使用して TIFF 画像から **検索可能なPDF** を作成するために必要なすべてをカバーしました。Aspose.OCR のインストール、画像の読み込み、言語設定、OCR の実行、そして検索可能な出力の検証まで、他の形式にも適用できる堅実な **c# ocr example** を手に入れました。  

さらに進めたい場合は、以下を試してください：

* **Convert TIFF to PDF** を使用して検索不可のアーカイブを作成（OCR ステップを省略）。  
* **image to searchable pdf** を実験的に試す

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}