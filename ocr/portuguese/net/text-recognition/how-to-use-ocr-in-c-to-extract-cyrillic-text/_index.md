---
category: general
date: 2026-09-10
description: Como usar OCR em C# para extrair texto cirílico, pré-processar imagens
  e convertê-las em arquivos PDF ou HTML em um único exemplo executável.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- preprocess image for OCR
- convert image to PDF
- convert image to HTML
- extract Cyrillic text
language: pt
lastmod: 2026-09-10
og_description: Como usar OCR em C# para extrair texto cirílico, pré-processar imagens
  e exportar os resultados como PDF ou HTML. Siga este guia passo a passo.
og_image_alt: Diagram illustrating how to use OCR to extract Cyrillic text and convert
  images
og_title: Como usar OCR em C# – extrair texto cirílico e converter imagens
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: How to use OCR in C# to extract Cyrillic text, preprocess images, and
    convert them to PDF or HTML files in a single, runnable example.
  headline: How to use OCR in C# to extract Cyrillic text
  type: TechArticle
tags:
- OCR
- C#
- Cyrillic
- Image processing
- PDF conversion
title: Como usar OCR em C# para extrair texto cirílico
url: /pt/net/text-recognition/how-to-use-ocr-in-c-to-extract-cyrillic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR em C# para extrair texto cirílico

Se você precisa **como usar OCR** em C# para extrair texto cirílico de documentos escaneados, este guia mostra uma solução completa, pronta‑para‑executar. Você também aprenderá como **preprocessar imagem para OCR**, e como **converter imagem para PDF** ou **converter imagem para HTML** depois que o texto for reconhecido.

Projetos de digitalização de documentos frequentemente se deparam com dois problemas: escaneamentos de baixa qualidade e a necessidade de armazenar os resultados em múltiplos formatos. Este tutorial resolve ambos usando a biblioteca Aspose.OCR, que baixa automaticamente pacotes de idioma ausentes, oferece auxiliares de processamento de imagem integrados e pode exportar o resultado OCR para PDF ou HTML com uma única chamada.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.7+).
* Visual Studio 2022 ou qualquer editor que suporte projetos C#.
* O pacote NuGet **Aspose.OCR**. Instale‑o com:

```bash
dotnet add package Aspose.OCR
```

* Um arquivo de imagem que contém caracteres cirílicos (por exemplo, `sample_cyrillic.jpg`).  
  Coloque o arquivo em uma pasta que você possa referenciar como `YOUR_DIRECTORY`.

A biblioteca baixará o pacote de idioma cirílico na primeira vez que você definir `ocrEngine.Language = Language.Cyrillic;`, portanto não é necessário download manual.

## Passo 1 – Inicializar o motor OCR (como usar OCR)

Criar uma instância de `OcrEngine` prepara o motor para todas as operações subsequentes.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine – the first step in how to use OCR with Aspose
        var ocrEngine = new OcrEngine();
```

**Por que isso importa:** O motor mantém configurações como idioma, definições de processamento de imagem e opções de saída. Inicializá‑lo uma vez mantém o restante do código limpo e thread‑safe.

## Passo 2 – Escolher o idioma cirílico (extrair texto cirílico)

```csharp
        // Select Cyrillic language; the pack is fetched automatically if missing
        ocrEngine.Language = Language.Cyrillic;
```

**Por que isso importa:** A precisão do OCR depende fortemente do modelo de idioma correto. Ao selecionar explicitamente `Language.Cyrillic`, o motor aplica tabelas de frequência de caracteres adequadas para russo, ucraniano, búlgaro, etc.

## Passo 3 – Pré‑processar a imagem para OCR

Escaneamentos de baixa qualidade contêm inclinação, manchas ou iluminação desigual. O `ImageProcessor` integrado pode melhorar as taxas de reconhecimento com apenas duas chamadas.

```csharp
        // Optional but strongly recommended: deskew and despeckle the image
        ocrEngine.ImageProcessor.Deskew();      // Aligns rotated text
        ocrEngine.ImageProcessor.Despeckle();  // Removes isolated noise pixels
