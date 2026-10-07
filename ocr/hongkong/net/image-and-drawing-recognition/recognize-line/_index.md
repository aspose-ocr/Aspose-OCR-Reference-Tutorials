---
date: 2026-02-22
description: 學習如何使用 Aspose.OCR for .NET 從圖像中提取文字、將 PNG 轉換為文字，並在 C# 應用程式中提升 OCR 準確度。
linktitle: Extract Text from Image – Recognize Line with Aspose.OCR
second_title: Aspose.OCR .NET API
title: 從圖像提取文字 – 使用 Aspose.OCR 識別行
url: /zh-hant/net/image-and-drawing-recognition/recognize-line/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像中擷取文字 – 使用 Aspose.OCR 辨識行

## 介紹

光學字元辨識 (OCR) 已成為將文字圖片轉換為可搜尋、可編輯內容的首選解決方案。若您想要快速且可靠地 **從影像中擷取文字**，Aspose.OCR for .NET 提供功能強大、開發者友善的 API，支援完整的 .NET Framework 與 **ASP OCR .NET Core** 專案。本教學將逐步說明如何辨識影像中的行、將這些行轉換為純文字，並顯示結果，全部使用簡潔易懂的 C# 程式碼。

## 快速回答
- **Aspose.OCR 的功能是什麼？** 讀取影像格式中的印刷或手寫文字，並回傳純字串。  
- **支援哪些影像格式？** PNG、JPEG、BMP、GIF、TIFF 等多種格式。  
- **測試需要授權嗎？** 開發階段可使用免費試用版；正式上線需購買授權。  
- **可以在 .NET Core 上執行嗎？** 可以 – 此函式庫支援 .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6。  
- **簡單的行辨識需要多久？** 標準 PNG 通常在一秒內完成。

## 什麼是「從影像中擷取文字」？

從影像中擷取文字即是利用 OCR 技術分析視覺像素、辨識字元，並將其輸出為機器可讀的文字。這可應用於數位化掃描文件、從收據自動輸入資料，或建立可搜尋的檔案庫等情境。

## 為什麼選擇 Aspose.OCR for .NET？

- **高準確度**，支援多種語言與字型。  
- **無外部相依** – 純受管理程式碼，易於整合。  
- **完整的格式支援** – 可處理 PNG、JPEG、BMP 等多種格式。  
- **簡易 API** – 幾行程式碼即可完成影像到文字的轉換。  

### 這如何協助您 **將 PNG 轉換為文字**？

因為 Aspose.OCR 能直接讀取 PNG 檔案，您只需將掃描的 PNG 影像傳入 `RecognizeLine` 方法，即可取得乾淨的字串，無需任何中間轉換步驟。

## 前置條件

在開始之前，請確保您已具備：

- **開發環境** – Visual Studio 2022（或任何您偏好的 .NET IDE）。  
- **Aspose.OCR for .NET** – 從 [download link](https://releases.aspose.com/ocr/net/) 下載。  
- **文件目錄** – 您機器上存放範例影像 (`sample_line.png`) 的資料夾。請在程式碼中將 “Your Document Directory” 替換為實際路徑。

## 匯入命名空間

在 .NET 中，命名空間讓您取得所需的類別。於 C# 檔案頂部加入以下 using 陳述式：

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## 使用 Aspose.OCR 從影像中擷取文字的方法

以下為逐步實作。每個程式碼區塊皆保持原樣，確保邏輯不變。

### 步驟 1：初始化 Aspose.OCR

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
// ExEnd:1
```

> **小技巧：** 使用絕對路徑或 `Path.Combine` 可避免不同作業系統間的路徑分隔符問題。

### 步驟 2：辨識影像行

```csharp
// ExStart:3
// Recognize image
string result = api.RecognizeLine(dataDir + "sample_line.png");
// ExEnd:3
```

`RecognizeLine` 方法專注於單一行文字，當您已知影像版面配置時非常適用。它也是在文件僅含單行重要資料時 **讀取掃描影像文字** 的好方法。

### 步驟 3：顯示辨識結果

```csharp
// ExStart:4
// Display the recognized text
Console.WriteLine(result);
// ExEnd:4
```

執行程式後，會在主控台印出擷取的行文字，證明 **從影像中擷取文字** 的操作已成功。

### 步驟 4：完成訊息

```csharp
Console.WriteLine("RecognizeLine executed successfully");
```

看到此訊息表示 OCR 流程已順利完成，未發生錯誤。

## 如何提升 Aspose.OCR 的辨識準確度？

- **使用高解析度影像**（300 dpi 或以上）。  
- **進行影像前處理**，如二值化或除噪，可使用 `api.PreprocessImage`。  
- **選擇正確語言**，例如 `api.Language = OcrLanguage.English;`（或相應的語言列舉）。  
- **裁切邊框**，去除不相關的背景。

以上調整可協助您 **提升 OCR 準確度**，特別是面對低品質掃描時。

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| `FileNotFoundException` | `dataDir` 路徑不正確 | 核對資料夾路徑，確保 `sample_line.png` 存在。 |
| 準確度低 | 影像解析度不足 | 使用更高解析度的來源或進行前處理（如二值化）。 |
| 不支援的格式 | 影像不在支援清單內 | 在呼叫 `RecognizeLine` 前將影像轉為 PNG 或 JPEG。 |

## 常見問答

### Q1：Aspose.OCR 是否支援所有影像格式？

A1：Aspose.OCR 支援多種影像格式，包括 PNG、JPEG、GIF、BMP 等。詳情請參考 [documentation](https://reference.aspose.com/ocr/net/)。

### Q2：在試用期間可以將 Aspose.OCR 用於商業專案嗎？

A2：可以，您可在試用期間於商業專案中探索 Aspose.OCR 的功能。若需長期使用，請考慮 [購買授權](https://purchase.aspose.com/buy)。

### Q3：如何取得協助或參與 Aspose.OCR 社群？

A3：可前往 [support forum](https://forum.aspose.com/c/ocr/16) 與活躍的 Aspose.OCR 社群互動，取得協助與合作機會。

### Q4：Aspose.OCR 是否提供臨時授權？

A4：提供，您可取得臨時授權以評估功能。詳情請見 [here](https://purchase.aspose.com/temporary-license/)。

### Q5：Aspose.OCR for .NET 的系統需求是什麼？

A5：請參考 [documentation](https://reference.aspose.com/ocr/net/) 取得完整的系統需求說明。

## 結論

透過本教學，您已學會如何使用 Aspose.OCR for .NET **從影像中擷取文字**，特別是辨識單行文字。此功能可協助自動化資料擷取、建立可搜尋的檔案庫，並將 OCR 整合至任何 .NET 應用程式，無論是完整框架或 **ASP OCR .NET Core**。

---

**最後更新：** 2026-02-22  
**測試版本：** Aspose.OCR 24.12 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}