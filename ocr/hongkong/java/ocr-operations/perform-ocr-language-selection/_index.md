---
date: 2025-12-13
description: 學習如何使用 Aspose.OCR for Java 從圖像中提取文字並選擇語言。此一步一步的 Aspose OCR Java 教程展示了精確的
  OCR 設定。
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: 使用 Aspose.OCR 進行語言選擇的圖像文字提取方法
url: /zh-hant/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.OCR 透過語言選擇從圖像提取文字

## 簡介

從圖像檔案提取文字是常見需求，無論是將掃描文件數位化、處理收據，或是建立可搜尋的檔案庫。Aspose.OCR for Java 讓這項工作變得簡單，並提供對語言選擇、傾斜校正與識別區域的細緻控制。在本教學中，我們將一步步示範完整的實作範例，說明 **如何使用特定語言設定從圖像提取文字**，讓您今天就能在 Java 應用程式中整合可靠的 OCR 功能。

## 快速答覆
- **什麼程式庫處理 Java 中的 OCR？** Aspose.OCR for Java  
- **哪個設定用於選擇語言？** `settings.setLanguage(Language.Eng)` (或任何支援的語言)  
- **開發時需要授權嗎？** 免費評估授權可用於測試；正式環境需要商業授權。  
- **我可以將 OCR 限制在圖像的某個區域嗎？** 可以，使用 `RecognitionSettings.setRecognitionAreas()` 並搭配矩形。  
- **一般執行時間是多少？** 在標準筆記本電腦上每頁幾秒鐘，視圖像大小與語言複雜度而定。

## 什麼是「從圖像提取文字」？
從圖像提取文字（OCR）將字符的視覺表現轉換為機器可讀的字串。這使得搜尋、分析與資料抽取工作流程得以自動化，免除手動轉錄的需求。

## 為什麼要使用具語言選擇功能的 Aspose.OCR？
- **多語言支援** – 選擇圖像中實際出現的語言以提升準確度。  
- **細緻控制** – 調整傾斜、定義識別區域，並設定自動傾斜行為。  
- **純 Java API** – 無原生相依性，易於整合至任何 Java 專案。  
- **豐富的結果資料** – 一次呼叫即可取得純文字、JSON、邊界矩形與警告。

## 先決條件

在開始之前，請確保您已具備：

- 已安裝 **Java Development Kit (JDK)**（JDK 8 或以上）。  
- **Aspose.OCR for Java** 程式庫 – 從官方網站[此處](https://reference.aspose.com/ocr/java/)下載。  
- 包含欲提取文字的圖像檔案，例如 `p3.png`。

## 匯入套件

在您的 Java 原始碼檔案中，加入所需的 Aspose.OCR 類別與標準 Java 工具：

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

確保 `file` 變數指向您要處理的精確圖像檔案。

### 步驟 3：建立 Aspose.OCR API 實例

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 物件讓您可以存取所有 OCR 操作。

### 步驟 4：設定識別選項（語言選擇）

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

1. 停用自動傾斜，因為我們提供手動傾斜值。  
2. 定義矩形區域（`RecognitionAreas`），將 OCR 限制在實際包含文字的圖像部分。  
3. 設定 **語言** 為英文（`Language.Eng`）。根據來源圖像，可改為 `Language.Fra`、`Language.Spa` 等。

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

`RecognizePage` 呼叫會使用您定義的圖像與設定執行 OCR 引擎，結果儲存在 `RecognitionResult` 物件中。

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

控制台輸出會顯示：

- 完整提取的文字（`recognitionText`）。  
- 每個定義矩形的文字（`recognitionAreasText`）。  
- 邊界矩形座標。  
- JSON 表示，便於後續處理。  
- 偵測到的傾斜角度及任何警告。

現在您可以將 `result.recognitionText` 送入業務邏輯——儲存、索引，或傳遞給其他服務。

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **亂碼** | 選擇了錯誤的語言 | 設定正確的 `Language` 列舉（例如 `Language.Fra` 代表法文）。 |
| **未返回文字** | 識別區域未覆蓋文字 | 調整 `Rectangle` 座標，或移除 `RecognitionAreas` 以處理整張圖像。 |
| **效能緩慢** | 圖像過大或解析度過高 | 在 OCR 前縮小圖像，或為 JVM 增加記憶體配置。 |
| **不支援格式的警告** | 圖像格式未被識別 | 將圖像轉換為 PNG、JPEG 或 TIFF 後再處理。 |

## 常見問答

**Q: 我可以在一次 OCR 呼叫中辨識多種語言嗎？**  
A: 可以。使用 `settings.setLanguage(Language.Eng | Language.Fra)` 以啟用多語言辨識。

**Q: Aspose.OCR 支援哪些圖像格式？**  
A: PNG、JPEG、BMP、TIFF、GIF 等多種格式。只需提供正確的檔案路徑。

**Q: 圖像大小有上限嗎？**  
A: 沒有硬性上限，但非常大的圖像會增加記憶體使用與處理時間。建議對大型檔案進行縮放。

**Q: 我該如何取得正式授權？**  
A: 從 Aspose 官方網站購買授權，並依照 Aspose 文件示範使用 `License` 類別套用。

**Q: 我可以直接從 PDF 頁面提取文字嗎？**  
A: Aspose.OCR 無法直接處理 PDF。需先將 PDF 頁面轉為圖像（例如使用 Aspose.PDF），再執行 OCR。

## 結論

您現在已了解如何使用 Aspose.OCR for Java 在選擇適當語言並限制識別區域的情況下 **從圖像提取文字**。此方法提供高準確度與高效能的 OCR，能輕鬆嵌入任何基於 Java 的工作流程，無論是文件管理系統還是資料擷取管線。

---

**最後更新：** 2025-12-13  
**測試版本：** Aspose.OCR 24.11 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}