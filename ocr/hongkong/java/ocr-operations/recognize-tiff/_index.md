---
date: 2025-12-15
description: 學習如何使用 Aspose.OCR for Java 辨識 TIFF 圖像中的文字。本分步教學涵蓋環境設定、程式碼與最佳實踐。
linktitle: OCR Recognizing TIFF Images in Aspose.OCR for Java
second_title: Aspose.OCR Java API
title: 如何使用 Aspose.OCR for Java 辨識 TIFF 圖像中的文字
url: /zh-hant/java/ocr-operations/recognize-tiff/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.OCR for Java 中辨識 TIFF 圖像的 OCR

## 簡介

歡迎閱讀終極 **aspose ocr java tutorial**，本教學將示範如何使用 Aspose.OCR for Java **recognize text in tiff** 圖像。無論您是資深開發者或剛接觸 OCR，本指南都會一步步帶領您，從專案設定到提取乾淨、可搜尋的文字。完成後，您將擁有一個可直接執行的範例，並可依需求套用於自己的應用程式。

## 快速解答
- **What does “recognize text in tiff” mean?** 它指的是使用 OCR 技術從 TIFF 格式的圖像中提取可讀的字元。  
- **Which library is required?** Aspose.OCR for Java（可從官方 Aspose 網站下載）。  
- **Do I need a license for testing?** 提供免費試用版；商業使用則需購買授權。  
- **Can I process multi‑page TIFF files?** 是的，`RecognizeTiff` 方法可直接處理多頁 TIFF 文件。  
- **What Java version is supported?** 建議使用 Java 8 或更高版本。

## 什麼是 “recognize text in tiff”？

TIFF（Tagged Image File Format）常用於高解析度的掃描文件。**recognize text in tiff** 操作利用先進的影像分析技術定位字元、單詞與段落，並將其轉換為可編輯的文字，便於儲存、搜尋或建立索引。

## 為什麼要使用 Aspose.OCR for Java？

- **High accuracy** 支援多種語言與字體，具備高準確度。  
- **Built‑in support** 支援多頁 TIFF、PDF 及其他影像格式。  
- **Simple API** 只需少量程式碼即可使用。  
- **No external dependencies** – 完全基於純 Java，無需外部相依。

## 先決條件

在開始本教學之前，請確保已具備以下先決條件：

- 已在電腦上安裝 Java Development Kit（JDK）。  
- 已下載 Aspose.OCR for Java 程式庫並加入專案。您可於 [here](https://releases.aspose.com/ocr/java/) 下載。  
- 一個包含欲辨識文字的 TIFF 圖像檔案。

## 匯入套件

在 Java 專案中，請確保匯入使用 Aspose.OCR 所需的套件：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.DetectAreasMode;
import com.aspose.ocr.DocumentRecognitionSettings;
import com.aspose.ocr.Language;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionResult.LinesResult;
import com.aspose.ocr.pdf.AsposeOCRPdf;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.util.ArrayList;
```

現在，讓我們將範例程式碼拆解為多個步驟，完整說明如何在 TIFF 圖像上執行文字辨識。

## 步驟 1：設定專案

首先建立一個新的 Java 專案，並將 Aspose.OCR for Java 程式庫加入 classpath。

## 步驟 2：定義文件目錄與影像路徑

```java
String dataDir = "Your Document Directory";
String file = dataDir + "multipage.tif";
```

將 `"Your Document Directory"` 替換為您專案文件目錄的實際路徑。

## 步驟 3：建立 AsposeOCR 實例

```java
AsposeOCR api = new AsposeOCR();
```

初始化 `AsposeOCR` 類別的實例，用於文字辨識。

## 步驟 4：設定辨識選項

```java
DocumentRecognitionSettings settings = new DocumentRecognitionSettings(2);
settings.setDetectAreasMode(DetectAreasMode.PHOTO);
```

設定辨識參數，依需求指定模式及其他選項。

## 步驟 5：執行文字辨識

```java
ArrayList<RecognitionResult> result = api.RecognizeTiff(file, settings);
```

呼叫 `RecognizeTiff` 方法，使用先前設定的參數對指定的 TIFF 圖像執行 OCR。

## 步驟 6：列印辨識結果

```java
for (RecognitionResult r : result) {
    printResult(r);
}
```

遍歷辨識結果，列印擷取的文字、段落、行、字元、警告、JSON 以及拼寫校正後的文字。

## 步驟 7：實作 `printResult` 方法

```java
static void printResult(RecognitionResult result) {
    // Your implementation here
}
```

定義 `printResult` 方法，以結構化方式顯示 OCR 結果。

完成！您已成功使用 Aspose.OCR for Java 實作 **recognize text in tiff**。可依需求自行客製化程式碼，例如變更偵測模式或處理不同語言。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **No text returned** | 檔案路徑不正確或 TIFF 壓縮格式不支援。 | 請確認 `dataDir` 路徑，並確保 TIFF 檔案未損毀。 |
| **Garbage characters** | 影像解析度過低或對比度不足。 | 在 OCR 前先對影像進行前處理（提升 DPI、增強對比度）。 |
| **Unsupported language** | `DocumentRecognitionSettings` 中未設定語言。 | 加入 `settings.setLanguage(Language.SPANISH);`（或您目標的語言）。 |

## 常見問答

### Q1：Aspose.OCR 是否適用於辨識多種語言的文字？

A1：是的，Aspose.OCR 支援多語言文字辨識，為各種應用提供彈性。

### Q2：我可以將 Aspose.OCR 整合到 Web 應用程式中嗎？

A2：當然可以！Aspose.OCR 可無縫整合至桌面與 Web 應用程式。

### Q3：Aspose.OCR 有哪些授權方案可供選擇？

A3：是的，您可於 [here](https://purchase.aspose.com/buy) 查看授權方案並購買。

### Q4：Aspose.OCR for Java 是否提供免費試用？

A4：是的，您可於 [here](https://releases.aspose.com/) 取得免費試用版。

### Q5：我可以在哪裡找到 Aspose.OCR 的其他支援或社群討論？

A5：請前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 取得社群支援與討論。

---

**最後更新:** 2025-12-15  
**測試於:** Aspose.OCR for Java 24.11 (latest at time of writing)  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}