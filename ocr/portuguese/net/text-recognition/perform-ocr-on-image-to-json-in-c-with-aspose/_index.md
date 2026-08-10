---
category: general
date: 2026-04-08
description: Aprenda como realizar OCR em imagens e gerar um arquivo JSON em C# usando
  Aspose OCR. Este tutorial de Aspose OCR em C# mostra a conversão de imagem OCR para
  JSON com valores de confiança.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: pt
og_description: Execute OCR em imagem e exporte os resultados para um arquivo JSON
  em C#. Este tutorial cobre todo o fluxo de trabalho do Aspose OCR em C#, incluindo
  pontuações de confiança.
og_title: Realize OCR em Imagem para JSON em C# – Guia de OCR da Aspose
tags:
- Aspose
- OCR
- C#
- JSON
title: Realizar OCR em imagem para JSON em C# com Aspose
url: /pt/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em Imagem para JSON em C# com Aspose

Já precisou **executar OCR em imagens** mas não tinha certeza de como obter os resultados em um formato estruturado? Você não está sozinho—os desenvolvedores perguntam constantemente: “Como transformar uma foto escaneada em dados utilizáveis?” A boa notícia é que o Aspose.OCR torna isso muito fácil, e você pode até **write JSON file C#**‑style com pontuações de confiança incluídas.

Neste guia, percorreremos um **aspose OCR C# tutorial** completo que cobre tudo, desde o carregamento de uma imagem até a exportação do texto reconhecido como JSON. Ao final, você terá um aplicativo de console executável que **perform OCR on image**, converte a saída para JSON (incluindo valores de confiança) e a salva com uma única linha de código. Sem etapas ocultas, sem scripts externos—apenas C# puro.

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 SDK ou posterior (o código funciona também com .NET Core e .NET Framework)
- Visual Studio 2022 (ou qualquer editor de sua preferência)
- Uma licença válida do **Aspose.OCR for .NET** ou uma licença temporária gratuita (o teste gratuito funciona para experimentação)
- Um arquivo de imagem (`input.png`) que você deseja processar (qualquer formato comum—PNG, JPG, BMP—serve)

É isso. Se estiver faltando algum desses itens, obtenha‑os agora; o resto do tutorial assume que já estão configurados.

## Etapa 1: Instalar o Pacote NuGet Aspose.OCR

Primeiro de tudo—adicione a biblioteca ao seu projeto. Abra um terminal na pasta do projeto e execute:

```bash
dotnet add package Aspose.OCR
```

## Etapa 2: Inicializar o Motor OCR (Perform OCR on Image)

Agora criamos uma instância de `OcrEngine` e informamos qual idioma usar. Inglês (`"en"`) é o mais comum, mas você pode trocá‑lo por `"fr"`, `"de"` ou qualquer idioma suportado.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Por que inicializamos aqui:** O `OcrEngine` contém toda a configuração necessária para o processo de reconhecimento. Definir o idioma antecipadamente garante que o motor use o conjunto de caracteres correto, o que melhora drasticamente a precisão.

## Etapa 3: Reconhecer a Imagem e Capturar a Confiança

Com o motor pronto, alimentamos o arquivo de imagem. O método `RecognizeImage` retorna um objeto `OcrResult` que contém tanto o texto extraído quanto uma pontuação de confiança para cada palavra.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**O que está acontecendo nos bastidores?** Aspose executa um reconhecedor baseado em rede neural que analisa cada bloco de pixels, compara‑o com seu modelo de idioma e anexa um valor de confiança (0‑100) que indica o quão certo está sobre cada palavra.

## Etapa 4: Converter o Resultado para JSON (OCR Image to JSON)

Aspose torna a conversão simples. Ao passar `includeConfidence: true` obtemos um payload JSON que se parece com isto:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Aqui está o código que produz a string JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Por que incluir a confiança?** Se você pretende alimentar os dados em processos subsequentes (por exemplo, validação, destaque na UI), saber quais palavras são incertas permite decidir se deve solicitar confirmação ao usuário.

## Etapa 5: Gravar o Arquivo JSON no Estilo C#

Agora realmente **write JSON file C#**. O método `File.WriteAllText` é atômico e funciona em múltiplas plataformas, tornando‑o perfeito para aplicativos de console.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Esse é todo o fluxo de trabalho—cinco etapas concisas que **perform OCR on image**, transformam a saída em JSON e a persistem.

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em `Program.cs`. Certifique‑se de que `input.png` esteja na mesma pasta que o binário compilado ou ajuste os caminhos conforme necessário.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Saída Esperada

Ao executar o programa (`dotnet run`), você verá algo como:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

E `output.json` conterá o JSON estruturado mostrado anteriormente, completo com percentuais de confiança para cada palavra.

## Dicas Profissionais & Casos de Borda

- **Missing file handling:** Envolva a chamada `RecognizeImage` em um `try/catch` para `FileNotFoundException` se você esperar caminhos dinâmicos.
- **Different languages:** Defina `ocrEngine.Language = "fr"` para francês, ou carregue um pacote de idioma personalizado via `ocrEngine.LoadLanguage("custom.lang")`.
- **Large documents:** Para PDFs de várias páginas, converta cada página em imagem primeiro (por exemplo, usando `Aspose.PDF`) e itere pelas etapas de OCR.
- **Performance tuning:** Se você precisar apenas de resultados rápidos, troque para `RecognitionMode.Fast`—você perde um pouco de precisão, mas ganha velocidade.
- **JSON formatting:** Quer JSON formatado de forma legível? Use `JsonConvert.SerializeObject` do Newtonsoft com `Formatting.Indented` após desserializar a string JSON do Aspose.

## Perguntas Frequentes

**Q: Isso funciona com .NET Framework?**  
A: Absolutamente. O mesmo pacote NuGet tem alvo .NET Standard 2.0, então você pode referenciá‑lo a partir do .NET Framework 4.6.1 e versões mais recentes.

**Q: E se eu precisar da confiança para o documento inteiro, não por palavra?**  
A: O `OcrResult` também expõe `OverallConfidence`. Você pode adicioná‑la manualmente ao JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Posso transmitir o JSON diretamente para uma API web?**  
A: Sim. Substitua `File.WriteAllText` por um POST de `HttpClient` que envia `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}