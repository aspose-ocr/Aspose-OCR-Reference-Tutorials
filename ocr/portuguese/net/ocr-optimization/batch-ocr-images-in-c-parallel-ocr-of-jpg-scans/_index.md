---
category: general
date: 2026-04-29
description: Faça OCR em lote de imagens rapidamente com Aspose OCR em C#. Aprenda
  como extrair texto de arquivos jpg, ler texto de digitalizações e processar a lista
  de imagens em paralelo.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: pt
og_description: Faça OCR em lote de imagens rapidamente com o Aspose OCR. Este guia
  mostra como extrair texto de JPG, ler texto de digitalizações e processar uma lista
  de imagens em paralelo.
og_title: Processamento em lote de OCR de imagens em C# – OCR paralelo de digitalizações
  JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: OCR em lote de imagens em C# – OCR paralelo de digitalizações JPG
url: /pt/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR em lote de imagens em C# – OCR paralelo de digitalizações JPG

Já precisou fazer **batch OCR images** mas não tinha certeza de como escalar o trabalho entre vários arquivos? Você não está sozinho—desenvolvedores frequentemente encontram um obstáculo ao tentar ler texto de digitalizações uma a uma. A boa notícia é que com Aspose OCR você pode **extract text from jpg** files, **read text from scans**, e **process image list** items em paralelo com apenas algumas linhas de C#.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra exatamente como fazer isso. Ao final, você terá um aplicativo console autônomo que reconhece uma pasta de digitalizações JPEG, imprime o texto de cada página e informa quanto tempo cada operação levou. Sem documentos externos para procurar, sem trechos de código incompletos—apenas uma solução completa que você pode inserir no Visual Studio e executar.

## O que você precisará

- **.NET 6.0** ou posterior (o código também compila no .NET Framework 4.6+)
- **Aspose.OCR** pacote NuGet (`Install-Package Aspose.OCR`)
- Um conjunto de arquivos JPG ou imagens digitalizadas que você deseja processar
- Qualquer IDE que preferir; eu estou usando Visual Studio 2022, mas VS Code funciona bem também

É isso. Se você já tem o pacote NuGet, está pronto para começar.

## Etapa 1 – Inicializar o mecanismo OCR (Configuração de Batch OCR Images)

A primeira coisa que fazemos é criar uma instância de `OcrEngine` e informar a linguagem a ser procurada. Na maioria dos casos, o inglês é suficiente, mas você pode substituir `OcrLanguage.English` por qualquer linguagem suportada.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Por que isso importa:* Inicializar o mecanismo uma única vez e reutilizá‑lo em todas as imagens é muito mais eficiente do que criar uma nova instância por arquivo. Também permite que a Aspose compartilhe recursos internos, o que é essencial para **parallel OCR processing**.

## Etapa 2 – Construir a lista de imagens (Process Image List)

Em seguida, definimos a coleção de caminhos de arquivos que queremos alimentar ao reconhecedor em lote. Você pode gerar essa lista dinamicamente com `Directory.GetFiles`, mas para clareza vamos codificar manualmente algumas entradas.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Dica:* Se você tem milhares de digitalizações, considere usar `Directory.EnumerateFiles` com um filtro como `*.jpg` para evitar carregar a lista inteira na memória de uma só vez.

## Etapa 3 – Executar o reconhecimento em lote (Parallel OCR Processing)

Agora vem a parte central: chamar `BatchRecognize`. O método aceita um argumento `maxDegreeOfParallelism`, que controla quantas threads a Aspose criará. Por padrão, ele usa quatro threads, mas você pode aumentar esse número se sua CPU tiver mais núcleos.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*O que está acontecendo nos bastidores?* A Aspose divide a coleção `imagePaths` em blocos, entrega cada bloco a uma thread separada e agrega os resultados. Esta é a forma mais eficiente de **extract text from jpg** files quando você tem uma **process image list** que pode ser tratada simultaneamente.

## Etapa 4 – Exibir os resultados (Read Text from Scans)

Finalmente, iteramos sobre a coleção `recognitionResults` e imprimimos o texto e o tempo de processamento de cada arquivo. O objeto `OcrResult` também fornece o nome do arquivo de origem, o que ajuda quando você precisa registrar ou armazenar a saída.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Saída esperada (exemplo):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Observe como cada bloco informa o nome do arquivo, quanto tempo o OCR levou e o texto extraído. Essa é exatamente a informação que você precisa ao **reading text from scans** em um pipeline de produção.

## Lidando com casos de borda comuns

| Situação | O que observar | Correção rápida |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` lançada dentro de `BatchRecognize` | Validar caminhos com `File.Exists` antes de adicioná‑los a `imagePaths`. |
| **Unsupported format** | Aspose lida apenas com imagens raster (JPG, PNG, BMP, TIFF). | Converter PDFs para imagens primeiro (usar Aspose.PDF) ou pular esses arquivos. |
| **Memory pressure** | Imagens muito grandes podem consumir muita RAM quando muitas threads são executadas. | Reduzir `maxDegreeOfParallelism` ou redimensionar imagens antes do OCR. |
| **Non‑English text** | Linguagem definida como English perderá outros scripts. | Alterar `Language = OcrLanguage.French` (ou uma combinação multilíngue). |

Essas dicas mantêm seu trabalho em lote robusto, especialmente quando você está **processing an image list** que vem de uploads de usuários ou de um arquivo digitalizado.

## Dica Pro – Ajustando o paralelismo

Se você executar isso em uma máquina de 8 núcleos, aumente o paralelismo para 6 ou 8 e observe a velocidade melhorar. Contudo, lembre‑se de que cada thread também consome memória para o bitmap. Uma boa regra prática:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Insira `maxThreads` em `BatchRecognize` para uma configuração dinâmica, consciente da máquina.

## Exemplo completo funcional (pronto para copiar e colar)

Abaixo está o programa completo, pronto para compilar. Basta substituir `YOUR_DIRECTORY` pelo caminho que contém suas digitalizações JPG.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Nota:** A linha `using System.IO;` é necessária para o auxiliar `Directory`. O código imprime uma mensagem amigável se nenhum JPG for encontrado, evitando uma falha silenciosa.

## Conclusão

Acabamos de demonstrar um fluxo de trabalho limpo de **batch OCR images** que **extracts text from jpg** files, **reads text from scans**, e processa eficientemente uma **process image list** usando **parallel OCR processing**. O exemplo completo e executável mostra exatamente como configurar o mecanismo, alimentá‑lo com uma coleção de arquivos e lidar com os resultados—tudo enquanto mantém o uso de memória e a contagem de threads sob controle.

Pronto para o próximo passo? Experimente trocar a linguagem para francês, adicionar conversão de PDF para imagem, ou armazenar o texto OCR em um banco de dados. O padrão permanece o mesmo: inicializar uma vez, alimentar uma lista e deixar a Aspose fazer o trabalho pesado em paralelo.

Tem perguntas ou quer compartilhar suas próprias adaptações? Deixe um comentário abaixo, e feliz codificação! 

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}