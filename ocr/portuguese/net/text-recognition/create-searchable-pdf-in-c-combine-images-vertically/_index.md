---
category: general
date: 2026-02-28
description: Crie PDF pesquisável em C# combinando imagens verticalmente. Aprenda
  como empilhar imagens verticalmente e converter páginas escaneadas em PDF com Aspose
  OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: pt
og_description: Crie PDF pesquisável em C# combinando imagens verticalmente. Este
  guia mostra como empilhar imagens verticalmente e converter páginas escaneadas em
  PDF usando o Aspose OCR.
og_title: Criar PDF pesquisável em C# – Combinar imagens verticalmente
tags:
- Aspose OCR
- C#
- PDF generation
title: Criar PDF pesquisável em C# – Combinar imagens verticalmente
url: /pt/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável em C# – Combinar Imagens Verticalmente

Já precisou **criar PDF pesquisável** a partir de alguns PNGs digitalizados, mas não sabia por onde começar? Você não está sozinho. Em muitos projetos de automação de documentos, o maior ponto crítico é transformar uma pilha de arquivos de imagem em um PDF pesquisável, organizado, que você possa indexar e compartilhar.  

Neste tutorial, percorreremos um exemplo completo, pronto‑para‑executar, que mostra como **empilhar imagens verticalmente**, **combinar imagens verticalmente** e, finalmente, **converter páginas digitalizadas em PDF** em um único documento pesquisável usando o motor acelerado por GPU do Aspose.OCR. Ao final, você terá um programa autônomo que pode ser inserido em qualquer solução .NET.

> **O que você aprenderá**
> - Inicializar um motor OCR com suporte a GPU.
> - Processar um lote de imagens em paralelo.
> - **Combinar imagens verticalmente** para imitar uma digitalização de várias páginas.
> - Exportar um PDF pesquisável e um relatório JSON detalhado para análise posterior.

## Pré-requisitos

- .NET 6+ (o código compila com .NET 6, .NET 7 ou .NET 8)
- Pacote NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Uma máquina com GPU habilitada se você quiser manter a configuração `ProcessingMode.Gpu` (fallback para CPU também funciona)
- Uma pasta com alguns arquivos PNG/JPEG digitalizados (a demonstração usa `page1.png`, `page2.png`, `page3.png`)

Sem serviços externos, sem arquivos de configuração ocultos — apenas C# puro.

## Etapa 1 – Configurar o Motor OCR para **Criar PDF pesquisável**

