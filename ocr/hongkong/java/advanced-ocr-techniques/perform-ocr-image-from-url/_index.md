---
date: 2025-12-18
description: 解鎖在 Java 中使用 Aspose.OCR 無縫提取圖像文字的功能。高準確度 OCR，輕鬆整合。
linktitle: Performing OCR on Image from URL in Aspose.OCR for Java
second_title: Aspose.OCR Java API
title: 如何使用 Aspose.OCR for Java 從 URL 中的圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-image-from-url/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 URL 使用 Aspose.OCR for Java 提取圖像文字

## 介紹

在本步驟式 **aspose ocr java tutorial** 中，您將學習如何 **從圖像檔案提取文字**，這些檔案位於網路上。完成本指南後，您將擁有一段可從 URL 取得圖像、執行高精度 OCR，並返回識別文字及有用 JSON 中繼資料的 Java 程式碼片段。此方法非常適合網路爬蟲、文件處理管線，或任何需要從遠端圖片讀取文字的應用程式。

## 快速解答
- **Aspose.OCR 能從圖像 URL 提取文字嗎？** 是 – 使用 `RecognizePageFromUri`。  
- **它支援多語言 OCR 嗎？** 當然；您可以在設定中設定語言套件。  
- **OCR 的精確度高嗎？** 在正確的識別區域且停用 auto‑skew 的情況下，精確度屬於同類最佳。  
- **開始前需要什麼？** Java 8+、Aspose.OCR for Java，以及生產環境的有效授權。  
- **如何處理授權？** 請參閱下方 *aspose ocr licensing* 章節了解詳情。

## 什麼是“從圖像中提取文字”？

從圖像提取文字是指將字符的視覺表示轉換為機器可讀的字串。OCR（光學字符識別）引擎會分析像素模式，辨識字符形狀，並輸出純文字，您可以將其儲存、搜尋或以程式方式操作。

## 為什麼選擇 Aspose.OCR 來實現高精度 OCR？

Aspose.OCR 提供 **高精度 OCR** 引擎，支援廣泛的圖像格式、自訂識別區域及語言套件。此函式庫為全託管型，無需原生相依性，且能與 Java 專案順利整合——是企業級文字提取的可靠選擇。

## 先決條件

1. **Java 開發環境** – 可運作的 JDK（8 或更新）以及您選擇的 IDE 或建置工具。  
2. **Aspose.OCR 函式庫** – 下載並安裝 Aspose.OCR for Java 函式庫。您可於 [Aspose.OCR website](https://reference.aspose.com/ocr/java/) 找到函式庫及相關文件。  

## 導入包

在您的 Java 專案中，匯入 Aspose.OCR 所需的套件：

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

## 步驟 1：建立 API 實例

初始化 `AsposeOCR` 類別的實例：

```java
AsposeOCR api = new AsposeOCR();
```

## 步驟 2：定義圖片 URL
指定您想要執行 OCR 的圖像 URL：

```java
String uri = "https://www.example.com/your-image.png";
```

## 步驟 3：設定識別選項

設定識別參數，例如停用 auto‑skew 以及定義識別區域：

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Define recognition areas using rectangles
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## 步驟 4：執行 OCR

呼叫 OCR 識別程序：

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## 步驟 5：列印結果

顯示識別結果，包括提取的文字、識別區域文字、JSON 輸出以及任何警告：

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

重複上述步驟，即可將 Aspose.OCR 整合至您的 Java 應用程式，並精確地從圖像提取文字。

## 常見問題及解決方案

| 問題 | 為何發生 | 解決方案 |
|-------|----------------|-----|
| **空的“識別文本”** | URL 錯誤或網路逾時。 | 確認 URL 可存取，並加入適當的例外處理。 |
| **亂碼字符** | 旋轉圖像仍啟用 auto‑skew。 | 保持 `settings.setAutoSkew(false)` 或提供正確的旋轉資訊。 |
| **缺少語言支持** | 預設語言套件僅包含英文。 | 透過 `settings.setLanguage("fra")`（或其他 ISO 代碼）載入額外語言套件。 |
| **未應用許可證** | 試用模式可能限制頁數。 | 使用 `License license = new License(); license.setLicense("Aspose.OCR.lic");` 套用有效授權。 |

## 常見問題解答

**Q: Aspose.OCR 在圖像文字辨識上的精確度如何？**  
A: Aspose.OCR 提供 **高精度 OCR**，特別是當您定義精確的識別區域並停用 auto‑skew 時。

**Q: Aspose.OCR 能處理多語言 OCR 嗎？**  
A: 能，該引擎支援多種語言；您只需在 `RecognitionSettings` 中載入相應的語言套件。

**Q: 在商業專案中使用 Aspose.OCR 有授權考量嗎？**  
A: 當然。請檢視 **aspose ocr licensing** 細節，並從 [purchase.aspose.com](https://purchase.aspose.com/buy) 取得商業授權。

**Q: 如何取得 Aspose.OCR 相關問題的支援？**  
A: 前往 [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) 取得社群協助，或從 [Temporary License](https://purchase.aspose.com/temporary-license/) 獲得臨時授權以取得高級支援。

**Q: 是否有 Aspose.OCR for Java 的免費試用？**  
A: 有，您可於 [releases.aspose.com](https://releases.aspose.com/) 取得免費試用，探索完整功能。

## 結論

利用 Aspose.OCR for Java，您可以獲得 **強大且高精度的 OCR** 解決方案，能夠快速且可靠地 **從圖像 URL 提取文字**。依照上述步驟操作，調整識別設定以符合您的文件版面，即可將強大的文字提取功能整合至任何基於 Java 的工作流程中。

---

**最後更新：** 2025-12-18  
**測試版本：** Aspose.OCR 24.11 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}