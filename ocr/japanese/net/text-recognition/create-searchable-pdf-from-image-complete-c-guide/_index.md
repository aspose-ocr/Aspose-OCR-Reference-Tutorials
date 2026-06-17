---
category: general
date: 2026-03-23
description: Aspose OCR を使用して画像から検索可能な PDF を作成します。高圧縮で TIFF を PDF に変換し、数分で画像のテキストを認識する方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: ja
og_description: Aspose OCR を使用して画像から検索可能な PDF を作成します。このチュートリアルでは、TIFF を PDF に変換し、検索可能なテキスト層を追加し、高圧縮を適用する方法を示します。
og_title: 画像から検索可能なPDFを作成 – 完全C#ガイド
tags:
- Aspose OCR
- C#
- PDF generation
title: 画像から検索可能なPDFを作成する – 完全C#ガイド
url: /ja/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像から検索可能な PDF を作成 – 完全 C# ガイド

スキャンしたドキュメントから **検索可能な PDF** を作成したいけど、どこから始めればいいか分からないことはありませんか？同じ壁にぶつかる開発者は多いです。TIFF スキャンを検索可能な PDF に変換する際に。朗報です！Aspose OCR を使えば **tiff を pdf に変換** し、隠しテキストレイヤーを重ね、さらに **高圧縮 pdf** オプションでファイルサイズを削減できます。C# の数行で実現できます。

このチュートリアルでは、必要な NuGet パッケージのインストールから、TIFF 画像の読み込み、テキスト認識、検索可能な PDF のエクスポートまで、全工程を順に解説します。最後には、**画像テキストを認識**し、コンパクトで検索可能な PDF を生成するコンソール アプリが完成します。余計なツールや手動 OCR 手順は不要です。コードと簡単な説明だけです。

## 前提条件と必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。API はどちらでも動作しますが、.NET 6 では最新のランタイム改善が利用できます。  
- **Visual Studio 2022** もしくはお好みの IDE。  
- **Aspose.OCR** と **Aspose.OCR.Gpu** NuGet パッケージ（GPU パッケージは任意ですが、対応ハードウェアがある場合は認識が高速化します）。  
- サンプル TIFF ファイル（例: `invoice.tif`）を任意のフォルダーに配置しておくこと。  

すでにこれらが揃っていれば、次へ進んでください。まだの場合は、以下のインストール手順で全てカバーします。

## Step 1: Install Aspose OCR Packages

まず、プロジェクト フォルダーをターミナルで開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

これでコア OCR エンジンと GPU 加速ライブラリの両方が取得されます。GPU が見つからない環境でもエンジンは CPU モードにフォールバックします。  

> **プロのコツ:** 本番環境向けにビルドする際は、`csproj` にパッケージ バージョンを固定して、予期せぬ破壊的変更を防ぎましょう。

## Step 2: Set Up the Project Skeleton

まだコンソール アプリがない場合は、次のコマンドで作成します。

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

自動生成された `Program.cs` を、後述の完全コードに差し替えてください。プログラムの流れは以下の通りです。

1. GPU サポート付きで `OcrEngine` を初期化。  
2. TIFF 画像を読み込む。  
3. OCR を実行し、失敗した場合は優雅に終了。  
4. **PdfExportOptions** を設定し、検索可能レイヤーと **高圧縮** を有効化。  
5. 出力ファイルを書き出す。

## Step 3: Write the Complete Code (Full Example)

以下が *全体* のソース ファイルです。`Program.cs` にコピー＆ペーストしてください。コメントは「何をするか」だけでなく「なぜそうするか」も説明しています。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Why This Works

- **GPU 加速** により、最新のカードでは認識時間が秒単位からミリ秒単位に短縮されます。大量処理に便利です。  
- **IncludeTextLayer** は OCR で取得したテキストを目に見えない形で埋め込み、PDF ビューアが画像の外観を変えずに検索できるようにします。  
- **高圧縮** は画像ストリームに Flate（ZIP）圧縮を適用し、ロスレスながらファイルサイズを大幅に削減します。大量の請求書を保存するのに最適です。

