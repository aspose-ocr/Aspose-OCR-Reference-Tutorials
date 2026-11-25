---
category: general
date: 2026-06-03
description: Aspose.OCR を使用して、動画からフレームを抽出し、MP4 などの動画ファイルからテキストを読み取る方法を示すビデオ字幕 OCR
  チュートリアル。
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: ja
og_description: Aspose.OCRで動画字幕のOCRを学びましょう。動画からフレームを抽出し、動画内のテキストを読み取り、MP4からテキストを数分で抽出します。
og_title: C#で動画字幕OCR – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: C#でのビデオ字幕OCR – 完全ガイド
url: /ja/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# におけるビデオ字幕 OCR 完全ガイド

ビデオ字幕 OCR が必要だったが、どこから始めればいいかわからなかったことはありませんか？ あなたは一人ではありません。講義録画をデジタル化したり、トレーニングビデオからキャプションを抽出したり、単にビデオからテキストを読むことに興味があるだけでも、このチュートリアルでは C# と Aspose.OCR を使って正確にやり方を示します。  

次の数分でビデオからフレームを抽出し、これらのフレームに OCR を実行し、最終的に字幕テキストをフレームごとに表示します。最後まで読めば、**ビデオからテキストを読む**（MP4 を含む）ことが、サードパーティツールを探さずにできるようになります。

## 作成するもの

小さなコンソールアプリを作ります。このアプリは:

1. MP4（またはサポートされている任意の形式）を個々の `Bitmap` フレームにデコードします。  
2. OCR の対象領域を字幕バンドに限定し、エンジンが画像全体に惑わされないようにします。  
3. 各フレームを Aspose の `VideoOcrProcessor` で処理します。  
4. 認識された字幕テキストをコンソールに出力します。

余計な説明は省き、実際にプロジェクトに組み込めるエンドツーエンドのサンプルを提供します。

## 前提条件

- **.NET 6.0** 以上（コードは .NET Framework 4.7+ でも動作します）。  
- **Aspose.OCR for .NET** – NuGet でインストール: `Install-Package Aspose.OCR`。  
- ビデオファイル（MP4 が最適）。  
- ビデオフレームをデコードする手段 – デモではプレースホルダー メソッドを使用していますが、FFmpeg、OpenCV、または `Bitmap` オブジェクトを返す任意のライブラリを組み込めます。  

> **プロのコツ:** Windows 環境では `System.Drawing.Common` パッケージが `Bitmap` に対して問題なく動作します。Linux/macOS ではネイティブの `libgdiplus` 依存関係が必要です。

## Step 1 – ビデオからフレームを抽出

最初のハードルは、動く映像を静止画像に変換することです。以下の `GetVideoFrames` メソッドは意図的に空欄にしていますので、お好みのデコーダで置き換えてください。以下は FFmpeg‑Core を使った簡易スケッチ例です（データ構造の形を示すだけです）:

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **なぜ重要か:** フレームを抽出することで OCR エンジンは静止画像を処理でき、ビデオストリームから直接読む場合に比べて精度が大幅に向上します。

## Step 2 – VideoOcrProcessor の設定

`Bitmap` オブジェクトのシーケンスが手に入ったら、Aspose.OCR に渡します。`VideoOcrProcessor` では **Region of Interest (ROI)** を定義でき、字幕が通常フレームの上部または下部にある場合に最適です。

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **ROI を限定する理由:** 画像の残りの部分を無視することでノイズが減り、処理時間が短縮され、背景グラフィックによる誤検出を防げます。

## Step 3 – フレームシーケンスに対して OCR を実行

プロセッサの準備ができたら、フレームの投入はワンライナーです。`Process` メソッドは `OcrResult` オブジェクトの列挙可能オブジェクトを返し、各フレームに対応する認識テキストが含まれます。

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **内部で何が起きているか:** Aspose.OCR は各ビットマップを正規化し、ニューラルネットワークベースの認識器で処理し、最後に句読点や改行を改善するポストプロセスを行います。

## Step 4 – 抽出したテキストを表示

最後に結果をイテレートして各字幕行を出力します。SRT ファイルへの書き出しやデータベース保存、翻訳サービスへの送信などにも応用できます。

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### 完全動作サンプル

すべてを組み合わせると、自己完結型のコンソールプログラムが完成します:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**期待される出力（サンプル）**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

特定のフレームで OCR がうまくいかない場合は空文字列が出力されます。これは ROI を調整するか、フレーム抽出レートを上げるサインです。

## Common Pitfalls & How to Fix Them

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **文字化け** | 解像度が低いフレームや過度の圧縮 | ビットレートを上げてフレームを抽出するか、OCR 前にビットマップを拡大 (`Bitmap.Clone(new Size(...), ...)`) |
| **テキストが返らない** | ROI が字幕バンドをカバーしていない | 矩形座標を確認（スクリーンショットツールで測定） |
| **パフォーマンスがボトルネック** | 30 fps すべてを処理している | 多くの字幕ストリームでは 1‑2 fps にダウンサンプリングすれば十分 |
| **FFmpeg が見つからない** | `ffmpeg.exe` が `PATH` に無い | `ProcessStartInfo.FileName` にフルパスを指定するか、FFmpeg をシステム全体にインストールする |

## Extending the Solution

- **SRT へエクスポート** – タイムスタンプと OCR テキストを結合し、SubRip ファイルを書き出す。  
- **多言語対応** – `ocrProcessor.Language = OcrLanguage.Spanish`（またはサポートされている任意の言語）を設定。  
- **リアルタイム処理** – ディスクから読む代わりにライブストリームからフレームを直接パイプする。  

これらのバリエーションもすべて、**ビデオからフレームを抽出する**、**ビデオからテキストを読む**、**mp4 からテキストを抽出する** というコアアイデアに基づいています。

## Conclusion

本稿では C# における **ビデオ字幕 OCR** ワークフローを完全に解説しました。ビデオからフレームを抽出し、字幕バンドに OCR を限定し、結果をイテレートすることで、MP4 などのビデオファイルから確実に **テキストを読む** ことができます。コードはコピー＆ペースト可能で、モジュラー設計により好きなフレームデコーダに差し替えられます。

次のステップは？ 結果を SRT ファイルにエクスポートしたり、ROI のサイズを変えて実験したり、字幕を翻訳 API に送って多言語キャプションを作成したりしてみてください。テキスト抽出の基本をマスターすれば、可能性は無限です。

Happy coding, and may your subtitles always be crystal‑clear!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Aspose.OCR を使用した言語選択付き画像テキスト抽出（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose.OCR .NET を使用した画像からのテキスト抽出](/ocr/english/net/image-and-drawing-recognition/)
- [Aspose.OCR for .NET による画像テキスト抽出の最適化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}