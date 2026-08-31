---
date: 2026-02-20
description: 學習如何使用 Aspose.OCR for Java 從圖像中提取文字、設定允許的字元以及套用臨時授權——完整的 Aspose OCR Java
  教學。
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: 使用 Aspose.OCR 從圖像提取文字 – 允許的字元
url: /zh-hant/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 從圖像提取文字 – 允許的字符

## 介紹

從圖像中提取文字是現代應用程式中的常見需求——無論是處理發票、掃描收據，或是數位化印刷文件。本教學將逐步說明完整的 **aspose ocr java tutorial**，示範如何使用 Aspose.OCR for Java **extract text from images**、設定允許的字符，並在僅測試函式庫時套用臨時授權。

## 快速解答
- **Aspose.OCR 的功能是什麼？** 它能以高準確度從圖像中提取文字，並支援自訂字符集。  
- **我需要授權嗎？** 生產環境使用需有臨時或永久授權。  
- **支援哪個 JDK 版本？** 最新的 JDK 版本皆相容。  
- **我可以限制辨識的字符嗎？** 可以——使用 `setAllowedCharacters` API 來限制輸出。  
- **設定需要多久？** 基本實作約需 10‑15 分鐘。

## 什麼是「從圖像提取文字」？

從圖像提取文字是指將視覺文字（例如印刷或手寫文字）轉換為機器可讀的字串的過程。這使得後續的搜尋、索引或資料分析等工作成為可能。

## 為什麼使用 Aspose.OCR for Java？

- **High accuracy** 跨多種語言與字型皆具高準確度。  
- **Simple API** 可整合至任何 Java 專案。  
- **Customizable** 可自訂字符集、語言包與圖像前處理。  
- **No external dependencies**——函式庫自給自足。

## 前置作業

在開始之前，請確保您已具備以下條件：

### Java Development Kit (JDK)

確保您的系統已安裝最新的 Java Development Kit。您可以從 [此處](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。

### Aspose.OCR for Java Library

從 [下載連結](https://releases.aspose.com/ocr/java/) 下載並安裝 Aspose.OCR for Java 函式庫。

### Aspose.OCR License

欲發揮 Aspose.OCR 的全部功能，請取得有效授權。您可從 [此處](https://purchase.aspose.com/buy) 取得，或探索 [temporary license](https://purchase.aspose.com/temporary-license/) 以獲得試用授權。

## 如何套用臨時授權

在評估產品時，臨時授權會移除評估浮水印，並在有限期間內解鎖全部功能。於 Aspose 入口網站產生授權字串，然後如以下程式碼範例所示傳入 `AsposeOCR` 建構子。正式部署時，請以永久授權取代臨時金鑰。

## OCR 圖像前處理技巧

良好的圖像品質能顯著提升辨識結果。呼叫 OCR 引擎前，請考慮以下事項：

- 將圖像轉為灰階。
- 提升對比度，使字符更突出。
- 使用二值化濾鏡去除背景噪聲。
- 將低解析度圖像調整至至少 300 dpi。

這些步驟屬於 **ocr image preprocessing**，可於呼叫 Aspose.OCR 前使用任何標準的 Java 影像函式庫完成。

## 匯入套件

完成前置作業後，將必要的套件匯入您的 Java 專案：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 步驟說明

### 步驟 1：設定文件目錄

定義一個資料夾，用於儲存 OCR 處理後的結果。此路徑稍後會用來定位圖像檔案。

```java
String dataDir = "Your Document Directory";
```

### 步驟 2：指定圖像路徑

將 API 指向您欲分析的圖像。

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 步驟 3：建立 Aspose.OCR 實例

使用您的授權金鑰實例化 OCR 引擎。金鑰可以是臨時或永久授權字串。

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 步驟 4：執行 OCR 辨識

呼叫 `RecognizeLine` 方法以從圖像中提取一行文字。結果為純文字字串，您可進一步處理或儲存。

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **專業提示：** 若需將輸出限制於特定字符集（例如僅限數字），請在呼叫 `RecognizeLine` 前於 `AsposeOCR` 實例上使用 `setAllowedCharacters` 方法。這可確保引擎忽略定義集合之外的字符。

## 常見問題與解決方案

| 問題 | 原因 | 解決方案 |
|-------|--------|-----|
| **沒有輸出或空字串** | 圖像路徑不正確或使用不支援的圖像格式 | 確認 `imagePath` 並使用支援的格式（JPEG、PNG、BMP） |
| **辨識錯誤** | 低解析度圖像或背景噪聲 | 在 OCR 前先前處理圖像（提升對比、二值化） |
| **授權未套用** | 缺少或無效的授權金鑰 | 確保授權字串正確且已放入 `AsposeOCR` 建構子中 |

## 常見問答

**Q: 如何取得 Aspose.OCR 的臨時授權？**  
A: 請前往 [temporary license page](https://purchase.aspose.com/temporary-license/) 申請試用授權。

**Q: 在哪裡可以找到 Aspose.OCR 的支援？**  
A: 加入 [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) 社群取得協助與討論。

**Q: 我可以在 Aspose.OCR 中指定允許的字符嗎？**  
A: 可以，使用 `setAllowedCharacters` API 來自訂字符集。詳情請參考官方文件。

**Q: Aspose.OCR 是否相容於最新的 JDK 版本？**  
A: 絕對相容——Aspose.OCR 會定期更新，以保持與最新 Java 版本相容。

**Q: 除了行辨識外，還有其他 OCR 功能嗎？**  
A: 有，函式庫支援區塊、段落與整頁辨識，亦提供語言包與圖像前處理選項。

## 結論

透過本 **aspose ocr java tutorial**，您已擁有可 **extract text from images** 且能控制辨識字符的完整解決方案。探索完整的 [documentation](https://reference.aspose.com/ocr/java/) 以發現多語言支援、自訂前處理與批次處理等進階功能。

---

**最後更新：** 2026-02-20  
**測試環境：** Aspose.OCR for Java 24.11  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}