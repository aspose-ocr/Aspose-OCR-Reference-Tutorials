---
date: 2025-12-06
description: 學習如何使用 Aspose.OCR for Java 從圖像中提取文字。本分步教學示範如何使用 BufferedImage 將圖像轉換為
  Java 文字。
linktitle: 'Extract Text from Image Java: OCR on BufferedImage with Aspose.OCR'
second_title: Aspose.OCR Java API
title: 從圖像提取文字（Java） - 使用 Aspose.OCR 對 BufferedImage 進行 OCR
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字（Java）：使用 Aspose.OCR 在 BufferedImage 上的 OCR

## 介紹

在本 **Aspose OCR Java 教程** 中，您將了解如何使用功能強大的 Aspose.OCR 函式庫 **從圖像提取文字（Java）**。無論您需要讀取掃描文件、處理收據，或從螢幕截圖中提取文字，對 `BufferedImage` 進行 OCR 可為您提供一種乾淨且程式化的方式將圖像轉換為文字（Java）。我們將逐步說明設定、必要的匯入以及您在數秒內取得結果的完整程式碼。

## 快速解答
- **哪個函式庫最適合 Java OCR？** Aspose.OCR for Java。  
- **可以直接處理 BufferedImage 嗎？** 可以 – `RecognizePage` 方法接受 `BufferedImage`。  
- **測試是否需要授權？** 免費試用可用於開發；正式上線需購買授權。  
- **支援哪些圖像格式？** PNG、JPEG、BMP、TIFF 等。  
- **一般圖像處理需要多長時間？** 標準尺寸圖像通常在一秒內完成。

## 什麼是 OCR 以及為何使用它來從圖像提取文字（Java）？

光學字符辨識（OCR）會分析圖像中的視覺模式，並將其轉換為可編輯的文字。對於 Java 開發者而言，OCR 能自動化資料輸入、建立可搜尋的檔案庫，並為 AI 工作流程提供文字來源，免除手動轉錄的繁瑣。

## 為何選擇 Aspose.OCR for Java？

- **高準確度**，支援多種語言和字型。  
- **簡易 API** – 一行程式碼即可辨識整頁。  
- **無外部相依性** – 可直接使用純 `BufferedImage`。  
- **完整文件** 與定期更新（請參閱頁底的信任指標）。

## 前置條件

在開始之前，請確保您已具備以下項目：

1. **Java Development Kit (JDK)** – 版本 8 或更新。從 [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.OCR for Java** – 從 Aspose 官方網站取得最新 JAR，點擊[此處](https://releases.aspose.com/ocr/java/)。  
3. **圖片資料夾** – 在電腦上建立目錄並放入要處理的圖片。將程式碼中的 `dataDir` 變數更新為該資料夾路徑。

## 匯入套件

先匯入必要的類別。`AsposeOCR` 類別提供 OCR 引擎，而 `ImageIO` 與 `BufferedImage` 負責圖像載入。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

## 步驟指南：從圖像提取文字（Java）

### 步驟 1：定義文件目錄與圖像路徑  

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

將 `"Your Document Directory"` 替換為 PNG/JPEG 檔案所在的絕對路徑。此路徑即為 **將圖像轉換為文字（Java）** 的讀取來源。

### 步驟 2：建立 AsposeOCR 實例  

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 物件讓您可以使用所有 OCR 方法，包括語言選擇與進階設定（如有需要，可於稍後設定）。

### 步驟 3：載入圖像並辨識文字  

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

在此我們：

1. 將圖像檔案載入為 `BufferedImage`。  
2. 呼叫 `api.RecognizePage(loaded)` – 這是核心的 **從圖像提取文字（Java）** 呼叫。  
3. 將辨識出的字串輸出至主控台。

對每張需要處理的圖像重複上述三個步驟，只需調整 `imagePath` 即可。

## 常見問題與除錯

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| `null` 輸出 | 找不到圖像檔案或檔案不可讀 | 核對 `dataDir` 與檔名；確保圖像格式受支援 |
| 文字亂碼 | 語言設定錯誤 | 在 `RecognizePage` 前使用 `api.setLanguage(Language.<desired>)` |
| 大圖像處理緩慢 | 圖像解析度過高 | 調整圖像尺寸或傳入縮放過的 `BufferedImage` 給 API |

## 常見問答（補充）

**Q1：Aspose.OCR 能處理多種語言嗎？**  
A：可以 – 內建支援數十種語言。您可使用 `api.setLanguage(Language.English)`（或其他支援的語言）設定目標語言。

**Q2：Aspose.OCR 是否相容不同的圖像格式？**  
A：絕對相容。PNG、JPEG、BMP、TIFF 以及 GIF 均受支援。

**Q3：Aspose.OCR 更新頻率如何？**  
A：Aspose 定期釋出更新。請於[文件頁面](https://reference.aspose.com/ocr/java/)查看最新發行說明。

**Q4：購買前可以先試用 Aspose.OCR 嗎？**  
A：可以 – 免費試用可於[此處](https://releases.aspose.com/)取得。

**Q5：哪裡可以取得 Aspose.OCR 的社群支援？**  
A：請前往[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)參與討論。

## 結論

您現在已掌握如何使用 Aspose.OCR 的 `BufferedImage` 工作流程 **從圖像提取文字（Java）**。此方法讓您能快速且可靠地 **將圖像轉換為文字（Java）**，為應用程式提供可搜尋、可編輯的內容。您亦可探索語言選擇、PDF 上的 OCR 或批次處理等進階功能，進一步擴充解決方案。

---

**最後更新：** 2025-12-06  
**測試環境：** Aspose.OCR for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}