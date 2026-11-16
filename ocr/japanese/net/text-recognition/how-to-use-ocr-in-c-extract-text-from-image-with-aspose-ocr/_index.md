---
category: general
date: 2026-02-24
description: C#でOCRを使用して画像ファイルからテキストを抽出する方法。PNGをテキストに変換し、画像を非同期に読み取り、一般的な落とし穴への対処法を学びます。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: ja
og_description: C#でOCRを使用して画像からテキストを抽出する方法。このガイドでは、Asposeを使ったステップバイステップの非同期OCRを紹介し、変換、エラーハンドリング、ベストプラクティスをカバーします。
og_title: C#でOCRを使用する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – Aspose OCRで画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – 画像からテキストを抽出する

画像から手動で入力せずにテキストを抽出する **OCRの使い方** を考えたことがありますか？ あなたは一人ではありません。PNG などの *画像からテキストを抽出* する必要があるとき、多くの開発者が壁にぶつかります。通常のコピー＆ペーストではうまくいきません。  

このチュートリアルでは、Aspose.OCR ライブラリを使用して **PNG をテキストに変換** する完全な非同期ソリューションを順を追って解説します。最後まで読むと、画像ファイルの読み取り方法、エラー処理、結果を自分のアプリに統合する方法が正確に分かります。  

NuGet パッケージの設定から OCR エンジンの精度向上のための調整まで、すべてをカバーします。また、画像が鮮明でない場合の対処法も紹介します。ドキュメントへのリンクを追いかける必要はありません—必要な情報はすべてここにあります。

## 必要なもの

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作します）  
- Visual Studio 2022（またはお好みの IDE）  
- **Aspose.OCR** NuGet パッケージ（`Install-Package Aspose.OCR`）  
- 処理したい画像ファイル（PNG、JPG、BMP）— ここでは `input.png` と呼びます  

以上です。これらの項目が揃っていれば、すぐに始められます。

![OCR ワークフローの図 – 画像からテキストを抽出する方法](/images/ocr-workflow.png)

## 手順 1: Aspose.OCR をインストールし、名前空間を追加する

まず、ライブラリをプロジェクトに追加します。Package Manager Console を開き、以下を実行してください。

```powershell
Install-Package Aspose.OCR
```

次に、C# ファイルの先頭に必要な名前空間を追加します。

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **プロのコツ:** .NET 6 のミニマル API を使用している場合、これらの `using` 文をグローバル ファイルに配置すれば、複数のクラスで繰り返す必要がなくなります。

### なぜ重要か

`Aspose.OCR` 名前空間を使用すると、実際に画像を読み取るコアクラス `OcrEngine` にアクセスできます。これがなければ、ピクセル解析コードを自前で実装しなければならず、非常に手間がかかります。名前空間を追加することでコードがすっきりし、コンパイラに使用する型の場所を示すことができます。

## 手順 2: 非同期 OCR エンジンを作成する

OCR の呼び出しを `async` メソッドでラップすれば、UI が応答し続け、サーバー側のコードもスケールしやすくなります。以下はコンソール アプリの雛形です。

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 説明

- **`OcrEngine ocrEngine = new OcrEngine();`** – デフォルト設定でエンジンをインスタンス化します。後で言語や検出モード、前処理フィルタを調整できます。  
- **`await ocrEngine.RecognizeImageAsync(...)`** – 非同期メソッドは `Task<OcrResult>` を返します。await することで OCR がバックグラウンドで実行されている間、スレッドが解放されます。  
- **`ocrResult.Text`** – エンジンが読み取ったすべてのテキストのプレーンテキスト表現です。これは画像からテキストを抽出する *テキストを抽出する方法* の核心です。

## 手順 3: 精度向上のためにエンジンを微調整する

標準の OCR はクリーンで高コントラストな画像ではうまく機能しますが、実際の写真はしばしば少し手を加える必要があります。`RecognizeImageAsync` を呼び出す前に、いくつかのプロパティを調整できます。

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### これらの設定を使用すべき場面

- **Low‑quality scans** – ノイズ除去のために `ImagePreprocessingOptions.Auto` を有効にします。  
- **Multilingual PDFs** – `Language` を `OcrLanguage.French` に変更するか、ビットマスクで複数言語を組み合わせます。  
- **Form fields** – 誤検出を減らすために `Characters` を数字や大文字に限定します。

