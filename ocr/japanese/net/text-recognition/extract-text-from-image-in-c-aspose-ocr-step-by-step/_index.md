---
category: general
date: 2026-03-05
description: C#で Aspose OCR を使用して画像からテキストを抽出します。C#で画像ファイルの読み取り方法、DJVU をテキストに変換する方法、そして
  OCR 画像を文字列に素早く変換する方法を学びましょう。
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このガイドでは、画像ファイルをC#で読み取り、DJVUをテキストに変換し、OCR画像を文字列に簡単に処理する方法を示します。
og_title: C#で画像からテキストを抽出 – 完全なAspose OCRガイド
tags:
- Aspose OCR
- C#
- Image Processing
title: C#で画像からテキストを抽出 – Aspose OCR ステップバイステップ
url: /ja/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する C# – 完全な Aspose OCR ガイド

画像から **テキストを抽出** したいけれど、どのライブラリが信頼できるか分からないことはありませんか？DJVU スキャンが大量にあって、サードパーティーツールをいじらずにプレーンテキストだけが欲しい、というケースもあるでしょう。このチュートリアルでは、Aspose OCR for .NET を使って数分でその問題を解決します。

C# で画像ファイルを読み込み、DJVU ドキュメントをテキストに変換し、OCR 画像をクリーンな文字列に変換する手順を順に解説します。最後には、認識したテキストをコンソールに出力する実行可能なコンソールアプリが完成します。「ドキュメントを参照してください」的な曖昧なリンクはありません—完全なコピペ可能ソリューションです。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.6+ でも動作します）。  
- **Aspose.OCR for .NET** NuGet パッケージ（無料トライアルライセンスでテスト可能）。  
- DJVU ファイルまたはサポートされている画像（PNG、JPEG、BMP など）。  
- Visual Studio、Rider、またはお好みのエディタ。

上記が揃っていない場合は、以下のコマンドで NuGet パッケージをインストールしてください：

```bash
dotnet add package Aspose.OCR
```

これでセットアップは完了です。さっそく始めましょう。

## Step 1: OCR エンジンの初期化 – extract text from image

最初に `OcrEngine` のインスタンスを作成します。これはピクセルを文字に変換する「脳」のようなものです。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

なぜファイルを読み込む前にエンジンをインスタンス化するのか？Aspose の設計では、設定（ライセンスなど）と実際の画像データを分離しているため、同じエンジンを複数ファイルで再利用でき、オブジェクトの再生成を避けられます。これが小さなパフォーマンス向上につながります。

## Step 2: Aspose OCR ライセンスの適用（任意だが推奨）

商用ライセンスをお持ちの場合は、ここで設定してください。省略するとデモモードになり、出力に透かしが入ったりページ数が制限されたりします。

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**プロのコツ:** ライセンスファイルはソース管理の外（例: 環境変数）に置き、誤ってコミットしないようにしましょう。

## Step 3: 画像の読み込み – read image file c# made easy

Aspose は多くのフォーマットに対応しており、マイナーな DJVU もサポートしています。`ImageStream.FromFile` ヘルパーを使ってファイルをエンジンにロードします。

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

データベースから取得した `byte[]` で画像を扱いたい場合は、`ImageStream.FromBytes(byteArray)` を使用できます。この柔軟性により、**read image file C#** をディスクではなくストリームから行うことが可能です。

## Step 4: OCR の実行 – ocr image to string in a single call

ここで魔法が起きます。`Recognize()` を呼び出すと OCR エンジンが実行され、抽出されたテキストや信頼度スコアなどを含む `RecognitionResult` が返ります。

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

`Recognize().Text` だけを呼び出さない理由は何か？呼び出しを分割することで、後で `result.Confidence` や `result.Regions` を確認でき、デバッグや低信頼度単語をハイライトする UI の構築に役立ちます。

## Step 5: 抽出テキストの表示 – your final output

最後にコンソールへテキストを書き出します。実際のアプリではファイルやデータベース、あるいは API へ送信することも考えられます。

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**期待される出力**（簡略化）:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

OCR エンジンが文字を認識できなかった場合、`recognizedText` は空文字列になります。その際は画像品質を再確認するか、エンジンの言語設定（例: `ocrEngine.Language = Language.English;`）を調整してください。

## DJVU をテキストに変換 – recognize text from djvu in bulk

多数の DJVU ファイルを処理したい場合は、先ほどのロジックをループで回します：

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

このスニペットは **DJVU をテキストに変換** し、各ソースファイルの隣に `.txt` を自動生成します。レガシーなスキャン文書から検索可能なアーカイブを素早く作る方法です。

## エッジケースの処理 – 画像がノイズだらけだったら？

画像がぼやけていたり、コントラストが低かったり、カラー背景があると OCR の精度は低下します。Aspose OCR では前処理オプションが用意されています：

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

また、エンジンに言語を自動検出させることも可能です：

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

これらの調整により、60 % の精度が 95 % に向上することもあります。`Threshold`、`Denoise`、`Deskew` メソッドを試してみてください。

## 完全動作サンプル – copy, paste, run

以下はコンパイル可能なフルプログラムです。`"YOUR_DIRECTORY/input.djvu"` を実際のパスに置き換え、ライセンスファイルが参照可能であることを確認してください。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

実行は次のコマンドで：

```bash
dotnet run
```

先ほどの例と同様に、抽出されたテキストがコンソールに表示されます。

## よくある質問と落とし穴

- **PDF ファイルでも動作しますか？**  
  直接はできません。Aspose OCR はラスタ画像を対象とするため、PDF の場合は各ページを画像に変換（例: Aspose.PDF を使用）してから OCR エンジンに渡す必要があります。

- **サーバー上で大量バッチ処理したい場合は？**  
  **単一** の `OcrEngine` をインスタンス化し、スレッド間で再利用してください。エンジンは読み取り専用操作に対してスレッドセーフですが、同じ `Image` インスタンスを同時に共有しないように注意が必要です。

- **フォーマット情報（フォントやサイズ）も取得できますか？**  
  Aspose OCR はプレーンな Unicode テキストのみを返します。レイアウト情報を保持した抽出が必要な場合は、OCR‑ML などの高度なソリューションやレイアウト保持機能を持つ PDF ライブラリを検討してください。

## 次のステップ – ワークフローの拡張

**画像からテキストを抽出** できるようになったら、以下のような活用を検討してください：

- 抽出結果を Elasticsearch に保存し、全文検索を実現。  
- テキストを言語モデルに渡して要約を生成。  
- ASP.NET Core でシンプルな UI を作り、ファイルアップロードと OCR 結果の即時表示を実装。

これらはすべて、今回紹介したコアコードをベースに拡張できるので、次のステップへスムーズに進めます。

---

### クイックまとめ

- `OcrEngine` を **初期化**（Aspose OCR の心臓部）。  
- **ライセンス** を適用してフル機能をアンロック。  
- `ImageStream.FromFile` で DJVU ファイルを **ロード**。  
- `Recognize()` を呼び出し、**ocr image to string** 結果を取得。  
- **抽出テキスト** をコンソールに出力。  

これで、DJVU を含む任意のサポート画像を C# で検索可能なテキストに変換する完全なレシピが完成です。

---

さまざまな画像フォーマットで実験したり、前処理設定を調整したり、他の Aspose ライブラリと組み合わせてみてください。問題が発生したらコメントで教えてください—ハッピーコーディング！

![画像からテキストを抽出する例](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}