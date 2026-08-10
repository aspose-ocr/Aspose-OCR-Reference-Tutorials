---
category: general
date: 2026-06-28
description: 學習 Aspose OCR Java 範例，從圖像 Java 專案中提取文字，並設定 GPU 記憶體上限以獲得更快的結果。
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: zh-hant
og_description: Aspose OCR Java 範例，示範如何在設定 GPU 記憶體上限以獲得最佳效能的同時，從圖像中提取文字的 Java 程式碼。
og_title: Aspose OCR Java 範例 – 快速 GPU 加速文字提取
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Aspose OCR Java 範例 – 使用 GPU 從圖像提取文字
url: /zh-hant/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java 範例 – 使用 GPU 從圖像提取文字

有沒有想過如何在 **extract text from image Java** 應用程式中提取圖像文字，而不會把 CPU 磨到停不下來？你並不孤單。在許多實際情況下——例如收據掃描、身分驗證或大量文件歸檔——瓶頸往往是 OCR 引擎本身。

好消息：這個 **Aspose OCR Java example** 會一步步帶你完成一個完整、即時可執行的程式，利用 GPU 加速，甚至示範如何 **set GPU memory limit**，讓你的伺服器保持順暢。閱讀完本指南後，你將擁有一個可運作的 Java 類別，能讀取圖像檔案、在 GPU 上執行 OCR，並將辨識出的文字輸出到主控台。沒有模糊的說明，只有具體的程式碼與清晰的解釋。

我們將涵蓋從授權到 GPU 微調的所有內容，無論你是資深 Java 開發者還是剛涉足電腦視覺的新手，都能在此獲得價值。唯一的前置條件是具備 Java 開發環境（JDK 8 或更新版本）以及可支援 CUDA 或 OpenCL 的 GPU。

---

## 前置條件

- **Java Development Kit (JDK) 8+** – 你可以從 Oracle 或採用 OpenJDK 下載。  
- **Aspose.OCR for Java** 函式庫 – 從 Aspose 官方網站或 Maven Central 取得 JAR。  
- **有效的 Aspose OCR 授權檔** (`Aspose.OCR.Java.lic`)。免費試用可用於測試，但授權可移除評估水印。  
- **具備 CUDA 或 OpenCL 支援的 GPU** – 示範會自動偵測最佳模式，但需先安裝驅動程式。  
- **測試用圖像** – 清晰的收據、簽名或任何印刷文字的 PNG 或 JPEG。  

如果上述項目有任何不熟悉的，請勿驚慌。以下步驟會指引你至正確的下載連結，並說明檔案放置位置。

---

## 步驟 1：Aspose OCR Java Example – 設定專案

首先，建立一個新的 Maven 專案（或如果你偏好純 `javac`，則建立一個簡單資料夾）。在 `pom.xml` 中加入 Aspose OCR 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **專業提示：** Maven 會自動下載所有傳遞相依性，包括 GPU 支援函式庫，讓你不必額外搜尋 JAR。

將你的 `Aspose.OCR.Java.lic` 檔案放置於專案根目錄（或任何稍後會引用的資料夾）。我們正在建立的 **aspose ocr java example** 會預期授權路徑為 `"Aspose.OCR.Java.lic"`。

---

## 步驟 2：套用 Aspose OCR 授權

授權步驟至關重要——若未套用授權，OCR 引擎會以評估模式運作，且在輸出前加上水印。以下是你需要的最小程式碼：

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

在應用程式啟動時執行一次，即可確保 **所有後續的 OCR 呼叫** 均已完整授權。

---

## 步驟 3：設定 GPU 加速 – 設定 GPU 記憶體上限

現在來到有趣的部分：告訴 Aspose 使用 GPU，並可選擇 **set GPU memory limit**。此函式庫提供 `GpuEngineOptions`，讓你開關 GPU 模式、選擇裝置，並限制記憶體使用量。在共享伺服器上限制記憶體相當實用，避免 OCR 工作佔用整個 GPU。

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **為何要設定記憶體上限？** 若你的 OCR 任務涉及非常大的圖像或同時執行多個工作，GPU 可能很快耗盡 VRAM，導致當機。透過限制分配，你可以將程序維持在安全範圍內，讓其他工作負載和平共存。

