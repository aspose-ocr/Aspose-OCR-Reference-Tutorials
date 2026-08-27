---
description: 學習如何使用 Aspose.OCR for .NET 保存 OCR 結果——將圖像轉換為 PDF、從 PNG 提取文字，並將識別的文字儲存為
  DOCX、TXT、PDF 或 XLSX。
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: 如何將 OCR 結果儲存為文件
url: /zh-hant/net/ocr-settings/save-result-as-document/
weight: 10
---

Now produce final content with same shortcodes.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將 OCR 結果儲存為文件

## 簡介

在本教學中，您將學會 **如何儲存 OCR** 輸出，使用 Aspose.OCR for .NET。我們將示範如何辨識圖像中的文字，然後將文字轉換為常見的文件格式，如 DOCX、 TXT、 PDF 與 XLSX。完成後，您即可自動從圖片提取資料，並將其存成可搜尋、可編輯的檔案——非常適合歸檔、報告或後續處理。

## 快速答案
- **「如何儲存 OCR」是什麼意思？** 它指的是將從圖像中辨識出的文字持久化為 DOCX、PDF 等檔案格式。  
- **可以匯出哪些格式？** 支援 DOCX、TXT、PDF 與 XLSX。  
- **需要授權嗎？** 免費試用可用於評估；正式環境需購買商業授權。  
- **可以直接將圖像轉成 PDF 嗎？** 可以——將 OCR 結果儲存為 PDF，即可得到可搜尋的 PDF 文件。  
- **支援 PNG 嗎？** 當然可以；您可以 **從 PNG 圖像中提取文字**，使用相同的 API。

## 什麼是 OCR 以及為什麼要將結果儲存為文件？

光學字符辨識（OCR）將圖像中的印刷或手寫文字轉換為機器可讀的字串。將這些字串儲存為文件可讓您：

* 建立可搜尋的 PDF 以符合合規需求。  
* 填入試算表（XLSX）以進行資料分析。  
* 產生可編輯的報告（DOCX）。  
* 歸檔純文字日誌（TXT）以便快速搜尋。

## 先決條件

在開始之前，請確保您已：

- 安裝 Aspose.OCR for .NET。您可以在 **[此處](https://releases.aspose.com/ocr/net/)** 下載。  
- 在電腦上建立一個資料夾，用來放置來源圖像與輸出文件。請在程式碼中將 `dataDir` 變數指向該資料夾。

## 匯入命名空間

我們需要幾個 .NET 命名空間來存取檔案 I/O 與 Aspose OCR 類別。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 步驟 1：初始化 Aspose.OCR

設定工作目錄路徑，並建立 OCR 引擎的實例。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 步驟 2：辨識圖像

將圖像檔案（例如 PNG）傳入辨識器。此步驟會 **辨識文字圖像**，並產生 `RecognitionResult`。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 步驟 3：以不同格式儲存結果

現在將辨識出的文字匯出。依需求選擇適合的格式——無論是 **將圖像轉成 PDF**、**從 PNG 提取文字**，或是產生試算表。

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 步驟 4：顯示成功訊息

簡單的主控台訊息會確認程序已順利完成且無錯誤。

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## 常見陷阱與技巧

- **檔案路徑：** 請使用絕對路徑，或確保 `dataDir` 以路徑分隔符（`\` 或 `/`）結尾。  
- **圖像品質：** 高解析度圖像可提升辨識準確度；建議先行前處理（去斜、去噪）以獲得更佳結果。  
- **授權模式：** 評估模式下輸出可能會有浮水印；請套用有效授權以移除浮水印。

## 常見問題

**Q1. Aspose.OCR 是否相容於不同的圖像格式？**  
A1: 是的，Aspose.OCR 支援多種圖像格式，讓您的 OCR 任務更具彈性。

**Q2: 我可以自訂辨識設定以提升準確度嗎？**  
A2: 當然！Aspose.OCR 提供 `RecognitionSettings`，可依您的需求微調 OCR 流程。

**Q3: 有免費試用版嗎？**  
A3: 有，您可在 **[此處](https://releases.aspose.com/)** 取得免費試用。

**Q4: 如何取得 Aspose.OCR 的臨時授權？**  
A4: 臨時授權可於 **[此處](https://purchase.aspose.com/temporary-license/)** 申請。

**Q5: 我可以在哪裡尋求協助或加入社群？**  
A5: 歡迎加入 Aspose.OCR 社群 **[Aspose Forum](https://forum.aspose.com/c/ocr/16)**，獲取支援與討論。

---

**最後更新：** 2026-02-12  
**測試環境：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}