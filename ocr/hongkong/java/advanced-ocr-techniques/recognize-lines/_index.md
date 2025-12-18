---
date: 2025-12-09
description: 學習 Aspose OCR Java 範例，從圖像 Java 專案中提取文字。輕鬆整合，為 Java 應用程式提供高精度 OCR。
linktitle: Aspose OCR Java Example – Recognizing Lines in Images
second_title: Aspose.OCR Java API
title: Aspose OCR Java 範例 – 識別圖像中的行
url: /zh-hant/java/advanced-ocr-techniques/recognize-lines/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java 範例 – 識別圖像中的行

## 介紹

如果您需要一個 **aspose ocr java example** 能快速從圖像中提取文字，您來對地方了。在本教學中，我們將逐步說明一個完整、可直接執行的 Java 程式，使用 Aspose.OCR for Java 識別單行文字。完成後，您將了解為何 Aspose OCR 是 Java 開發者的可靠選擇，以及如何將行級別的識別整合到任何應用程式中。

## 快速回答
- **範例的功能是什麼？** 識別提供之圖像中的單行文字。  
- **需要哪個函式庫？** Aspose.OCR for Java（最新版本）。  
- **需要授權嗎？** 開發階段可使用免費試用版；正式上線需購買商業授權。  
- **可以從任何圖像格式提取文字嗎？** 可以——支援 JPEG、PNG、TIFF、BMP 等多種格式。  
- **實作需要多長時間？** 大約 10‑15 分鐘，完成路徑設定後即可執行。

## 什麼是 Aspose OCR Java 範例？
**aspose ocr java example** 是一段簡潔的程式碼範例，示範如何在 Java 中呼叫 Aspose.OCR API。它展示了關鍵步驟——環境設定、辨識設定配置，以及取得辨識結果——讓您能輕鬆套用到自己的專案。

## 為什麼使用 Aspose OCR for Java 來 *extract text image java*？
- **高準確度** – 先進演算法能處理噪點或低解析度的圖像。  
- **多格式支援** – 支援 JPEG、PNG、TIFF、BMP、GIF 等。  
- **簡易 API** – 只需少量程式碼即可取得可靠結果。  
- **可擴充** – 適用於桌面工具、伺服器端服務或行動後端。

## 前置條件
在開始之前，請確保您已具備：

1. **Java Development Kit (JDK)** – 已安裝 8 版或更新版本，並完成設定。  
2. **Aspose.OCR for Java 函式庫** – 從官方頁面下載最新 JAR [here](https://releases.aspose.com/ocr/java/)。  
3. **一張包含欲辨識文字的圖像檔**。請在程式碼中將 `imagePath` 變數指向此檔案。

## 步驟說明

### 步驟 1：匯入套件
首先，匯入所需的 Aspose.OCR 類別與標準 Java 工具。

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

### 步驟 2：設定文件目錄
定義存放圖像檔的資料夾。

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

將 `"Your Document Directory"` 替換為測試圖像所在的絕對路徑。

### 步驟 3：設定圖像路徑
讓 OCR 引擎指向您要處理的特定圖像。

```java
// The image path
String imagePath = dataDir + "0001460985.Jpeg";
```

自行修改檔名以符合您的圖像檔案。

### 步驟 4：建立 API 實例
實例化主要的 OCR 類別——此物件提供辨識方法。

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### 步驟 5：配置辨識設定
告訴 Aspose.OCR 您的需求。本範例啟用 **單行** 辨識。

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setRecognizeSingleLine(true);
```

若需偵測多行，請改為 `setRecognizeSingleLine(false)`。

### 步驟 6：執行 OCR 辨識
執行 OCR 引擎，並將辨識出的行文字輸出至主控台。

```java
RecognitionResult result = api.RecognizePage(imagePath, settings);
System.out.println("File: " + imagePath);
System.out.println("Result line: " + result.recognitionText);
```

執行程式後，您應該會看到檔案路徑以及提取出的文字行。

## 常見問題與解決方案
| 問題 | 解決方案 |
|-------|----------|
| **`java.lang.NoClassDefFoundError`** | 確認已將 Aspose.OCR JAR 加入專案的 classpath。 |
| **輸出為空白** | 檢查圖像是否包含清晰、水平的文字行，且 `setRecognizeSingleLine(true)` 符合您的情境。 |
| **不支援的圖像格式** | 在處理前將圖像轉換為支援的格式（如 JPEG 或 PNG）。 |
| **大型圖像效能下降** | 在 OCR 前將圖像大小或解析度調整至合理範圍（寬度 ≤ 1500 px）。 |

## 常見問答

**Q: Aspose.OCR 能辨識圖像中的多行文字嗎？**  
A: 能。將 `settings.setRecognizeSingleLine(false)` 即可啟用多行偵測。

**Q: 支援哪些圖像格式？**  
A: 完全支援 JPEG、PNG、TIFF、BMP、GIF 以及其他多種格式。

**Q: 文字提取的準確度如何？**  
A: 由於採用專有辨識引擎，Aspose.OCR 在清晰、高解析度的圖像上可提供極高的準確度。

**Q: 可以在 Web 應用程式中使用此函式庫嗎？**  
A: 當然可以。相同的 Java 程式碼可在 Spring Boot、Tomcat 或任何 Servlet 容器等伺服器端環境執行。

**Q: 有提供試用版嗎？**  
A: 有。可從 Aspose 官方網站 [here](https://releases.aspose.com/) 下載免費試用版。試用版功能完整，但會在輸出中加入小水印。

---

**最後更新時間：** 2025-12-09  
**測試環境：** Aspose.OCR for Java 24.11（撰寫時最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}