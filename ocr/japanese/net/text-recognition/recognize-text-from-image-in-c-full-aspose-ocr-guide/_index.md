---
category: general
date: 2026-04-03
description: C#でAspose OCRを使用して画像からテキストを認識します。OCR用に画像を読み込み、画像からテキストを抽出し、C#でJSONファイルを書き込み、PNGでOCRを実行する方法を学びます。
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを認識する。OCR用に画像を読み込み、画像からテキストを抽出し、C#でJSONファイルを書き込み、PNGでOCRを実行するステップバイステップガイド。
og_title: C#で画像からテキストを認識する – 完全なAspose OCRチュートリアル
tags:
- OCR
- C#
- Aspose
title: C#で画像からテキストを認識する – 完全なAspose OCRガイド
url: /ja/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像からテキストを認識する – 完全 Aspose OCR チュートリアル

Ever needed to **画像からテキストを認識する** but weren't sure which library to pick? Maybe you have a batch of scanned receipts, a PNG screenshot, or a handwritten note that you want to turn into searchable data. The good news: with Aspose.OCR you can do it in a few lines of C# code, and you’ll even get a tidy JSON file you can feed into other systems.

このチュートリアルでは、OCR 用に画像を読み込む方法、**画像からテキストを抽出する** 方法、結果を JSON ファイルにシリアライズする方法、そして PNG ファイルを手間なく処理する方法を順に解説します。最後までで、**画像からテキストを認識する** コンソールアプリが完成し、出力を *output.json* に書き込むことができます。

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework でも動作します）
- Aspose.OCR NuGet パッケージ（`Install-Package Aspose.OCR`）
- 処理したい PNG（またはサポートされている任意の形式）
- 好みの C# エディタ（Visual Studio、VS Code など）

追加のサードパーティライブラリは不要です—Aspose OCR エンジンと組み込みの `System.Text.Json` シリアライザだけで十分です。

## 手順 1: Aspose OCR を使用して画像からテキストを認識する

最初に行うべきことは `OcrEngine` インスタンスを作成することです。このオブジェクトが裏で重い処理を担当します。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**なぜ重要か:** `OcrEngine` を一度だけインスタンス化して再利用する方が、ファイルごとに新しいエンジンを作成するより効率的です。`RecognizeToResult` 呼び出しは、抽出されたテキスト、信頼度スコア、バウンディングボックスをすでに含む `OcrResult` オブジェクトを返すため、下流の処理に最適です。

## 手順 2: OCR 用に画像を読み込む – 異なるフォーマットの取り扱い

Aspose OCR は PNG、JPEG、BMP など多数のフォーマットを読み取れます。透過を含む PNG を扱う場合、予期せぬ空白を防ぐために先にフラット化すると良いでしょう。

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**プロのコツ:** 画像のサイズが妥当か常に確認してください（例: 幅 > 50 px）。非常に小さい画像は OCR エンジンが文字を見逃す原因となり、信頼度スコアが低くなります。

## 手順 3: C# で JSON ファイルを書き出す – 出力を利用しやすくする

`System.Text.Json` シリアライザは高速で組み込み型ですが、カスタムコンバータが必要な場合は `Newtonsoft.Json` に置き換えることもできます。上記の例ではすでに `WriteIndented = true` を使用しているため、生成されたファイルは人間が読みやすい形式になります。

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

OCR データを JSON 形式で保持すれば、データベースへのインポート、HTTP 経由での送信、機械学習パイプラインへの入力などが簡単に行えます。

## 手順 4: 結果を検証する – 簡易サニティチェック

プログラム実行後、`output.json` を開き `"Text"` フィールドを確認してください。期待通りの文字列が含まれていれば、**画像からテキストを抽出する** に成功したことになります。信頼度が低い場合は、画像の前処理（例: コントラストの上げ方や二値化しきい値の適用）を検討してください。

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

コンソールを実行すると、次のような出力が表示されます:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

これは OCR が期待通りに動作したことを示す確かなサインです。

## よくある落とし穴とエッジケース

| 問題 | 発生原因 | 対処方法 |
|-------|----------------|------------|
| **空白出力** | 画像が暗すぎる、またはサポートされていないカラースペースである | グレースケールに変換し、明るさを上げる、または PNG をフラット化する（手順 2 を参照） |
| **文字化け** | DPI が低い（< 72）またはノイズが多い | `RecognizeToResult` に渡す前に画像を拡大するか、ノイズ除去フィルタを適用する |
| **大きなファイルでメモリ圧迫** | `Bitmap` にマルチメガピクセル PNG を読み込むと RAM を消費する | 画像を分割して処理するか、可読性を保ちつつ縮小する |
| **JSON シリアライズエラー** | `OcrResult` に循環参照が含まれている（可能性は低い） | `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` を使用する |

## ボーナス: PNG をバッチループで OCR 実行

PNG ファイルが多数入ったフォルダーがある場合、デモを拡張してそれらを順に処理できます:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

これでプログラムは PNG ファイルを一括で **OCR 実行** し、各画像に対応する JSON ファイルを書き出します。

## 結論

これで、C# と Aspose OCR を使って **画像からテキストを認識する** 方法、**OCR 用に画像を読み込む**、**画像からテキストを抽出する**、そして結果を保存する **C# で JSON ファイルを書き出す** 方法を学びました。完全で実行可能なサンプルは必須ステップを網羅し、各要素が重要な理由を解説し、PNG 固有の注意点にも対応しています。

次のステップは？JSON を検索インデックスに投入したり、言語検出と組み合わせたり、アップロードをリアルタイムで処理する Web API に統合したりしてみてください。また、用途に応じて Aspose の手書き認識サポートを調べるのもおすすめです。

エッジケースやパフォーマンスチューニングに関する質問がありますか？下にコメントを残してください—楽しいコーディングを！

![画像からテキストを認識するデモ](/images/ocr-demo.png "Aspose OCR が画像からテキストを認識する様子を示す図")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}