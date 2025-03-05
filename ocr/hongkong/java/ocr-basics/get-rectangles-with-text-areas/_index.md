---
title: 在 Aspose.OCR 中取得帶有文字區域的矩形
linktitle: 在 Aspose.OCR 中取得帶有文字區域的矩形
second_title: Aspose.OCR Java API
description: 釋放 Aspose.OCR for Java 的強大功能。在本逐步指南中了解如何從圖像中無縫提取文字。立即下載以進行高效率的文字辨識。
type: docs
weight: 12
url: /zh-hant/java/ocr-basics/get-rectangles-with-text-areas/
---
## 介紹

您是否希望將強大的光學字元辨識 (OCR) 功能整合到您的 Java 應用程式中？ Aspose.OCR for Java 是您從圖像中準確且有效率地提取文字的首選解決方案。本教學將引導您完成使用 Aspose.OCR 取得帶有文字區域的矩形的過程，幫助您充分利用這個 Java OCR 庫的潛力。

## 先決條件

在深入學習本教程之前，請確保您具備以下先決條件：

- Java 開發環境：確保您的系統上安裝了 Java。
-  Aspose.OCR for Java Library：下載並設定 Aspose.OCR 函式庫。你可以找到下載鏈接[這裡](https://releases.aspose.com/ocr/java/).

## 導入包

在您的 Java 專案中，匯入必要的套件以利用 Aspose.OCR 的功能：

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 第 1 步：設定您的項目

確保您已準備好 Java 項目，並且整合了 Aspose.OCR 庫。

## 步驟2：定義文件目錄和映像路徑

```java
//文檔目錄的路徑。
String dataDir = "Your Document Directory";

//影像路徑
String imagePath = dataDir + "p3.png";
```

## 步驟3：建立Aspose.OCR實例

```java
//建立Aspose.OCR實例
AsposeOCR api = new AsposeOCR();
```

## 第四步：辨識圖像中的文本

```java
try {
    //透過文件的完整路徑識別頁面
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## 第 5 步：取得帶有文字區域的矩形

```java
//取得影像中帶有文字區域的矩形。
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

//列印每個文字區域矩形
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## 結論

在本教程中，您學習如何將 Aspose.OCR for Java 整合到您的專案中，以有效地從圖像中提取文字。 Aspose.OCR 簡化了 OCR 任務，提供準確的結果以實現無縫的使用者體驗。

## 常見問題解答

### Q1：Aspose.OCR 與 Java 11 相容嗎？

A1：是的，Aspose.OCR 與 Java 11 及更高版本相容。

### Q2：我可以將 Aspose.OCR 用於個人和商業專案嗎？

 A2：是的，Aspose.OCR 可用於個人和商業項目。有關許可詳細信息，請訪問[這裡](https://purchase.aspose.com/buy).

### Q3：如何取得 Aspose.OCR 的臨時許可證？

 A3：您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).

### Q4：哪裡可以找到對 Aspose.OCR 的支援？

A4：如需支持與討論，請訪問[Aspose.OCR 論壇](https://forum.aspose.com/c/ocr/16).

### Q5：Aspose.OCR支援多執行緒嗎？

A5：是的，Aspose.OCR 支援多線程，以提高並發環境中的效能。
