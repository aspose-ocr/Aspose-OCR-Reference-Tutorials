---
category: general
date: 2026-10-11
description: Aprenda a realizar OCR em imagens em C# com Aspose.OCR, incluindo a instalação
  do System.Drawing.Common e a extração de texto de arquivos JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: pt
lastmod: 2026-10-11
og_description: Realize OCR em imagem em C# usando Aspose.OCR. Este guia mostra como
  instalar System.Drawing.Common, carregar uma imagem para OCR e extrair texto de
  JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Realize OCR em imagem em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Como realizar OCR em imagem no C# usando Aspose.OCR
url: /pt/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como realizar OCR em imagem em C# usando Aspose.OCR

Se você precisar **perform OCR on image** arquivos em uma aplicação .NET, este guia mostra uma solução completa. Usando Aspose.OCR você pode rapidamente **recognize text from picture** arquivos como JPGs e exibir o resultado em uma janela de console.

Você aprenderá como:

* **install System.Drawing.Common package** – a biblioteca que fornece a classe `Image`,
* **load image for OCR** – ler um JPEG ou PNG na memória,
* configure o modelo de linguagem,
* **perform OCR on image** e finalmente,
* **extract text from JPG** e output it.

Os passos foram escritos para .NET 6+, mas também funcionam com .NET Framework 4.6.1 ou posterior.

---

## Prerequisites

| Requisito | Por que é importante |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Fornece o runtime para o aplicativo console C#. |
| Visual Studio 2022 (or any IDE) | Facilita a adição de pacotes NuGet e a execução do programa. |
| Internet connection (first run only) | Aspose.OCR baixa o módulo de idioma automaticamente. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Usado para demonstrar **extract text from JPG**. |

---

## Etapa 1: Instalar o pacote System.Drawing.Common

O pacote NuGet `System.Drawing.Common` fornece a classe `Image` que você **load image for OCR**. Abra o Package Manager Console e execute:

```powershell
Install-Package System.Drawing.Common
```

> **Dica profissional:** Alvo `net6.0-windows` ou adicione `<UseWindowsForms>true</UseWindowsForms>` ao arquivo de projeto se encontrar avisos específicos de plataforma no Linux/macOS.

---

## Etapa 2: Adicionar o pacote NuGet Aspose.OCR

Aspose.OCR contém o motor OCR e os modelos de idioma. Instale-o com:

```powershell
Install-Package Aspose.OCR
```

O pacote é leve; os dados de idioma necessários (por exemplo, Cyrillic) são baixados na primeira vez que você definir `OcrEngine.Language`.

---

## Etapa 3: Como carregar imagem para OCR

Carregar a imagem é o primeiro passo concreto antes de você poder **perform OCR on image**. O método `Image.FromFile` lê qualquer formato suportado pelo GDI+, incluindo JPG, PNG, BMP e TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Se o arquivo não existir, `FileNotFoundException` será lançada – envolva a chamada em um bloco try/catch para código de produção.*

---

## Etapa 4: Configurar o motor e **perform OCR on image**

Crie uma instância `OcrEngine`, selecione o modelo de idioma, atribua a imagem carregada e chame `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

O método `Recognize()` retorna um objeto `OcrResult` que contém o texto extraído, pontuações de confiança e caixas delimitadoras. O módulo de idioma é baixado automaticamente na primeira utilização, portanto nenhum arquivo extra é necessário.

---

## Etapa 5: **Extract text from JPG** e exiba-o

Agora você pode **recognize text from picture** e imprimir o resultado. A propriedade `Text` de `OcrResult` contém a string simples.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Saída esperada no console

```
Recognized text:
Пример текста на кириллице
```

Se a imagem de origem contiver texto em inglês, a saída será a frase em inglês que você colocou na imagem.

---

## Casos de borda e dicas de boas práticas

| Situação | Recomendação |
|-----------|----------------|
| **Large images ( > 5 MB )** | Redimensione a imagem para ≤ 2000 px no lado mais longo antes do OCR para reduzir o uso de memória e melhorar a velocidade. |
| **Multiple languages in one picture** | Chame `ocrEngine.AddLanguage(OcrLanguage.English)` além do Cyrillic, então defina `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Aumente o contraste com `System.Drawing.Graphics` antes de passar o bitmap para o motor. |
| **Running on Linux/macOS** | Certifique‑se de que a dependência nativa `libgdiplus` esteja instalada (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Reutilize a mesma instância `OcrEngine` e apenas substitua `ocrEngine.Image` para evitar carregamento repetido do módulo. |

---

## Programa completo e executável

Abaixo está a aplicação console completa que incorpora todos os passos anteriores. Copie o código para um novo projeto console C#, substitua o caminho da imagem e execute-o.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** prints the recognized string to the console, confirming that you have successfully **performed OCR on image** and **extracted text from JPG**.

---

## Conclusão

Agora você sabe como **perform OCR on image** arquivos em C# usando Aspose.OCR, desde a instalação do necessário **System.Drawing.Common package** até **loading image for OCR**, seleção do idioma apropriado e, finalmente, **extracting text from JPG**. Este exemplo de ponta a ponta fornece uma base sólida para construir pipelines de processamento de documentos mais avançados, como processamento em lote de pastas de imagens ou integração do OCR em uma API web.

### O que vem a seguir?

* Explore **recognize text from picture** em PDFs convertendo cada página em uma imagem primeiro.  
* Experimente as propriedades `Resolution`, `Threshold` e `MaxProcessingTime` do `OcrEngine` para ajustar a precisão em digitalizações ruidosas.  
* Combine a saída do OCR com uma biblioteca de processamento de linguagem natural para categorizar automaticamente o conteúdo extraído.

Sinta-se à vontade para adaptar o código para outros formatos de imagem, adicionar tratamento de erros ou integrá‑lo em aplicações maiores. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem em C# – Guia Completo Aspose OCR](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Como Realizar Extração de Texto de Imagem a partir de Stream Usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}