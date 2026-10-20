---
category: general
date: 2026-03-13
description: Como fazer OCR em lote de forma rápida e confiável enquanto aprende a
  extrair texto de arquivos TIFF usando Aspose.OCR. Siga este tutorial passo a passo.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: pt
og_description: Aprenda a fazer OCR em lote em C# e extrair texto de arquivos TIFF
  com Aspose.OCR. Este guia cobre a configuração, o código e dicas de boas práticas.
og_title: Como fazer OCR em lote em C# – Guia completo de programação
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Como fazer OCR em lote no C# – Guia completo de programação
url: /pt/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em C# – Guia de Programação Completo

Já se perguntou **como fazer OCR em lote** em uma montanha de faturas escaneadas sem precisar escrever um script separado para cada arquivo? Você não está sozinho. Em muitos projetos do mundo real, o ponto crítico não é a precisão do OCR em si, mas o grande volume de imagens — frequentemente TIFFs — que precisam ser convertidas em texto pesquisável.  

Este tutorial mostra a você **como fazer OCR em lote** usando o `BatchProcessor` do Aspose.OCR, ao mesmo tempo em que ensina **como extrair texto de tiff** arquivos em uma única execução limpa. Ao final, você terá um aplicativo console pronto‑para‑executar que processa uma pasta inteira, aproveita a aceleração opcional de GPU e gera resultados em texto simples onde você precisar.

## O que você precisará

- **.NET 6+** (ou .NET Framework 4.7.2 se preferir o runtime clássico)  
- **Aspose.OCR for .NET** – você pode obter o pacote NuGet com `dotnet add package Aspose.OCR`.  
- Uma pasta de imagens **TIFF** que você deseja ler (o tutorial usa `Invoices` como exemplo).  
- Opcional: uma GPU que suporte DirectX 11 ou CUDA se você quiser acelerar o processo.  

Sem serviços extras, sem chaves de nuvem — apenas um projeto C# local e a biblioteca Aspose.

## Etapa 1: Configurar o Projeto e Instalar o Aspose.OCR

Primeiro, crie um aplicativo console.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você está no Windows e planeja usar aceleração de GPU, certifique‑se de que o driver gráfico mais recente está instalado. Caso contrário, a flag `UseGpu = true` retornará automaticamente para a CPU.

## Etapa 2: Criar a Configuração do BatchProcessor

Agora vamos configurar o `BatchProcessor`. Este é o coração de **como fazer OCR em lote** — você informa ao Aspose qual idioma esperar, quais filtros de pré‑processamento aplicar e se deve usar a GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Por que essas configurações?**  
- `Language = Language.English` indica ao motor para usar o modelo de idioma inglês, que é muito mais preciso que o modelo genérico.  
- `UseGpu` pode reduzir o tempo de processamento pela metade em uma GPU decente, mas é seguro deixá‑lo `false` se você estiver em um laptop sem GPU.  
- O pipeline de filtros reflete o que um humano faria: endireitar a página e limpar manchas antes de enviá‑la ao motor de OCR.

## Etapa 3: Apontar o Processador para sua Pasta TIFF

A próxima parte de **como fazer OCR em lote** é informar à biblioteca onde os arquivos de origem estão. Curingas são suportados, então você pode capturar todos os arquivos `.tif` de uma vez.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Caso extremo:** Se suas imagens têm extensões misturadas (`.tiff`, `.tif`, `.png`), chame `AddFolder` várias vezes ou use `*.*` e filtre depois no código.

## Etapa 4: Escolher Onde os Resultados do OCR Serão Salvos

Você pode se perguntar: “Onde o texto extraído termina?” Essa é a terceira base de **como fazer OCR em lote** — definir o local e o formato de saída. Vamos armazenar arquivos de texto simples ao lado dos originais.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Se você precisar de JSON ou XML em vez de texto simples, basta trocar `OutputFormat.PlainText` por `OutputFormat.Json` ou `OutputFormat.Xml`. A biblioteca cuida da conversão para você.

## Etapa 5: Executar o Trabalho em Lote e Relatar Resultados

Finalmente, dispare o trabalho. O método `Execute` bloqueia até que todos os arquivos sejam processados, então você pode inspecionar `ProcessedCount` para confirmar o sucesso.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Saída Esperada

Quando você executar o programa, o console imprimirá algo como:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Na pasta `Output` você encontrará um arquivo `.txt` para cada TIFF de origem, cada um nomeado como a imagem original (por exemplo, `Invoice_001.txt`). Abra qualquer arquivo e você verá o texto OCR bruto — perfeito para alimentar um índice de busca ou um pipeline de extração de dados subsequente.

## Lidando com Problemas Comuns

### 1. GPU Não Disponível

Se `UseGpu = true` mas nenhum dispositivo compatível for encontrado, o Aspose reverte silenciosamente para a CPU. Para ser explícito, você pode capturar a `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Arquivos Não‑TIFF na Mesma Pasta

Quando você tem uma pasta mista, filtre programaticamente:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Arquivos Grandes Excedendo a Memória

Para TIFFs multi‑página gigantes, habilite streaming:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Dicas Profissionais para Melhor Precisão ao **extrair texto de tiff**

- **Resolução importa** – Almeje 300 dpi ou mais. Abaixo disso, o motor de OCR pode perder caracteres.  
- **Cor vs. Escala de Cinza** – Converta digitalizações coloridas para escala de cinza antes do OCR; o `DeskewFilter` já faz isso nos bastidores, mas você pode adicionar `ColorDepthReductionFilter` para maior velocidade.  
- **Pós‑processamento** – Depois de ter o texto simples, execute uma verificação ortográfica ou limpeza com regex para corrigir peculiaridades comuns do OCR (por exemplo, “0” vs “O”).

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo que você pode compilar e executar. Basta substituir os caminhos de placeholder pelos seus próprios diretórios.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Compile e execute:

```bash
dotnet run
```

Agora você deve ter um conjunto organizado de arquivos `.txt` — cada um o resultado de **extrair texto de tiff** por meio de um processo em lote totalmente automatizado.

## Conclusão

Nós percorremos **como fazer OCR em lote** em C# do início ao fim, cobrindo tudo que você precisa para **extrair texto de tiff** arquivos de forma eficiente. Os principais pontos são:

1. Use o `BatchProcessor` do Aspose.OCR para evitar escrever loops repetitivos.  
2. Aproveite os filtros de pré‑processamento (deskew, despeckle) para maior precisão.  
3. Habilite a aceleração de GPU quando possível, mas sempre tenha um fallback para CPU.  
4. Armazene os resultados em uma estrutura de pastas previsível para que trabalhos subsequentes possam capturá‑los automaticamente.

A partir daqui você pode explorar:

- Alimentar o texto simples em um **índice de busca** (ex.: Elasticsearch) para tornar as faturas pesquisáveis.  
- Converter a saída para **JSON** e enviá‑la a um modelo de aprendizado de máquina que extrai itens de linha.  
- Adicionar **tratamento de erros** para TIFFs corrompidos ou problemas de permissão.

Experimente,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}