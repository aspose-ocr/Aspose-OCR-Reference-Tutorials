---
category: general
date: 2026-05-21
description: C# を使用して画像の OCR を実行します。OCR 用に画像を読み込む方法、PNG からテキストを抽出する方法、そして小さなコードサンプルで画像からテキストを認識する方法を学びましょう。
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: ja
og_description: C#で画像のOCRを高速に実行します。このガイドでは、OCR用に画像を読み込む方法、PNGからテキストを抽出する方法、レイアウトを考慮したHTML出力で画像からテキストを認識する方法を示します。
og_title: C#で画像のOCRを実行する – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: C#で画像のOCRを実行する – 完全ステップバイステップガイド
url: /ja/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像の OCR を実行する – 完全ステップバイステップガイド

重い GUI なしで **画像の OCR を実行** したいと思ったことはありませんか？ あなたは一人ではありません。領収書をデジタル化したり、スキャンしたフォームからデータを抽出したり、単に PNG を検索可能なテキストに変換したりする場合でも、数行の C# で作業を完了できます。

このチュートリアルでは、OCR 用に画像を読み込む方法、画像からテキストを認識する方法、そして最終的に PNG からクリーンな HTML を抽出する方法を順に解説します。最後まで読むと、**画像の OCR を実行** し、元のレイアウトを保持したコンソールアプリがすぐに実行できる状態になります。

## 作成するもの

- PNG（またはサポートされている任意の画像）を読み込む最小限のコンソールプログラム  
- OCR エンジンを使用して **画像からテキストを認識**  
- レイアウト情報を保持した HTML として結果を保存し、元画像を埋め込む  
- **OCR 用に画像を読み込む** 方法、**PNG からテキストを抽出** する方法、一般的なエッジケースの対処法を紹介  

> **前提条件**  
> - .NET 6.0 SDK 以降（.NET Framework 4.7+ でも可）  
> - NuGet 対応の OCR ライブラリ – 例では *Aspose.OCR* を使用していますが、同様の API を持つ任意のライブラリで構いません  
> - 基本的な C# の知識（特別な前提はなし）  

これらは揃っていますか？ では、始めましょう。

## OCR の実装 – 完全コード解説

以下は **完全に実行可能** なプログラムです。新しいコンソールプロジェクト（`dotnet new console`）に貼り付けて **F5** を押すだけです。

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **期待される出力**  
> ```
> HTML with layout saved.
> ```  
> 実行後、PNG と同じディレクトリに `form.html` が生成されます。ブラウザで開くとレイアウトはそのままですが、テキストが選択可能かつ検索可能になっています。

### OCR 用に画像を読み込む

`engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` の行が **OCR 用に画像を読み込む** 部分です。`ImageStream` ヘルパーはファイル形式の詳細を抽象化するため、JPEG、BMP、TIFF でもコードを変更せずに扱えます。  

**なぜ `Bitmap` を直接渡さないのか？**  
多くの OCR SDK は DPI メタデータを含むストリームを期待します。ライブラリ組み込みのローダーを使用することで、エンジンは画面上に表示される通りの画像を取得でき、精度が向上します。

#### プロのコツ
バッチ処理する場合は、ロード処理を `try/catch` で囲み、`FileNotFoundException` をログに記録しましょう。これにより、1 つのファイルが欠けていてもバッチ全体がクラッシュしなくなります。

### PNG からテキストを抽出する

`engine.Recognize()` が完了すると、OCR エンジンは内部に認識結果を保持します。レイアウトが不要で生テキストだけが欲しい場合は、次のように文字列として取得できます：

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

これは **PNG からテキストを抽出** する最速の方法です。多くのデータ入力作業ではプレーンテキストで十分です – CSV にインポートする際は改行をトリムすることを忘れないでください。

### 画像からテキストを認識する

`Recognize()` 呼び出しが本格的な処理を行います。内部ではエンジンが次の手順を実行します。

1. 画像を正規化（傾き補正、ノイズ除去）  
2. 行と単語に分割  
3. 数百万のグリフで学習したニューラルネットワークで分類  

`Language = OcrLanguage.English` を設定しているため、英語固有の辞書が適用され、誤認識が大幅に減少します。多言語対応が必要な場合は、言語の配列を渡すだけです：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### レイアウト対応 HTML 出力の取り扱い

多くの開発者はプレーンテキストで止めてしまいますが、ここで使用した `HtmlSaveOptions` により **画像の OCR を実行** しつつ視覚的構造を保持できます。重要なフラグは 2 つです。

- `PreserveLayout = true` – 列、テーブル、間隔を保持  
- `EmbedImages = true` – 元の PNG を Base64 エンコードした `<img>` 要素として埋め込み、HTML を単体で完結させる  

ファイルサイズを抑えたい場合は `EmbedImages = false` に設定すれば、HTML はディスク上の PNG を参照する形になります。

#### エッジケース: 大容量ファイル

画像が 5 MB を超える場合、埋め込みにより HTML サイズが急増します。その際は外部画像参照に切り替え、事前に `ImageProcessor.Compress` で PNG を圧縮すると良いでしょう。

## よくある落とし穴とプロのコツ

| 症状 | 考えられる原因 | 対策 |
|--------|--------------|-----|
| 文字化け | 言語設定が間違っている、または言語パックが不足 | 適切な言語データをインストールし、`engine.Language` を正しく設定 |
| 出力にテキストがない | 画像が暗すぎる、解像度が低すぎる | `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` で前処理 |
| HTML のレイアウトが崩れる | `PreserveLayout` がデフォルトの `false` のまま | `HtmlSaveOptions` で `PreserveLayout = true` を設定 |
| 多ページ処理が遅い | ファイルごとにエンジンを再初期化している | 同じ `OcrEngine` インスタンスを再利用し、ループ毎に `engine.Image` だけを差し替える |

### 複数ファイルへのスケーリング

フォルダー内の **画像の OCR を実行** したい場合は、コアロジックをシンプルなループで包みます：

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

ループ内で **OCR 用に画像を読み込む** ことは変わりませんが、`engine` と `htmlOptions` オブジェクトは使い回すことでメモリ消費と処理時間を削減できます。

## 発展編: PDF や DOCX へのエクスポート

同じ `engine` で他フォーマットにも保存可能です：

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

下流システムが検索可能な PDF を要求する場合、1 行の変更で対応でき、別途変換パイプラインを作る必要はありません。

## まとめ

C# で **画像の OCR を実行** し、**PNG からテキストを抽出** し、最終的にレイアウト対応 HTML に変換する手順を示しました。完全なサンプルはそのまま実行可能で、各ステップの意味、言語設定の変更方法、注意すべき落とし穴が理解できたはずです。

次は英語以外のロケールに差し替えてみたり、`PreserveLayout = false` にして軽量 HTML を生成したり、プレーンテキスト出力をデータベースに流し込んで検索アーカイブを作ったりしてみてください。堅実な OCR エンジンと数行の C# があれば、可能性は無限です。

マルチページ TIFF の取り扱いや ASP.NET Core API への統合方法について質問があれば、下のコメント欄で教えてください。Happy coding!

## 関連チュートリアル

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}