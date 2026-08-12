---
category: general
date: 2026-02-22
description: Aspose OCR を使用して検索可能な PDF を生成し、画像からテキストを抽出します。画像を PDF に変換し、プレーンテキストを出力する方法をひとつのチュートリアルで学びましょう。
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: ja
og_description: Aspose OCR を使用してスキャン画像から検索可能な PDF を生成します。このガイドでは、画像からテキストを抽出し、プレーンテキストを出力し、画像を
  PDF に変換する方法を示します。
og_title: 画像から検索可能なPDFを生成する – 完全C#チュートリアル
tags:
- C#
- OCR
- PDF generation
- Aspose
title: C#で画像から検索可能なPDFを生成する – ステップバイステップガイド
url: /ja/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像から検索可能な PDF を生成する – 完全チュートリアル

スキャンした画像から **検索可能な PDF** を生成したいと思ったことはありませんか？でも、どこから始めればいいか分からないことも多いでしょう。開発者の多くが OCR に初めて触れるときに壁にぶつかります。良いニュースは、Aspose OCR を使えば **画像からテキストを抽出** し、**プレーンテキストを出力**、そして **画像を PDF に変換** することが、C# の数行で実現できるということです。

このガイドでは、PNG ファイルの読み込みから検索可能な PDF とプレーンテキストファイルの保存まで、全工程を順に解説します。最後まで読むと、任意の .NET プロジェクトに貼り付けて使える再利用可能なコードスニペットが手に入ります。余計な説明は省き、実際に仕事を完了させるための内容だけです。

## 学べること

- .NET コンソールアプリで **Aspose.OCR** を設定する方法。  
- **output plain text** と **searchable PDF** モードの違い。  
- 画像から **テキストを抽出** し、`.txt` ファイルに書き込む方法。  
- 元のビットマップを保持しつつ、隠しテキストレイヤーを追加した **画像を PDF に変換** する方法。  
- 大量バッチ処理のコツ、よくある落とし穴、精度向上のために設定を調整すべきポイント。

> **前提条件** – .NET 6+（または .NET Framework 4.7+）、Visual Studio 2022（または任意のエディタ）、そして Aspose OCR のライセンス（または無料トライアル）が必要です。他のサードパーティライブラリは不要です。

![検索可能な PDF 生成例](image-placeholder.png "生成された検索可能な PDF の例")

## ステップ 1: Aspose OCR をインストールしエンジンを作成する

まずは **まず**、プロジェクトに NuGet パッケージを追加します：

```bash
dotnet add package Aspose.OCR
```

これで OCR エンジンを起動し、対象言語を指定できます。デフォルトは英語ですが、`Language` 列挙体を変更することでフランス語やスペイン語などに切り替えられます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**なぜ重要か:** エンジンは言語、出力形式、オプションの前処理フラグなどすべての設定を保持します。一度設定して再利用することで、**各ファイルごとに新しいインスタンスを作成するオーバーヘッド** を回避できます。

## ステップ 2: テキストを抽出してプレーンテキストとして保存する

生の文字だけが必要な場合は、エンジンを `OutputFormat.Text` に切り替えます。これにより Aspose OCR は PDF 生成を完全にスキップし、文字列を返します。

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**プロのコツ:** `plainTextResult.Text` は既に OCR のレイアウトに属する **改行** を除去しています。元の間隔が必要な場合は、代わりに `plainTextResult.TextBlocks` を確認してください。

### 期待される結果

`output.txt` を開くと、以下のような内容が表示されるはずです：

```
Hello, world!
This is a sample scanned document.
```

これがチュートリアルの **output plain text** 部分です。高速で軽量、そして下流処理（例: インデックス作成）に最適です。

## ステップ 3: 検索可能な PDF モードに切り替える

それでは **検索可能な PDF** を作成しましょう。エンジンは元のビットマップを埋め込み、OCR で生成されたテキストをその下にレイヤーとして追加します。これにより、任意の PDF ビューアで文書を検索可能になります。

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**なぜ再認識するのか:** OCR エンジンは最後に処理した画像をキャッシュしていますが、出力形式が返すデータを決定します。形式を切り替えることで、隠しテキストレイヤーを含む新たな処理が強制されます。

### PDF の見た目

`output.pdf` を Adobe Reader などのビューアで開き、テキスト選択を試してみてください。元のビットマップの見た目はそのままですが、内容をコピー、検索、ハイライトできることが分かります。これが **convert scanned image pdf** の特徴です。

