---
category: general
date: 2026-03-13
description: 即時 OCR 教學示範如何設定 OCR 語言並使用 Aspose.OCR 即時偵測影片串流中的文字。請依循逐步指南。
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: zh-hant
og_description: 即時 OCR 教學說明如何在 C# 中使用 Aspose.OCR Live 設定 OCR 語言並偵測文字影片串流，並附上完整程式碼。
og_title: Live OCR 教學：影片即時文字偵測
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 即時 OCR 教學：使用 C# 偵測影片中的文字
url: /zh-hant/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Live OCR 教學：使用 C# 在影片中偵測文字

有沒有需要一個實際可在影片串流上運作的 **live OCR 教學**？也許你正在開發智慧相機應用程式或即時翻譯疊加層，卻卡在「如何從每一幀抓取文字？」好消息是，你不需要重新發明輪子。本指南將逐步示範一個完整、可執行的範例，**設定 OCR 語言**、從相機擷取影格，並即時 **偵測影片文字**。

我們將使用 Aspose.OCR 的 `LiveOcr` 類別，它專為低延遲情境設計。閱讀完本篇文章後，你將擁有一個會印出第一段偵測到文字後即結束的主控台應用程式——非常適合作為更複雜流程的起點。

## 前置條件

- .NET 6.0 SDK（或任何較新的 .NET 版本）  
- Visual Studio 2022 或 VS Code（你喜愛的 IDE）  
- NuGet 套件 `Aspose.OCR`（透過 `dotnet add package Aspose.OCR` 安裝）  
- 網路攝影機或任何能提供 `Bitmap` 影格的影片來源  

不需要額外的原生函式庫；Aspose.OCR 已內建所有必要的元件。

## 步驟 1：安裝 Aspose.OCR 並加入命名空間

在撰寫任何程式碼之前，先確保已參考 Aspose OCR 函式庫。於專案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

接著，在 `Program.cs` 的最上方匯入我們將使用的命名空間：

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **小技巧：** 若你使用 Visual Studio，IDE 會在你輸入類別名稱後自動建議 `using` 陳述式。

## 步驟 2：建立並設定 LiveOcr 實例

本教學的核心是 `LiveOcr` 物件。我們需要告訴它要偵測哪種語言，並可選擇套用前處理濾鏡（例如去斜）以提升準確度。

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

為什麼要設定語言？OCR 引擎會使用特定語言的字典與字元模型；指定 English 可減少誤判並加快辨識速度。若需其他語言，只要將 `Language.English` 改成 `Language.Spanish`、`Language.French` 等即可。

## 步驟 3：從相機擷取影格

在實際專案中，你會將佔位方法 `CaptureFrameFromCamera()` 換成真實的擷取程式碼——可能使用 `AForge.Video`、`OpenCvSharp` 或 Windows Media Capture API。為了教學方便，我們保留此方法為抽象，但會示範一個使用 `AForge` 的簡易範例。

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

> **邊緣情況：** 若相機無法使用，`CaptureFrameFromCamera` 會回傳 `null`。在正式程式碼中務必做好防護。

## 步驟 4：處理每一幀直到找到文字

現在我們會以固定次數（或無限）迴圈每一幀，將 `Bitmap` 送入 `LiveOcr.ProcessFrame`。只要取得非空字串，就印出並跳出迴圈。

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

### 為什麼要暫停？

`Thread.Sleep(30)` 讓相機驅動程式稍作休息，降低 CPU 使用率。在高效能情境下，你可以改用更精細的影格率控制機制。

## 步驟 5：將所有程式包裝成主控台應用程式

把以上所有步驟整合起來，以下是完整、可直接複製貼上的程式。將它存為 `Program.cs`，放入新建立的主控台專案（`dotnet new console`），然後執行 `dotnet run`。

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

### 預期輸出

當相機偵測到可辨識的英文文字（例如印刷標籤）時，會看到類似以下的輸出：

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

若畫面中沒有文字，迴圈會在 100 次後結束並印出 “Live OCR session ended.”。你可以調整迭代次數，或將 `for` 迴圈改為 `while (true)` 以進行無限監控。

## 常見問題與注意事項

| 問題 | 回答 |
|----------|--------|
| **可以同時處理多種語言嗎？** | 可以。將 `Language = Language.English | Language.Spanish;`（位元 OR）設定，即可啟用多語言字典。 |
| **如果影格太大導致 OCR 速度變慢怎麼辦？** | 在呼叫 `ProcessFrame` 前先縮小 bitmap。例如：`Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **使用 Aspose.OCR 是否需要授權？** | 臨時評估授權可使用至多 30 天。正式環境請購買授權以移除浮水印。 |
| **如何處理旋轉的文字？** | `DeskewFilter` 已能校正輕微旋轉。若角度過大，可在流程中加入 `RotateFilter`。 |
| **此方法是否支援多執行緒？** | `LiveOcr` 實例不是執行緒安全的。每個執行緒建立一個實例，或使用 lock 保護存取。 |

## 延伸教學

既然已具備 **live OCR 教學** 的基礎，接下來可以考慮以下延伸步驟：

1. **串流至 UI** – 使用 `Windows Forms` 或 `WPF` 顯示即時影片，並在上面疊加 OCR 結果。  
2. **批次處理** – 將影格排入佇列，並在背景工作池中執行 OCR，以提升吞吐量。  
3. **語言偵測** – 結合語言辨識函式庫，即時切換 `LiveOcr.Language`。  
4. **結果持久化** – 將偵測到的字串寫入資料庫或 CSV 檔，以供分析。  

上述每項延伸仍仰賴我們先前討論的核心概念：初始化 `LiveOcr`、**設定 OCR 語言**，以及即時 **偵測影片文字** 影格。

---

### TL;DR

- 透過 NuGet 安裝 Aspose.OCR。  
- 建立 `LiveOcr` 物件，**設定 OCR 語言**（範例中為 English）。  
- 從相機擷取 `Bitmap` 影格。  
- 迴圈處理每一影格，呼叫 `ProcessFrame`，文字出現即停止。  
- 上述完整程式已可直接執行，是任何即時文字偵測專案的堅實基礎。

試著跑一次，調整前處理管線，讓你的應用程式逐幀讀取世界。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}