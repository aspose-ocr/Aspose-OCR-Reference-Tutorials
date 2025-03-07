---
title: 在 Aspose.OCR 中透過語言選擇執行 OCR
linktitle: 在 Aspose.OCR 中透過語言選擇執行 OCR
second_title: Aspose.OCR Java API
description: 使用 Aspose.OCR for Java 從圖像中精確提取文字。請按照我們的逐步指南進行準確的 OCR 和語言選擇。
weight: 11
url: /zh-hant/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.OCR 中透過語言選擇執行 OCR

## 介紹

在不斷發展的技術領域，光學字元辨識 (OCR) 在從影像中提取有意義的資訊方面發揮關鍵作用。 Aspose.OCR for Java 是一款功能強大的工具，使開發人員能夠將 OCR 功能無縫整合到他們的 Java 應用程式中。在本逐步指南中，我們將探索如何使用 Aspose.OCR 執行 OCR 和語言選擇，從而釋放精確處理不同內容的潛力。

## 先決條件

在深入學習本教程之前，請確保您具備以下先決條件：

- Java 開發環境：確保您的系統上安裝了 Java，並且您的開發環境已設定。

-  Aspose.OCR 函式庫：下載並安裝適用於 Java 的 Aspose.OCR 函式庫。您可以找到該庫和相關文檔[這裡](https://reference.aspose.com/ocr/java/).

- 圖像檔案：準備一個包含要提取的文字的圖像檔案。例如，讓我們使用名為“p3.png”的檔案。

## 導入包

在您的 Java 專案中，匯入必要的套件以利用 Aspose.OCR 功能。在 Java 檔案的開頭新增以下行：

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

## 第 1 步：設定您的文件目錄

```java
//文檔目錄的路徑。
String dataDir = "Your Document Directory";
```

將「您的文件目錄」替換為圖片檔案所在目錄的實際路徑。

## 步驟2：定義影像路徑

```java
//影像路徑
String file = dataDir + "p3.png";
```

調整檔案變數以指向您的特定影像檔案。

## 步驟3：建立Aspose.OCR API實例

```java
//建立API實例
AsposeOCR api = new AsposeOCR();
```

初始化 AsposeOCR 物件以存取其功能。

## 第 4 步：設定識別選項

```java
//設定識別選項
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

根據您的要求自訂識別設定。調整傾斜、語言和識別區域等參數。

## 第 5 步：執行 OCR 並檢索結果

```java
//取得結果對象
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

使用指定的影像檔案和設定執行 OCR 操作。在 RecognitionResult 物件中擷取結果。

## 第 6 步：列印並使用結果

```java
//列印結果
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

列印提取的文字、識別區域、JSON 表示、傾斜角度和任何警告。根據您的應用程式的需要使用結果。

## 結論

在本教程中，我們深入研究了 Aspose.OCR for Java 的無縫集成，以透過語言選擇執行 OCR。這個強大的函式庫為旨在從圖像中準確提取文字的開發人員打開了一個充滿可能性的世界。

## 常見問題解答

### Q1：我可以在一次辨識過程中使用 Aspose.OCR 進行多種語言嗎？

A1：是的，您可以在識別設定中設定多種語言，以提高多語言內容的辨識準確性。

### Q2：如何使用 Aspose.OCR 處理不同的影像格式？

A2：Aspose.OCR支援多種影像格式，包括PNG、JPEG和TIFF。只需在影像路徑變數中提供正確的檔案路徑即可。

### Q3：Aspose.OCR 可以處理的圖片大小有限制嗎？

A3：Aspose.OCR可以處理不同尺寸的影像，但較大的影像可能需要更多的處理時間和資源。

### Q4：我可以微調影像中特定區域的辨識設定嗎？

A4：當然。利用 RecognitionAreas 功能定義影像中的特定矩形以進行目標辨識。

### Q5：Aspose.OCR 適合個人和商業項目嗎？

A5：是的，Aspose.OCR 提供靈活的授權選項，使其適合個人和商業用途。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
