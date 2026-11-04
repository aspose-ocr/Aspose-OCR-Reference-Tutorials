---
category: general
date: 2026-03-17
description: C#でOCRを実行し、アラビア語テキストを抽出し、画像から文字を認識して画像をテキストに変換する方法を、完全なコード例とともに学びましょう。
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: ja
og_description: C#でOCRを実行する方法は？このガイドでは、アラビア語テキストの抽出、画像からのテキスト認識、画像をテキストに変換する手順を数ステップで紹介します。
og_title: C#でOCRを行う方法 – アラビア語テキストの抽出
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: C#でOCRを実行する方法 – 画像からアラビア語テキストを抽出する
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 画像からアラビア語テキストを抽出する

アラビア語の請求書やスキャンした文書で **OCRの実行方法** を疑問に思ったことはありませんか？ あなたは一人ではありません。多くの開発者がビットマップからアラビア文字を取り出す際に壁にぶつかります。朗報は、数行のC#コードで画像ファイルからテキストを認識し、画像をテキストに変換し、最終的に **アラビア語テキストを抽出** して下流処理に利用できるということです。

このチュートリアルでは、OCRの実行方法、各ステップの重要性、右から左へ書くスクリプトを扱う際の注意点を示す、完全に実行可能なサンプルを順を追って解説します。最後まで読むと、アラビア語、ウルドゥー語、クルド語、またはOCRエンジンがサポートする任意の言語で **画像からテキストを抽出** できるようになります。

## Prerequisites

- .NET 6.0 以降（コードは .NET Core でもコンパイル可能）  
- `OcrEngine` を提供する OCR ライブラリへの参照（例: `MyOcrSdk.dll`）  
- `invoice_arabic.png` のようなアラビア語テキストを含む画像ファイル  
- C# コンソールアプリケーションの基本的な知識

> **Pro tip:** OCR SDK が手元にない場合は、*MyOcrSdk* の無料コミュニティエディションを使用すればテストが可能で、今回使用する言語もサポートされています。

---

## Step 1 – Set Up the Project and Import the OCR Namespace

**画像からテキストを認識** する前に、プロジェクトの雛形と適切な `using` ディレクティブが必要です。

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*Why this matters:* 正しい名前空間をインポートすることで `OcrEngine`、`Language`、`ImageStream` にアクセスできるようになります。このステップを省くと、初心者にとってフラストレーションの原因となるコンパイルエラーが発生します。

---

## Step 2 – Create an OCR Engine Instance (Primary Keyword Included)

実際にエンジンをインスタンス化して **OCR を実行** します。

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

`OcrEngine` オブジェクトは処理の中心で、設定を保持し、重い処理を実行し、抽出された文字列を含む結果オブジェクトを返します。言い換えれば、**画像をテキストに変換** する「脳」のようなものです。

---

## Step 3 – Choose the Language for Recognition

アラビア語、ウルドゥー語、クルド語は同じ文字体系を共有するため、エンジンに期待する言語を伝える必要があります。これにより精度が劇的に向上します。

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*Why this matters:* OCR エンジンは言語モデルに依存しています。正しいモデルを選択することで、特に右から左へ書くスクリプトにおいて、見た目が似ている文字の誤認識が大幅に減少します。

---

## Step 4 – Load the Image Containing the Text

エンジンが解析できるビットマップが必要です。ヘルパー `ImageStream.FromFile` はファイル I/O の詳細を抽象化します。

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

パスが **有効な画像** を指していることを確認してください。ファイルが存在しない、または破損している場合、エンジンは例外をスローし、**画像からテキストを抽出** に失敗します。

---

## Step 5 – Run the OCR Process and Retrieve the Result

最後に `Recognize()` を呼び出し、抽出された文字列を表示します。

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

`ocrResult.Text` プロパティには、エンジンが読み取れたすべてのテキストがプレーンテキスト形式で格納されます。多くの場合、アラビア文字と数字が混在した結果が得られ、データベースへの挿入や翻訳といったさらなる処理に最適です。

### Expected Output

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

文字化けが発生した場合は、言語設定を再確認し、画像の解像度が高い（300 dpi 以上が理想）ことを確認してください。

---

## Full Working Example

以下は **完全な自己完結型プログラム** です。新しいコンソールプロジェクトにコピー＆ペーストしてすぐに実行できます。

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **Note:** OCR SDK がライセンスを必要とする場合は、ステップ 1 の前にライセンスを初期化してください（例: `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`）。簡潔さのためこの行は省略しています。

---

## Handling Common Edge Cases

| Situation | Why it Happens | Quick Fix |
|-----------|----------------|-----------|
| **ぼやけた低解像度画像** | OCR の精度が 70 % 以下に低下 | 300 dpi でスキャンするか、エンジンに渡す前にバイキュービックアルゴリズムでアップスケール |
| **混在言語（アラビア語＋英語）** | エンジンが最初の言語ブロックで停止することがある | マルチ言語モードを有効化: `ocrEngine.Config.Language = Language.Arabic \| Language.English;` |
| **右から左への表示問題** | コンソールが左から右へ文字を出力するため、アラビア語が逆向きに見える | `Console.OutputEncoding = System.Text.Encoding.UTF8;` を使用し、RTL スクリプトに対応したターミナルを利用 |
| **多数ページの PDF を分割** | メモリ使用量が急増 | ページごとに処理: 各ページを別々の画像として読み込み、OCR フローを繰り返す |
| **特殊記号（通貨、日付）** | 一部の OCR モデルがノイズとして扱う | 正規表現で `ocrResult.Text` を後処理し、既知パターンを正規化 |

---

## Extending the Solution – From OCR to Data Extraction

**OCR の実行方法** を習得したら、抽出したアラビア語テキストで何ができるか考えてみましょう。以下は自然に思い浮かぶ活用例です。

1. **請求書の解析** – 正規表現で請求書番号、日付、合計金額を抽出  
2. **翻訳 API への送信** – Azure Translator や Google Cloud Translate にアラビア語文字列を送る  
3. **データベースへの保存** – クリーンアップしたテキストを SQL テーブルに挿入し、レポート作成に利用  
4. **ワークフローのトリガー** – RabbitMQ などのメッセージキューと組み合わせて下流処理を開始  

これらのシナリオすべてで共通するのは、**画像をテキストに変換** し、その結果を操作するという基本操作です。

---

## Conclusion

本稿では、C# で **OCR を実行** し、画像から **アラビア語テキストを抽出** するために必要なすべての手順を網羅しました。プロジェクトのセットアップ、`OcrEngine` のインスタンス化、言語設定、ビットマップの読み込み、認識実行、結果の出力までを順に解説し、一般的な落とし穴と実務パイプラインへの拡張方法も紹介しました。

画像パスを差し替えたり、言語をウルドゥー語に変更したり、出力をデータベースに連携したりして試してみてください。**画像からテキストを認識** し、**画像をテキストに変換** できるようになれば、可能性は無限に広がります。

---

### Related Topics You Might Want to Explore

- **Extract text from image** using Tesseract OCR (open‑source alternative)  
- **Batch OCR processing** for thousands of scanned PDFs  
- **Improving OCR accuracy** with image pre‑processing (thresholding, noise removal)  
- **Handling right‑to‑left scripts** in .NET UI frameworks (WPF, WinForms)

質問や問題があればコメントで教えてください。また、このパターンを自分のプロジェクトにどのように適用したかシェアしていただけると嬉しいです。Happy coding!  

![how to perform OCR example](images/ocr_flow.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}