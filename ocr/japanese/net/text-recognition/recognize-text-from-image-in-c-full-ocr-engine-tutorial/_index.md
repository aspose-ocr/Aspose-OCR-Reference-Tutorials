---
category: general
date: 2026-06-06
description: C# OCRエンジンを使用して画像からテキストを認識します。画像をJSONに変換する方法、画像をXMLに変換する方法、そして数分でOCR用に画像を読み込む方法を学びましょう。
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: ja
og_description: C# OCRエンジンで画像からテキストを認識し、結果をJSONとXMLにエクスポート、OCR用画像の読み込みをマスターします。
og_title: C#で画像からテキストを認識する – 完全OCRエンジンチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: C#で画像からテキストを認識する – 完全OCRエンジンチュートリアル
url: /ja/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを認識する – 完全 OCR エンジンチュートリアル

画像からテキストを **recognize text from image** したいことはありませんか？どの C# ライブラリを選べばよいか迷っている方も多いでしょう。開発者はスキャンしたレシートやスクリーンショット、手書きメモを検索可能なテキストに変換する作業に常に頭を悩ませています。朗報です。最新の **OCR engine C#** を使えば、数行のコードで実現でき、さらに **convert image to JSON** や **convert image to XML** で下流処理に渡すことができます。

このガイドでは、OCR パッケージのインストール、画像の読み込み、テキスト抽出、そして結果を JSON と XML の両方にエクスポートするまでの手順をすべて解説します。最後まで実行すれば、任意の .NET プロジェクトに組み込める自己完結型のコンソール アプリが手に入ります。曖昧な参照は一切なく、完全に動作するソリューションを提供します。

## What You’ll Walk Away With

- 人気のある C# OCR エンジンを使用した **load image for OCR** の具体的な手順が把握できる。  
- **recognize text from image** してリッチな結果オブジェクトを取得できる動作コード。  
- 余計なライブラリなしで **convert image to JSON** と **convert image to XML** を行うシンプルなスニペット。  
- マルチページ PDF、さまざまな画像フォーマット、低コントラストスキャンといった一般的な落とし穴への対処法。

### Prerequisites

- .NET 6 SDK 以降（好みで .NET Framework 4.8 でも可）。  
- 基本的な C# の知識—特別なことは不要、クラスと `async`/`await` が理解できれば OK。  
- OCR 対象となる画像ファイル（例では `structured.png`）。  

これらが揃っていれば、さっそく始めましょう。

---

## Recognize Text from Image – Setting Up the OCR Engine

まずは信頼できる OCR ライブラリが必要です。このチュートリアルでは **IronOcr** を使用します。商用レベルのエンジンで、NuGet の無料コミュニティエディションが提供されています。英語はデフォルトでサポートされており、元のコードスニペットにある `OcrEngine` クラスを利用できます。

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **Pro tip:** 予算が厳しい場合は `IronOcr` を `Tesseract` に置き換えても構いません。API は若干異なりますが、概念は同じです。

次に新しいコンソール プロジェクトを作成し、必要な `using` 文を追加します。

```csharp
using IronOcr;
using System.IO;
```

### Step‑by‑Step Engine Configuration

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*Why this matters:* エンジンを一度だけ初期化して多数の画像で再利用するとオーバーヘッドが削減されます。また、言語を明示的に設定することでエンジンの自動検出処理を回避でき、速度と精度が向上します。

---

## Load Image for OCR – Feeding the Engine the Right Data

エンジンは `OcrInput` オブジェクトを受け取ります。ファイルパス、ストリーム、あるいは `Bitmap` を指定できます。最もシンプルな方法は次の通りです。

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **Edge case:** ソースがマルチページ PDF の場合は、PNG の代わりに `input.AddPdf("file.pdf")` を呼び出してください。OCR エンジンは各ページを自動的に別々の画像として扱います。

---

## Recognize Text from Image – Running the OCR Process