Primeiro criamos um `OcrEngine`, ativamos a aceleração por GPU, selecionamos o inglês como idioma e adicionamos alguns filtros de pré‑processamento. Esses filtros melhoram a precisão ao endireitar páginas inclinadas (`DeskewFilter`) e remover ruído (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Por que isso importa:** O motor OCR realiza o trabalho pesado de reconhecer texto. Habilitar `ProcessingMode.Gpu` pode reduzir o tempo de reconhecimento pela metade em uma placa gráfica moderna, enquanto os filtros reduzem artefatos comuns de digitalização que, de outra forma, produziriam saída confusa.

## Etapa 2 – Configurar um Processador em Lote para **Converter Páginas Digitalizadas em PDF** de Forma Eficiente

Processar cada página individualmente funciona para algumas imagens, mas projetos reais frequentemente envolvem dezenas ou centenas de páginas. O `OcrBatchProcessor` do Aspose.OCR permite executar reconhecimentos em paralelo, acelerando drasticamente a etapa de **converter páginas digitalizadas em pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Dica profissional:** Se você estiver em uma máquina apenas com CPU, defina `ProcessingMode = ProcessingMode.Cpu`. O processador em lote ainda respeitará `MaxDegreeOfParallelism`, permitindo ajustá‑lo para evitar sobrecarga da máquina.

## Etapa 3 – Executar OCR no Lote e Coletar Resultados

Agora realmente reconhecemos o texto. O método `Recognize` retorna uma lista de objetos `OcrResult`, cada um contendo tanto a imagem original quanto o texto extraído.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Neste ponto você tem tudo que precisa para **criar PDF pesquisável**: as imagens (ainda na memória) e as camadas de texto associadas.

## Etapa 4 – **Combinar Imagens Verticalmente** e Gerar o PDF Pesquisável

A maioria dos documentos digitalizados são PDFs de várias páginas, portanto precisamos unir as imagens de cada página em uma única imagem alta que reflita uma pilha física. O Aspose.OCR fornece `Image.CombineVertical` exatamente para esse propósito.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

O arquivo resultante (`combined_searchable.pdf`) contém texto selecionável e pesquisável sob cada imagem de página — exatamente o que você precisa para **criar PDF pesquisável** a partir de fontes digitalizadas.

![Exemplo de criação de PDF pesquisável](/images/create-searchable-pdf.png "exemplo de criação de pdf pesquisável")

*Texto alternativo da imagem: exemplo de criação de PDF pesquisável mostrando um PDF combinado com texto pesquisável.*

**Por que empilhar verticalmente?** Muitas bibliotecas OCR tratam cada imagem como uma página separada. Ao empilhá‑las, mantemos a ordem das páginas do PDF intacta enquanto ainda utilizamos uma única passagem de OCR para todo o documento.

## Etapa 5 – Exportar JSON Detalhado da Primeira Página (Ótimo para Fluxos de Trabalho Posteriores)

Às vezes você precisa de mais do que um PDF; talvez queira alimentar os dados de OCR em um banco de dados ou em um pipeline de aprendizado de máquina. O Aspose.OCR permite serializar cada `OcrResult` para JSON, preservando caixas delimitadoras, pontuações de confiança e muito mais.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Trecho esperado de JSON (truncado):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Agora você pode enviar esse JSON para qualquer sistema posterior — seja indexando o texto no Elasticsearch ou alimentando um painel de análise personalizado.

---

## Como **Empilhar Imagens Verticalmente** – Um Resumo Rápido

Se você está se perguntando **como empilhar imagens verticalmente** sem o Aspose, poderia usar `System.Drawing` para criar um novo bitmap e desenhar cada página uma após a outra. No entanto, o `Image.CombineVertical` nativo do Aspose lida com DPI, formato de pixel e gerenciamento de memória para você, tornando‑a a escolha mais confiável para código de produção.

### Alternativa: Usando `System.Drawing` (apenas por curiosidade)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

A abordagem manual funciona, mas você perde a conveniência do tratamento automático de DPI e a capacidade de alimentar diretamente o resultado de volta ao `RecognizeToPdf`. Mantenha `CombineVertical` a menos que tenha um requisito muito específico.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Erros de falta de memória** ao processar dezenas de digitalizações de alta resolução | Cada imagem permanece na memória até que o PDF seja escrito | Descarte os objetos `Image` assim que terminar (`blocos using`) ou reduza a escala das imagens antes de combinar |
| **Texto lixo** após OCR | Digitalizações inclinadas ou baixo contraste | Mantenha o `DeskewFilter` e o `DenoiseFilter`; considere adicionar `ContrastFilter` se necessário |
| **Camada pesquisável ausente** | Usou `Recognize` em vez de `RecognizeToPdf` | Certifique‑se de chamar `ocrEngine.RecognizeToPdf` na imagem combinada |
| **Falha no fallback da GPU** em máquinas sem drivers adequados | `ProcessingMode.Gpu` lança uma exceção | Envolva a criação do motor em um try/catch e faça fallback para `ProcessingMode.Cpu` |

## Próximos Passos – Estendendo o Fluxo de Trabalho

Agora que você sabe como **criar PDF pesquisável**, talvez queira:

- **Processar em lote pastas inteiras** usando `Directory.GetFiles` e um loop `foreach`.
- **Adicionar marcas d'água** a cada página antes de combinar (use `ImageProcessor` do Aspose.Imaging).
- **Dividir o PDF pesquisável de volta em páginas individuais** se precisar de PDFs por página mais tarde (`PdfDocument.Split` do Aspose.PDF).
- **Integrar com Azure Blob Storage** para obter imagens da nuvem e enviar o PDF final de volta.

Todas essas extensões naturalmente envolvem os mesmos conceitos principais: configuração de OCR, manipulação de imagens e exportação de PDF.

---

## Conclusão

Cobremos tudo o que você precisa para **criar PDF pesquisável** a partir de uma coleção de imagens digitalizadas em C#. Ao inicializar um `OcrEngine` habilitado para GPU, executar um lote paralelo com `OcrBatchProcessor`, **combinar imagens verticalmente**, e finalmente chamar `RecognizeToPdf`, você obtém um documento organizado e pesquisável pronto para arquivamento ou indexação. A exportação adicional em JSON fornece total visibilidade dos resultados de OCR, abrindo portas para análises ou fluxos de trabalho personalizados.

Experimente, teste diferentes filtros e observe seu pipeline de automação de documentos ficar muito mais fluido. Se encontrar algum problema, deixe um comentário — feliz codificação!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}