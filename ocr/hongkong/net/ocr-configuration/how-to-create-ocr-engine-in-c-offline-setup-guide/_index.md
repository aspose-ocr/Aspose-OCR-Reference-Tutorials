---
category: general
date: 2026-03-04
description: 學習如何在 C# 中建立離線 OCR，無需網際網路。本分步指南亦會示範如何使用本機資源離線執行 OCR。
draft: false
keywords:
- how to create OCR
- how to run OCR
- offline OCR C#
- local OCR resources
- OcrEngine setup
language: zh-hant
og_description: 如何在 C# 中建立不需要網路呼叫的 OCR。請跟隨本指南學習如何使用 LocalResourceProvider 在本機執行 OCR。
og_title: 如何在 C# 中建立 OCR 引擎 – 離線設定
tags:
- OCR
- C#
- Offline Processing
title: 如何在 C# 中建立 OCR 引擎 – 離線設定指南
url: /zh-hant/net/ocr-configuration/how-to-create-ocr-engine-in-c-offline-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立 OCR 引擎 – 離線設定指南

有沒有想過 **how to create OCR** 從不連接網路？也許你正在打造安全的桌面應用程式，或是單純不喜歡不穩定的網路呼叫。無論如何，你都會想要一個完全在客戶端機器上運行的 OCR 引擎。  

好消息是？其實相當簡單。在本教學中，我們將逐步說明 **how to create OCR**，接著示範如何使用 `LocalResourceProvider` 於離線模式 **how to run OCR**。完成後，你將擁有一段可自行放入任何 .NET 專案的獨立 C# 程式碼——不需要外部服務。

## 你將學到什麼

- 離線 OCR 設定的最小前置條件。  
- 如何實例化 `OcrEngine` 並指向本機資源資料夾。  
- 使用本機提供者可消除網路延遲並提升隱私。  
- 常見陷阱（檔案遺失、路徑錯誤）以及如何避免。  

所有需要的程式碼皆已包含，另有快速驗證步驟，讓你在複製貼上後即可看到引擎運作。

## 前置條件

在深入之前，請確保你已具備以下條件：

1. **.NET 6.0 或更新版本** – 我們將使用的 OCR 函式庫目標為 .NET Standard 2.0，任何較新的執行環境皆可運作。  
2. **包含 OCR 資源的資料夾** – 語言套件、訓練資料檔案以及任何輔助二進位檔。如果尚未取得，請從供應商的離線套件下載相應的套件，並解壓縮至 `C:\MyApp\OcrResources`。  
3. **Visual Studio 2022**（或任何你偏好的 IDE）。  

就這樣——執行時不會有任何連線至網路的 NuGet 套件。

![離線 OCR 流程圖 – 如何在不連網的情況下建立 OCR 引擎](offline-ocr-diagram.png)

*圖片說明：離線建立 OCR 引擎圖示*

---

## 步驟 1：加入 OCR 函式庫參考

首先，在專案中參考 OCR SDK 組件。如果你有供應商提供的 `.dll`，在 **References → Add Reference** 上點右鍵，然後瀏覽至 `OcrSdk.dll`。或者，若 SDK 以支援離線模式的 NuGet 套件形式提供，執行以下指令：

```bash
dotnet add package OcrSdk --version 3.2.1
```

> **專業提示：** 鎖定版本號。之後升級可能會帶來破壞性變更，影響離線資源路徑。

---

## 步驟 2：建立 OCR 引擎實例  

現在我們將透過建構 `OcrEngine` 物件實際 **how to create OCR**。此物件是所有辨識任務的入口點。

