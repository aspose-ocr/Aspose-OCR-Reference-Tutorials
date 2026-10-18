---
category: general
date: 2026-10-18
description: 使用 Maven 的 clean、compile 與 exec 命令，於命令列編譯 Java 專案並執行。學習如何高效建置與執行 Java
  應用程式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: zh-hant
lastmod: 2026-10-18
og_description: 編譯 Java 專案（使用 Maven）並從指令列執行，提供一步一步的指南。精通 Maven clean compile run，構建並執行
  Java 應用程式。
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: 編譯 Java 專案 Maven – 從命令列執行
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: 使用 Maven 編譯 Java 專案並從命令列執行
url: /zh-hant/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Maven 編譯 Java 專案並從命令列執行

如果你需要 **compile java project maven** 並直接從終端機啟動產生的類別，本指南會完整說明步驟。完成本教學後，你將能清除舊的產物、編譯原始碼，並使用單一 Maven 指令鏈 **execute java class command line**。

本教學涵蓋了使用 Maven **build and run java app** 所需的全部知識，包括必要的外掛程式、常見陷阱以及 Windows 與 Unix 系統 shell 的使用技巧。無需額外文件——只要依照以下步驟操作即可。

## Prerequisites

在開始之前，請確保你已具備：

* 已安裝 Java Development Kit (JDK) 8 或更新版本，且已設定 `JAVA_HOME`。
* Apache Maven 3.6+ 已加入 `PATH`。
* 一個 Maven 專案，內含 `pom.xml` 與具備 `public static void main(String[] args)` 方法的 Java 類別（本範例的類別為 `com.aspose.ocr.examples.SimpleOcrDemo`）。

## 編譯 Java 專案 (Maven)

第一步是移除先前編譯的類別及其他建置產物。執行 `mvn clean` 可確保全新開始，避免過時的位元組碼導致執行時錯誤。

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Why clean?* Maven 會將編譯好的類別存放於 `target/`。若省略 clean 階段，舊的 `.class` 檔案可能仍在，會隱藏編譯問題，尤其在重新命名套件後更是如此。

## 從命令列執行 Java 類別

清除完成後，編譯來源檔案。Maven 的 `compile` 階段會將所有 `src/main/java` 的原始碼轉譯成位元組碼，並放置於 `target/classes`。

```bash
# Step 2: Compile the source code
mvn compile
```

此時已產生可供執行的 **maven compile source code** 輸出。接下來的指令會直接執行編譯好的類別，無需額外的 JAR。

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java` 目標屬於 **maven clean compile run** 外掛，會直接從編譯輸出目錄啟動指定的類別。這是在開發期間最快的 **execute java class command line** 方式。

### 預期輸出

當示範成功執行時，你應該會看到類似以下的輸出：

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

若收到 `ClassNotFoundException`，請再次確認完整的類別名稱，並確保其位於 `src/main/java` 之下。

## Maven clean compile run 工作流程

將這三個指令結合起來即可得到簡潔且可重複的工作流程：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Why chain them?* 結合這些階段可免除三次按下 **Enter**，降低遺漏步驟的機會。Maven 會依照出現的順序執行各階段，確保在執行前完成乾淨的建置。

### 提升工作流程順暢度的技巧

| Tip | Description |
|-----|-------------|
| **Use a profile** | 定義一個 Maven profile，將 `clean`、`compile` 與 `exec:java` 打包在一起，這樣就能執行 `mvn demo`，而不必手動輸入完整指令鏈。 |
| **Add JVM options** | 傳入 `-Dexec.args="-Xmx512m"` 以提升記憶體需求較高的應用程式之堆積大小。 |
| **Cross‑platform** | 在 Windows 上使用 `mvn.cmd`，而 Unix shell 則使用 `mvn`。相同指令可在兩種環境中執行。 |

## 使用 Maven 建置與執行 Java 應用程式

如果你需要可分發的產物，可讓 Maven 將編譯好的類別打包成可執行的 JAR，然後使用標準的 `java -jar` 指令執行：

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

當需要在未安裝 Maven 的伺服器上 **build and run java app** 時，此方法相當有用。然而，對於快速開發而言，**maven clean compile run** 的流程更快，因為省略了打包步驟。

## Maven compile source code – 常見陷阱

即使指令相當簡單，開發者仍常會遇到以下問題：

1. **Missing `exec-maven-plugin`**  
   若 Maven 找不到 `exec:java` 目標，請在 `pom.xml` 中加入此外掛：

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven 會編譯至 `target/classes`。若手動搬移檔案或變更預設輸出目錄，`exec:java` 目標可能找不到你的類別。除非有特別需求，否則請保留預設目錄結構。

3. **Using the wrong JDK version**  
   Maven 會從 `JAVA_HOME` 繼承 JDK。若以 JDK 11 編譯原始碼卻在 JDK 8 上執行，會產生 `UnsupportedClassVersionError`。請使用 `java -version` 與 `mvn -v` 檢查 JDK 版本。

4. **Shell quoting problems**  
   在 Unix 系統上，若 `-Dexec.mainClass` 的值含有特殊字元，請以單引號包住：  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`。  
   在 Windows 上則可直接使用雙引號。

針對上述問題加以處理後，即可在任何環境中可靠地 **execute java class command line**。

## 專業提示：使用腳本自動化

對於需要頻繁重建示範的團隊，可建立一個小型 shell 或 batch 腳本：

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

將其設為可執行 (`chmod +x run-demo.sh`) 並執行 `./run-demo.sh`。此方式可避免輸入錯誤，確保每位開發者皆遵循相同的 **maven clean compile run** 流程。

## 結論

現在你已了解如何 **compile java project maven**，並使用 Maven 的 clean、compile 與 exec 目標即時 **execute java class command line**。一步一步的工作流程確保全新建置、消除過時產物，並能以單一指令 **build and run java app**。

接下來，你可以探索：

* 加入 **shade plugin** 以產生可部署的 uber‑JAR。
* 為不同環境（開發、測試、正式）設定 Maven profile。
* 在編譯步驟之前，使用 `mvn test` 整合單元測試。

嘗試這些變化，將工作流程套用到自己的專案中，你將擁有一套穩定、可重複的建置管線，能在 Windows、macOS 與 Linux 上順利運作。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}