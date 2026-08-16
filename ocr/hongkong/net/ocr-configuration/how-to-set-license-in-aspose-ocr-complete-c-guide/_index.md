---
category: general
date: 2026-04-06
description: 如何在 Aspose OCR 中使用 C# 設定授權 – 只需幾個步驟，即可學習如何嵌入資源、取得嵌入資源，並從檔案或串流載入授權。
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: zh-hant
og_description: 一步一步說明如何在 Aspose OCR 中設定授權。了解如何嵌入授權、取得授權，以及使用授權串流以實現無縫整合。
og_title: 如何在 Aspose OCR 中設定授權 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- .NET licensing
title: 如何在 Aspose OCR 中設定授權 – 完整 C# 指南
url: /zh-hant/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose OCR 中設定授權 – 完整 C# 指南

在 Aspose OCR 中設定授權是開發人員常見的障礙。在本教學中，我們將逐步說明設定授權、將其嵌入為資源，以及從串流載入的完整步驟，讓你可以在沒有惱人的試用模式浮水印下開始進行 OCR。

有沒有遇過執行 OCR 工作時，只看到「Evaluation version」的橫幅？那是授權遺失或未正確套用的徵兆。完成本指南後，你將擁有完整授權的 Aspose OCR 實例，無論是將 `.lic` 檔案與二進位檔案放在同一目錄，或是隱藏在組件內部。

## 您需要的條件

- **Aspose.OCR for .NET**（撰寫本文時的最新 NuGet 套件 – 23.10）
- 一個 **有效的 Aspose OCR 授權檔案** (`Aspose.OCR.lic`)
- Visual Studio 2022 或任何相容 C# 的 IDE
- 具備 .NET 資源嵌入的基本概念（我們會說明）

不需要額外的第三方函式庫；所有功能皆包含於 Aspose 套件內。

![設定授權說明圖](image.png "如何設定授權")

## 步驟 1：安裝 Aspose.OCR NuGet 套件

在撰寫任何授權程式碼之前，請先確保已參考此函式庫：

```bash
dotnet add package Aspose.OCR
```

或是透過 Visual Studio 的 NuGet 管理員，搜尋 **Aspose.OCR** 並點選 *Install*。這會將 `Aspose.OCR.dll` 及其相依性下載至專案。

> **專業提示：** 目標設定為 .NET 6 或更新版本，可享有最新的 API 介面與更佳效能。

## 步驟 2：建立 License 物件 – 「如何設定授權」的核心

Aspose 使用簡單的 `License` 類別來套用商業金鑰。建立此物件是任何授權工作流程的第一步：

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

為什麼這很重要：`License` 例項會讀取 `.lic` 內容，並在目前的 AppDomain 中全域註冊。註冊後，你建立的每個 `OcrEngine` 都會以完整功能模式運作。

## 步驟 3：從檔案套用授權（傳統的「如何載入授權」）

如果你想把授權檔案放在執行檔旁邊，只需以檔案路徑呼叫 `SetLicense`：

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### 注意事項

- **絕對路徑與相對路徑：** 相對路徑會以行程的 *working directory* 為基準，通常是 bin 資料夾。
- **檔案權限：** 執行應用程式的帳號必須具備讀取 `.lic` 檔案的權限。
- **例外處理：** 若路徑錯誤，`SetLicense` 會拋出 `FileNotFoundException`，因此建議以 `try/catch` 包住，以免程式直接失敗。

## 步驟 4：如何嵌入資源 – 將授權隱藏於組件內

將授權嵌入可免除額外檔案的部署需求。以下說明如何 **how to embed resource** 到 .NET 專案：

1. 將 `.lic` 檔案加入專案（例如放在 `Resources` 資料夾下）。
2. 右鍵點擊該檔案 → *Properties* → 將 **Build Action** 設為 **Embedded Resource**。
3. 編譯專案；授權即成為編譯後 DLL 的一部份。

現在你可以使用 **get embedded resource** 的程式碼取得它。

## 步驟 5：取得嵌入資源串流

以下程式碼示範如何使用 **get embedded resource** 搭配反射。請依你的專案命名空間與資源名稱調整：

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **為什麼使用反射？** `Assembly.GetExecutingAssembly()` 會指向目前執行的組件，確保程式在 console app、網站或 Azure Function 中皆能正常運作。

## 步驟 6：使用授權串流 – 「use license stream」模式

取得串流後，使用 **use license stream** 直接套用授權，無需觸碰檔案系統：

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

當 `SetLicense` 接收到 `Stream` 時，Aspose 會直接讀取位元組、註冊授權，並在離開 `using` 區塊時釋放串流。這是最乾淨的隱藏授權方式。

### 完整範例程式

將所有步驟整合，以下是一個自包含的程式，示範檔案、嵌入資源與串流三種方式。只需將不需要的區段註解掉即可。

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**預期輸出**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

如果授權未成功套用，Aspose 會拋出 `LicenseException`，或在 OCR 結果中看到評估浮水印。

## 常見陷阱與避免方式

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 「Evaluation version」橫幅仍然出現 | 授權未載入或路徑錯誤 | 再次確認檔案路徑或嵌入資源名稱。 |
| `NullReferenceException` 發生於 `GetManifestResourceStream` | 資源名稱拼寫錯誤或 Build Action 未設為 Embedded Resource | 檢查完整的命名空間限定名稱，並確保 Build Action 正確設定。 |
| 本機測試授權正常，但部署後失效 | 伺服器缺少讀取權限 | 為應用程式池身分授予 `.lic` 檔案的讀取權限，或改用嵌入資源方式。 |
| 建立多個 `License` 物件卻無效 | 在第一次之後對不同的實例呼叫 `SetLicense` | 每個 AppDomain 只保留單一 `License` 例項；在啟動時呼叫一次即可，或重複使用同一實例。 |

## 何時選擇各種方式

- **檔案式** – 快速原型開發，無需重新編譯即可替換。
- **嵌入資源** – 適用於桌面或函式庫發佈，避免授權檔案外露。
- **串流式** – 完美適用於雲端環境（Azure Functions、AWS Lambda），可從安全保管庫取得授權並直接傳入。

## 往後步驟 – 擴展授權知識

既然已掌握 **how to set license**，你可以進一步探索：

- **How to embed resource** 在更複雜的多專案解決方案中使用。
- 從衛星組件取得 **Get embedded resource**，以支援在地化情境。
- 從 Azure Key Vault 或 AWS Secrets Manager **How to load license** 動態載入授權。
- 結合依賴注入使用 **Use license stream**，讓啟動程式碼更簡潔。

上述主題皆以本教學的基礎為出發點，協助你打造既安全又易於維護的授權策略。

---

### 簡要重點

我們已示範 **how to set license** 在 Aspose OCR 中的三種可靠技巧：從檔案載入、將 `.lic` 嵌入為資源、以及透過串流套用。遵循程式碼、留意常見陷阱，你的 OCR 引擎即可全速運作——不會出現試用浮水印，也不會有意外情況。

祝開發順利，願你的 OCR 結果晶瑩剔透！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}