---

## 步驟 4：Extract Text from Image Java – 載入圖像

在完成授權與 GPU 設定後，我們終於可以使用 **extract text from image Java** 程式碼。以下程式碼片段會使用 GPU 選項建立 `OcrEngine`、載入圖像檔案，並執行辨識。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**關鍵要點** 在此 **aspose ocr java example** 中：

- `OcrInput.add()` 可接受多張圖像；引擎會依序處理。  
- `ocrResult.getText()` 會回傳純文字字串，保留換行但不包含版面資訊。  
- 整個流程在 GPU 上執行，對於高解析度圖像而言，可比僅使用 CPU 快 **5‑10 倍**。

---

## 步驟 5：執行示範並驗證輸出

編譯並執行程式：

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

如果一切設定正確，你應該會看到類似以下的輸出：

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

具體文字取決於你的圖像，但重要的是主控台會印出 **辨識出的文字**，且不會出現「Evaluation version」水印。若遇到 `CUDA driver not found` 錯誤，請再次確認 GPU 驅動程式已更新，且 CUDA 工具組已加入系統路徑。

---

## 常見問題與避免方法

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `OutOfMemoryError: CUDA out of memory` | GPU 記憶體不足 | 降低 `setMemoryLimitMb`（例如 1024）或改以較小的圖像區塊處理。 |
| `LicenseException` | 授權檔遺失或路徑錯誤 | 確保 `Aspose.OCR.Java.lic` 可被存取且路徑正確。 |
| 未返回文字 | 圖像過於模糊或色彩空間不正確 | 在送入 OCR 前先前處理圖像（提升對比、轉為灰階）。 |
| GPU 未被使用 | `setEnableGpu(false)` 被設定或缺少驅動程式 | 確認 `gpuOptions.setEnableGpu(true)` 並重新安裝 GPU 驅動程式。 |

---

## 擴充範例

既然你已擁有完整的 **aspose ocr java example**，接下來可能想要：

- **批次處理資料夾** – 迴圈讀取檔案並將結果儲存至資料庫。  
- **偵測語言** – 使用 `ocrEngine.setLanguage(OcrLanguage.English)` 或加入多種語言。  
- **套用後處理** – 使用正規表達式清理原始字串，或送至拼寫檢查器。  

所有這些擴充功能皆重用相同的授權與 GPU 設定程式碼，只需加入業務邏輯即可。

---

## 最後的想法

你剛剛看到一個完整的 **aspose ocr java example**，它在 **extract text from image Java** 應用程式中，同時 **setting GPU memory limit**，提供穩健的效能。核心概念——提前授權、設定 GPU、載入圖像、讀取文字——可在無數專案中重複使用，從收據掃描器到自動表單輸入系統皆適用。

從此，你可以自由嘗試不同的 `GpuEngineOptions` 設定、使用更大的圖像，或將 OCR 步驟整合至 Spring Boot 微服務。只要有想像力，便無限制，而得益於 GPU 加速，效能上限遠高於以往。

有任何問題或需要協助微調特定硬體的記憶體設定嗎？在下方留下評論，我們會協助你。祝開發愉快！

---

![Aspose OCR Java 範例圖示，展示從圖像輸入 → GPU 加速 OCR → 文字輸出 的流程](https://example.com/images/aspose-ocr-java-example-diagram.png "aspose ocr java example 圖示")

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何在 Java 中設定授權並驗證 Aspose.OCR 授權](/ocr/english/java/ocr-basics/set-license/)
- [使用 Aspose.OCR 偵測區域模式在 Java 中提取圖像文字](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [在 Java 中使用 Aspose.OCR BufferedImage 將圖像轉換為文字](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}