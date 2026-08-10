---
category: general
date: 2026-04-04
description: Aspose OCR フィルターを使用して画像からテキストを抽出し、OCR を改善する方法。写真からテキストを認識し、OCR 用に画像を読み込む方法を学びましょう。
draft: false
keywords:
- how to improve ocr
- extract text from image
- recognize text from photo
- how to extract text
- load image for ocr
language: ja
og_description: OCR を迅速に改善する方法。このガイドでは、画像からテキストを抽出し、写真からテキストを認識し、Aspose を使用して OCR
  用に画像を読み込む方法を示します。
og_title: OCRを改善する方法 – ステップバイステップガイド
tags:
- OCR
- C#
- Aspose
title: OCRを改善する方法 – Asposeで画像からテキストを抽出
url: /ja/net/ocr-optimization/how-to-improve-ocr-extract-text-from-images-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR の精度向上 – Aspose を使用した画像からのテキスト抽出

画像が粒状で歪んでいたり、単にノイズが多い場合、**OCR の精度を向上させる方法**を考えたことはありませんか？ あなただけではありません。実際のプロジェクトでは、ぼやけたレシートや傾いた身分証明書が標準的な OCR エンジンの性能を大きく低下させることがあります。  

朗報です。いくつかのスマートなフィルタを追加し、画像を正しく読み込むだけで、**画像からテキストを抽出**する際のミスを大幅に減らすことができます。このチュートリアルでは、**写真からテキストを認識**する方法と、Aspose OCR を C# で使用する際の **OCR 用画像の読み込み** 方法も紹介します。  

ライブラリのインストールから、デノイズとデスキュー フィルタの微調整まで、すべての手順を順に解説します。これにより、ドキュメントを探し回ることなく、クリーンで読みやすいテキストを得られます。

## 学べること

- 画像強調フィルタが OCR の精度に重要な理由。  
- Aspose の `ImageStream` を使用した **OCR 用画像の読み込み** 方法。  
- **画像からテキストを抽出**し、コンソールに出力する、完全で実行可能なコード。  
- 極端な回転や大量のノイズといったエッジケースの対処法。  

**前提条件:** .NET 6 以上（または .NET Framework 4.7.2 以上）、Visual Studio 2022 または VS Code、そして Aspose OCR のライセンスまたは一時評価キー。その他のサードパーティ パッケージは不要です。

---

## フィルタで OCR の精度を向上させる方法

フィルタは、揺れたスナップショットを OCR エンジンが扱えるクリーンな入力に変える秘訣です。特に有用なものとして以下の 2 つがあります：

| フィルタ | 機能 | 使用タイミング |
|----------|------|----------------|
| **Denoise** | 文字認識を妨げるランダムなピクセルノイズを低減します。 | 低照度の写真、スキャンしたレシート。 |
| **Deskew** | 画像を水平に回転させます。 | 斜めに撮影された写真、完全に平らでないスキャンページ。 |

`Recognize()` を呼び出す **前に** これらのフィルタを適用すると、多くの場合で成功率が 20 %‑30 % 向上します。

### コードスニペット – フィルタの追加

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Add a denoise filter – strength is a value between 0 (off) and 1 (max)
ocrEngine.Filters.Add(new Denoise { Strength = 0.7 });

