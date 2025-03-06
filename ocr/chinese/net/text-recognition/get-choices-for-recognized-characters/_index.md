---
title: 在 OCR 图像识别中获取已识别字符的选择
linktitle: 在 OCR 图像识别中获取已识别字符的选择
second_title: Aspose.OCR .NET API
description: 使用 Aspose.OCR 增强您的 .NET 应用程序，以实现准确的字符识别。按照我们的分步指南检索图像识别中已识别字符的选择。
weight: 10
url: /zh/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 OCR 图像识别中获取已识别字符的选择

## 介绍

在当今的数字时代，释放光学字符识别 (OCR) 的力量至关重要，而 Aspose.OCR for .NET 是准确字符识别的强大解决方案。在本教程中，我们将深入研究一个特定功能：获取已识别字符的选择。在本指南结束时，您将将此功能无缝集成到您的 .NET 应用程序中。

## 先决条件

在深入学习本教程之前，请确保您具备以下先决条件：

- C# 和 .NET 开发的基础知识。
- Visual Studio 安装在您的计算机上。
-  Aspose.OCR for .NET 库，您可以下载[这里](https://releases.aspose.com/ocr/net/).

## 导入命名空间

在您的 C# 项目中，首先导入必要的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 第1步：初始化Aspose.OCR

首先初始化 Aspose.OCR 的实例：

```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";

//初始化 AsposeOcr 实例
AsposeOcr api = new AsposeOcr();
```

## 第2步：指定图像路径

设置要分析的图像的路径：

```csharp
//图像路径
string fullPath = dataDir + "sample.png";
```

## 第三步：识别图像

执行图像识别过程：

```csharp
//识别图像
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    //默认或自定义设置
});
```

## 第 4 步：获取已识别字符的选择

检索已识别字符的选择：

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## 第 5 步：打印结果

显示识别文本和选项：

```csharp
//打印结果
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

重复这些步骤，根据您的应用程序的要求进行自定义。

## 结论

在本教程中，我们探讨了如何利用 Aspose.OCR for .NET 来获取图像识别中已识别字符的选择。此功能为您的 OCR 功能增添了新的维度，增强了应用程序的多功能性。

## 常见问题解答

### Q1：Aspose.OCR for .NET适合大规模文档处理吗？

A1：当然！ Aspose.OCR for .NET 旨在高效、准确地处理大量文档。

### Q2：我可以在 Web 应用程序中使用 Aspose.OCR for .NET 吗？

A2：是的，您可以将 Aspose.OCR for .NET 集成到 Web 应用程序中，使其适用于各种开发场景。

### 问题 3：Aspose.OCR for .NET 有可用的许可选项吗？

 A3：是的，您可以探索许可选项并进行购买[这里](https://purchase.aspose.com/buy).

### 问题 4：如何获得有关 Aspose.OCR for .NET 的支持或提出问题？

 A4：访问[Aspose.OCR 论坛](https://forum.aspose.com/c/ocr/16)获得支持、提出问题并与社区建立联系。

### Q5：Aspose.OCR for .NET 有免费试用版吗？

 A5：是的，您可以免费试用[这里](https://releases.aspose.com/)体验 Aspose.OCR for .NET 的功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