## 手順 4: エラーを適切に処理する

OCR は魔法ではなく、ファイルが存在しない、破損している、またはサポート外の形式の場合に失敗することがあります。非同期呼び出しを try/catch ブロックでラップしてください。

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### これが役立つ理由

明確なエラーメッセージを提供することでデバッグが迅速になり、エンドユーザーの体験も向上します。汎用的なクラッシュではなく、パス、ファイル形式、または OCR エンジンの設定を確認すべきかを示す有用なプロンプトが表示されます。

## 手順 5: すべてを統合 – 完全な動作例

以下は **OCR の使い方** を示す、前処理を適用しエラー処理も行う、完全な実行可能コンソール プログラムです。新しい `.csproj` にコピー＆ペーストして F5 を押してください。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**期待される出力**（`input.png` に “Hello World” というフレーズが含まれていると仮定）:

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

画像がぼやけている場合、余分な文字や欠落した単語が出力されることがあります。そこが手順 3 の前処理オプションが重要になるポイントです。

## 手順 6: ソリューションの拡張 – PNG から PDF やテキストファイルへ

場合によっては **PNG をテキストに変換** し、結果を `.txt` に保存したり PDF レポートに埋め込んだりする必要があります。以下は OCR 出力を書き込む簡単なコードです。

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

あるいは、Aspose.PDF を使用して PDF を生成する場合は次のようにします。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

これらの拡張は **画像の読み取り方法** がレポート生成、検索インデックス作成、あるいは言語モデルへの入力といった下流プロセスにどのように活用できるかを示しています。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| *サポートされている画像形式は何ですか？* | Aspose.OCR は PNG、JPEG、BMP、TIFF、GIF をサポートします。PDF がある場合は、まずページを画像として抽出してください。 |
| *複数の画像を並列に処理できますか？* | はい。各 `RecognizeImageAsync` 呼び出しを個別のタスクでラップし、`Task.WhenAll` を使用します。ただしメモリ使用量に注意してください。 |
| *OCR が空のテキストを返した場合は？* | 画像の品質を確認してください。コントラストが低い、またはテキストが回転していると失敗しやすいです。`ImagePreprocessingOptions.Deskew` を有効にするか、OCR 前に画像を手動で回転させてください。 |
| *画像サイズに制限はありますか？* | 大きな画像（10 MP 超）は `OutOfMemoryException` を引き起こす可能性があります。認識前に適切な解像度（例: 300 DPI）に縮小してください。 |
| *Aspose.OCR のライセンスは必要ですか？* | 開発モードは一時ライセンスで動作しますが、本番環境では評価用の透かしを除去するために購入したライセンスが必要です。 |

## パフォーマンスのヒント

- **`OcrEngine` インスタンスを再利用** してバッチ処理を行いましょう。画像ごとに新しいエンジンを作成するとオーバーヘッドが増えます。  
- **未使用の言語をオフに** して検出を高速化します。余分な言語はそれぞれ小さな処理コストを加えます。  
- **バックグラウンド スレッドで OCR を実行**（上記参照）すると、デスクトップや Web アプリの UI スレッドが軽快に保たれます。

## 結論

C# で **OCR の使い方** を最初から最後までカバーしました：Aspose.OCR のインストール、非同期メソッドの作成、ノイズの多い画像向け設定の調整、エラー処理、結果の永続化です。これで *画像からテキストを抽出* し、*PNG をテキストに変換* し、さらに PDF 生成などの他のワークフローにテキストを流し込む信頼できる方法が手に入りました。

次のチャレンジに挑みますか？OCR 出力を検索可能な Azure Cognitive Search インデックスに流し込んだり、エンジンに `OcrLanguage.Spanish | OcrLanguage.French` を追加して多言語 OCR を試したりしてみてください。プログラムで **画像データの読み取り方法** を知っていれば、可能性は無限です。

---

*このガイドが役に立ったと思ったら、GitHub でスターを付けたり、チームメンバーと共有したり、以下にあなたの OCR テクニックをコメントで教えてください。Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}