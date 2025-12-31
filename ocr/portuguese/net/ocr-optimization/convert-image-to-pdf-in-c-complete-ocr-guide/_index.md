---
category: general
date: 2025-12-30
description: Converter imagem em PDF usando Aspose OCR em C#. Aprenda como pré‑processar
  a imagem para OCR, reconhecer imagens de texto em coreano e criar rapidamente um
  PDF pesquisável.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: pt
og_description: Converter imagem em PDF com Aspose OCR. Este tutorial mostra como
  pré‑processar a imagem para OCR, reconhecer texto coreano em imagem e criar um PDF
  pesquisável a partir da imagem.
og_title: Converter imagem para PDF em C# – Guia completo de OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Converter imagem para PDF em C# – Guia completo de OCR
url: /pt/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter Imagem para PDF em C# – Guia Completo de OCR

Já precisou **convert image to PDF** mas também queria que o texto interno fosse pesquisável? Você não é o único. Muitos desenvolvedores encontram o mesmo obstáculo ao lidar com páginas escaneadas, especialmente as escritas em coreano. A boa notícia é que com Aspose OCR você pode **preprocess image for OCR**, **recognize Korean text image**, e finalmente **create searchable PDF image** em apenas algumas linhas.

Neste tutorial, percorreremos todo o pipeline — desde o carregamento de um JPEG bruto de uma página de livro em coreano, limpeza, extração do texto e empacotamento de tudo como um PDF pesquisável. Ao final, você terá um aplicativo de console C# pronto‑para‑executar que pode ser inserido em qualquer projeto .NET.

## O que você precisará

- **.NET 6.0 or later** (o código funciona tanto no .NET Core quanto no .NET Framework)  
- **Aspose.OCR for .NET** NuGet package (`Aspose.OCR`) – chaves de avaliação gratuitas estão disponíveis no site da Aspose.  
- Uma imagem de exemplo contendo texto em coreano (por exemplo, `korean_book_page.jpg`).  
- Um ambiente de desenvolvimento de sua escolha (Visual Studio, VS Code, Rider – eu estou usando VS 2022).

> **Pro tip:** Mantenha seus arquivos de imagem em uma pasta dedicada como `Resources/` para que o caminho permaneça consistente entre máquinas.

## Visão geral do processo

1. **Initialize the OCR engine** com suporte a GPU para maior velocidade.  
2. **Add preprocessing filters** (deskew, denoise) para melhorar a precisão do reconhecimento.  
3. **Download and load the Korean language model** – Aspose faz isso automaticamente se necessário.  
4. **Run the recognition** na imagem de entrada.  
5. **Export the result as a searchable PDF** usando o exportador interno.  
6. **Optionally, serialize the result to JSON** para análise ou registro adicional.  

A seguir, detalharemos cada passo, explicaremos *por que* ele importa e forneceremos o código exato que você pode copiar‑colar.

---

## ## Converter Imagem para PDF – Fluxo Completo

O trecho a seguir é o programa *completo*. Sinta-se à vontade para criar um novo projeto de console (`dotnet new console -n OcrPdfDemo`) e substituir o `Program.cs` gerado automaticamente por este código.

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

- **GPU acceleration** reduz o tempo de reconhecimento em cerca de metade comparado ao modo somente CPU.  
- **Deskew** e **Denoise** são técnicas clássicas de *preprocess image for OCR*; elas corrigem defeitos comuns de digitalização que, de outra forma, fariam o motor perder caracteres.  
- **Language model loading** é essencial para **recognize Korean text image** – sem o modelo coreano, o motor recairia para um alfabeto latino genérico e produziria lixo.  
- O **SearchablePdfExporter** agrupa o bitmap original e uma camada de texto invisível, proporcionando um resultado de **create searchable pdf image** que você pode indexar em qualquer visualizador de PDF.

---

## ## Preprocess Image for OCR – Dicas & Truques

Embora os dois filtros que adicionamos geralmente sejam suficientes, você pode encontrar imagens difíceis. Aqui estão alguns passos extras que você pode tentar:

| Problema | Filtro Adicional | Como Adicionar |
|----------|------------------|----------------|
| Baixo contraste | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Ruído de fundo intenso | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientação mista (retrato e paisagem) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** Adicionar muitos filtros pode desacelerar o processamento. Teste cada alteração em uma única página antes de escalar.

---

## ## Recognize Korean Text Image – Armadilhas Comuns

Os scripts coreanos contêm sílabas Hangul que são visualmente densas. Se você notar saída corrompida:

1. **Ensure the language model is fully downloaded** – verifique o console para uma mensagem como “Downloading Korean model…”.  
2. **Increase the `MaxAngle`** em `DeskewFilter` se suas digitalizações estiverem rotacionadas além de 12°.  
3. **Boost GPU memory** definindo `ocrEngine.GpuMemoryLimit = 2048;` (valor em MB).  

Esses ajustes influenciam diretamente o sucesso de **recognize Korean text image**.

---

## ## Create Searchable PDF Image – Verificando o Resultado

Após o programa terminar, abra `korean_page.pdf` em qualquer leitor de PDF (Adobe Acrobat Reader, Foxit, até mesmo Chrome). Você deverá ser capaz de:

- **Select text** com o mouse como se fosse um PDF nativo.  
- **Search** por palavras coreanas usando a caixa de busca integrada.  

Se a camada de texto aparecer em branco, verifique novamente se o método `Export` recebeu o caminho de imagem correto e se o resultado do OCR contém `RecognitionResult.Text` não vazio.

---

## ## Full JSON Output – O que esperar

O console imprime uma carga JSON formatada de forma agradável. Um exemplo resumido se parece com isto:

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

---

## ## Solução de Problemas & FAQ

**Q: Meu PDF está enorme comparado à imagem original.**  
A: O exportador incorpora o bitmap original em sua resolução nativa. Se o tamanho for um problema, redimensione a imagem *antes* do reconhecimento:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: O OCR retorna strings vazias.**  
A: Verifique se o caminho da imagem está correto e se o arquivo não está corrompido. Também, assegure-se de que o driver da GPU está atualizado; drivers antigos podem causar falhas silenciosas.

**Q: Posso processar várias páginas em um loop?**  
A: Claro. Envolva os passos 4‑6 em um loop `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` e altere o caminho de saída do PDF de acordo.

---

## ## Conclusão

Acabamos de **convert image to PDF** preservando texto pesquisável, tudo graças ao pipeline poderoso do Aspose OCR. Ao **preprocess image for OCR**, você aumenta a precisão; ao **recognize Korean text image**, você lida com scripts complexos; e ao **create searchable pdf image**, você obtém um documento portátil e indexável.

Pegue o código, aponte-o para suas próprias digitalizações e experimente filtros ou modelos de linguagem adicionais. O mesmo padrão funciona para Chinês, Japonês ou qualquer idioma baseado em latim — basta trocar `LanguageModel.Korean` pelo enum apropriado.

Tem mais perguntas? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}