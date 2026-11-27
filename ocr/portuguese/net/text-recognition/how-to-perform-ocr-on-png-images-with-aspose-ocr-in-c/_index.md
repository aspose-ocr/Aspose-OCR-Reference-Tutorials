---
category: general
date: 2026-11-26
description: Aprenda a realizar OCR em arquivos PNG, converter PNG em texto e extrair
  texto cirílico usando Aspose.OCR – guia passo a passo para desenvolvedores.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: pt
lastmod: 2026-11-26
og_description: Como realizar OCR em arquivos PNG e extrair texto cirílico usando
  Aspose.OCR em C#. Siga este tutorial completo para converter PNG em texto.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Como realizar OCR em imagens PNG com Aspose.OCR – Guia C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Como realizar OCR em imagens PNG com Aspose.OCR em C#
url: /pt/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como realizar OCR em imagens PNG com Aspose.OCR em C#

Se você precisa **como realizar OCR** em um arquivo PNG, este guia mostra as etapas exatas para converter PNG em texto usando Aspose.OCR. Seja extraindo texto cirílico de documentos escaneados ou simplesmente reconhecendo texto de capturas de tela PNG, a solução funciona imediatamente e requer apenas algumas linhas de código C#.

Neste tutorial você aprenderá a:

* **carregar imagem para OCR** a partir de uma pasta local,
* configurar o motor para **extrair texto cirílico**,
* **reconhecer texto de PNG** e obter uma string limpa,
* lidar com armadilhas comuns, como módulos de idioma ausentes e imagens grandes.

Nenhuma experiência prévia com Aspose.OCR é necessária — apenas um ambiente de desenvolvimento .NET e uma imagem PNG que você deseja processar.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 (ou superior) instalado.  
* Uma cópia licenciada ou de avaliação do **Aspose.OCR for .NET**. Você pode obter uma avaliação gratuita no site da Aspose.  
* Visual Studio 2022 (ou qualquer IDE que suporte .NET).  
* Um arquivo PNG contendo o texto que você deseja extrair (o exemplo usa `sample_image.png`).

## Etapa 1: Instalar o pacote NuGet Aspose.OCR

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

O pacote inclui o motor OCR central e todos os módulos de idioma. Quando você solicita um idioma que não está presente localmente, o Aspose.OCR baixa automaticamente o módulo necessário.

## Etapa 2: Criar uma instância do motor OCR (como realizar OCR)

A primeira ação prática em qualquer fluxo de trabalho OCR é instanciar o motor. Esse objeto gerencia todas as operações subsequentes, como carregar a imagem e executar o reconhecimento.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Por que isso importa:** A classe `OcrEngine` encapsula o pipeline OCR. Criar uma única instância e reutilizá‑la em várias imagens reduz o consumo de memória e melhora o desempenho.

## Etapa 3: Carregar imagem para OCR – especificar o arquivo PNG de origem

