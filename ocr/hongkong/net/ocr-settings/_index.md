---
date: 2026-05-19
description: 了解如何使用 Aspose.OCR for .NET 從圖像提取文字、將圖像轉換為文件，並提升應用程式中的 OCR 準確度。
keywords:
- extract text from images
- convert image to document
- improve ocr accuracy
- ocr image to txt
- save ocr as pdf
linktitle: OCR 設定
second_title: Aspose.OCR .NET API
title: 從圖像提取文字 – 使用 Aspose.OCR 的 OCR 設定
url: /zh-hant/net/ocr-settings/
weight: 26
---

{{< blocks/products/pf/main-wrap-class >}}  
{{< blocks/products/pf/main-container >}}  
{{< blocks/products/pf/tutorial-page-section >}}  

# 從圖像提取文字 – Aspose.OCR OCR 設定  

## 簡介  

在當今快速發展的數位世界中，**extract text from images** 是從發票處理到可搜尋檔案庫等各種應用的關鍵能力。Aspose.OCR for .NET 為您提供功能強大、即時可用的引擎，能將任何圖片轉換為可編輯的文字、PDF、DOCX 或純文字檔。本指南將逐一說明最常用的 OCR 設定，解釋 *為何* 每項設定重要，並示範如何在實務情境中套用，讓您提升應用程式的準確度、速度與彈性。  

## 快速解答  
- **What does “extract text from images” mean?** 它是辨識圖片檔案內的字元並將其輸出為可編輯文字的過程。  
- **Which library handles this best in .NET?** Aspose.OCR for .NET 提供業界領先的準確度與多語言支援。  
- **Can I convert the OCR result to PDF or DOCX?** 是的 – “Save Result as Document” 教學示範如何一次呼叫即匯出為 PDF、DOCX 或 TXT。  
- **How do I speed up OCR for large batches?** 增加執行緒數量（請參閱 “Set Threads Count”）以平行辨識，提高速度。  
- **Is fine‑tuning possible?** 當然可以 – 您可以設定閾值、白名單允許的字元、黑名單忽略的字元，並載入語言套件以取得最佳結果。  

## 什麼是 “extract text from images”？  

它透過分析像素模式、套用二值化與降噪等前處理，並使用訓練好的語言模型辨識每個字形，將字元的視覺表現轉換為可編輯的 Unicode 文字。產生的字串可在您的應用程式中儲存、搜尋、索引或進一步處理。  

## 為什麼使用 Aspose.OCR for .NET？  

載入 Aspose.OCR 函式庫，即可立即取得 **50+ 輸入與輸出格式** 支援——包括 JPEG、PNG、BMP、TIFF、PDF 轉圖像等，且能處理高達 **500 MB** 的檔案而不會耗盡記憶體。此引擎在乾淨掃描件上可達 **最高 98 % 的準確率**，並提供內建前處理，將低對比或噪點圖像提升至接近完美的結果。  

## 在 OCR 圖像辨識中將結果儲存為文件  

`SaveResultAsDocument` saves the OCR output directly to a document file.  

當您呼叫 `ocrEngine.SaveResultAsDocument(outputPath, SaveFormat.Pdf)` 時，Aspose.OCR 會將文字寫入具可選取文字層的 PDF，從而實現搜尋與複製貼上功能，且無需額外的後處理。  

## 在 OCR 圖像辨識中設定執行緒數量  

調整執行緒池可控制同時處理的圖像頁數。  

**Definition:** `ThreadsCount` 屬性決定引擎將產生的平行 OCR 工作執行緒的最大數量。  

將此值從預設的 **1** 提升至 **4**（在多核心伺服器上可更高），可在大型批次處理時將處理時間縮短 **30‑70 %**，同時仍遵守您在應用程式設定中設定的記憶體上限。  

## 在 OCR 圖像辨識中設定閾值  

閾值處理將灰階圖像轉換為黑白點陣圖，對於低對比度來源至關重要。  

**Definition:** `Threshold` 屬性設定二值化時使用的亮度閾值（0‑255）。  

對於褪色的掃描件，設定 **180** 的閾值通常能產生更乾淨的字元邊緣，較預設自動設定可將誤判率降低最高 **15 %**。  

## 在 OCR 圖像辨識中指定允許的字元  

有時您只需要特定子集的字元，例如序號的數字。  

**Definition:** `AllowedCharacters` 集合充當白名單，限制辨識僅包含您指定的字元。  

將引擎限制為 `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` 可消除標點噪音，並將字母數字碼的準確度提升 **20 %**。  

## 在 OCR 圖像辨識中指定忽略的字元  

相反地，您可能想忽略那些常出現的噪音字元。  

**Definition:** `IgnoredCharacters` 集合是黑名單，指示 OCR 引擎在辨識時捨棄符合的符號。  

