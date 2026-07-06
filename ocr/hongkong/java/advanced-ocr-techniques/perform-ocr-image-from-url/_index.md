---
date: 2026-07-04
description: 了解如何使用 Aspose.OCR for Java 從 URL 擷取文字——高精度 OCR、多語言支援，且易於整合。
keywords:
- extract text from url
- url image to text
- java extract image text
linktitle: 在 Aspose.OCR for Java 中對來自 URL 的圖片執行 OCR
schemas:
- author: Aspose
  dateModified: '2026-07-04'
  description: Learn how to extract text from URL with Aspose.OCR for Java – high‑accuracy
    OCR, multi‑language support, and easy integration.
  headline: Extract text from URL using Aspose.OCR for Java
  type: TechArticle
- questions:
  - answer: Aspose.OCR delivers **high‑accuracy OCR**, typically exceeding 98 % character
      accuracy on clean printed documents when you define precise recognition areas
      and disable auto‑skew.
    question: How accurate is Aspose.OCR in recognizing text from images?
  - answer: Yes, the engine supports over 30 languages; simply load the appropriate
      language pack via `RecognitionSettings.setLanguage`.
    question: Can Aspose.OCR handle OCR multiple languages?
  - answer: Absolutely. Production use requires a commercial license; trial licenses
      impose page limits and embed a watermark. For purchasing a license, see the
      [Aspose purchase page](https://purchase.aspose.com/buy).
    question: Are there any licensing considerations for commercial projects?
  - answer: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community
      assistance, or obtain premium support with a temporary license from [Temporary
      License](https://purchase.aspose.com/temporary-license/).
    question: Where can I get help if I run into problems?
  - answer: Yes, you can download a fully‑featured trial from [releases.aspose.com](https://releases.aspose.com/)
      and evaluate all features without cost.
    question: Is a free trial available for Aspose.OCR for Java?
  type: FAQPage
second_title: Aspose.OCR Java API
title: 使用 Aspose.OCR for Java 從 URL 擷取文字
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-image-from-url/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR for Java 從 URL 提取文字

在本實作 **Aspose OCR Java 教程** 中，您將學會如何 **從 URL** 主持的圖片提取文字，只需幾行程式碼。完成本指南後，您將擁有一段可直接執行的 Java 程式碼，能從網路位址下載圖片，執行 Aspose.OCR 的高精度引擎，並回傳純文字與詳細的 JSON 中繼資料。此工作流程非常適合網路爬蟲、自動化文件管線，或任何需要將線上圖片轉換為可搜尋文字的系統。

## 快速解答
- **Aspose.OCR 能直接從 URL 讀取圖片嗎？** 是 – 呼叫 `RecognizePageFromUri`，函式庫會自行處理下載。  
- **引擎支援多語言嗎？** 當然；可透過 `RecognitionSettings.setLanguage` 載入所需語言包。  
- **OCR 的準確度如何？** 關閉 auto‑skew 並正確設定辨識區域時，Aspose.OCR 在乾淨的印刷文件上可達 >98 % 的字元準確率。  
- **最低需求是什麼？** Java 8+、Aspose.OCR for Java，以及生產環境的有效授權。  
- **如何套用授權？** 在任何 OCR 呼叫前使用 `License license = new License(); license.setLicense("Aspose.OCR.lic");`。

## 什麼是「從圖片提取文字」？

從圖片提取文字是指將視覺上的字元轉換為機器可讀的字串。Aspose.OCR 會讀取像素模式，對照語言模型，並以純文字、JSON 負載以及可選的區域結果回傳辨識出的字元。這讓您能在不需人工轉錄的情況下，儲存、索引或進一步處理內容。

## 為什麼使用 Aspose.OCR 進行高精度 OCR？

Aspose.OCR 支援 **50+ 輸入與輸出格式**——包括 PNG、JPEG、BMP、TIFF 與 PDF——同時透過串流大型檔案降低記憶體使用。基準測試顯示，它在 2.5 GHz CPU 上可於 12 秒內處理 300 頁 PDF，對印刷英文文字的準確率超過 **98 %**（前提是已定義辨識區域）。此純 Java 函式庫不需本機 DLL，且內建超過 30 種語言的語言包。

## 前置條件
- **Java Development Kit** – 已安裝並設定 JDK 8 或更新版本。  
- **IDE 或建置工具** – Maven、Gradle，或您偏好的任何 IDE。  
- **Aspose.OCR for Java** – 從官方 [Aspose.OCR 網站](https://reference.aspose.com/ocr/java/) 下載。  
- **有效授權** – 生產環境必須使用；免費試用可用於評估。  
- **商業授權** – 購買授權請前往 [Aspose 購買頁面](https://purchase.aspose.com/buy)。

## 步驟 1：建立 API 實例

`AsposeOCR` 類別是提供 OCR 功能的主要入口點。  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 步驟 2：定義圖片 URL

您可直接將圖片 URL 傳入 OCR 方法，函式庫會在內部處理下載。  

```java
AsposeOCR api = new AsposeOCR();
```

## 步驟 3：設定辨識選項

`RecognitionSettings` 讓您設定語言、auto‑skew 以及自訂辨識矩形。  

```java
String uri = "https://www.example.com/your-image.png";
```

## 步驟 4：執行 OCR

`RecognizePageFromUri` 會一次完成下載與 OCR，回傳結果物件。  

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Define recognition areas using rectangles
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## 步驟 5：列印結果

`RecognitionResult` 包含提取的文字、每個區域的字串，以及 JSON 摘要。  

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## 何時應該從網路圖片提取文字？

只要需要從視覺來源取得可搜尋、可索引的內容時，都應該從網路圖片提取文字——例如爬取商品目錄、保存新聞圖形、或將雲端儲存桶中的掃描 PDF 轉換。自動化此步驟可消除人工資料輸入、提升可及性，並讓您的數位資產支援全文搜尋。

## 如何使用 Aspose.OCR 從網路圖片提取文字？

將遠端圖片 URL 傳入 `RecognizePageFromUri`，依需求設定語言或區域，然後呼叫該方法。函式庫會下載圖片、執行 OCR 引擎，並在單一次呼叫中回傳辨識文字與 JSON 中繼資料，無需額外的網路程式碼。

## 常見問題與解決方案

| 問題 | 發生原因 | 解決方式 |
|------|----------|----------|
| **`recognitionText` 為空** | URL 錯誤或網路逾時。 | 確認 URL 可存取，並加入適當的例外處理。 |
| **雜訊字元** | 在旋轉的圖片上啟用了 auto‑skew。 | 保留 `settings.setAutoSkew(false)` 或提供正確的旋轉資訊。 |
| **缺少語言支援** | 預設語言包僅包含英文。 | 透過 `settings.setLanguage("fra")`（或其他 ISO 代碼）載入額外語言包。 |
| **授權未套用** | 試用模式可能限制頁數。 | 使用 `License license = new License(); license.setLicense("Aspose.OCR.lic");` 套用有效授權。 |

## 常見問答

**問：Aspose.OCR 從圖片辨識文字的準確度如何？**  
**答：** Aspose.OCR 提供 **高精度 OCR**，在乾淨的印刷文件上，若定義精確的辨識區域並關閉 auto‑skew，通常可超過 98 % 的字元準確率。

**問：Aspose.OCR 能處理多語言 OCR 嗎？**  
**答：** 可以，引擎支援超過 30 種語言；只需透過 `RecognitionSettings.setLanguage` 載入相應語言包。

**問：商業專案有什麼授權考量？**  
**答：** 必須購買商業授權才能在生產環境使用；試用授權會限制頁數並加上浮水印。購買授權請參閱 [Aspose 購買頁面](https://purchase.aspose.com/buy)。

**問：如果遇到問題該向哪裡求助？**  
**答：** 可前往 [Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16) 尋求社群協助，或使用臨時授權取得高級支援，詳情請見 [Temporary License](https://purchase.aspose.com/temporary-license/)。

**問：Aspose.OCR for Java 有免費試用嗎？**  
**答：** 有，您可從 [releases.aspose.com](https://releases.aspose.com/) 下載完整功能的試用版，免費評估所有功能。

---

**最後更新：** 2026-07-04  
**測試環境：** Aspose.OCR 24.11 for Java  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [提取文字圖片 – Aspose.OCR for Java OCR 基礎](/ocr/java/ocr-basics/)
- [使用 Aspose.OCR 偵測區域模式從 Java 圖片提取文字](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [使用 Aspose.OCR 以語言辨識圖片文字](/ocr/java/ocr-operations/perform-ocr-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```