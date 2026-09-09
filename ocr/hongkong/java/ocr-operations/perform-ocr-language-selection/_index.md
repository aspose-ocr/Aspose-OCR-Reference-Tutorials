---
date: 2026-02-12
description: 學習如何使用 Aspose.OCR for Java 進行語言選擇的影像文字 OCR。本逐步指南涵蓋 Java 文字提取、OCR 斜率校正等內容，還有更多技巧。
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: 如何使用 Aspose.OCR 以語言進行圖像文字 OCR
url: /zh-hant/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR 進行語言 OCR 圖像文字

## 簡介

從圖像檔案中提取文字是一項常見需求，無論是數位化掃描文件、處理收據，或建立可搜尋的檔案庫。在本教學中，我們將逐步示範完整的實作範例，說明**如何使用特定語言設定進行圖像文字 OCR**，讓您今天即可將可靠的 OCR 整合至 Java 應用程式中。您還會看到如何處理 OCR 歪斜校正與基於區域的辨識，以獲得最佳準確度。

## 快速回答
- **什麼函式庫在 Java 中處理 OCR？** Aspose.OCR for Java  
- **哪個設定用於選擇語言？** `settings.setLanguage(Language.Eng)`（或任何支援的語言）  
- **開發時需要授權嗎？** 免費評估授權可用於測試；正式環境需購買商業授權。  
- **我可以將 OCR 限制在圖像的特定區域嗎？** 可以，使用 `RecognitionSettings.setRecognitionAreas()` 搭配矩形。  
- **一般執行時間為多少？** 在一般筆記型電腦上每頁數秒，視圖像大小與語言複雜度而定。

## 如何在選擇語言的情況下 OCR 圖像文字
本節將說明核心問題——在已知文字語言的情況下**如何 OCR** 圖像。正確選擇語言可大幅提升辨識準確度，因為 OCR 引擎會套用語言特定的字典與字元模型。

### 為什麼這很重要
- **更高的準確度** – 語言特定模型可減少誤辨。  
- **效能提升** – 引擎會跳過不必要的語言檢查。  
- **更佳的變音符處理** – 當使用相符的 `Language` 列舉時，法文、西班牙文、德文等的變音符會被正確辨識。

## 什麼是「從圖像提取文字」？
從圖像提取文字（OCR）將字元的視覺呈現轉換為機器可讀的字串。這使得搜尋、分析與資料擷取工作流程得以自動化，否則必須手動轉錄。

## 為什麼要使用 Aspose.OCR 並選擇語言？
- **多語言支援** – 選擇圖像中實際出現的語言以提升準確度。  
- **精細控制** – 調整歪斜、定義辨識區域，並設定自動歪斜行為。  
- **純 Java API** – 無原生相依，易於整合至任何 Java 專案。  
- **豐富的結果資料** – 一次呼叫即可取得純文字、JSON、邊界矩形與警告訊息。

## 先決條件

在開始之前，請確保您已具備：

- **Java Development Kit (JDK)** 已安裝（JDK 8 或更新版本）。  
- **Aspose.OCR for Java** 函式庫 – 從官方網站[此處](https://reference.aspose.com/ocr/java/)下載。  
- 包含欲提取文字的圖像檔，例如 `p3.png`。

## 匯入套件

在您的 Java 原始檔中，加入所需的 Aspose.OCR 類別與標準 Java 工具：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 逐步指南

### 步驟 1：設定文件目錄

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

將 `"Your Document Directory"` 替換為 `p3.png` 所在的絕對路徑。

### 步驟 2：定義圖像路徑

```java
// The image path
String file = dataDir + "p3.png";
```

確保 `file` 變數指向您欲處理的正確圖像。

### 步驟 3：建立 Aspose.OCR API 實例

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 物件讓您可以使用所有 OCR 操作。

### 步驟 4：設定辨識選項（語言選擇）

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

在此我們：

1. 停用自動歪斜校正，因為我們提供手動的歪斜值。  
2. 定義矩形區域（`RecognitionAreas`），將 OCR 限制於實際包含文字的圖像部分。  
3. 將 **語言** 設為英文（`Language.Eng`）。根據來源圖像，可改為 `Language.Fra`、`Language.Spa` 等。

### 步驟 5：執行 OCR 並取得結果

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` 呼叫會使用您定義的圖像與設定執行 OCR 引擎。結果會存入 `RecognitionResult` 物件。

### 步驟 6：列印並使用結果

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

主控台輸出會顯示：

- 完整的提取文字（`recognitionText`）。  
- 每個定義矩形的文字（`recognitionAreasText`）。  
- 邊界矩形座標。  
- 便於後續處理的 JSON 表示。  
- 偵測到的歪斜角度與任何警告。

現在您可以將 `result.recognitionText` 送入業務邏輯——儲存、建立索引，或傳遞給其他服務。

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **雜訊字元** | 選擇了錯誤的語言 | 設定正確的 `Language` 列舉（例如法文使用 `Language.Fra`）。 |
| **未返回文字** | 辨識區域未覆蓋文字 | 調整 `Rectangle` 座標，或移除 `RecognitionAreas` 以處理整張圖像。 |
| **效能緩慢** | 圖像過大或解析度過高 | 在 OCR 前縮小圖像，或為 JVM 增加記憶體配置。 |
| **不支援格式的警告** | 圖像格式未被識別 | 在處理前將圖像轉換為 PNG、JPEG 或 TIFF。 |

## 常見問答

**Q: 我可以在一次 OCR 呼叫中辨識多種語言嗎？**  
A: 可以。使用 `settings.setLanguage(Language.Eng | Language.Fra)` 以啟用多語言辨識。

**Q: Aspose.OCR 支援哪些圖像格式？**  
A: PNG、JPEG、BMP、TIFF、GIF 以及其他多種格式。只需提供正確的檔案路徑。

**Q: 圖像大小有上限嗎？**  
A: 沒有硬性上限，但非常大的圖像會增加記憶體使用與處理時間。建議調整大型檔案的尺寸。

**Q: 我該如何取得正式授權？**  
A: 從 Aspose 官方網站購買授權，並依照 Aspose 文件示範，使用 `License` 類別套用授權。

**Q: 我能直接從 PDF 頁面提取文字嗎？**  
A: Aspose.OCR 無法直接處理 PDF。需先將 PDF 頁面轉為圖像（例如使用 Aspose.PDF），再執行 OCR。

## 結論

現在您已了解如何使用 Aspose.OCR for Java **從圖像提取文字**，同時選擇適當的語言並將辨識限制於特定區域。此方法提供高準確度與高效能的 OCR，可嵌入任何基於 Java 的工作流程——從文件管理系統到資料擷取管線。準備好前進了嗎？試著更換語言列舉、實驗不同的辨識區域，並將結果整合至您自己的應用程式邏輯中。

---

**最後更新：** 2026-02-12  
**測試環境：** Aspose.OCR 24.11 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}