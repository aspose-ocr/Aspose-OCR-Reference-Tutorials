---
date: 2026-05-24
description: 了解如何在 Java 中使用 Aspose.OCR 的 OCR 功能，從圖像中提取文字、設定允許的字符，並在數分鐘內套用臨時授權。
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: 在 Aspose.OCR 中指定允許的字符
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: 如何使用 OCR – 使用 Aspose.OCR 從圖像中提取文字
url: /zh-hant/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR – 使用 Aspose.OCR 從圖像提取文字

在現代 Java 應用程式中，**如何使用 OCR** 是常見問題，尤其是當您需要將掃描的發票、收據或列印表單轉換為可搜尋的文字時。本教學將帶您完成完整的 **Aspose.OCR for Java** 範例：從圖像提取文字、限制輸出為自訂字元集，並套用臨時授權以快速評估。

## 快速解答
- **Aspose.OCR 的功能是什麼？** 它能高精度地從圖像中提取文字，且允許限制辨識的字元。  
- **我需要授權嗎？** 生產環境必須使用臨時或永久授權；臨時金鑰可移除浮水印。  
- **支援哪個 JDK 版本？** 此函式庫相容於最新的 JDK 版本（JDK 17、19、21）。  
- **我可以限制辨識的字元嗎？** 可以——使用 `setAllowedCharacters` 方法即可限制輸出。  
- **設定需要多久？** 基本的端對端實作大約需要 10‑15 分鐘。

## 什麼是「從圖像提取文字」？
從圖像提取文字，也稱為光學字符辨識（OCR），將視覺字符——無論是列印、手寫或打字——轉換為機器可讀的字串。此轉換使應用程式能以程式方式搜尋、索引、編輯與分析內容，支援如發票處理、文件歸檔與資料輸入自動化等工作流程。

## 為什麼要在 Java 中使用 Aspose.OCR？
Aspose.OCR 支援 **60+ 種語言**，可處理最高 **10 MB** 的圖像而不需將整個檔案載入記憶體，且在乾淨的掃描件上提供 **>95 % 的準確率**。此函式庫為自包含式，不需外部 OCR 引擎，簡化部署並降低授權成本。

## 先決條件

### Java Development Kit (JDK)

請確保已安裝最新的 Java Development Kit。您可以從 [此處](https://www.oracle.com/java/technologies/javase-downloads.html) 下載。

### Aspose.OCR for Java 程式庫

從 [下載連結](https://releases.aspose.com/ocr/java/) 下載並安裝 Aspose.OCR for Java 程式庫。

### Aspose.OCR 授權

若要解鎖全部功能，請取得授權。您可從 [此處](https://purchase.aspose.com/buy) 購買，或申請 [臨時授權](https://purchase.aspose.com/temporary-license/) 以供試用。

## 如何在 Java 中使用 Aspose.OCR 進行 OCR？

載入圖像、設定 OCR 引擎，並呼叫辨識方法——只需幾行簡單程式碼。本段落直接告訴您要怎麼做：建立帶有授權字串的 `AsposeOCR` 實例、設定允許的字元（如需），然後對目標圖像呼叫 `RecognizeLine` 取得提取的文字。API 會在內部處理圖像前置處理，讓您無需額外程式碼即可得到乾淨的結果。

### 匯入套件

`AsposeOCR` 類別位於 `com.aspose.ocr` 套件。請先匯入所需類別。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## 逐步指南

### 步驟 1：設定文件目錄

選擇一個資料夾，用於儲存 OCR 結果與暫存檔。此路徑稍後會用來定位要處理的圖像。

```java
String dataDir = "Your Document Directory";
```

### 步驟 2：指定圖像路徑

提供完整的檔案系統路徑或 class‑path 資源位置，指向您要分析的圖像。

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### 步驟 3：建立 Aspose.OCR 實例

`AsposeOCR` 是執行光學字符辨識的核心引擎。以臨時或永久授權字串實例化它。

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### 步驟 4：執行 OCR 辨識

`RecognizeLine` 從提供的圖像中提取單行文字，並以純 Java `String` 回傳。對於多行文件，您可以重複呼叫此方法。

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **專業提示：** 若需將輸出限制為純數字（例如發票號碼），請在呼叫 `RecognizeLine` 前於 `AsposeOCR` 實例上執行 `setAllowedCharacters("0123456789")`。此方法會強制引擎忽略任何非數字符號。  
> `setAllowedCharacters` 為 `AsposeOCR` 的方法，用於將 OCR 輸出限制在指定的白名單字元集合中。

## 常見問題與解決方案

| 問題 | 原因 | 解決方法 |
|-------|--------|-----|
| **沒有輸出或空字串** | 圖像路徑不正確或不支援的格式 | 確認 `imagePath` 並使用支援的格式（JPEG、PNG、BMP） |
| **辨識錯誤** | 低解析度圖像或雜訊背景 | 在 OCR 前先處理圖像（提升對比度、二值化） |
| **授權未套用** | 缺少或無效的授權金鑰 | 確保授權字串正確且已傳遞給 `AsposeOCR` 建構子 |

## 常見問答

**問：我該如何取得 Aspose.OCR 的臨時授權？**  
答：前往 [臨時授權頁面](https://purchase.aspose.com/temporary-license/) 申請可移除評估浮水印的試用金鑰。

**問：我可以在哪裡找到 Aspose.OCR 的支援？**  
答：加入 [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) 社群，獲取協助與討論。

**問：我可以在 Aspose.OCR 中指定允許的字元嗎？**  
答：可以，使用 `setAllowedCharacters` API 定義自訂的字元白名單，特別適用於僅限數字的欄位。

**問：Aspose.OCR 是否相容於最新的 JDK 版本？**  
答：絕對相容——Aspose.OCR 會定期更新，以保持與最新 Java 版本的相容性。

**問：除了行辨識外，還有其他 OCR 功能嗎？**  
答：此函式庫亦支援區塊、段落與整頁辨識、語言套件以及進階圖像前置處理。

## 結論

透過本 **Aspose OCR Java 教學**，您已掌握 **如何使用 OCR** 從圖像提取文字、限制字元集，並套用臨時授權以快速測試。深入閱讀完整的 [文件說明](https://reference.aspose.com/ocr/java/) 以探索多語言支援、批次處理與自訂前置處理管線。

---

**Last Updated:** 2026-05-24  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [如何在 Java 中設定授權並驗證 Aspose.OCR 授權](/ocr/java/ocr-basics/set-license/)
- [在 Java 中使用 Aspose.OCR BufferedImage 將圖像轉換為文字](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java 範例 – 辨識圖像中的行](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}