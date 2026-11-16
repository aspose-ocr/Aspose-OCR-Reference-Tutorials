---
category: general
date: 2026-03-29
description: 如何在 C# 中執行 OCR 並讀取 PNG 檔案的文字。學習提取俄文文字、從 PNG 讀取文字，以及使用 Aspose OCR 提取文字的方法。
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: zh-hant
og_description: 如何使用 Aspose OCR 在 C# 中執行 OCR。本指南示範如何從 PNG 讀取文字、擷取俄文內容，並實作完整的 C# OCR
  解決方案。
og_title: 如何在 C# 中執行 OCR – 完整的 PNG 文字提取
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中對 PNG 圖像執行 OCR – 逐步指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中對 PNG 圖像執行 OCR – 完整教學

是否曾需要在螢幕截圖或掃描文件上 **perform OCR**，但不確定在 C# 中從何開始？你並非唯一。開發者不斷問：「如何在不將 PNG 檔案傳送至外部服務的情況下 **read text from PNG**？」好消息是，使用 Aspose.OCR，你可以 **extract Russian text**、**read text from png**，並在幾行程式碼內取得乾淨的字串。

在本教學中，我們將逐步說明你需要的所有內容：設定函式庫、選擇正確的語言模型、執行辨識以及處理常見陷阱。完成後，你將能夠 **how to extract text** 從任何 PNG 圖像，無論是英文、俄文，或是 Aspose 支援的 70 多種語言。內容直截了當，提供可直接放入主控台應用程式的實作範例。

---

## 你將學到什麼

- 安裝並參考 Aspose.OCR NuGet 套件。
- 以預設的 auto‑download 模式初始化 OCR 引擎。
- 使用西里爾文語言模型設定引擎以 **extract russian text**。
- 在本機 PNG 檔案上執行 OCR 並顯示結果。
- 提供排除缺少語言檔案及提升準確度的技巧。

**先決條件**：.NET 6+（或 .NET Framework 4.7.2+）、Visual Studio 2022 或 VS Code，且首次執行需有網際網路連線（語言模型會自動下載）。

---

## 第一步 – 安裝 Aspose.OCR 套件

要開始使用，先將 Aspose.OCR 函式庫加入專案。於專案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或者，如果你偏好使用 Visual Studio 介面，於 **Dependencies → Manage NuGet Packages** 右鍵點擊，搜尋 **Aspose.OCR**，然後點擊 **Install**。

> **專業提示**：此套件僅有數 MB，且語言模型會按需下載，避免你的應用程式因不必要的檔案而變大。

---

## 第二步 – 初始化 OCR 引擎（主要關鍵字示範）

建立引擎相當簡單。建構子會自動啟用 *auto‑download mode*，這表示首次請求本機未有的語言時，Aspose 會為你下載。

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **為何重要**：使用預設的 auto‑download 模式可避免手動處理檔案。如果之後需要在其他語言中 **read text from png**，只要將 `Language.RussianCyrillic` 改為相應的列舉值即可。

---

## 第三步 – 準備你的 PNG 圖像

確保要處理的圖像在執行時可被存取。將 `sample_russian.png` 放在編譯後的 `.exe` 同一資料夾，或視需求使用絕對路徑。圖像應為清晰的掃描或螢幕截圖；若 PNG 模糊或高度壓縮，OCR 準確度會大幅下降。

**常見邊緣情況**：若 PNG 包含多種語言，可設定 `ocrEngine.Language = Language.Multilingual;` 讓引擎自動偵測每個文字區塊。

---

## 第四步 – 執行應用程式並驗證輸出

編譯並執行程式：

```bash
dotnet run
```

你應該會在主控台看到提取出的俄文文字，類似以下內容：

```
Привет, мир! Это пример текста на русском языке.
```

如果得到空字串，請再次確認：

1. 檔案路徑正確。
2. 圖像不是全白或全黑。
3. 語言模型已成功下載（於使用者資料夾下尋找 `Aspose.OCR` 資料夾）。

---

## 第五步 – 進階調整以提升準確度

雖然預設設定已能滿足大多數情況，但你可能想微調引擎：

| Setting | What it does | When to use it |
|---------|---------------|----------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | 校正輕微旋轉 | 掃描文件未完全對齊時 |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | 過濾背景雜訊 | 手機相機拍攝的低品質 PNG |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | 限制字符僅為數字 | 從發票中提取數字 |

在呼叫 `RecognizeImage` 之前加入任一設定：

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## 第六步 – 匯出結果至檔案（可選）

如果需要將 **how to extract text** 匯出至檔案以供後續處理，只需將結果寫入磁碟：

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

現在你已擁有可持久保存的副本，可供資料庫、搜尋索引或翻譯引擎使用。

---

## 常見問答

**Q: 這是否支援其他影像格式，例如 JPEG 或 BMP？**  
A: 當然。`RecognizeImage` 接受 .NET `System.Drawing` 函式庫支援的任何格式，包括 JPEG、BMP 與 TIFF。

**Q: 若在同一次執行中需要提取英文文字該怎麼辦？**  
A: 建立第二個 `OcrEngine` 實例並使用 `Language.English`，或在呼叫之間切換語言屬性。

**Q: 能否在 Web API 中執行 OCR 而不阻塞主執行緒？**  
A: 可以。將辨識呼叫包在 `Task.Run` 中，或使用非同步重載 `RecognizeImageAsync`（在較新版本的 Aspose 中提供）。

**Q: PNG 的尺寸有沒有上限？**  
A: 函式庫能處理大型圖像，但記憶體使用量會隨解析度提升。若遭遇 `OutOfMemoryException`，建議先縮小圖像尺寸。

---

## 完整可執行範例（直接複製貼上）

以下為完整程式碼，你可將其貼入新建的主控台專案（`dotnet new console`）中，安裝 NuGet 套件後立即執行。

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**預期的主控台輸出**（假設範例包含「Привет, мир!」這句話）：

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## 結論

我們已說明如何在 C# 中對 PNG 圖像 **how to perform OCR**，從安裝 Aspose.OCR、客製化前處理選項到匯出結果。現在你知道如何 **read text from png**、在不同語言中 **how to extract text**，以及如何以最少程式碼 **extract russian text**。

準備好接受下一個挑戰了嗎？試著將 OCR 輸出餵入語言偵測函式庫，或結合 Azure Cognitive Services 進行翻譯。只要將可靠的 OCR 引擎與 C# 強大的生態系統結合，無所不能。

如果你覺得這篇 **c# ocr tutorial** 有幫助，請給予星標、分享給團隊成員，或留下你的技巧評論。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}