## Step 4: Run the Application and Verify Output

プロジェクト フォルダー内のターミナルで次を実行します。

```bash
dotnet run
```

正しく設定されていれば、以下のように表示されます。

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

`invoice.pdf` を任意の PDF リーダー（Adobe Acrobat、Edge、ブラウザーなど）で開き、元の TIFF に含まれる単語（例: “Total”）で検索してみてください。画像の一部であっても、ビューアがハイライト表示するはずです。これが **検索可能な pdf** の特徴です。

### Expected File Size

典型的なスキャン請求書（≈300 KB TIFF）は、`PdfCompression.High` を適用すると **約80 KB** に縮小されます。正確なサイズは画像の複雑さに依存しますが、明らかな削減が確認できるでしょう。

## Step 5: Common Variations & Edge Cases

| Situation | What to Adjust | Why |
|-----------|----------------|-----|
| **GPU が利用できない** | `new OcrEngine(GpuMode.Enabled)` を `new OcrEngine(GpuMode.Disabled)` に変更 | GPU 初期化を試みず、短い遅延で済むようにします。 |
| **複数ページ（マルチページ TIFF）** | `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` を設定 | すべてのフレームを読み込み、Aspose が各ページを処理してマルチページ PDF を生成します。 |
| **英語以外の OCR 言語が必要** | `ocrEngine.Language = Language.French;`（またはサポートされている任意の言語） | 英語以外の文書で精度が向上します。 |
| **隠しレイヤーではなく可視テキストオーバーレイが欲しい** | `pdfExportOptions.IncludeTextLayer = false;` にし、手動で `TextFragment` オブジェクトを追加 | 画像上に選択可能なテキストとして OCR 結果を表示したい場合に有用です。 |
| **極小 PDF が必要** | `PdfCompression.High` と併せて認識前に `ImageResolution = 150` DPI を設定 | DPI を下げることで画像データが減り、PDF がさらに小さくなりますが、画質は低下します。 |

> **注意:** 本番環境に展開する前に、必ず小さなサンプルでエッジケースをテストしてください。画像品質、ノイズ、言語によって OCR 精度は変わります。

## Step 6: Tips for Production‑Ready Implementations

1. **エラーロギング** – `Console.WriteLine` を Serilog や NLog といった本格的なロギング フレームワークに置き換えて、診断を容易にします。  
2. **バッチ処理** – コア ロジックを入力/出力パスを受け取るメソッドにまとめ、TIFF ファイルが格納されたディレクトリを走査します。  
3. **非同期 I/O** – Aspose OCR 自体は同期ですが、ファイルの読み書きを非同期にすれば UI スレッドの応答性が保たれます。  
4. **セキュリティ** – この機能を Web API 経由で提供する場合は、ファイルパスの検証とサイズ制限を行い、悪用を防止します。  
5. **バージョン固定** – ビルド間で挙動を統一するために、正確なバージョン番号（例: `<PackageReference Include="Aspose.OCR" Version="23.12.0" />`）を使用します。

## Conclusion

今回、**スキャン画像から検索可能な PDF を作成**し、**tiff を pdf に変換**、さらに **高圧縮 pdf** 設定で **画像テキストを認識**する **完全なエンドツーエンド ソリューション**を構築しました。生成された **画像から検索可能な pdf** は軽量で検索可能、インデックス作成、アーカイブ、e‑discovery などの次工程にすぐに利用できます。

大量の請求書がありますか？メソッドをループに組み込み、フォルダーを指定すれば Aspose OCR が重い作業を代行します。圧縮レベルや言語パックを変えて実験したいですか？コードはモジュール化されているので、数秒でオプションを差し替えられます。

---

*さらにレベルアップしたいですか？* ウォーターマークの追加、メタデータ埋め込み、複数の OCR 処理済み PDF を結合することにも挑戦してみましょう。Aspose スイートは多くの拡張機能を提供しています—ドキュメントを探検し、勢いを保ち続けてください。Happy coding!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}