Carregar a imagem é o ponto onde você **carrega imagem para OCR**. Aspose.OCR aceita vários tipos de entrada; o mais direto é `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Dica profissional:** Use um caminho absoluto ou `Path.Combine` para evitar erros de tempo de execução em diferentes ambientes.

### Manipulando imagens grandes

Se o PNG for maior que 2 MB, considere redimensioná‑lo antes do reconhecimento para acelerar o processamento:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Etapa 4: Configurar idioma – extrair texto cirílico

Por padrão, o Aspose.OCR assume inglês. Para **extrair texto cirílico**, defina a propriedade `Language` como `Language.Cyrillic`. O módulo necessário será baixado automaticamente na primeira execução do código.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Se precisar reconhecer vários idiomas (por exemplo, inglês e cirílico), você pode combiná‑los:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Caso de borda: Módulo de idioma ausente

Se o download falhar (por exemplo, ambiente offline), o motor lança uma `OcrException`. Capture‑a para fornecer uma alternativa elegante:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Etapa 5: Executar a operação de reconhecimento (reconhecer texto de PNG)

Agora que a imagem e o idioma estão definidos, você pode **reconhecer texto de PNG**. O método `Recognize` executa o pipeline OCR de forma síncrona.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Por que funciona:** Internamente, o Aspose.OCR aplica pré‑processamento (binarização, remoção de ruído) antes de alimentar a imagem a um reconhecedor baseado em rede neural ajustado para o idioma selecionado.

## Etapa 6: Recuperar e exibir o texto reconhecido (converter PNG em texto)

Após o reconhecimento, a string extraída está disponível via a propriedade `Text`. Esta é a etapa final em **converter PNG em texto**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Saída esperada

Se `sample_image.png` contiver a frase cirílica “Привет мир”, o console exibirá:

```
=== OCR Result ===
Привет мир
```

A saída pode incluir quebras de linha e pontuação exatamente como aparecem na imagem. Você pode pós‑processar a string com `String.Trim()`, `Regex` ou outras utilidades de limpeza de texto, se necessário.

## Etapa 7: Opcional – Salvar o resultado em um arquivo

Armazenar o resultado OCR permite processamento posterior (por exemplo, indexação, tradução). Aqui está uma maneira rápida de gravar o texto em um arquivo UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Armadilhas comuns e como evitá‑las

| Problema | Sintoma | Solução |
|----------|----------|---------|
| **Módulo de idioma ausente** | `OcrException` ao definir `Language = Language.Cyrillic` | Garanta conectividade com a internet na primeira execução ou pré‑baixe os módulos via pacote offline da Aspose. |
| **Imagem borrada ou de baixo contraste** | Baixa precisão, muitos caracteres “?” | Pré‑processar a imagem: aumentar contraste, aplicar nitidez ou converter para escala de cinza antes de enviá‑la ao motor. |
| **PNG muito grande** | Tempo de processamento longo, possível `OutOfMemoryException` | Redimensione conforme mostrado na Etapa 3 ou divida uma imagem multipágina em blocos separados. |
| **Caracteres não‑UTF‑8** | Saída corrompida | Verifique se o console ou o gravador de arquivos usa codificação UTF‑8 (`Encoding.UTF8`). |

## Exemplo completo e executável

Abaixo está o programa completo que incorpora todas as etapas acima. Copie‑o para um novo projeto de console e execute‑o após ajustar os caminhos dos arquivos.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Como funciona

1. **Engine creation** – prepara o pipeline OCR.  
2. **Image loading** – suporta tanto PNG bruto quanto versões redimensionadas para desempenho.  
3. **Language selection** – demonstra **extrair texto cirílico** enquanto lida com módulos ausentes.  
4. **Recognition** – a chamada central **reconhecer texto de PNG**.  
5. **Result handling** – mostra **converter PNG em texto** e grava a saída em um arquivo.

Execute o programa com `dotnet run`. Se tudo estiver configurado corretamente, você verá o texto reconhecido impresso no console e salvo em `ocr_output.txt`.

## Conclusão

Neste tutorial você aprendeu **como realizar OCR** em arquivos PNG usando Aspose.OCR para .NET, cobrindo tudo desde **carregar imagem para OCR** até **extrair texto cirílico** e **converter PNG em texto**. O exemplo completo e executável demonstra o fluxo de trabalho padrão, casos de borda comuns e dicas práticas que mantêm seu pipeline OCR confiável.

**Próximos passos**

* Explore **reconhecer texto de PNG** com idiomas adicionais (Árabe, Chinês) combinando flags `Language`.  
* Integre o resultado OCR ao Azure Cognitive Search para arquivos de documentos pesquisáveis.  
* Experimente as configurações do `OcrEngine` do Aspose.OCR, como `Resolution

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como baixar o modelo Aspose.OCR e extrair texto de PNG em C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Como realizar OCR em C# – Reconhecer texto cirílico com Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Como fazer OCR em lote em C# – Forma rápida de extrair texto de arquivos PNG](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}