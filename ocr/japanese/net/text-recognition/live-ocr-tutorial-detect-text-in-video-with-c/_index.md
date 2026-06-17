---
category: general
date: 2026-03-13
description: ライブOCRチュートリアルでは、Aspose.OCRを使用してOCR言語を設定し、リアルタイムでテキストビデオストリームを検出する方法を示します。ステップバイステップのガイドに従ってください。
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: ja
og_description: Live OCR チュートリアルでは、C# で Aspose.OCR Live を使用して OCR 言語を設定し、テキストビデオストリームを検出する方法を解説しています。完全なコードが含まれています。
og_title: ライブOCRチュートリアル：動画内のリアルタイム文字検出
tags:
- OCR
- C#
- Aspose
- Video Processing
title: ライブOCRチュートリアル：C#で動画内のテキストを検出
url: /ja/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ライブ OCR チュートリアル: C# でビデオ内のテキストを検出する

実際にビデオフィード上で動作する **ライブ OCR チュートリアル** が欲しかったことはありませんか？ スマートカメラアプリやリアルタイム翻訳オーバーレイを作っていて、各フレームからテキストを取得する方法で詰まっているかもしれません。良いニュースは、ゼロから作り直す必要はないということです。このガイドでは、**OCR 言語を設定し**、カメラからフレームを取得し、**テキスト ビデオ ストリームをリアルタイムで検出**する完全な実行可能サンプルを順を追って解説します。

低遅延シナリオ向けに設計された Aspose.OCR の `LiveOcr` クラスを使用します。この記事の最後までに、最初に検出したテキストをコンソールに出力して終了するコンソール アプリが完成します。これをベースに、より高度なパイプラインを構築できます。

## 前提条件

- .NET 6.0 SDK（または最近の .NET バージョン）  
- Visual Studio 2022 または VS Code（お好みの IDE）  
- NuGet パッケージ `Aspose.OCR`（`dotnet add package Aspose.OCR` でインストール）  
- `Bitmap` フレームを供給できるウェブカメラまたは任意のビデオ ソース  

追加のネイティブ ライブラリは不要です。Aspose.OCR が必要なものはすべて同梱しています。

## 手順 1: Aspose.OCR をインストールし名前空間を追加

コードを書く前に、Aspose OCR ライブラリが参照されていることを確認してください。プロジェクト フォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

次に、`Program.cs` の先頭に使用する名前空間をインポートします。

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **プロのコツ:** Visual Studio を使用している場合、クラス名を入力すると IDE が自動的に `using` 文を提案してくれます。

## 手順 2: LiveOcr インスタンスを作成・設定

チュートリアルの中心は `LiveOcr` オブジェクトです。対象言語を指定し、必要に応じて前処理フィルタ（デスキューなど）を適用して精度を向上させます。

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

なぜ言語を設定するかというと、OCR エンジンは言語固有の辞書と文字モデルを使用するため、英語を指定すると誤検出が減り、認識速度も向上します。別の言語が必要な場合は、`Language.English` を `Language.Spanish`、`Language.French` などに置き換えるだけです。

## 手順 3: カメラからフレームを取得

実際のプロジェクトでは、プレースホルダー メソッド `CaptureFrameFromCamera()` を `AForge.Video`、`OpenCvSharp`、または Windows Media Capture API などを使った実装に置き換えます。このチュートリアルでは抽象的に保ちつつ、`AForge` を使った簡単な例を示します。

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **エッジケース:** カメラが利用できない場合、`CaptureFrameFromCamera` は `null` を返します。実運用コードでは必ずチェックしてください。

## 手順 4: テキストが見つかるまで各フレームを処理

固定回数（または無限）でフレームをループし、各ビットマップを `LiveOcr.ProcessFrame` に渡します。空でない文字列が取得できたら出力し、ループを抜けます。

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### なぜ一時停止するのか？

`Thread.Sleep(30)` はカメラ ドライバーに余裕を与え、CPU 使用率を下げます。高性能が求められるシナリオでは、より洗練されたフレームレート制御に置き換えることができます。

## 手順 5: コンソール アプリにまとめる

すべてを統合した、コピー＆ペーストで動作する完全版プログラムです。新しいコンソール プロジェクト（`dotnet new console`）内に `Program.cs` として保存し、`dotnet run` で実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### 期待される出力

カメラが読み取り可能な英語テキスト（例: 印刷されたラベル）を捉えると、次のように表示されます。

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

何も写っていない場合、ループは 100 回のイテレーション後に終了し “Live OCR session ended.” と表示されます。イテレーション回数を増やすか、`for` ループを `while (true)` に置き換えて無限監視にすることも可能です。

## よくある質問と落とし穴

| Question | Answer |
|----------|--------|
| **Can I process multiple languages simultaneously?** | Yes. Set `Language = Language.English | Language.Spanish;` (bitwise OR) to enable a multilingual dictionary. |
| **What if my frames are large and OCR feels slow?** | Downscale the bitmap before calling `ProcessFrame`. Example: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Do I need a license for Aspose.OCR?** | A temporary evaluation license works for up to 30 days. For production, purchase a license to remove the watermark. |
| **How do I handle rotated text?** | The `DeskewFilter` already corrects minor rotations. For extreme angles, add a `RotateFilter` to the pipeline. |
| **Is this approach thread‑safe?** | `LiveOcr` instances are not thread‑safe. Create one per thread or protect access with a lock. |

## チュートリアルの拡張

**ライブ OCR チュートリアル** の基礎ができたので、次のステップを検討してください。

1. **UI へのストリーミング** – `Windows Forms` や `WPF` を使ってライブ映像に OCR 結果をオーバーレイ表示。  
2. **バッチ処理** – フレームをキューに流し、バックグラウンド ワーカー プールで OCR を実行してスループットを向上。  
3. **言語検出** – 言語識別ライブラリを組み込んで、`LiveOcr.Language` を動的に切り替える。  
4. **結果の永続化** – 検出文字列をデータベースや CSV ファイルに書き出し、分析に活用。  

これらの拡張もすべて、`LiveOcr` の初期化、**OCR 言語の設定**、リアルタイムでの **テキスト ビデオ フレームの検出** というコア概念に基づいています。

---

### TL;DR

- NuGet で Aspose.OCR をインストール。  
- `LiveOcr` オブジェクトを作成し、**OCR 言語**（例では英語）を設定。  
- カメラから `Bitmap` フレームを取得。  
- フレームをループし `ProcessFrame` を呼び出し、テキストが出たら停止。  
- 上記プログラムはすぐに実行可能で、リアルタイム文字検出プロジェクトの堅実な土台となります。

ぜひ試してみて、前処理パイプラインを調整しながら、アプリがフレームごとに世界を読み取る様子を体感してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}