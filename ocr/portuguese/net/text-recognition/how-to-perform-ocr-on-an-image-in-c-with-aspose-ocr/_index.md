---
category: general
date: 2026-10-18
description: Realize OCR em uma imagem em C# rapidamente. Aprenda a extrair texto
  de JPG, converter a imagem em texto e ler texto da imagem usando Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: pt
lastmod: 2026-10-18
og_description: Execute OCR em uma imagem em C# com Aspose.OCR. Este tutorial mostra
  como extrair texto de JPG, converter a imagem em texto e ler o texto da imagem em
  minutos.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Realize OCR em uma imagem em C# – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Como realizar OCR em uma imagem em C# com Aspose.OCR
url: /pt/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como realizar OCR em uma imagem em C# com Aspose.OCR

Se você precisar **perform OCR on an image** em uma aplicação .NET, este guia mostra uma solução completa, pronta‑para‑executar. Você verá como **load image for OCR**, reconhecer caracteres cirílicos e **extract text from JPG** arquivos sem escrever nenhum código de processamento de imagem de baixo nível.

Neste tutorial você irá:

* Instalar o pacote NuGet Aspose.OCR.  
* Carregar um arquivo de imagem (JPG, PNG, BMP, etc.).  
* Executar o motor OCR para **convert image to text**.  
* **Read text from image** na saída do console.  

As etapas funcionam com qualquer imagem compatível com .NET, portanto você pode adaptá‑las para PDFs, recibos digitalizados ou capturas de tela.

## Pré-requisitos

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.7+).  
* Visual Studio 2022 ou qualquer editor C# que preferir.  
* Acesso à Internet na primeira execução – Aspose.OCR baixa o módulo de idioma Cyrillic automaticamente.  

> **Dica profissional:** Mantenha o pacote NuGet atualizado; versões mais recentes melhoram a precisão do reconhecimento e adicionam pacotes de idioma.

## Etapa 1: Instalar Aspose.OCR

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

O pacote contém a classe `OcrEngine` usada para **perform OCR on image** arquivos. Após o comando terminar, a referência ao pacote aparece no seu arquivo *.csproj*.

## Etapa 2: Criar um esqueleto de programa console

Crie um novo projeto console se ainda não houver um:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Substitua o *Program.cs* gerado pelo código mostrado nas próximas seções. O esqueleto inclui as diretivas `using` necessárias e um método `Main` que controla o processo OCR.

## Etapa 3: Carregar imagem para OCR

A primeira linha funcional de código **loads the image** que você deseja analisar. Aspose.OCR aceita qualquer stream, portanto você pode carregar um arquivo do disco, uma URL da web ou um recurso incorporado.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Por que isso importa*: Usar `ImageStream.FromFile` abstrai o tratamento de formatos, garantindo que o motor OCR receba um bitmap consistente independentemente do tipo de arquivo original. Ele também libera o stream automaticamente graças à instrução `using`.

## Etapa 4: Inicializar o motor OCR e definir o idioma (opcional)

Por padrão, Aspose.OCR tenta detectar o idioma automaticamente. Para texto cirílico, você pode solicitar explicitamente o módulo `Language.Cyrillic`, o que acelera o download na primeira vez.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Se você omitir a atribuição de idioma, o motor baixará o módulo necessário na primeira vez que chamar `Recognize`. O download ocorre via HTTPS e é armazenado em cache localmente para execuções subsequentes.

## Etapa 5: Executar OCR e converter imagem em texto

Agora você realmente **perform OCR on image** e obtém uma string de texto simples. O método `Recognize` faz todo o trabalho pesado: pré‑processamento, análise de layout e classificação de caracteres.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

O `recognizedText` retornado contém quebras de linha que correspondem ao layout original, facilitando o pós‑processamento ou o armazenamento em um banco de dados.

## Etapa 6: Exibir o resultado – read text from image

Finalmente, **read text from image** escrevendo o resultado no console. Esta etapa verifica se o OCR foi bem‑sucedido e mostra exatamente o que foi extraído.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Ao executar o programa (`dotnet run`), você deverá ver uma saída semelhante a:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Nota:** A saída exata depende da qualidade do JPG de origem. Imagens claras e de alta resolução produzem os melhores resultados.

## Código-fonte completo e executável

Abaixo está o programa completo que você pode copiar‑colar em *Program.cs* e executar sem modificações (exceto o caminho da imagem).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Executar o programa imprime os caracteres extraídos no console, provando que você extraiu com sucesso **extracted text from JPG** e **converted image to text**.

## Lidando com variações comuns

| Cenário | Ajuste |
|----------|------------|
| **Different language** | Defina `engine.Language = Language.English;` ou outro enum suportado. |
| **Multi‑page PDF** | Converta cada página em uma imagem (por exemplo, usando `Aspose.PDF`) e chame o loop OCR para cada imagem. |
| **Large batch** | Envolva a chamada OCR em um loop `Parallel.ForEach`; reutilize uma única instância `OcrEngine` para reduzir o consumo de memória. |
| **Low‑resolution image** | Pré‑procese com `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` para reduzir ruído antes do reconhecimento. |

## Dicas de desempenho

* **Cache language modules** – o primeiro download pode levar alguns segundos; execuções subsequentes são instantâneas. |
* **Reuse the `OcrEngine`** instance for multiple images to avoid repeated initialization costs. |
* **Limit image size** – fotos extremamente grandes aumentam o uso de memória. Redimensione para no máximo 2000 px de largura antes de enviá‑las ao motor.

## Conclusão

Agora você sabe como **perform OCR on image** arquivos em C# usando Aspose.OCR. Carregando uma imagem, configurando o motor e chamando `Recognize`, você pode **extract text from JPG**, **convert image to text** e **read text from image** com apenas algumas linhas de código.  

A partir daqui você pode explorar:

* Armazenar os resultados OCR em um banco de dados para arquivos pesquisáveis.  
* Integrar o fluxo de trabalho em uma API web que aceita imagens enviadas.  
* Usar outros módulos de idioma (Árabe, Hindi, etc.) para ampliar o alcance da sua aplicação.

Sinta‑se à vontade para experimentar diferentes formatos de imagem, idiomas e estratégias de processamento em lote. O padrão central — **load image for OCR → recognize → handle the plain‑text output** — permanece o mesmo, proporcionando uma base sólida para qualquer projeto de extração de texto.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}