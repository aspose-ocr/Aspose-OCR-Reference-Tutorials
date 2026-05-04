---
date: 2026-02-17
description: 學習如何使用 Aspose.OCR for Java 從圖像中提取文字。此一步步教學將示範如何使用 BufferedImage 將圖像轉換為文字（Java）。
linktitle: 'Extract Text from Image Java: OCR on BufferedImage with Aspose.OCR'
second_title: Aspose.OCR Java API
title: 在 Java 中使用 Aspose.OCR BufferedImage 將影像轉換為文字
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中將圖像轉換為文字：使用 Aspose.OCR 於 BufferedImage 進行 OCR

## 簡介

在本 **Aspose OCR Java 教學** 中，您將學習如何使用功能強大的 Aspose.OCR 函式庫 **將圖像轉換為文字**。無論您需要 **處理掃描文件**、讀取收據，或從螢幕截圖中提取文字，對 `BufferedImage` 進行 OCR 可為您提供一種乾淨、程式化的方式，在幾秒鐘內 **extract text java**（提取文字 java）。我們將逐步說明設定、必要的匯入以及取得快速結果的完整程式碼。

## 快速解答
- **什麼函式庫是 Java OCR 的最佳選擇？** Aspose.OCR for Java.  
- **我可以直接處理 BufferedImage 嗎？** 是 – `RecognizePage` 方法接受 `BufferedImage`.  
- **測試是否需要授權？** 免費試用可用於開發；正式環境需要授權.  
- **支援哪些圖像格式？** PNG、JPEG、BMP、TIFF 等.  
- **一般圖像處理需要多長時間？** 標準尺寸圖像通常在一秒內完成.

## 什麼是 OCR，為何在 Java 中使用它來 **將圖像轉換為文字**？

光學字符識別（OCR）會分析圖像中的視覺模式，並將其轉換為可編輯的文字。對於 Java 開發者而言，OCR 開啟了自動化資料輸入、建構可搜尋檔案庫以及在無需手動轉錄的情況下驅動 AI 工作流程的可能性。

## 為何選擇 Aspose.OCR for Java？

- **高準確度**，支援多種語言與字型。  
- **簡易 API** – 一行程式碼即可辨識整頁。  
- **無外部相依性** – 可直接使用純 `BufferedImage`.  
- **完整文件** 與定期更新（請參閱頁底的信任指標）.

## 先決條件

在深入之前，請確保您具備以下條件：

1. **Java Development Kit（JDK）** – 8 版或更新版本。從 [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。  
2. **Aspose.OCR for Java** – 從 Aspose 官方網站取得最新 JAR，點擊[此處](https://releases.aspose.com/ocr/java/)。  
3. **圖像資料夾** – 在本機建立目錄，放入欲處理的圖像。於程式碼中將 `dataDir` 變數指向此資料夾。

## 匯入套件

首先匯入必要的類別。`AsposeOCR` 類別提供 OCR 引擎，而 `ImageIO` 與 `BufferedImage` 用於載入圖像。

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

### 步驟 1：定義文件目錄與圖像路徑  

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

將 `"Your Document Directory"` 替換為存放 PNG/JPEG 檔案的絕對路徑。此路徑即為 **convert image to text** 處理所讀取的來源。

### 步驟 2：建立 AsposeOCR 實例  

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` 物件讓您存取所有 OCR 方法，未來若需語言選擇或進階設定亦可使用。

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

1. 將圖像檔載入為 `BufferedImage`.  
2. 呼叫 `api.RecognizePage(loaded)` – 這是核心的 **extract text java** 呼叫.  
3. 將辨識出的字串印至主控台.

對每張需處理的圖像重複上述三個步驟，只需調整 `imagePath` 即可。

## 常見問題與故障排除

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `null` 輸出 | 找不到圖像檔或無法讀取 | 檢查 `dataDir` 及檔名；確保圖像為支援格式 |
| 文字亂碼 | 語言設定錯誤 | 在 `RecognizePage` 前使用 `api.setLanguage(Language.<desired>)` |
| 大型圖像效能緩慢 | 圖像解析度過高 | 調整圖像大小或傳入縮放過的 `BufferedImage` 給 API |

## 常見問答（補充）

**Q1：Aspose.OCR 能處理多種語言嗎？**  
A：可以 – 內建支援數十種語言。可使用 `api.setLanguage(Language.English)`（或其他支援語言）設定目標語言。

**Q2：Aspose.OCR 相容於不同的圖像格式嗎？**  
A：絕對支援。PNG、JPEG、BMP、TIFF 以及 GIF 均可使用。

**Q3：Aspose.OCR 更新頻率如何？**  
A：Aspose 定期釋出更新。請於[文件頁面](https://reference.aspose.com/ocr/java/) 查看最新發行說明。

**Q4：購買前可以試用 Aspose.OCR 嗎？**  
A：可以 – 可於[此處](https://releases.aspose.com/) 取得免費試用。

**Q5：在哪裡可以取得 Aspose.OCR 的社群支援？**  
A：請前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 參與討論。

## FAQ – Java OCR 教學快速參考

**Q：開始 **java ocr tutorial** 的最簡單方法是什麼？**  
A：安裝 JDK，將 Aspose.OCR JAR 加入專案，並依照上述三步程式碼範例執行。

**Q：我可以使用此方法批次 **process scanned documents** 嗎？**  
A：可以。遍歷目錄中的檔案，重複使用同一個 `AsposeOCR` 實例，並收集每個結果。

**Q：英文文字需要設定語言嗎？**  
A：English 為預設語言，但可使用 `api.setLanguage(Language.English)` 明確設定。

**Q：在伺服器上執行會有性能影響嗎？**  
A：引擎輕量；一般圖像（<2 MB）處理時間在一秒以內。高吞吐量情境建議先縮放圖像或使用多執行緒。

**Q：如何在正式環境處理授權？**  
A：在建立 `AsposeOCR` 實例前，先載入授權檔案，例如 `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

## 結論

您現在已掌握如何在 Java 中使用 Aspose.OCR 的 `BufferedImage` 工作流程 **將圖像轉換為文字**。此方法可讓您快速且可靠地 **extract text java**，為應用程式提供可搜尋、可編輯的內容來源。可進一步探索語言選擇、PDF 上的 OCR 或批次處理等功能，以擴充您的解決方案。

---

**最後更新：** 2026-02-17  
**測試環境：** Aspose.OCR for Java 24.11（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}