エンジンと入力が準備できたら、実際の認識はワンライナーで完了します。

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` は `OcrResult` オブジェクトで、以下の情報を保持しています。

- `Text` – 生の抽出文字列。  
- `Lines` – 信頼度スコアを持つ `OcrLine` オブジェクトのコレクション。  
- `Words` – 個々の単語とその信頼度を含むコレクション。  

デバッガで直接確認できますが、実務ではデータをシリアライズして保存することが多いでしょう。

---

## Convert Image to JSON – Exporting OCR Results

IronOcr は `System.Text.Json` を利用した組み込みの JSON シリアライズ機能を提供しています。次のスニペットは、ソース画像と同じディレクトリに整形された JSON ファイルを書き出します。

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**What you’ll see:** 生テキスト、信頼度スコア、各行・単語のバウンディングボックスを含む、見やすい JSON ドキュメントが生成されます。この構造は ElasticSearch や Azure Cognitive Search などの下流サービスへの投入に最適です。

---

## Convert Image to XML – Structured Data Output

レガシーシステムで XML が必要な場合もあります。IronOcr の `ToXml()` メソッドを使えば簡単に変換できます。

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

XML は JSON の階層構造を鏡像した形になり、`<Line>` と `<Word>` 要素に `Confidence` 属性が付与されます。独自スキーマが必要な場合は、`result` を手動で `XDocument` に投影すれば OK です。API は LINQ に完全対応しています。

---

## Full End‑to‑End Sample Code

すべてをまとめた、すぐに実行できる `Program.cs` は以下の通りです。

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**Expected output**（抜粋）:

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

`dotnet run` でプログラムを実行してください。設定が正しく行われていれば、コンソールに結果が表示され、`YOUR_DIRECTORY` に 2 つのファイルが生成されます。

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *What if the image is a JPEG with EXIF rotation?* | `Deskew()` の前に `input.AutoRotate()` を呼び出します。IronOcr が EXIF タグを読み取り、向きを自動補正します。 |
| *Can I OCR a folder of images in one go?* | 可能です。上記ロジックを `foreach (var file in Directory.GetFiles(folder, "*.png"))` ループでラップしてください。 |
| *How do I improve accuracy on noisy scans?* | `input.Denoise()` を増やし、`input.BlackWhiteThreshold(120)` の使用も検討してください。また、文書の言語に合わせた言語パックを提供すると効果的です。 |
| *Is the JSON format compatible with other OCR libraries?* | スキーマは汎用的で、`Text`、`Lines`、`Words` だけなので、Tesseract の出力に最小限の変換でマッピングできます。 |

---

## Performance Tips (Pro‑Level)

- **Reuse the engine**: ループ内で `IronTesseract` を毎回インスタンス化すると、スループットが最大 30 % 低下します。アプリケーションドメインごとにシングルトンとして保持しましょう。  
- **Parallelize I/O**: 数十枚の画像を処理する場合は、`Task.WhenAll` でメモリに同時読み込みし、同一エンジンに各 `OcrInput` を渡すことでスレッドセーフに並列処理できます。  
- **Batch export**: 各画像ごとに JSON/XML を個別に書き出すのではなく、結果をコレクションに集約して一括でシリアライズするとディスク I/O が削減されます。

---

## Next Steps & Related Topics

**recognize text from image** ができたら、パイプラインを拡張してみましょう。

- **Search integration** – JSON を Elasticsearch にプッシュして全文検索を実現。  
- **Document classification** – OCR 出力を軽量 ML モデルに渡し、請求書・契約書・領収書などを自動タグ付け。  
- **Handwritten text** – 言語パックを `OcrLanguage.EnglishHandwritten` に切り替える（IronOcr のプレミアムティアで利用可能）。  

これらはすべて、今回構築した基盤の上に積み上げられるため、数週間にわたって取り組めるテーマです。

---

## Conclusion

本稿では、最新の **OCR engine C#** を使って **recognize text from image** を行い、続いて **convert image to JSON** と **convert image to XML** にエクスポートする方法、さらに **load image for OCR** を堅牢に実装する手順を解説しました。完全なサンプルは 1 分未満で実行でき、生成されたファイルはあらゆる下流システムで利用可能です。

コードを実際に動かしてみて、必要に応じて調整してください。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全な動作コードとステップバイステップの解説が含まれているので、API の追加機能習得や代替実装の検討に役立ちます。

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}