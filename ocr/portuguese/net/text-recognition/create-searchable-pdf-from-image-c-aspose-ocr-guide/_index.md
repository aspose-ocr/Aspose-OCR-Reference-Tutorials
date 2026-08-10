---
category: general
date: 2026-05-06
description: Crie PDF pesquisável a partir de uma imagem usando Aspose OCR em C#.
  Aprenda a converter PNG para PDF, extrair texto da imagem e gerar um PDF pesquisável.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem usando Aspose OCR em C#.
  Este tutorial passo a passo mostra como converter PNG para PDF, extrair texto da
  imagem e produzir um PDF pesquisável.
og_title: Criar PDF pesquisável a partir de imagem – Guia de OCR Aspose em C#
tags:
- Aspose
- C#
- OCR
- PDF
title: Criar PDF pesquisável a partir de imagem – Guia de OCR Aspose em C#
url: /pt/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie PDF pesquisável a partir de Imagem – Guia C# Aspose OCR

Já precisou **criar PDF pesquisável** a partir de uma foto escaneada, mas não sabia por onde começar? Talvez você tenha um recibo em PNG, um JPEG de um contrato ou qualquer bitmap que queira transformar em um PDF que realmente possa ser pesquisado. Esse é um ponto de dor comum, especialmente quando você lida com escaneamentos antigos que ficam parados em uma pasta.

A boa notícia é que, com Aspose OCR, você pode **converter imagem para PDF**, extrair o texto oculto e obter um documento totalmente pesquisável — tudo em poucas linhas de C#. Neste guia também mostraremos como **converter png para PDF**, **extrair texto de imagem**, e ainda abordaremos o caso de uso de TIFFs de várias páginas. Ao final, você terá uma solução autônoma que pode ser inserida em qualquer projeto .NET.

## O que você vai precisar

- **.NET 6+** (o código também funciona no .NET Framework 4.6+)
- **Visual Studio 2022** ou qualquer IDE de sua preferência
- Pacote NuGet **Aspose.OCR** (ele traz o Aspose.PDF automaticamente)
- Um arquivo de imagem (PNG, JPEG, BMP, TIFF) que você deseja transformar em PDF pesquisável

Sem truques de licenciamento extra, sem serviços externos — apenas uma referência NuGet e alguns minutos de codificação.

## Etapa 1: Instale o Pacote NuGet Aspose.OCR

Primeiro, adicione a biblioteca ao seu projeto. Abra o **Package Manager Console** e execute:

```powershell
Install-Package Aspose.OCR
```

Esse único comando traz tanto o **Aspose.OCR** quanto o assembly **Aspose.Pdf** do qual ele depende, deixando você pronto para ler a imagem e gravar o PDF.

> **Dica profissional:** Se estiver usando a CLI do .NET, o equivalente é `dotnet add package Aspose.OCR`.

## Etapa 2: Inicialize o Motor OCR

Criar uma instância de `OcrEngine` é a porta de entrada para todo o trabalho de OCR. Pense nele como o cérebro que vai analisar sua foto e começar a “ler” os caracteres.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Você pode se perguntar, *por que não chamar um método estático?* A abordagem orientada a objetos permite ajustar configurações posteriormente (idioma, resolução, etc.) sem mudar o fluxo geral.

## Etapa 3: Carregue a Imagem que Você Quer Converter

É aqui que **convertemos imagem para PDF** em espírito — alimentando o bitmap no motor OCR. Substitua `"YOUR_DIRECTORY/input.png"` pelo caminho real do seu arquivo.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Se você tem um cenário de **converter png para pdf**, basta apontar para o PNG. Para TIFFs de várias páginas, o Aspose.OCR tratará automaticamente cada quadro como uma página separada.

## Etapa 4: Execute o OCR e Opcionalmente Capture o Texto

Chamar `Recognize()` faz o trabalho pesado: ele analisa a foto, detecta os caracteres e devolve um resultado estruturado. Você pode manter o texto para registro, indexação de busca ou exibição.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Por que extrair texto?** Mesmo que o incorporemos no PDF final, ter a string bruta pode ser útil para validação ou análises.

## Etapa 5: Configure as Opções de PDF para um Documento Pesquisável

O Aspose.PDF oferece um modo especial `PdfSaveOptions` chamado **CreateSearchablePdf**. Ele indica à biblioteca que incorpore o texto OCR como uma camada invisível atrás da imagem, tornando o PDF pesquisável.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Se precisar de um PDF apenas com imagem (sem texto oculto), pode mudar para `PdfSaveOptions.CreatePdf()`. Mas para o nosso objetivo — **criar PDF pesquisável** — o modo pesquisável é o destaque.

## Etapa 6: Salve o PDF Pesquisável no Disco

Agora juntamos tudo. O método `SavePdf` grava a imagem e o texto oculto em um único arquivo.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

Neste ponto você tem um **PDF pesquisável** que pode abrir no Adobe Reader, digitar uma palavra na caixa de busca e pular instantaneamente para a localização correspondente — mesmo que a página visível ainda seja apenas a imagem original.

## Exemplo Completo Funcional

Juntando todas as peças, aqui está um aplicativo de console pronto‑para‑executar. Copie‑e‑cole em um novo projeto C#, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Saída Esperada

Ao executar o programa, o console exibirá algo como:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

E em `YOUR_DIRECTORY` você encontrará `output.pdf`. Abra-o, pressione **Ctrl F**, digite “Invoice” e você será levado direto à palavra — mesmo que a página pareça um escaneamento plano.

## Lidando com Variações Comuns

### Convertendo Várias Imagens de Uma Só Vez

Se você tem uma pasta cheia de PNGs e quer um único PDF pesquisável, faça um loop sobre os arquivos e adicione cada um como página separada:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Também é possível usar `PdfFileEditor` do Aspose.PDF para mesclar os PDFs temporários em um arquivo final.

### Lidando com Escaneamentos de Baixa Resolução

A precisão do OCR cai quando o DPI da imagem está abaixo de 150. Antes de alimentar a imagem, você pode aumentá‑la:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Selecionando um Idioma Específico

Se seu documento não está em inglês, defina o idioma antes de `Recognize()`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Esses ajustes garantem que **extrair texto de imagem** funcione de forma confiável em diferentes cenários.

## Resultado Visual

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*A captura de tela acima mostra um PDF onde a imagem está visível, mas a camada de texto pode ser pesquisada.*

## Conclusão

Agora você tem uma receita completa e pronta para produção para **criar PDF pesquisável** a partir de qualquer imagem usando Aspose OCR e C#. Abordamos como **converter imagem para PDF**, **extrair texto de imagem**, e ainda tocamos nos casos de **converter png para pdf** e **ocr image to pdf**. O código é totalmente autônomo, roda em qualquer runtime .NET e pode ser estendido para processamento em lote ou suporte a idiomas personalizados.

Qual o próximo passo? Experimente adicionar uma marca d’água, criptografar o PDF ou alimentar o texto extraído em um índice de busca como Elasticsearch. As possibilidades são infinitas, e o mesmo padrão — carregar → reconhecer → salvar — servirá bem para qualquer fluxo de trabalho orientado a OCR.

Se encontrar algum obstáculo ou tiver um caso de uso interessante para compartilhar, deixe um comentário abaixo. Boa codificação e aproveite para transformar aqueles escaneamentos teimosos em ouro pesquisável!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}