在目標資料中不包含 “#” 或 “$” 等常見雜訊時將其移除，可大幅降低誤辨率，尤其在掃描表單中。  

## 在 OCR 圖像辨識中使用不同語言  

Aspose.OCR 隨附 **超過 30 種文字** 的語言套件，涵蓋拉丁文、斯拉夫文、阿拉伯文及亞洲文字等。  

**Definition:** `Language` 屬性選擇指導字形分析的語言模型。  

載入相應的套件（例如 `ocrEngine.Language = Language.French`）可使多語言文件的準確度提升 **10‑25 %**，因為引擎會套用特定文字的啟發式演算法。  

## OCR 設定教學  
### [在 OCR 圖像辨識中將結果儲存為文件](./save-result-as-document/)  
釋放 Aspose.OCR for .NET 的潛能。輕鬆辨識圖像文字，並將結果儲存為各種文件格式。  
### [在 OCR 圖像辨識中設定執行緒數量](./set-threads-count/)  
在 .NET 中提升 OCR 效率。使用 Aspose.OCR 輕鬆設定執行緒數量，提升準確度與速度。  
### [在 OCR 圖像辨識中設定閾值](./set-threshold-value/)  
探索 Aspose.OCR for .NET 的強大 OCR 解決方案。輕鬆設定自訂閾值，提升應用程式中的文字辨識效果。  
### [在 OCR 圖像辨識中指定允許的字元](./specify-allowed-characters/)  
使用 Aspose.OCR 在 .NET 中解鎖精準 OCR。輕鬆辨識圖像文字。立即下載，獲得顛覆性的開發體驗。  
### [在 OCR 圖像辨識中指定忽略的字元](./specify-ignored-characters/)  
探索 Aspose.OCR for .NET 的進階 OCR 功能。高效、準確且友善開發者。  
### [在 OCR 圖像辨識中使用不同語言](./working-with-different-languages/)  
釋放 Aspose.OCR for .NET 的多語言 OCR 魔力。輕鬆在各種語言中提取文字。  

## 如何使用 Aspose.OCR 提取圖像文字 – 常見設定概覽  

載入 OCR 引擎，設定所需參數，然後呼叫 `Recognize` —— 這是 **少於 10 行程式碼** 的核心工作流程。掌握以下常見設定後，您即可根據專案需求，為速度、精度或多語言支援量身調整引擎。  

| 設定 | 目的 | 使用時機 |
|---------|---------|-------------|
| **Save Result as Document** | 將 OCR 輸出匯出為 PDF/DOCX/TXT | 需要可重複使用且可搜尋的文件時 |
| **Threads Count** | 控制平行處理 | 大量批次或對效能要求高的應用程式 |
| **Threshold Value** | 調整圖像二值化 | 低對比或噪點圖像 |
| **Allowed Characters** | 白名單特定符號 | 領域特定資料（例如序號） |
| **Ignored Characters** | 黑名單不需要的符號 | 移除標點等噪音 |
| **Language Packs** | 啟用多語言辨識 | 包含非拉丁文字的文件 |

## 常見問題  

**Q: Can I use Aspose.OCR in a .NET Core project?**  
A: 是的，Aspose.OCR for .NET 完全支援 .NET Core、.NET 5+ 與 .NET 6+，且 API 介面相同。  

**Q: How do I improve OCR accuracy on low‑resolution images?**  
A: 提高 `Threshold` 值，啟用相應的 `Language` 套件，並考慮設定 `AllowedCharacters` 以限制字元集，即可提升低解析度圖像的 OCR 準確度。  

**Q: Is it possible to extract text from PDFs directly?**  
A: 雖然 Aspose.OCR 主要針對圖像檔案，但您可先使用 Aspose.PDF 將 PDF 頁面轉為圖像，然後對產生的圖像執行 OCR。  

**Q: What licenses are required for production use?**  
A: 部署時需購買商業版 Aspose.OCR 授權；亦提供免費 30 天試用版供評估使用。  

**Q: Are there any size limits for the images I can process?**  
A: 此函式庫可輕鬆處理最高 **500 MB** 的圖像；若檔案更大，請提升 `ThreadsCount` 並相應調整記憶體設定。  

---  

**最後更新：** 2026-05-19  
**測試版本：** Aspose.OCR 24.11 for .NET  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 優化](/ocr/net/ocr-optimization/)
- [設定執行緒數量以提升 .NET 中的 OCR 準確度](/ocr/net/ocr-settings/set-threads-count/)
- [使用 Aspose OCR 辨識多語言文字圖像](/ocr/net/ocr-settings/working-with-different-languages/)


{{< /blocks/products/pf/tutorial-page-section >}}  
{{< /blocks/products/pf/main-container >}}  
{{< /blocks/products/pf/main-wrap-class >}}