---
date: 2026-05-04
description: 學習如何使用 Aspose.OCR for Java 進行影像轉文字的 Java 程式。此一步一步的教學會示範如何使用 BufferedImage
  從影像中擷取文字。
keywords:
- image to text java
- extract text from image
- recognize text from png
linktitle: 在 Java 中從圖像提取文字：使用 Aspose.OCR 對 BufferedImage 進行 OCR
second_title: Aspose.OCR Java API
title: 圖像轉文字 Java：使用 Aspose.OCR 將圖像轉換為文字
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中將圖像轉換為文字：使用 Aspose.OCR 於 BufferedImage 的 OCR

## 簡介

在本 **Aspose OCR Java 教學** 中，您將學會如何使用功能強大的 Aspose.OCR 函式庫 **將圖像轉換為文字**。**本指南將帶您透過 Aspose.OCR 的 BufferedImage 支援完成 image to text java**，無論是處理掃描文件、讀取收據，或從螢幕截圖中擷取文字。我們將逐步說明設定、必要的匯入，以及取得快速結果所需的完整程式碼。

## 快速答案
- **哪個函式庫最適合 Java OCR？** Aspose.OCR for Java。  
- **我可以直接處理 BufferedImage 嗎？** 可以 – `RecognizePage` 方法接受 `BufferedImage`。  
- **測試時需要授權嗎？** 免費試用可用於開發；正式上線需購買授權。  
- **支援哪些圖像格式？** PNG、JPEG、BMP、TIFF 等。  
- **一般圖像處理需要多長時間？** 標準尺寸圖像通常在一秒內完成。

## 什麼是 image to text java？

光學字符辨識（OCR）會分析圖像中的視覺模式，並將其轉換為可編輯的文字。在 Java 中，OCR 讓您能以程式方式 **從圖像中擷取文字**，從而實現自動化資料輸入、可搜尋的檔案庫，以及不需人工轉錄的 AI 工作流程。

## 為什麼選擇 Aspose.OCR for Java？

- **高精度**：支援多種語言與字型。  
- **簡易 API**：一行程式碼即可辨識整頁。  
- **無外部相依性**：直接使用純 `BufferedImage`。  
- **完整文件** 及定期更新（請參閱底部的信任指標）。

## 先決條件

在開始之前，請確保您具備以下條件：

1. **Java Development Kit (JDK)** – 版本 8 或更新。從 [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.OCR for Java** – 從 Aspose 官方網站 [here](https://releases.aspose.com/ocr/java/) 取得最新 JAR。  
3. **A folder with images** – 在您的機器上建立資料夾，放入欲處理的圖像。於程式碼中將 `dataDir` 變數指向此資料夾。

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

## 如何在 Java 中 **將圖像轉換為文字** – 步驟指南

### 步驟 1：定義文件目錄和圖像路徑  

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

將 `"Your Document Directory"` 替換為存放 PNG/JPEG 檔案的絕對路徑。這就是 **image to text java** 會讀取的來源位置。

### 步驟 2：建立 AsposeOCR 實例  

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 物件讓您存取所有 OCR 方法，包含語言選擇與進階設定，日後若有需要亦可使用。

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

1. 將圖像檔載入為 `BufferedImage`。  
2. 呼叫 `api.RecognizePage(loaded)` – 這是核心 **extract text java** 呼叫。  
3. 將辨識出的字串印到主控台。

> **Pro tip:** 您也可以使用相同方法 **recognize text from png** 檔案；只要將 `imagePath` 指向 PNG 圖像即可。

對每張需處理的圖像重複上述三個步驟，只需調整 `imagePath`。

## 常見使用情境

- **發票處理：** 從掃描的 PDF 或 PNG 收據中擷取明細項目。  
- **文件歸檔：** 將掃描的合約轉換為可搜尋的文字，以便快速檢索。  
- **自動化機器人：** 從網頁或桌面應用程式的螢幕截圖中擷取文字。

## 常見問題與疑難排解

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| `null` output | 找不到圖像檔案或無法讀取 | 驗證 `dataDir` 與檔名；確保圖像為支援的格式 |
| 文字亂碼 | 語言設定錯誤 | 在 `RecognizePage` 前使用 `api.setLanguage(Language.<desired>)` |
| 大型圖像處理速度慢 | 圖像解析度過高 | 調整圖像大小或傳遞縮放過的 `BufferedImage` 給 API |

## 常見問題 (補充)

**Q1: Aspose.OCR 能處理多種語言嗎？**  
A: 可以 – 它內建支援數十種語言。您可使用 `api.setLanguage(Language.English)`（或其他支援語言）設定目標語言。

**Q2: Aspose.OCR 與不同圖像格式相容嗎？**  
A: 完全相容。支援 PNG、JPEG、BMP、TIFF 以及 GIF。

**Q3: Aspose.OCR 更新頻率如何？**  
A: Aspose 定期發布更新。請於 [documentation page](https://reference.aspose.com/ocr/java/) 查看最新發行說明。

**Q4: 購買前可以先試用 Aspose.OCR 嗎？**  
A: 可以 – 免費試用版可於 [here](https://releases.aspose.com/) 取得。

**Q5: 哪裡可以取得 Aspose.OCR 的社群支援？**  
A: 加入 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 參與討論。

## FAQ – Java OCR 教學快速參考

**Q: 開始 **java ocr 教學** 的最簡單方法是什麼？**  
A: 安裝 JDK，將 Aspose.OCR JAR 加入專案，然後依照上方的三步驟程式碼範例執行。

**Q: 我可以使用此方法大量 **process scanned documents** 嗎？**  
A: 可以。遍歷目錄中的檔案，重複使用同一個 `AsposeOCR` 實例，並收集每個結果。

**Q: 是否需要為英文文字設定語言？**  
A: 英文為預設語言，但若需明確指定，可使用 `api.setLanguage(Language.English)`。

**Q: 在伺服器上執行會有性能影響嗎？**  
A: 引擎輕量；一般圖像（<2 MB）處理時間均在一秒以內。高吞吐量情境建議先行縮放圖像或使用多執行緒。

**Q: 生產環境如何處理授權？**  
A: 在建立 `AsposeOCR` 實例前，先載入授權檔案：`License license = new License(); license.setLicense("Aspose.OCR.lic");`。

---

**最後更新：** 2026-05-04  
**測試環境：** Aspose.OCR for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}