---
category: general
date: 2026-03-23
description: Extrair texto de imagem usando Aspose OCR em C# e aprender como adicionar
  um logger de console para feedback em tempo real.
draft: false
keywords:
- extract text from image
- add console logger
language: pt
og_description: Extraia texto de imagem com Aspose OCR e adicione um logger de console
  para monitorar o processo. Tutorial passo a passo em C#.
og_title: Extrair Texto de Imagem em C# – Guia Completo de Programação
tags:
- OCR
- C#
- logging
title: Extrair Texto de Imagem em C# – Guia Completo
url: /pt/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em C# – Guia Completo

Precisa **extrair texto de imagem** de forma rápida e confiável? Com o Aspose OCR você pode fazer exatamente isso em poucas linhas de C#.  
Vamos também mostrar como **adicionar logger de console** para que você possa observar o motor OCR sussurrando seu progresso diretamente no seu terminal.

Imagine que você tem um recibo escaneado, uma nota manuscrita ou uma página PDF salva como PNG. Você quer os caracteres brutos sem abrir uma interface pesada. Este tutorial guia você por uma solução completa, pronta‑para‑copiar‑e‑colar, que funciona hoje com .NET 6+ e a biblioteca mais recente do Aspose OCR.

Ao final deste guia você será capaz de:

* Carregar um arquivo de imagem e executar OCR para **extrair texto de imagem**.  
* Conectar um logger de console ao Aspose AI para ver o que a biblioteca está fazendo nos bastidores.  
* Aplicar o pós‑processador de verificação ortográfica embutido para limpar erros de OCR.  

> **Pré‑requisitos** – Um ambiente de desenvolvimento .NET funcional (Visual Studio 2022, VS Code ou Rider), .NET 6 SDK ou superior, e uma licença Aspose OCR (ou um teste gratuito). Nenhum outro pacote de terceiros é necessário.

---

## O que Você Precisa

| Item | Por que é importante |
|------|----------------------|
| **Aspose.OCR** NuGet package | Provides the `OcrEngine` class that actually reads the image. |
| **Aspose.OCR.AI** NuGet package | Gives you the `AsposeAI` post‑processor framework, including spell‑check. |
| **Microsoft.Extensions.Logging** (optional) | Supplies the `ILogger` interface for the **add console logger** step. |
| **An input image** (`input.png`) | The source file from which we’ll **extract text from image**. |

Você pode instalar os pacotes via terminal:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Etapa 1 – Extrair Texto de Imagem com Aspose OCR

A primeira coisa que fazemos é entregar a imagem ao motor OCR. Este bloco faz o trabalho pesado e devolve uma string bruta que ainda pode conter erros de ortografia.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Por que isso funciona:** `OcrEngine` abstrai todo o pré‑processamento de imagem de baixo nível (binarização, correção de inclinação, etc.). Quando `Recognize()` retorna `true`, a propriedade `Text` já contém os caracteres com a melhor estimativa.  

> **Dica:** Se sua imagem for grande, considere redimensioná‑la para ≤ 2000 px no lado mais longo antes de enviá‑la ao motor. Isso acelera o processamento sem prejudicar a precisão.

---

## Etapa 2 – Adicionar Logger de Console para Visão em Tempo Real

Agora trazemos a parte **add console logger**. O logging não serve apenas para depuração; ele oferece visibilidade sobre downloads de modelos, etapas do processador de IA e quaisquer avisos que a biblioteca possa emitir.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Você pode agora conectar esse logger ao Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**O que você verá:** Quando o modelo de verificação ortográfica for baixado automaticamente, o console imprimirá uma linha como:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Essa é a vantagem do **add console logger** – você nunca ficará em dúvida se uma operação em segundo plano foi bem‑sucedida.

---

## Etapa 3 – Configurar e Registrar o Processador Pós‑Processamento de Verificação Ortográfica

Aspose AI vem com um prático pós‑processador de verificação ortográfica que limpa erros comuns de OCR (por exemplo, “rec0gn1ze” → “recognize”). Vamos configurá‑lo, opcionalmente informar à biblioteca onde armazenar o modelo e, em seguida, registrá‑lo.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Por que você pode querer um caminho personalizado:** Em pipelines CI/CD costuma‑se armazenar modelos em um diretório conhecido para evitar downloads repetidos. O sinalizador `AllowAutoDownload` garante que o modelo seja obtido na primeira execução do código.

---

## Etapa 4 – Executar o Pós‑Processador no Resultado do OCR

Com o texto OCR em mãos e o processador de verificação ortográfica pronto, entregamos a string bruta ao `AsposeAI`. O motor executa o modelo, e o processador armazena o texto corrigido internamente.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Após esta chamada, `spellProcessor` contém uma coleção de objetos `RecognitionResult`, cada um com a propriedade `RecognitionText` que contém a versão limpa.

---

## Etapa 5 – Recuperar e Exibir o Texto Corrigido

Finalmente extraímos a string corrigida do processador e a imprimimos. Este é o momento em que você realmente vê o benefício tanto do OCR quanto do fluxo **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Saída esperada** (supondo que a imagem contenha a frase “Aspose OCR demo” com alguns defeitos de OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Observe como o logger informou que o modelo estava pronto, e a linha corrigida aparece limpa.

---

## Etapa 6 – Limpar Recursos

Tanto `AsposeAI` quanto `OcrEngine` implementam `IDisposable`. Dispor deles libera memória nativa e handles de arquivos, o que é especialmente importante em serviços de longa duração.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Exemplo Completo Funcional

Abaixo está o programa inteiro que você pode copiar‑colar em um novo projeto console (`dotnet new console`). Substitua `"YOUR_DIRECTORY"` por uma pasta real na sua máquina.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}