## ステップ 4: �数ファイルの処理（オプション）

実際のプロジェクトでは単一画像だけを扱うことは稀です。以下はフォルダ内のすべての PNG を処理し、対応する `.txt` と `.pdf` ファイルを生成する簡易ループです。

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**エッジケースの注意:** 大きな画像はメモリを使い果たす可能性があります。`OutOfMemoryException` が発生した場合は、認識前に `Image.Resize` で縮小するか、ファイルを小さなバッチに分けて処理してください。

## ステップ 5: OCR 精度の微調整

Aspose OCR では調整できる設定がいくつか用意されています：

| 設定 | 機能 | 使用する場面 |
|------|------|--------------|
| `ocrEngine.PageSegmentationMode` | エンジンが画像をテキストブロックに分割する方法を制御します。 | 複数列レイアウトに有用。 |
| `ocrEngine.Deskew` | わずかに傾いたページを自動で回転させます。 | 完全に揃っていないスキャン文書。 |
| `ocrEngine.RemoveNoise` | 斑点や背景のアーティファクトを除去しようとします。 | 低品質のスキャンやファックスページ。 |

例：

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

これらのオプションを有効にすると処理時間が増加する可能性がありますが、**extract text from image** の品質向上は多くの場合価値があります。

## ステップ 6: プログラムで出力を検証する

PDF に実際に検索可能なテキストが含まれているか（例: 自動テストで）確認したいことがあります。最も簡単なチェックは、PDF のバイト配列が空でなく、`RawData` の長さが画像サイズを超えていることを検証することです。

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

より詳細な検証には、PDF ライブラリ（例: iTextSharp）を使用してテキストストリームを抽出し、`plainTextResult.Text` と比較することができます。

## よくある落とし穴と回避策

- **ライセンス未取得** – 有効な Aspose ライセンスがないと、ライブラリは評価モードで動作し、PDF に透かしが追加されます。ライセンスは早めに登録してください（`License license = new License(); license.SetLicense("Aspose.OCR.lic");`）。
- **パスが不正** – 絶対パスをハードコーディングすると自分のマシンでは動作しますが、他の環境では失敗します。移植性のために `Path.Combine` と `AppDomain.CurrentDomain.BaseDirectory` を使用してください。
- **サポート外の画像形式** – 複数フレームを持つ GIF や TIFF は特別な処理（`Image.LoadMultiPage`）が必要です。最初のページだけが必要な場合は、まず PNG/JPEG に変換してください。
- **パフォーマンスのボトルネック** – ループ内で `OcrEngine` を再作成するとコストがかかります。示したように、単一インスタンスを保持し、`OutputFormat` だけを変更してください。

## まとめ

Aspose OCR を使用してスキャン画像から **検索可能な PDF** を生成するための全工程をカバーしました：

1. NuGet パッケージをインストールし、`OcrEngine` を作成する。  
2. `OutputFormat.Text` を設定して **プレーンテキストを出力** し、`.txt` ファイルに書き込む。  
3. `OutputFormat.SearchablePdf` に切り替えて、隠しテキストレイヤー付きの **画像を PDF に変換** する。  
4. PDF バイト列を保存し、必要に応じてディレクトリをループしてバッチ処理を行う。  
5. デスクュー、ノイズ除去、ページ分割オプションで精度を微調整する。

これらすべてが、Visual Studio にコピー＆ペーストできるコンパクトで自己完結型のプログラムに収まっています。

## 次に試すことは？

- **バッチ処理** を UI フロントエンド（WinForms または WPF）で実装し、ユーザーがファイルをドラッグ＆ドロップできるようにする。  
- **言語検出** – Aspose OCR は言語を自動検出できます。`ocrEngine.Language = Language.AutoDetect` を試してみてください。  
- **ポストプロセッシング** – 抽出したテキストを検索インデックス（ElasticSearch、Azure Cognitive Search など）に投入し、即座に文書を取得できるようにする。  
- **代替出力** – `OutputFormat.Hocr` を使用して HTML ベースの OCR 結果を取得し、ウェブプレビューに活用する。

さまざまな画像解像度、カラーモード、OCR 設定を試してみてください。試行すればするほど、速度と精度のトレードオフをより深く理解できるようになります。

---

**ハッピーコーディング！** 問題が発生したら下にコメントを残すか、Aspose OCR のドキュメントで詳しく調べてみてください。請求書処理、アーカイブ、検索可能なナレッジベースの構築など、次のプロジェクトが格段に楽になります。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}