```

**Por que isso importa:** O pré‑processamento reduz caracteres falsos e aumenta a pontuação de confiança. Texto inclinado costuma gerar saída confusa; a correção de inclinação (deskew) o alinha. A remoção de manchas elimina pequenos artefatos que o motor OCR poderia interpretar como letras.

> **Dica profissional:** Se suas imagens de origem já estiverem limpas, você pode pular essas chamadas. Para escaneamentos muito degradados, considere etapas adicionais como `Binarize()` ou `ContrastStretch()`.

## Passo 4 – Executar OCR na imagem de entrada

```csharp
        // The image path can be absolute or relative to the executable
        string inputPath = Path.Combine("YOUR_DIRECTORY", "sample_cyrillic.jpg");
        ocrEngine.Process(inputPath);
```

**Por que isso importa:** `Process` executa o pipeline de reconhecimento na bitmap fornecida. Ele retorna `void`; o texto reconhecido fica disponível através da propriedade `Text`.

## Passo 5 – Recuperar o texto reconhecido e salvá‑lo em um arquivo

```csharp
        // Access the recognized string
        string recognizedText = ocrEngine.Text;

        // Save the plain‑text result
        string txtOutput = Path.Combine("YOUR_DIRECTORY", "result.txt");
        File.WriteAllText(txtOutput, recognizedText);
        Console.WriteLine("Text saved to: " + txtOutput);
```

**Por que isso importa:** Armazenar o texto bruto permite processamento posterior, como pesquisa, indexação ou alimentação em serviços de tradução.

## Passo 6 – Exportar o resultado OCR para outros formatos (converter imagem para PDF & converter imagem para HTML)

```csharp
        // Export as PDF – useful for archival or sharing with non‑technical users
        string pdfOutput = Path.Combine("YOUR_DIRECTORY", "result.pdf");
        ocrEngine.SaveResultAsPdf(pdfOutput);
        Console.WriteLine("PDF saved to: " + pdfOutput);

        // Export as HTML – retains basic layout and can be displayed in browsers
        string htmlOutput = Path.Combine("YOUR_DIRECTORY", "result.html");
        ocrEngine.SaveResultAsHtml(htmlOutput);
        Console.WriteLine("HTML saved to: " + htmlOutput);
    }
}
```

**Por que isso importa:** Converter o resultado OCR para PDF ou HTML permite manter o contexto visual da imagem original enquanto fornece texto pesquisável. Isso é especialmente valioso para fluxos de trabalho legais ou de arquivamento.

### Saída esperada

Executar o programa com um escaneamento cirílico claro produz três arquivos:

* `result.txt` – texto Unicode simples, por exemplo, `Пример текста на кириллице`.
* `result.pdf` – um PDF contendo a imagem com uma camada de texto invisível para pesquisa.
* `result.html` – uma página HTML mostrando a imagem e texto selecionável.

Abra qualquer um dos arquivos para verificar se os caracteres cirílicos foram extraídos corretamente.

## Perguntas comuns e casos de borda

| Pergunta | Resposta |
|----------|----------|
| **E se o pacote de idioma falhar ao baixar?** | Certifique‑se de que a máquina tem acesso à internet. Você também pode pré‑baixar o pacote do site da Aspose e colocá‑lo na pasta `bin`. |
| **Posso reconhecer outros alfabetos na mesma execução?** | Sim. Chame `ocrEngine.Language = Language.English;` (ou qualquer enum suportado) antes de `Process`. Pode ser necessário executar `Process` separadamente para cada idioma se a imagem misturar scripts. |
| **Minha imagem é um TIFF de múltiplas páginas – isso funciona?** | `OcrEngine` processa um bitmap por vez. Carregue cada página em um `Bitmap` e chame `Process` em um loop, concatenando os resultados. |
| **Como aumento o desempenho para grandes lotes?** | Reutilize uma única instância de `OcrEngine` e defina `ocrEngine.OptimizeMemory = true;`. Também considere processamento paralelo com instâncias de motor separadas por thread. |

## Conclusão

Agora você sabe **como usar OCR** em C# para **extrair texto cirílico**, **preprocessar imagem para OCR**, e **converter imagem para PDF** ou **converter imagem para HTML** em alguns passos concisos. O exemplo completo demonstra uma solução pronta para produção‑

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como usar AspOCR: filtros de pré‑processamento de imagem OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Como extrair texto OCR em C# – Guia completo passo a passo](/ocr/english/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/)
- [Como usar Aspose OCR para resultado JSON em reconhecimento de imagem](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}