// Add a deskew filter – maxAngle limits how far the engine will try to rotate
ocrEngine.Filters.Add(new Deskew { MaxAngle = 5.0 }); // degrees
```

> **プロのコツ:** 出力がまだ傾いていると感じたら、`MaxAngle` を 10° に上げてみてください。ただしやりすぎは禁物です。過度な回転はアーティファクトを生む可能性があります。

---

## OCR 用画像の読み込み

エンジンは `ImageStream` を期待します。ローカルファイル、メモリストリーム、あるいは URL（少しコードを追加する必要があります）を指定できます。ここでは最もシンプルな例として、ディスク上の JPEG を読み込む方法を示します。

```csharp
// Load the image you want to recognize
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\noisy-photo.jpg");
```

> **重要な理由:** パスが間違っている、またはサポートされていない形式を指定すると `FileNotFoundException` がスローされ、処理が中断します。割り当てる前に必ずファイルの存在を確認してください。

メモリ上の `byte[]` を扱う必要がある場合は、単にラップすれば OK です：

```csharp
byte[] rawBytes = File.ReadAllBytes(@"C:\Images\noisy-photo.jpg");
ocrEngine.Image = ImageStream.FromBytes(rawBytes);
```

---

## 写真からテキストを認識 – エンジンの実行

画像とフィルタの設定が完了したら、実際の OCR 呼び出しは 1 行です。エンジンは抽出された文字列や信頼度スコアなどを含む `OcrResult` オブジェクトを返します。

```csharp
// Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();

// Display the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**期待されるコンソール出力**（写真に “Invoice #12345” が含まれていると仮定）:

```
=== OCR Output ===
Invoice #12345
Date: 04/04/2026
Total: $256.78
```

結果が空だったり文字化けしている場合は、フィルタの強度を再確認し、画像が暗すぎないか確認してください。また、`ocrResult.Confidence` をチェックすれば簡易的な品質指標が得られます。

---

## 完全な動作例

以下は新しいコンソール プロジェクトにコピー＆ペーストできる完全なプログラムです。`using` 文から最後の `Console.ReadKey()` まで、ウィンドウが開いたままになるようすべてが含まれています。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Add optional image‑enhancement filters to improve accuracy
            ocrEngine.Filters.Add(new Denoise { Strength = 0.7 });
            ocrEngine.Filters.Add(new Deskew { MaxAngle = 5.0 }); // degrees

            // 3️⃣ Load the image you want to recognize
            // Make sure the path points to an existing file on your machine
            string imagePath = @"C:\Images\noisy-photo.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"File not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // 5️⃣ Display the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // Keep the console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

> **エッジケースの注意:** 画像のバッチ処理を行う場合は、認識呼び出しを `try/catch` ブロックで囲んでください。破損したファイルに対しては Aspose が `OcrException` をスローすることがありますが、適切に処理すればバッチ全体の停止を防げます。

---

## よくある質問と落とし穴

| 質問 | 回答 |
|------|------|
| *画像が PNG 形式の場合はどうすればいいですか？* | Aspose OCR は PNG、BMP、TIFF、GIF を標準でサポートしています。パスの拡張子を変更するだけで OK です。 |
| *Linux でも実行できますか？* | はい。Aspose OCR はクロスプラットフォームです。.NET 6 をサポートする任意の OS で `dotnet run` を使用してください。 |
| *文字ごとの信頼度を取得する方法はありますか？* | `OcrResult` オブジェクトには `Characters` コレクションがあり、各文字に `Confidence` プロパティがあります。細かい分析のために反復処理できます。 |
| *非常に暗い写真の結果を改善するには？* | `Denoise` の前に `Contrast` または `Brightness` フィルタを追加します。例: `ocrEngine.Filters.Add(new Brightness { Level = 0.2 });` |

---

## まとめ

画像を正しく読み込み、デノイズとデスキュー フィルタを適用し、最後に `Recognize()` を呼び出すことで **OCR の精度を向上させる** 方法を解説しました。完全な例は、コードをクリーンかつ保守しやすく保ちつつ **写真からテキストを認識** する実践的な手法を示しています。  

次のステップは？ `Denoise` の強度を変えてみたり、`Contrast` や `Sharpness` といった他のフィルタを試して、信頼度スコアの変化を確認してください。また、ラテン文字以外のスクリプトを読み取る必要がある場合は、Aspose の多言語サポートも検討してみましょう。  

問題が発生したら遠慮なくコメントを残してください。また、OCR を最大限に活用するための自分のコツも共有してください。コーディングを楽しんで、テキストが常に読みやすくありますように！  

---  

![OCR 改善例](/images/aspose-ocr-example.png "OCR 改善 – フィルタ適用前後")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}