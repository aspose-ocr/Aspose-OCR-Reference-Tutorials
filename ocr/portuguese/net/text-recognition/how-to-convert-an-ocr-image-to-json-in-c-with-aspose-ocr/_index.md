---
category: general
date: 2026-09-06
description: Conversão de OCR de imagem para JSON em C# usando Aspose.OCR – guia passo
  a passo para extrair texto da imagem e obter saída JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: pt
lastmod: 2026-09-06
og_description: OCR de imagem para JSON em C# com Aspose.OCR. Aprenda como carregar
  uma imagem para OCR, reconhecer texto a partir de foto e converter o resultado para
  JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Converter uma imagem OCR para JSON em C# – guia completo do Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Como converter uma imagem OCR para JSON em C# com Aspose.OCR
url: /pt/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter uma imagem OCR em JSON em C# com Aspose.OCR

Se você precisa **ocr image to json** em uma aplicação .NET, este guia mostra como fazer isso com Aspose.OCR. Vamos percorrer o carregamento de uma imagem para OCR, o reconhecimento de texto a partir de foto e a conversão do resultado em JSON para que você possa consumir os dados em APIs ou bancos de dados.

Extrair texto de arquivos de imagem é uma necessidade comum para processamento de faturas, digitalização de recibos e projetos de arquivamento. Ao final deste tutorial você será capaz de **convert image to text**, recuperar o resultado em texto simples e gerar um payload JSON estruturado que preserva as informações de layout.

## Pré-requisitos

- .NET 6.0 SDK ou posterior instalado  
- Visual Studio 2022 (ou qualquer editor que suporte .NET)  
- Um pacote NuGet Aspose.OCR (`Aspose.OCR`) adicionado ao seu projeto  
- Uma imagem de exemplo (`input.jpg`) colocada em uma pasta que você pode referenciar no código  

Você não precisa de nenhum motor OCR adicional; Aspose.OCR lida com o processamento pesado internamente.

## Etapa 1: Instalar o pacote NuGet Aspose.OCR

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

O pacote inclui a classe `Aspose.OCR.OcrEngine`, que fornece métodos para **load image for ocr**, seleção de idioma e exportação de resultados.

## Etapa 2: Criar um novo projeto de console C#

Se ainda não tem um projeto, crie um:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Adicione as diretivas `using` que você precisará:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Etapa 3: Carregar a imagem e configurar o motor OCR

O código a seguir demonstra como **load image for ocr**, definir o idioma e preparar o motor para o processamento. Neste exemplo usamos Cirílico, mas você pode mudar para `OcrLanguage.English`, `OcrLanguage.French`, etc., dependendo do idioma de origem.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Por que isso importa:** Definir o idioma correto melhora drasticamente a precisão quando você **recognize text from photo**. O motor usa dicionários e conjuntos de caracteres específicos do idioma.

## Etapa 4: Executar o processo OCR e recuperar os resultados

Agora execute o motor OCR. Se o processo for bem-sucedido, você pode **extract text from image** como texto simples, HTML ou JSON. Aspose.OCR fornece o método `SaveJson` que grava o resultado estruturado em um arquivo.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Estrutura JSON esperada

Um arquivo típico `output.json` tem a seguinte aparência (formatado para legibilidade):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

O payload JSON contém o texto de cada linha, uma pontuação de confiança e o retângulo que envolve a linha na foto original. Isso facilita mapear o resultado OCR de volta para elementos de UI ou campos de banco de dados.

## Etapa 5: Código-fonte completo para a demonstração

Abaixo está o programa completo, pronto‑para‑executar, que realiza o fluxo de trabalho **ocr image to json**. Copie-o para `Program.cs` e execute `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Executando o exemplo

1. Coloque uma imagem chamada `input.jpg` na raiz do projeto.  
2. Execute `dotnet run`.  
3. Observe a saída do console e abra `output.json` para ver os dados estruturados.

## Dicas profissionais e armadilhas comuns

| Situation | Recommendation |
|-----------|----------------|
| **Fotos de baixa resolução** | Aumente o DPI antes do processamento ou use `ocrEngine.Image = ImageStream.FromFile(path, 300)` para forçar 300 DPI. |
| **Idiomas mistos** | Defina `ocrEngine.Language = OcrLanguage.Multilingual` e, opcionalmente, forneça uma lista de idiomas via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Documentos grandes** | Processar uma página de cada vez para manter o uso de memória baixo; o motor suporta TIFFs multipáginas. |
| **Caracteres incorretos** | Verifique se o `OcrLanguage` correto está selecionado; usar o idioma errado reduz a precisão quando você **convert image to text**. |
| **Campos JSON ausentes** | Certifique-se de que está usando a versão 23.6 ou posterior do Aspose.OCR; versões mais antigas não expunham o método `SaveJson`. |

## Perguntas frequentes

**Q: Posso obter o resultado OCR como um array de bytes em vez de um arquivo?**  
A: Sim. Use `ocrEngine.SaveJson(Stream)` para gravar diretamente em um `MemoryStream`, então chame `stream.ToArray()`.

**Q: O motor suporta entrada PDF?**  
A: Aspose.OCR pode aceitar páginas PDF convertidas em imagens via Aspose.PDF, mas o motor OCR em si funciona em imagens raster. Converta PDFs em imagens primeiro, então **load image for ocr**.

**Q: Como lidar com scripts da direita para a esquerda, como o árabe?**  
A: Defina `ocrEngine.Language = OcrLanguage.Arabic`. O JSON inclui a direção correta do texto, que você pode renderizar em frameworks de UI que suportam RTL.

## Conclusão

Agora você tem uma solução completa para **ocr image to json** em C#. Ao carregar uma imagem, configurar o idioma, executar o motor OCR e exportar o resultado como JSON, você pode **extract text from image**, **convert image to text** e **recognize text from photo** em um fluxo de trabalho único e simplificado.  

A partir daqui você pode explorar:

- Integrar a saída JSON com uma Web API (`ASP.NET Core`)  
- Armazenar o resultado em um banco de dados NoSQL como MongoDB  
- Adicionar pós‑processamento para corrigir erros OCR comuns  

Sinta-se à vontade para experimentar diferentes idiomas, formatos de imagem e opções de saída para atender às necessidades do seu projeto. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [reconhecer texto de imagem em C# – Guia completo de OCR e JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Converter imagem em texto em C# com Aspose OCR – Guia passo a passo](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Como extrair texto de imagem usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}