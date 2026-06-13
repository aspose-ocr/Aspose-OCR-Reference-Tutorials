---
category: general
date: 2026-02-13
description: C#でOCRを使用して画像からテキストを抽出し、写真やJPGからテキストを認識し、インターネットなしで画像に対してOCRを実行する方法
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: ja
og_description: C#でOCRを使用して画像からテキストを抽出し、写真からテキストを認識し、完全な実行可能なサンプルで画像にOCRを実行する方法。
og_title: C#でOCRを使用する方法 – 画像からテキストを抽出
tags:
- OCR
- C#
- Image Processing
title: C#でOCRを使用する方法 – 画像からテキストを抽出し、写真から文字を認識する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – 画像からテキストを抽出し、写真からテキストを認識する

Ever wondered **how to use OCR** to pull words out of a screenshot, a scanned receipt, or a random photo you snapped on your phone? You're not the only one. In many real‑world apps we need to turn pictures into searchable text, and doing it locally—without a flaky internet connection—can feel like a puzzle.

That’s why this guide shows you a step‑by‑step way to **extract text from image** files using a C# OCR engine, and it also covers how to **recognize text from photo**, **recognize text from JPG**, and **run OCR on image** files that sit right on your disk. By the end you’ll have a complete, copy‑paste‑ready program that works out of the box.

## 学べること

- Simplified Chinese（簡体字中国語）用に OCR エンジンを設定する方法（または任意の言語）。  
- ローカルフォルダーから **load resources**（リソースをロード）するために必要な正確なコード（ネットワーク呼び出しは不要）。  
- JPEG、PNG、BMP などの **recognize text from photo** ファイルを認識する方法。  
- モデルファイルが欠如している、またはサポートされていない画像形式など、一般的なエッジケースの対処法。  
- Visual Studio に貼り付けてすぐに結果が確認できる、完全な実行可能サンプル。

### 前提条件

- .NET 6.0 以降（本稿で使用している API は .NET Standard 2.0 を対象としているため、古いバージョンでも動作します）。  
- C# と Visual Studio（またはお好みの IDE）に関する基本的な知識。  
- 使用している OCR ライブラリ（このスニペットは、言語モデルと共に提供される架空の `OcrEngine` クラスを前提としています）。  
- 必要な言語モデルファイルが格納されたフォルダー—エンジンが中国語文字を読むための「脳」に相当します。

> **Pro tip:** まだ中国語モデルファイルを持っていない場合は、ベンダーのサイトから一度ダウンロードし、`C:\OcrResources` のようなフォルダーに配置してください。エンジンは以後オンラインにアクセスする必要がなくなります。

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## OCR の使用方法：エンジンのセットアップ

最初に必要なのは、対象言語用に設定された OCR エンジンのインスタンスです。このチュートリアルでは **Simplified Chinese**（簡体字中国語）を対象としていますが、`OcrLanguage.ChineseSimplified` を `OcrLanguage.English`（または他の列挙値）に置き換えるだけで、ワンラインで変更できます。

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Why this matters:**  
`Language` プロパティを設定することで、エンジンが期待する文字セットを指定します。`ResourceFolder` はエンジンがニューラルネットワークの重みや言語辞書を探す場所で、脳の記憶バンクと考えてください。間違ったフォルダーを指定すると、エンジンは `FileNotFoundException` をスローし、処理が停止します。

## 画像からテキストを抽出 – リソースのロード

エンジンが実際に文字を読み取る前に、モデルファイルをメモリにロードする必要があります。このステップは **crucial**（重要）で、画像を処理するたびにネットワーク呼び出しを回避できます。

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**What could go wrong?**  
フォルダー パスが間違っている、またはファイルが破損している場合、`LoadResources()` は例外をスローします。上記の `try/catch` ブロックは、実運用で頻繁に必要となる、優雅なエラーハンドリングの例です。

## 写真からテキストを認識 – OCR の実行

さあ楽しいパートです：画像ファイルをエンジンに渡し、認識されたテキストを取得します。これは **run OCR on image** シナリオの核心で、画像が JPEG、PNG、あるいは BMP でも同様です。

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage` メソッドは `RecognitionResult`（または SDK が使用する任意の型）を返し、通常は以下を含みます。

- `Text` – プレーンテキストの文字起こし。  
- `Confidence` – 各行に対するエンジンの確信度を示す数値スコア。  
- `BoundingBoxes` – 各単語が画像上のどこにあるかを示すオプションの座標。

**Why you might care about confidence:**  
データ入力の自動化ツールを構築している場合、しきい値（例：0.85）を設定し、低信頼度の行についてユーザーに確認を求めることができます。これにより全体の精度が大幅に向上します。

## JPG からテキストを認識 – 異なるフォーマットの取り扱い

多くの開発者は OCR が PNG のみ対応と考えがちですが、最新のエンジンは **JPG** ファイルも問題なく処理できます。唯一の注意点は、JPEG 圧縮がモデルを混乱させるアーティファクトを生む可能性があることです。

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

`DenoiseAndDeskew` ヘルパーがない場合は、多くのライブラリ（例：OpenCvSharp）で同様の機能が提供されています。重要なポイントは、スキャナーやスマートフォンのカメラから取得した場合は、少しクリーニングした後に **run OCR on image** ファイルを実行することです。

## 画像で OCR を実行 – ヒント、エッジケース、ベストプラクティス

### 1. メモリ管理

Loading large language models can consume hundreds of megabytes. Dispose of the engine when you’re done:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. バッチ処理

If you need to process dozens of photos, load resources once, then loop:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. マルチ言語シナリオ

`ocrEngine.Language` を再割り当てし、`LoadResources()` を再度呼び出すことで、実行時に言語を切り替えることができます。ただし、追加のロード時間がかかる点に注意してください。

### 4. 空結果の処理

Sometimes the engine returns an empty string. That usually means the image is too blurry or the text color blends into the background. A quick check:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. セキュリティ上の考慮事項

ユーザーがアップロードしたファイルを検証せずに OCR エンジンに直接渡してはいけません。最低でもファイル拡張子とサイズを確認し、マルウェアスキャンを検討してください。

---

## 完全な動作例

以下は、単一の自己完結型プログラムで、新しいコンソール アプリ プロジェクトにコピーして使用できます。**how to use OCR**、**extract text from image**、**recognize text from photo**、**recognize text from JPG**、そして **run OCR on image** をすべて一度に実演します。

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Expected output (example):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

実際の出力は画像の内容に応じて異なりますが、コンソールに Unicode 文字のブロックと信頼度パーセンテージが表示されるはずです。

---

## 結論

ここまでで、C# における **how to use OCR** の全工程—エンジンの設定、言語リソースのロード、そしてインターネットに接続せずに **recognize text from photo** や **JPG** ファイルを認識する方法—を解説しました。上記の手順に従えば、**extract text from image** ファイルや **run OCR on image** アセットを扱い、初心者が陥りやすい一般的な落とし穴に対処できるようになります。

次のチャレンジに備えましたか？ エンジンに画像に変換した PDF ページを入力したり、別の言語パックで実験して信頼度スコアの変化を確認してみてください。あなたは…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}