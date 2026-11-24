---
category: general
date: 2026-08-09
description: Extraia texto de imagem com Aspose OCR em C#. Aprenda como carregar a
  imagem para OCR, definir o idioma do OCR, processar a imagem com OCR e converter
  a imagem em texto de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: pt
lastmod: 2026-08-09
og_description: Extrair texto de imagem usando Aspose OCR em C#. Este tutorial mostra
  como carregar a imagem para OCR, definir o idioma do OCR, processar o OCR da imagem
  e converter a imagem em texto em poucas linhas de código.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Extrair texto de imagem com Aspose OCR – Guia C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrair texto de imagem usando Aspose OCR em C#
url: /pt/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto de imagem usando Aspose OCR em C#

Se você precisa **extrair texto de imagem** em uma aplicação .NET, este guia o conduzirá por uma solução completa e pronta‑para‑executar. Você verá como **carregar imagem para OCR**, escolher o módulo de idioma adequado, executar o motor OCR e, finalmente, **converter imagem em texto** com apenas algumas linhas de C#.

O tutorial cobre tudo o que é necessário para obter resultados confiáveis com Aspose.OCR, incluindo armadilhas comuns como formatos de imagem não suportados e nuances específicas de idioma. Ao final, você terá um programa autônomo que imprime o texto reconhecido no console.

## O que você alcançará

* Carregar um arquivo de imagem no motor Aspose OCR.  
* **Definir idioma OCR** (Cirílico no exemplo, mas qualquer idioma suportado funciona).  
* **Processar OCR da imagem** e obter a representação textual.  
* **Converter imagem em texto** e exibi-lo, pronto para processamento ou armazenamento adicional.  

**Pré-requisitos**

* .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+).  
* Visual Studio 2022 (ou qualquer IDE que suporte C#).  
* Pacote NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  

---

## Extrair texto de imagem – walkthrough completo do código

Abaixo está o programa completo e executável. Copie-o para um novo projeto de console e substitua `YOUR_DIRECTORY/sample_cyrillic.jpg` pelo caminho da sua própria imagem.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Por que cada passo importa

1. **Criar uma instância do motor OCR** – O `OcrEngine` encapsula toda a funcionalidade de OCR. Dispor dela rapidamente libera recursos nativos, o que é crítico para serviços de longa duração.  
2. **Definir idioma OCR** – Selecionar o módulo de idioma correto melhora drasticamente a precisão. Aspose fornece mais de 30 pacotes de idioma; o padrão é English. O exemplo usa Cyrillic para demonstrar um script não‑latino.  
3. **Carregar imagem para OCR** – O motor trabalha com um `ImageStream`. Fornecer uma imagem de alta resolução (≥300 dpi) reduz erros de reconhecimento, especialmente para scripts complexos.  
4. **Processar OCR da imagem** – É aqui que ocorre o processamento pesado. O método retorna um `OcrResult` contendo o texto extraído, pontuações de confiança e dados de layout opcionais.  
5. **Converter imagem em texto** – `result.Text` é uma `string` simples. Você pode gravá‑la em um arquivo, enviá‑la para um índice de busca ou passá‑la para pipelines de NLP subsequentes.  

---

## Carregar imagem para OCR

O método `ImageStream.FromFile` suporta formatos raster comuns. Se você receber imagens como arrays de bytes (por exemplo, de uma API web), use `ImageStream.FromBytes(byte[])` em vez disso:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Dica profissional:** Sempre verifique se a imagem não está corrompida antes de passá‑la para o motor. Uma verificação rápida `try { Image.FromFile(...); } catch { ... }` impede exceções em tempo de execução.

---

## Definir idioma OCR

Aspose.OCR vem com pacotes de idioma que você pode habilitar em tempo de execução. Para listar todos os idiomas disponíveis:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Se precisar reconhecer múltiplos idiomas no mesmo documento, combine‑os com o operador OR bit a bit:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Caso de borda:** Misturar idiomas da direita para a esquerda (RTL) (por exemplo, Árabe) com scripts da esquerda para a direita pode exigir tratamento de layout adicional. Aspose detecta automaticamente a direção, mas você pode ajustá‑la via `engine.PageSegmentationMode`.

---

## Processar OCR da imagem

A chamada `Process` é síncrona e bloqueia até que o motor termine. Para lotes grandes ou aplicações UI, considere a sobrecarga assíncrona:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Armadilha comum:** Esquecer de definir `engine.Image` antes de chamar `Process` lança uma `InvalidOperationException`. Sempre atribua a imagem primeiro.

---

## Converter imagem em texto

A string extraída pode ser manipulada como qualquer outra `string` .NET. Por exemplo, para gravar a saída em um arquivo:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Se precisar manter quebras de linha exatamente como aparecem na imagem, use `result.Text` diretamente. Para pós‑processamento (por exemplo, remover espaços em branco extras), aplique métodos padrão de string:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Recapitulação do exemplo completo

Juntando tudo, o programa:

1. Instancia `OcrEngine`.
2. **Define idioma OCR** para Cyrillic (ou qualquer idioma que você escolher).
3. **Carrega imagem para OCR** do disco.
4. **Processa OCR da imagem** para obter o resultado textual.
5. **Converte imagem em texto** e a imprime.

Executar o exemplo com uma imagem Cyrillic clara produz uma saída semelhante a:

```
=== Recognized Text ===
Пример текста на кириллице
```

Se a imagem contiver texto em inglês, basta mudar `engine.Language = OcrLanguage.English;` e o mesmo código **extrairá texto da imagem** corretamente.

---

## Conclusão

Agora você sabe como **extrair texto de imagem** usando Aspose OCR em C#. O tutorial abordou o carregamento da imagem, a seleção do idioma apropriado, a execução do processo OCR e **converter imagem em texto** para uso posterior.

A partir daqui você pode:

* Experimentar com outros idiomas (`load image for OCR` → `set OCR language` → `process image OCR`).  
* Integrar a etapa OCR em um pipeline maior (por exemplo, ingestão de documentos, PDFs pesquisáveis).  
* Otimizar desempenho agrupando imagens ou usando a API assíncrona.

Sinta‑se à vontade para explorar a documentação do Aspose.OCR para recursos avançados, como dicionários personalizados, modos de segmentação de página e ajuste de precisão do OCR. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}