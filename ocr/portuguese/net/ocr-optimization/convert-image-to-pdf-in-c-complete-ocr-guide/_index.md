---
category: general
date: 2026-09-13
description: Aprenda como converter uma página escaneada em PDF em C# usando Aspose
  OCR. Este guia mostra o pré-processamento, o reconhecimento de texto em coreano
  e a criação de um PDF pesquisável.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aprenda como converter uma página escaneada em PDF em C# com Aspose
  OCR. O tutorial aborda o pré-processamento de imagens, OCR acelerado por GPU para
  texto em coreano e a geração de um PDF pesquisável em minutos.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Como converter uma página escaneada em PDF em C# com OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Como converter uma página escaneada em PDF em C# com OCR
url: /pt/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como transformar uma página escaneada em PDF em C# com OCR

Se você precisa **converter uma página escaneada em PDF** mantendo o texto pesquisável, está no lugar certo. Este tutorial orienta você a usar Aspose OCR para **preprocessar imagem para OCR**, **reconhecer imagem de texto em coreano**, e finalmente **criar imagem PDF pesquisável** – tudo a partir de um simples aplicativo de console C#.

## Respostas rápidas
- **Qual biblioteca lida com OCR?** Aspose.OCR for .NET  
- **Posso usar a GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Preciso de um pacote de idioma coreano?** It downloads automatically on first use  
- **A saída será pesquisável?** The generated PDF contains an invisible text layer  
- **Quais versões do .NET são suportadas?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Requisitos

- **.NET 6.0 ou posterior** – funciona em .NET Core, .NET Framework e .NET 5/6+  
- **Aspose.OCR for .NET** pacote NuGet (`Aspose.OCR`) – chaves de avaliação são gratuitas no site da Aspose  
- Uma imagem de exemplo com caracteres coreanos, por exemplo, `korean_book_page.jpg`  
- Seu IDE favorito (Visual Studio 2022, VS Code, Rider, etc.)

> **Dica profissional:** Armazene imagens em uma pasta `Resources/` para que os caminhos permaneçam consistentes entre máquinas.

## Visão geral do processo

1. Inicialize o motor OCR com suporte a GPU.  
2. Adicione filtros de **preprocess image for OCR** como deskew e denoise.  
3. Baixe e carregue o modelo de idioma coreano (processado automaticamente).  
4. Execute o OCR na imagem.  
5. Exporte o resultado com **SearchablePdfExporter** para **create searchable PDF image**.  
6. (Opcional) Serialize a saída do OCR para JSON para pipelines posteriores.

A seguir expandimos cada passo, explicamos *por que* isso importa e fornecemos o código exato que você pode copiar‑colar.

## Como funciona a conversão de página escaneada para PDF?

`OcrEngine` é a classe principal no Aspose.OCR que realiza reconhecimento óptico de caracteres em imagens.  
`SearchablePdfExporter` cria um PDF que contém a imagem original e uma camada de texto invisível para pesquisa.  
`RecognitionResult` contém o texto e os dados de confiança retornados pelo motor OCR.

Carregue sua imagem com `new OcrEngine()` e chame `engine.Recognize("korean_book_page.jpg")`, então passe o `RecognitionResult` para `SearchablePdfExporter.Export`. Esse fluxo de duas etapas lê o bitmap, extrai texto Unicode e incorpora ambos em um único PDF onde a camada de texto é invisível, mas pesquisável. A aceleração por GPU reduz o tempo de reconhecimento aproximadamente à metade, enquanto os filtros deskew e denoise aumentam a precisão em até 15 % em digitalizações ruidosas.

## Converter imagem para PDF – fluxo completo

O trecho a seguir é o programa *completo*. Crie um novo projeto de console (`dotnet new console -n OcrPdfDemo`) e substitua o `Program.cs` gerado automaticamente pelo código mostrado no placeholder.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Por que isso funciona

- **GPU acceleration** reduz o tempo de reconhecimento aproximadamente à metade em comparação ao modo apenas CPU.  
- **Deskew** e **Denoise** são técnicas clássicas de *preprocess image for OCR*; corrigem defeitos comuns de digitalização que, de outra forma, fazem o motor perder caracteres.  
- **Language model loading** é essencial para **recognize Korean text image** – sem o modelo coreano o motor recairia para um alfabeto latino genérico e produziria lixo.  
- O **SearchablePdfExporter** combina o bitmap original e uma sobreposição de texto invisível, fornecendo um resultado de **create searchable pdf image** que você pode indexar em qualquer visualizador de PDF.

