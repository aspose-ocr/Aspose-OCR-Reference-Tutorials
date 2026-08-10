---
category: general
date: 2026-05-02
description: Tutorial de OCR em C# que mostra como extrair texto de imagem em C# e
  reconhecer texto em PNG, depois escrever JSON indentado usando JsonSerializer em
  C#. Guia passo a passo para desenvolvedores.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: pt
og_description: Tutorial de OCR em C# que demonstra como extrair texto de imagem em
  C# e reconhecer texto em PNG, e então escrever JSON indentado com JsonSerializer
  C#. Exemplo completo e executável.
og_title: Tutorial de OCR em C# – Extrair Texto e Exportar como JSON Indentado
tags:
- OCR
- C#
- Aspose
- JSON
title: Tutorial de OCR em C# – Extrair texto de imagens e exportar como JSON indentado
url: /pt/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extrair Texto de Imagens e Exportar como JSON Indentado

Já precisou de um **c# ocr tutorial** que vá de uma foto de texto direto para um arquivo JSON bem formatado? Você não é o único. Em muitos projetos – pense em digitalização de faturas, análise de recibos ou até extração simples de texto de memes – você acaba com um arquivo PNG e se pergunta como extrair as palavras sem escrever um reconhecedor personalizado.  

Este guia oferece uma solução prática: vamos **extract text image c#** usando Aspose.OCR, **recognize png text**, e então **write indented json** com `JsonSerializer` em C#. Ao final, você terá um aplicativo console autônomo que pode ser inserido em qualquer solução .NET. Sem links vagos de “veja a documentação”, apenas um exemplo completo, pronto para copiar e colar.

## O que você precisará

- **.NET 6** (ou qualquer versão recente do .NET). Frameworks mais antigos funcionam, mas a sintaxe mostrada tem como alvo .NET 6+.
- **Aspose.OCR for .NET** – instale via NuGet: `dotnet add package Aspose.OCR`.
- Uma imagem PNG de exemplo (`text.png`) contendo texto claro e legível por máquina.
- Uma IDE ou editor de sua escolha – Visual Studio, VS Code, Rider, etc.

> **Dica profissional:** Se você planeja processar muitas imagens, considere reutilizar uma única instância de `OcrEngine` em vez de criar uma nova para cada arquivo. Isso reduz a sobrecarga e melhora o rendimento.

## Etapa 1: Configurar um Projeto c# ocr tutorial

Primeiro, crie um projeto console. Os comandos a seguir criam a estrutura e adicionam a biblioteca OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Agora abra o `Program.cs` gerado. Substituiremos seu conteúdo pelo exemplo completo mais tarde, mas por enquanto apenas verifique se o projeto compila:

```bash
dotnet build
```

Se não houver erros, você está pronto para prosseguir.

## Etapa 2: Reconhecer Texto PNG de uma Imagem

O núcleo de qualquer **c# ocr tutorial** é o próprio motor OCR. Aspose.OCR abstrai os detalhes de baixo nível e fornece uma classe `OcrEngine` limpa. A seguir, criamos o motor, apontamos para um arquivo PNG e solicitamos que reconheça o texto.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Por que isso funciona

- **`RecognizeImage`** aceita vários formatos (PNG, JPEG, BMP). Nós especificamente **recognize png text** porque PNG preserva detalhes sem perdas, o que é ideal para OCR.
- O `OcrResult` retornado contém não apenas o texto puro, mas também uma pontuação de confiança por glifo, útil caso você precise filtrar caracteres de baixa confiança posteriormente.

## Etapa 3: Escrever JSON Indentado com JsonSerializer c#

Agora que temos `ocrResult`, o próximo passo lógico em nosso **c# ocr tutorial** é transformar esse objeto em JSON legível por humanos. O serializador interno `System.Text.Json` faz o trabalho, e vamos configurá‑lo para **write indented json** por clareza.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Usando `JsonSerializer` corretamente

- A flag `WriteIndented` é a maneira mais simples de **write indented json** sem usar bibliotecas de terceiros.
- Se precisar de nomes de propriedades em camel‑case, adicione `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` às opções.
- A string `jsonOutput` pode ser salva com `File.WriteAllText("result.json", jsonOutput);` – um ajuste útil para pipelines do mundo real.

## Etapa 4: Executar e Verificar a Saída

Compile e execute o programa:

```bash
dotnet run
```

Assumindo que `text.png` contém a frase *“Hello, OCR World!”*, você deverá ver algo como:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Esse JSON está **indented**, facilitando a leitura em logs ou a entrega para serviços downstream.

### Casos de Borda e Dicas

| Situação | O que fazer |
|-----------|------------|
| **Imagem está borrada** | Aumente `ocrEngine.Config.Dpi` (por exemplo, `ocrEngine.Config.Dpi = 300`) antes de chamar `RecognizeImage`. |
| **Idioma não‑inglês** | Defina `ocrEngine.Config.Language = OcrLanguage.German` (ou qualquer idioma suportado). |
| **Grande lote de arquivos** | Percorra um diretório, reutilizando a mesma instância de `OcrEngine`; armazene cada resultado JSON com um nome de arquivo único. |
| **Precisa apenas de texto de alta confiança** | Filtre `ocrResult.Lines` onde `Confidence` ≥ 0.95 antes da serialização. |

## Exemplo Completo Funcional (Pronto para Copiar e Colar)

Abaixo está o programa *inteiro*, pronto para ser inserido em `Program.cs`. Ele inclui todas as etapas, tratamento de erros e comentários que tornam o código autoexplicativo.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Execute o código, inspecione o console ou o arquivo `.json` gerado, e você verá o texto extraído junto com as pontuações de confiança, tudo bem **indented**.

## Conclusão

Agora você tem um sólido **c# ocr tutorial** que mostra como **extract text image c#**, **recognize png text**, e **write indented json** usando `JsonSerializer`. O exemplo está completo, executável e inclui dicas práticas para cenários reais.  

Próximos passos? Experimente substituir o Aspose.OCR por outro motor (por exemplo, Tesseract) e veja como a estrutura do `OcrResult` muda, ou envie o JSON para uma API downstream que armazena os dados OCR em um banco de dados. Você também pode experimentar opções de **use jsonserializer c#** como conversores personalizados para formatação de datas ou tratamento de enumerações.

Feliz codificação, e que seus pipelines OCR sejam sempre precisos!  

---  

![diagrama do tutorial c# ocr](image.png "Diagrama ilustrando o fluxo OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}