```csharp
using OcrSdk;               // Namespace provided by the OCR library
using OcrSdk.Resources;    // Contains LocalResourceProvider

// ...

// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

為什麼需要專屬的引擎？`OcrEngine` 會保存設定、快取語言模型，並管理執行緒池。只建立一次並在多次掃描間重複使用，遠比每張影像都新建物件來得有效率。

---

## 步驟 3：將引擎指向本機資源資料夾  

以下關鍵步驟讓你 **how to run OCR** 時完全不需要連網。我們指派一個 `LocalResourceProvider`，從磁碟上的目錄讀取語言資料。

```csharp
// Step 3: Configure the engine to use offline resources
string resourcePath = @"C:\MyApp\OcrResources";
ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);
```

**底層發生了什麼？** `LocalResourceProvider` 實作與預設雲端提供者相同的介面，但會從 `resourcePath` 讀取 `.dat` 檔案。此技巧確保所有後續的 OCR 呼叫皆保持本機。

> **注意：** 若路徑錯誤或資料夾缺少必要檔案（`eng.traineddata`、`ocr_config.xml` 等），引擎會拋出 `ResourceNotFoundException`。指派前務必先驗證資料夾。

---

## 步驟 4：驗證引擎已就緒  

快速的健全性檢查可避免日後除錯。呼叫 `IsReady`（或等價屬性）並輸出結果。

```csharp
// Step 4: Verify the engine can locate its resources
if (ocrEngine.IsReady)
{
    Console.WriteLine("✅ OCR engine is ready – offline mode confirmed.");
}
else
{
    Console.WriteLine("❌ OCR engine failed to load resources. Check the path and files.");
    return;
}
```

你應該會在主控台看到綠色勾勾。若出現紅色叉叉，請再次確認 `resourcePath` 指向包含語言套件的資料夾。

---

## 步驟 5：在範例影像上執行 OCR  

最後，讓我們實際 **how to run OCR** 在圖片上。將名為 `sample.png` 的影像放在相同的資源資料夾（或任何可存取的位置），然後送入引擎。

```csharp
// Step 5: Perform OCR on a local image
string imagePath = Path.Combine(resourcePath, "sample.png");

// Load the image (the SDK may provide its own Image class)
var ocrImage = OcrImage.FromFile(imagePath);

// Run recognition – this call is completely offline
OcrResult result = ocrEngine.Recognize(ocrImage);

// Output the recognized text
Console.WriteLine("🖋️ Recognized Text:");
Console.WriteLine(result.Text);
```

**預期輸出**（假設 `sample.png` 包含文字 “Hello OCR!”）：

```
🖋️ Recognized Text:
Hello OCR!
```

若結果為空，請確認影像清晰且英文語言模型 (`eng`) 已存在於 `OcrResources` 中。

---

## 邊緣情況與常見陷阱  

| Situation | What Happens | How to Fix It |
|-----------|--------------|---------------|
| **Missing language file** | `ResourceNotFoundException` at step 3 | 確認資料夾中存在 `eng.traineddata`（或你的目標語言檔案）。 |
| **Corrupt image** | `OcrException` with “Unsupported format” | 在送入引擎前將影像轉為 PNG 或 BMP。 |
| **Multiple threads** | Race conditions if you create many engines | 重複使用單一 `OcrEngine` 實例；它對同時的 `Recognize` 呼叫是執行緒安全的。 |
| **Path contains spaces** | Engine fails to locate resources | 使用逐字字串 (`@"C:\Path With Spaces\OcrResources"`) 或跳脫反斜線。 |

---

## 完整範例程式  

以下是一個可直接執行的主控台程式，將所有步驟整合。將程式碼複製到新的 `.csproj` 專案中，然後按 **F5**。

```csharp
// File: Program.cs
using System;
using System.IO;
using OcrSdk;
using OcrSdk.Resources;

namespace OfflineOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Point to local resources (offline mode)
            string resourcePath = @"C:\MyApp\OcrResources";
            ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);

            // 3️⃣ Verify the engine can load resources
            if (!ocrEngine.IsReady)
            {
                Console.WriteLine("❌ Engine failed to initialize. Check your resource folder.");
                return;
            }
            Console.WriteLine("✅ Engine initialized successfully.");

            // 4️⃣ Load a test image
            string imagePath = Path.Combine(resourcePath, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            var ocrImage = OcrImage.FromFile(imagePath);

            // 5️⃣ Run OCR – entirely offline
            OcrResult result = ocrEngine.Recognize(ocrImage);

            // 6️⃣ Show the result
            Console.WriteLine("\n🖋️ Recognized Text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

**執行程式** 後應會印出確認訊息與擷取的文字，證明你已掌握 **how to create OCR** 與 **how to run OCR**，且全程不離開本機。

---

## 結論  

我們已說明在 C# 專案中 **how to create OCR** 所需的全部知識，並示範 **how to run OCR** 完全離線。透過設定 `LocalResourceProvider`，即可消除網路延遲、保護敏感資料，並完整掌控 OCR 的生命週期。  

準備好接受下一個挑戰了嗎？試著將英文模型換成其他語言，或是實驗不同的影像前處理步驟（灰階轉換、去斜）以提升準確度。模式相同——只要把引擎指向不同的資源資料夾即可。  

如果遇到任何問題，請重新檢視上方的邊緣情況表格或留下評論；祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}