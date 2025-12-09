---
date: 2025-12-09
description: 學習如何使用 Aspose.OCR for Java 從圖像中提取文字並指定允許的字元 – 完整的 Aspose OCR Java 教程。
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: 使用 Aspose.OCR 從圖像提取文字 – 允許的字元
url: /zh-hant/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 從圖像提取文字 – 允許的字元

## 介紹

從圖像提取文字是現代應用程式的常見需求——無論是處理發票、掃描收據，或是將印刷文件數位化。**Aspose.OCR for Java** 讓這項工作變得簡單，提供高精度的辨識與彈性的設定選項，例如指定允許的字元。本教學將帶領您完整走過 **aspose ocr java tutorial**，說明如何設定函式庫、執行 OCR，並限制字元集合以符合您的需求。

## 快速答覆
- **Aspose.OCR 的功能是什麼？** 它能以高精度從圖像中提取文字，並支援自訂字元集合。  
- **我需要授權嗎？** 在正式環境使用時必須擁有臨時或永久授權。  
- **支援哪個 JDK 版本？** 最新的 JDK 版本皆完全相容。  
- **我可以限制辨識的字元嗎？** 可以——使用 allowed‑characters API 來限制輸出。  
- **設定需要多長時間？** 基本實作大約 10‑15 分鐘即可完成。

## 什麼是「從圖像提取文字」？
從圖像提取文字是指將視覺上的文字（例如印刷或手寫文字）轉換為機器可讀的字串。這讓後續的搜尋、索引或資料分析等工作得以進行。

## 為什麼選擇 Aspose.OCR for Java？
- **高精度**，支援多種語言與字型。  
- **簡易 API**，可整合至任何 Java 專案。  
- **可自訂**的字元集合、語言套件與圖像前處理。  
- **無外部相依**——函式庫為獨立封裝。

## 前置條件

### Java Development Kit (JDK)
確保您的系統已安裝最新的 Java Development Kit。可從 [here](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。

### Aspose.OCR for Java 函式庫
從 [download link](https://releases.aspose.com/ocr/java/) 下載並安裝 Aspose.OCR for Java 函式庫。

### Aspose.OCR 授權
欲完整使用 Aspose.OCR 功能，請取得有效授權。可從 [here](https://purchase.aspose.com/buy) 取得，或使用 [temporary license](https://purchase.aspose.com/temporary-license/) 申請試用授權。

## 匯入套件

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 步驟說明

### 步驟 1：設定文件目錄
定義一個資料夾，用來儲 OCR 處理後的結果。此路徑稍後會用於定位圖像檔案。

```java
String dataDir = "Your Document Directory";
```

### 步驟 2：指定圖像路徑
將 API 指向您要分析的圖像。

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 步驟 3：建立 Aspose.OCR 實例
使用授權金鑰建立 OCR 引擎實例。金鑰可以是臨時或永久授權字串。

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 步驟 4：執行 OCR 辨識
呼叫 `RecognizeLine` 方法，從圖像中提取單行文字。結果為純文字字串，您可以進一步處理或儲存。

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **專業提示：** 若需將輸出限制在特定字元集合（例如僅限數字），請在呼叫 `RecognizeLine` 前於 `AsposeOCR` 實例上使用 `setAllowedCharacters` 方法。這樣引擎會忽略不在定義集合內的字元。

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| **沒有輸出或字串為空** | 圖像路徑不正確或使用不支援的圖像格式 | 確認 `imagePath` 並使用支援的格式（JPEG、PNG、BMP） |
| **辨識錯誤** | 影像解析度過低或背景雜訊過多 | 在 OCR 前先前處理圖像（提升對比、二值化） |
| **授權未套用** | 缺少或無效的授權金鑰 | 確保授權字串正確，且已放入 `AsposeOCR` 建構子中 |

## 常見問答

**Q: 如何取得 Aspose.OCR 的臨時授權？**  
A: 前往 [temporary license page](https://purchase.aspose.com/temporary-license/) 申請試用授權。

**Q: 我可以在哪裡取得 Aspose.OCR 的支援？**  
A: 加入 [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) 社群，獲得協助與討論。

**Q: 我可以在 Aspose.OCR 中指定允許的字元嗎？**  
A: 可以，您可使用 `setAllowedCharacters` API 來自訂字元集合。詳情請參考官方文件。

**Q: Aspose.OCR 是否相容於最新的 JDK 版本？**  
A: 當然——Aspose.OCR 會定期更新，以保持與最新的 Java 版本相容。

**Q: 除了行辨識外，還有其他 OCR 功能嗎？**  
A: 有，函式庫支援區塊、段落與整頁辨識，亦提供語言套件與圖像前處理選項。

## 結論

透過本 **aspose ocr java tutorial**，您已擁有可用的解決方案，能 **從圖像提取文字** 並控制辨識的字元。請探索完整的 [documentation](https://reference.aspose.com/ocr/java/) 以發現多語言支援、客製化前處理與批次處理等進階功能。

**最後更新：** 2025-12-09  
**測試環境：** Aspose.OCR for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}