## Por que isso funciona

- **GPU acceleration** reduz o tempo de reconhecimento aproximadamente à metade em comparação ao modo apenas CPU.  
- **Deskew** e **Denoise** são técnicas clássicas de *preprocess image for OCR*; corrigem defeitos comuns de digitalização que, de outra forma, fazem o motor perder caracteres.  
- **Language model loading** é essencial para **recognize Korean text image** – sem o modelo coreano o motor recairia para um alfabeto latino genérico e produziria lixo.  
- O **SearchablePdfExporter** combina o bitmap original e uma sobreposição de texto invisível, fornecendo um resultado de **create searchable pdf image** que você pode indexar em qualquer visualizador de PDF.

## Preprocess image for OCR – dicas & truques

`DeskewFilter` corrige a rotação das páginas escaneadas.  
`ContrastFilter` ajusta o contraste da imagem para melhorar a precisão do OCR.  
`BinarizationFilter` converte a imagem para preto‑e‑branco com base em um limiar, reduzindo o ruído de fundo.  
`OrientationFilter` detecta e corrige páginas com orientação mista (retrato/paisagem).  

| Problema | Filtro adicional | Como adicionar |
|-------|-------------------|------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Nota:** Adicionar muitos filtros pode desacelerar o processamento. Teste cada alteração em uma única página antes de escalar.

## Recognize Korean text image – armadilhas comuns

Os scripts coreanos contêm sílabas Hangul que são visualmente densas. Se você notar saída corrompida:

1. **Certifique‑se de que o modelo de idioma está totalmente baixado** – verifique o console por uma mensagem como “Downloading Korean model…”.  
2. **Aumente o `MaxAngle`** em `DeskewFilter` se suas digitalizações estiverem rotacionadas além de 12°.  
3. **Aumente a memória GPU** definindo `ocrEngine.GpuMemoryLimit = 2048;` (valor em MB).  

`LanguageModel.Korean` carrega os dados de idioma coreano para OCR, permitindo reconhecimento preciso de Hangul.  

Esses ajustes influenciam diretamente o sucesso de **recognize Korean text image**.

## Create searchable PDF image – verificando o resultado

Depois que o programa terminar, abra `korean_page.pdf` em qualquer leitor de PDF (Adobe Acrobat Reader, Foxit, até Chrome). Você deve ser capaz de:

- **Selecionar texto** com o mouse como se fosse um PDF nativo.  
- **Pesquisar** palavras coreanas usando a caixa de busca integrada.  

Se a camada de texto aparecer vazia, verifique novamente se o método `Export` recebeu o caminho de imagem correto e se o resultado do OCR contém `RecognitionResult.Text` não vazio.

## Saída JSON completa – o que esperar

O console imprime uma carga JSON formatada de forma agradável. Um exemplo reduzido se parece com isto:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Solução de Problemas & FAQ

**Q: Meu PDF está enorme comparado à imagem original.**  
A: O exportador incorpora o bitmap original em sua resolução nativa. Se o tamanho for um problema, reduza a escala da imagem *antes* do reconhecimento:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: O OCR retorna strings vazias.**  
A: Verifique se o caminho da imagem está correto e se o arquivo não está corrompido. Também, certifique‑se de que o driver da GPU está atualizado; drivers antigos podem causar falhas silenciosas.

**Q: Posso processar várias páginas em um loop?**  
A: Absolutamente. Envolva os passos 4‑6 em um loop `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` e altere o caminho de saída do PDF conforme necessário.

## Conclusão

Acabamos de **converter imagem em PDF** preservando texto pesquisável, tudo graças ao poderoso pipeline do Aspose OCR. Ao **preprocess image for OCR**, você aumenta a precisão; ao **recognize Korean text image**, você lida com scripts complexos; e ao **create searchable pdf image**, obtém um documento portátil e indexável.

Pegue o código, aponte para suas próprias digitalizações e experimente filtros ou modelos de idioma adicionais. O mesmo padrão funciona para Chinês, Japonês ou qualquer idioma baseado em latim — basta substituir `LanguageModel.Korean` pelo enum apropriado.

Tem mais perguntas? Deixe um comentário, e feliz codificação!

---

**Última atualização:** 2026-09-13  
**Testado com:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose

## Tutoriais Relacionados

- [Criar PDF pesquisável a partir de arquivos escaneados usando Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline de pré-processamento OCR Como reconhecer texto de imagem](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Reconhecer texto de imagem com Aspose Ocr Guia completo em C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}