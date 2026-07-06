---
category: general
date: 2026-04-26
description: Como fazer OCR em lote de imagens PNG rapidamente. Aprenda a extrair
  texto de PNG, converter imagens em texto, gravar o texto reconhecido e ler o diretório
  de PNG com Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: pt
og_description: Como fazer OCR em lote de imagens PNG em C# com Aspose OCR. Este guia
  mostra como extrair texto de PNG, converter imagens em texto e gravar o texto reconhecido
  de forma eficiente.
og_title: Como fazer OCR em lote de imagens PNG em C# – Passo a passo
tags:
- OCR
- C#
- Aspose
title: Como fazer OCR em lote de imagens PNG em C# – Guia completo
url: /pt/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote de imagens PNG em C# – Guia Completo

Já se perguntou **como fazer OCR em lote** de uma pasta inteira de arquivos PNG sem escrever um programa separado para cada imagem? Você não é o único lidando com dezenas de capturas de tela, recibos escaneados ou gráficos que precisam ser convertidos em texto pesquisável. Neste tutorial, vamos percorrer uma solução prática que **extrai texto de PNG**, **converte imagens em texto** e **grava o texto reconhecido** em arquivos individuais — tudo enquanto lê o diretório PNG automaticamente.

Ao final deste guia, você terá um aplicativo de console C# pronto‑para‑executar que processa qualquer quantidade de imagens de uma só vez. Sem scripts extras, sem copiar‑colar manual — apenas código puro que faz o trabalho pesado por você.

## O que você precisará

- **.NET 6.0** ou superior (o código funciona bem também no .NET Framework).  
- Pacote NuGet **Aspose.OCR for .NET** (a versão de avaliação gratuita funciona para testes).  
- Uma pasta com alguns arquivos *.png* que você deseja fazer OCR.  
- Visual Studio 2022 ou qualquer IDE C# de sua preferência.

Se você tem tudo isso, podemos ir direto à implementação.

## Etapa 1 – Prepare suas pastas de entrada e saída *(Ler diretório PNG)*

A primeira coisa que fazemos é apontar o programa para a pasta que contém as imagens e decidir onde os arquivos *.txt* resultantes serão armazenados. Usar `Directory.GetFiles` nos fornece um enumerável limpo de todos os PNGs no diretório.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Por que isso importa:**  
- Usar um curinga (`*.png`) garante que apenas arquivos de imagem sejam processados, ignorando quaisquer documentos soltos.  
- Criar a pasta de saída dinamicamente evita uma `DirectoryNotFoundException` mais tarde.

> **Dica profissional:** Se precisar suportar outros formatos (JPEG, BMP), basta estender o padrão de busca ou chamar `Directory.EnumerateFiles` com múltiplas extensões.

## Etapa 2 – Inicialize o motor OCR *(Converter imagens em texto)*

O Aspose.OCR vem com dois tipos de motor: um `OcrEngine` baseado em CPU e um `GpuOcrEngine` acelerado por GPU. Para a maioria dos trabalhos em lote, o motor CPU é perfeitamente adequado, mas você pode trocar o nome da classe se possuir uma GPU capaz.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Por que isso importa:**  
- Especificar o idioma melhora drasticamente a precisão porque o motor sabe qual conjunto de caracteres esperar.  
- Trocar para `GpuOcrEngine` é uma mudança de uma linha se você encontrar gargalos de desempenho em lotes grandes.

## Etapa 3 – Crie um Reconhecedor em Lote

O Aspose fornece um conveniente `BatchRecognizer` que aceita um enumerável de caminhos de arquivos e transmite os resultados um a um. Isso evita carregar todas as imagens na memória de uma só vez — um detalhe crucial para pastas grandes.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Por que isso importa:**  
- O reconhecedor em lote encapsula a lógica de loop, permitindo que nos concentremos no que fazer com cada resultado ao invés de como iterar com segurança.

## Etapa 4 – Execute OCR em todas as imagens e grave a saída *(Gravar texto reconhecido)*

Agora realmente executamos o OCR. O método `Recognize` retorna um `IEnumerable<RecognitionResult>` onde cada resultado contém o texto extraído e outros metadados.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Por que isso importa:**  
- Usar `File.WriteAllText` garante que o texto seja salvo com codificação UTF‑8 por padrão, preservando caracteres especiais.  
- A nomeação incremental (`out_0.txt`, `out_1.txt`) corresponde à ordem de processamento, o que é útil para depuração.

> **Caso extremo:** Se alguma imagem falhar no OCR (por exemplo, arquivo corrompido), `RecognitionResult.Text` ficará vazio. Você pode adicionar uma verificação simples dentro do loop para registrar falhas:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Etapa 5 – Junte tudo – Exemplo completo funcionando

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Ele inclui as diretivas `using`, validação de pastas e uma pequena interface de console para que você saiba quando o lote termina.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Saída esperada:**  
Executar o programa imprime algo como:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

E você verá `out_0.txt` … `out_11.txt` dentro da pasta de saída, cada um contendo a versão em texto puro da sua imagem correspondente.

## Perguntas Frequentes & Dicas

| Pergunta | Resposta |
|----------|----------|
| *Posso fazer OCR em subpastas também?* | Sim — substitua `Directory.GetFiles` por `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *E se eu precisar de um idioma diferente?* | Defina `ocrEngine.Language = Language.Spanish;` (ou qualquer enum suportado). |
| *Como lidar com lotes enormes (milhares de arquivos)?* | Considere processar em blocos ou usar `Parallel.ForEach` com um grau de paralelismo limitado para evitar esgotar a memória. |
| *A saída é sempre UTF‑8?* | `File.WriteAllText` tem UTF‑8 sem BOM como padrão, o que funciona para a maioria dos idiomas baseados em latim. Para scripts asiáticos pode ser necessário definir `Encoding.UTF8` explicitamente. |
| *Posso obter pontuações de confiança?* | `RecognitionResult` expõe `Confidence` — você pode registrá‑la junto ao texto para controle de qualidade. |

## Visão geral visual *(Como fazer OCR em lote – Diagrama)*

![Diagrama do fluxo de OCR em lote mostrando pasta de entrada → motor OCR → reconhecedor em lote → arquivos txt de saída](https://example.com/diagram-how-to-batch-ocr.png "Como fazer OCR em lote")

*O texto alternativo contém a palavra‑chave principal, atendendo aos requisitos de SEO para imagens.*

## Conclusão

Acabamos de cobrir **como fazer OCR em lote** de um diretório de arquivos PNG usando Aspose.OCR, desde a leitura do diretório PNG até a gravação de cada arquivo de texto reconhecido. A solução é totalmente autônoma, funciona em qualquer runtime .NET moderno e pode ser estendida para aceleração por GPU, suporte multilíngue ou processamento paralelo.

Pronto para o próximo passo? Experimente trocar `Language.Latin` por outro idioma, ou integre a saída em um índice de busca para que seus documentos se tornem pesquisáveis instantaneamente. O céu é o limite depois que você dominar o OCR em lote.

Feliz codificação, e me avise nos comentários se encontrar algum problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}