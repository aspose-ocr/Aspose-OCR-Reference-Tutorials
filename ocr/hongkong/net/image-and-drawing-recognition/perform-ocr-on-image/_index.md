---
date: 2026-02-22
description: 學習如何使用 Aspose.OCR for .NET 進行圖像 OCR 並提取圖像文字。本分步指南將教您快速將圖像轉換為文字。
linktitle: Perform OCR on Image in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: 如何對圖像進行 OCR – 在 OCR 圖像辨識中執行圖像 OCR
url: /zh-hant/net/image-and-drawing-recognition/perform-ocr-on-image/
weight: 14
---

 content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何對圖像進行 OCR – 在 OCR 圖像識別中執行圖像 OCR

## 介紹

在現代應用程式中，**how to OCR image** 是開發人員常見的問題，因為他們需要將掃描文件、螢幕截圖或照片轉換為可搜尋、可編輯的文字。Aspose.OCR for .NET 為您提供功能強大、易於使用的 API，讓您只需幾行程式碼即可 **extract image text**、**convert image to text**，以及 **recognize image text**。在本教學中，我們將逐步說明整個流程——從設定函式庫到顯示辨識文字——讓您在幾分鐘內將 OCR 功能整合到 C# 專案中。

## 快速回答
- **應該使用哪個函式庫？** Aspose.OCR for .NET
- **我可以處理 PNG、JPEG 與 TIFF 嗎？** 可以，支援所有常見的圖像格式
- **生產環境是否需要授權？** 需要，商業授權才能在正式環境使用
- **相容的 .NET 版本有哪些？** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6
- **基本 OCR 呼叫需要多長時間？** 通常在標準大小圖像下不到一秒

## 什麼是 OCR 圖像文字提取？

OCR（Optical Character Recognition）圖像文字提取是分析位圖圖像、識別字符，並將其輸出為可編輯文字的過程。此技術支援從可搜尋的 PDF 到自動化收據資料輸入等各種應用。

## 為何選擇 Aspose.OCR 作為您的 C# OCR 函式庫？

- **高準確度** – 內建語言模型即使在低品質掃描上也能提供可靠結果。  
- **廣泛格式支援** – 支援 PNG、JPEG、BMP、TIFF 等多種格式，讓您無論來源如何，都能輕鬆 **convert image to text**。  
- **無外部相依性** – 純 .NET 函式庫；無需安裝本機 OCR 引擎。  
- **可擴充** – 您可以微調辨識設定，或與其他 Aspose 產品整合，實現端到端文件工作流程。

## 先決條件

在深入程式碼之前，請確保您已具備以下項目：

1. **Aspose.OCR for .NET Library** – 從 [download link](https://releases.aspose.com/ocr/net/) 下載並安裝。  
2. **開發環境** – 任意相容 .NET 的 IDE（Visual Studio、Rider、VS Code 等）。  
3. **範例圖像** – 本教學將使用放置於您自行選擇資料夾中的 `sample.png`。

## 匯入命名空間

首先，加入必要的命名空間，讓編譯器知道 OCR 類別的所在位置：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 如何使用 Aspose.OCR for .NET 進行圖像 OCR

以下是完整的端對端工作流程，分為清晰的編號步驟。每一步都包含簡短說明以及您需要直接複製的程式碼。

### 步驟 1：指定文件目錄

```csharp
string dataDir = "Your Document Directory";
```

將 `"Your Document Directory"` 替換為包含 `sample.png` 的絕對或相對路徑。此設定告訴 API 圖像所在的位置。

### 步驟 2：初始化 Aspose.OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

建立 `AsposeOcr` 實例即可取得所有 OCR 方法，例如 `RecognizeImage`。

### 步驟 3：辨識圖像

```csharp
string result = api.RecognizeImage(dataDir + "sample.png");
```

`RecognizeImage` 方法會讀取圖像檔案，並以字串形式回傳提取出的文字。這就是執行 **recognize image text** 的核心步驟。

### 步驟 4：顯示辨識文字

```csharp
Console.WriteLine(result);
```

您可以將結果印到主控台、寫入檔案，或傳遞給其他元件以進一步處理。

### 步驟 5：完成流程

```csharp
Console.WriteLine("PerformOCROnImage executed successfully");
```

簡單的確認訊息可協助您驗證 OCR 呼叫已順利完成且未拋出例外。

## 將圖像轉換為文字 .NET – 其他提示

- **使用 `Path.Combine`** 在跨平台時安全地組合檔案路徑。  
- **設定 Language** 若處理非英文文字：`api.Language = "eng";`（或相應的 ISO 代碼）。  
- **調整圖像品質** 透過前置處理（例如縮放、二值化）提升低解析度掃描的辨識準確度。

## 常見問題與疑難排解

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 回傳空字串 | 圖像路徑不正確或找不到檔案 | 核對 `dataDir` 與檔名；使用 `Path.Combine` 以確保路徑安全 |
| 文字亂碼 | 圖像解析度過低或語言不支援 | 改用較高解析度的圖像；透過 `api.Language = "eng"` 設定語言選項 |
| 例外 `System.IO.FileNotFoundException` | 缺少 `sample.png` | 確認檔案已放置於指定資料夾中 |

## 常見問答

**Q: Aspose.OCR 能處理多種圖像格式嗎？**  
A: 可以，支援廣泛的格式，您可以從 PNG、JPEG、BMP、TIFF 等圖像 **extract image text**。

**Q: 是否提供測試用的臨時授權？**  
A: 當然可以。您可於 Aspose 入口網站申請 30 天評估授權。

**Q: 在哪裡可以找到 Aspose.OCR for .NET 的完整文件？**  
A: 官方說明位於 [Aspose.OCR documentation](https://reference.aspose.com/ocr/net/)。

**Q: 如何取得支援或加入社群尋求協助？**  
A: 前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 提問或分享使用經驗。

**Q: 購買前能免費試用 Aspose.OCR for .NET 嗎？**  
A: 可以，完整功能的 **free trial** 可於 [free trial](https://releases.aspose.com/) 頁面取得。

## 結論

依照上述步驟，您現在已掌握 **how to OCR image** 的完整流程，無論是建置文件管理系統、收據處理應用，或任何需要 **convert image to text** 的解決方案，這套函式庫都能提供簡單、高效的方式，將視覺資料轉換為可搜尋的內容。

---

**最後更新：** 2026-02-22  
**測試環境：** Aspose.OCR for .NET 24.12（撰寫時最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}