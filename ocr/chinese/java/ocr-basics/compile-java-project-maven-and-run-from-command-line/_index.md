---
category: general
date: 2026-10-18
description: 使用 Maven clean、compile 和 exec 命令在命令行编译 Java 项目并运行。学习如何高效构建和运行 Java 应用。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: zh
lastmod: 2026-10-18
og_description: 使用分步指南在命令行编译 Java 项目（Maven）并运行。掌握 Maven clean compile run，以构建和运行 Java
  应用。
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: 使用 Maven 编译 Java 项目 – 从命令行运行
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
title: 使用 Maven 编译 Java 项目并在命令行运行
url: /zh/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Maven 编译 Java 项目并从命令行运行

如果您需要 **compile java project maven** 并直接从终端启动生成的类，本指南将准确展示操作方法。教程结束时，您将能够清理旧的构件、编译源代码，并使用单个 Maven 命令链 **execute java class command line**。

本教程涵盖了使用 Maven **build and run java app** 所需的全部内容，包括必需的插件、常见陷阱以及针对 Windows 和 Unix Shell 的技巧。无需外部文档——只需按照以下步骤操作。

## 前置条件

* 已安装 Java Development Kit (JDK) 8 或更高版本，并已设置 `JAVA_HOME`。
* `PATH` 中可用 Apache Maven 3.6+。
* 包含 `pom.xml` 且拥有 `public static void main(String[] args)` 方法的 Java 类的 Maven 项目（本例中类为 `com.aspose.ocr.examples.SimpleOcrDemo`）。

## 编译 java 项目 maven

第一步是删除所有先前编译的类和其他构建产物。运行 `mvn clean` 可确保全新开始，防止过时的字节码导致运行时错误。

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*为什么要 clean？* Maven 将编译后的类存放在 `target/`。如果跳过 clean 阶段，旧的 `.class` 文件可能仍然存在，掩盖编译问题，尤其是在重构包名后。

## 执行 java 类 命令 行

清理后，编译源文件。Maven 的 `compile` 阶段会将所有 `src/main/java` 源码转换为字节码，并将结果放入 `target/classes`。

```bash
# Step 2: Compile the source code
mvn compile
```

现在您已经拥有可执行的 **maven compile source code** 输出。下一条命令将在无需单独 JAR 的情况下运行编译后的类。

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java` 目标属于 **maven clean compile run** 插件，可直接从编译输出目录启动指定类。这是在开发期间 **execute java class command line** 的最快方式。

### 预期输出

当示例成功运行时，您应该看到类似如下的输出：

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

如果收到 `ClassNotFoundException`，请再次检查全限定类名，并确保其位于 `src/main/java` 下。

## Maven clean compile run 工作流

将这三条命令组合在一起即可得到简洁、可重复的工作流：

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*为什么要链式执行？* 将这些阶段组合在一起可避免需要按 **Enter** 三次，并降低忘记某一步的风险。Maven 将按出现的顺序执行各阶段，确保在执行前进行 clean 构建。

### 提升工作流流畅度的技巧

| Tip | Description |
|-----|-------------|
| **使用 profile** | 定义一个 Maven profile，将 `clean`、`compile` 和 `exec:java` 捆绑在一起，这样您可以运行 `mvn demo` 而无需手动输入完整链。 |
| **添加 JVM 参数** | 传递 `-Dexec.args="-Xmx512m"` 以在内存密集型应用中增大堆大小。 |
| **跨平台** | 在 Windows 上使用 `mvn.cmd`，而在 Unix Shell 中使用 `mvn`。相同的命令在两种环境中均可工作。 |

## 使用 Maven 构建并运行 java 应用

如果您更倾向于可分发的产物，可以让 Maven 将编译后的类打包成可运行的 JAR，然后使用标准的 `java -jar` 命令执行：

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

当需要在未安装 Maven 的服务器上 **build and run java app** 时，此方法非常有用。然而，对于快速开发而言，**maven clean compile run** 序列更快，因为它省略了打包步骤。

## Maven 编译源代码 – 常见陷阱

尽管这些命令很直接，开发者仍常遇到以下问题：

1. **Missing `exec-maven-plugin`**  
   如果 Maven 找不到 `exec:java` 目标，请在 `pom.xml` 中添加该插件：

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
   Maven 编译到 `target/classes`。如果手动移动文件或更改默认输出目录，`exec:java` 目标可能找不到您的类。除非有特定原因，否则请保持默认布局。

3. **Using the wrong JDK version**  
   Maven 从 `JAVA_HOME` 继承 JDK。使用 JDK 11 编译源码而在 JDK 8 上运行会导致 `UnsupportedClassVersionError`。请使用 `java -version` 和 `mvn -v` 验证 JDK 版本。

4. **Shell quoting problems**  
   在 Unix 上，如果 `-Dexec.mainClass` 的值包含特殊字符，请使用单引号包裹：  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`。  
   在 Windows 上，双引号即可正常工作。

通过解决这些问题，您即可在任何环境中可靠地 **execute java class command line**。

## 专业提示：使用脚本自动化

对于经常重新构建示例的团队，创建一个小的 shell 或批处理脚本：

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

将其设为可执行 (`chmod +x run-demo.sh`) 并运行 `./run-demo.sh`。这可消除输入错误，确保每位开发者遵循精确的 **maven clean compile run** 序列。

## 结论

您现在已经了解如何使用 Maven 的 clean、compile 和 exec 目标 **compile java project maven** 并立即 **execute java class command line**。一步步的工作流确保全新构建，消除陈旧产物，并让您仅用一条命令 **build and run java app**。

接下来，您可以探索：

* 添加 **shade plugin** 以生成用于部署的 uber‑JAR。  
* 为不同环境（dev、test、prod）配置 Maven profiles。  
* 在编译步骤之前使用 `mvn test` 集成单元测试。

尝试这些变体，将工作流适配到您自己的项目中，您将拥有一个稳健、可重复的构建流水线，能够在 Windows、macOS 和 Linux 上运行。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 Java 中使用 OCR – 完整分步指南](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [使用 Java 对图像运行 OCR – 完整 Aspose OCR 指南](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [如何在 Java 中使用 Aspose OCR 执行 OCR – 分步指南](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}