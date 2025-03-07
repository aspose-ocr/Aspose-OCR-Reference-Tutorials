---
title: 在 Aspose.OCR for Java 中對來自 URL 的映像執行 OCR
linktitle: 在 Aspose.OCR for Java 中對來自 URL 的映像執行 OCR
second_title: Aspose.OCR Java API
description: 使用 Aspose.OCR 在 Java 中解鎖無縫圖像文字擷取。高精度 OCR，易於整合。
weight: 11
url: /zh-hant/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.OCR for Java 中對來自 URL 的映像執行 OCR

## 介紹

歡迎閱讀我們關於使用 Aspose.OCR for Java 對 URL 中的圖像執行光學字元辨識 (OCR) 的逐步指南。本教學旨在幫助您將 Aspose.OCR 無縫整合到您的 Java 應用程式中，讓您輕鬆從圖像中提取文字。 Aspose.OCR 是一個功能強大的 OCR 庫，支援各種圖像格式，使其成為需要文字擷取的應用程式的寶貴工具。

## 先決條件

在深入學習本教程之前，請確保您符合以下先決條件：

1. Java 開發環境：確保您的電腦上設定了有效的 Java 開發環境。

2.  Aspose.OCR 函式庫：下載並安裝 Aspose.OCR for Java 函式庫。您可以在以下位置找到該庫和相關文檔[Aspose.OCR 網站](https://reference.aspose.com/ocr/java/).

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

## 步驟1：建立API實例

初始化 AsposeOCR 類別的實例：

```java
AsposeOCR api = new AsposeOCR();
```

## 第 2 步：定義圖像 URL

指定要執行 OCR 的圖像的 URL：

```java
String uri = "https://www.example.com/your-image.png」；
```

## 第 3 步：設定識別選項

配置識別設置，例如停用自動傾斜和定義識別區域：

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

//使用矩形定義識別區域
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## 第 4 步：執行 OCR

呼叫OCR識別流程：

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## 第 5 步：列印結果

顯示識別結果，包括提取的文字、識別區域文字、JSON 輸出和任何警告：

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

重複這些步驟，將 Aspose.OCR 整合到您的 Java 應用程式中，並從圖像中精確提取文字。

## 結論

總而言之，利用 Aspose.OCR for Java 為 OCR 任務提供了強大的解決方案，使開發人員能夠從圖像中無縫提取文字。逐步指南可確保整合過程順利進行，適合各個層級的開發人員使用。

## 常見問題解答

### Q1：Aspose.OCR 從圖像中辨識文字的準確度如何？

A1：Aspose.OCR 提供高精度的文字識別，特別是在配置了精確的識別區域時。

### Q2：Aspose.OCR在OCR辨識時可以處理多種語言嗎？

A2：是的，Aspose.OCR 支援多種語言的文字識別，為不同的應用提供了多功能性。

### Q3：在商業項目中使用 Aspose.OCR 是否有任何許可注意事項？

A3：是的，確保遵守商業用途的 Aspose.OCR 授權條款。參考[購買.aspose.com](https://purchase.aspose.com/buy)了解許可詳細資訊。

### Q4：如何獲得 Aspose.OCR 相關問題的支援？

 A4：訪問[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16)以獲得社區支持和討論。如需進階支持，請考慮從以下機構取得臨時許可證[臨時執照](https://purchase.aspose.com/temporary-license/).

### Q5：Aspose.OCR for Java 有免費試用版嗎？

 A5：是的，透過以下網址的免費試用版探索 Aspose.OCR 的功能：[發布.aspose.com](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
