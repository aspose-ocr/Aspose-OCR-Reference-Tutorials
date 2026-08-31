---
category: general
date: 2026-01-02
description: Execute OCR em PNG rapidamente usando Aspose OCR e suporte GPU. Aprenda
  como reconhecer texto a partir de imagem, extrair texto de imagem e definir o limite
  de memória da GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: pt
og_description: Execute OCR em PNG de forma eficiente, aproveitando o Aspose OCR e
  a aceleração por GPU. Este tutorial mostra como reconhecer texto a partir de uma
  imagem, extrair texto da imagem e controlar o uso de memória da GPU.
og_title: Execute OCR em PNG com GPU – Guia Completo de C#
tags:
- OCR
- C#
- GPU
title: executar OCR em PNG com GPU – Guia Completo de C#
url: /pt/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em PNG com GPU – Guia Completo em C#

Já precisou **executar OCR em PNG** e se sentiu preso na questão de desempenho? Você não está sozinho. Em muitos pipelines do mundo real, um único PNG de alta resolução pode sobrecarregar um motor OCR apenas de CPU, transformando o que deveria ser uma busca rápida em uma espera de minutos.  

A boa notícia é que o Aspose OCR vem com extensões GPU que permitem **reconhecer texto de imagem** em uma fração do tempo. Neste tutorial, percorreremos um exemplo prático que mostra exatamente como **executar OCR em PNG** usando C#, como **extrair texto de imagem**, e até como **definir limite de memória GPU** para que você permaneça dentro do orçamento de hardware.  

Também abordaremos o “como” e o “por quê” de cada etapa, para que você saia com um modelo mental sólido — não apenas um trecho de código copy‑paste.

## O que você aprenderá

- Os pré‑requisitos para usar o suporte GPU do Aspose OCR.  
- Como carregar um PNG em um `Bitmap` e enviá‑lo para o motor OCR.  
- Como configurar `GpuDevice` e `GpuMemoryLimitMb` para desempenho ideal.  
- Como **reconhecer texto de imagem** e recuperar o resultado em texto simples.  
- Dicas para lidar com casos de borda comuns, como GPUs com pouca memória ou PNGs de várias páginas.  

Ao final deste guia, você será capaz de **executar OCR em PNG** com velocidade de GPU e controlar com confiança a pegada de memória de seus trabalhos OCR.

![Diagrama mostrando execução de OCR em PNG com aceleração GPU](run-ocr-on-png-diagram.png "exemplo de execução de OCR em PNG")

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

1. .NET 6.0 ou posterior (o código funciona com .NET Core e .NET Framework também).  
2. Uma GPU NVIDIA com suporte a CUDA (o exemplo escolhe o índice de dispositivo 0).  
3. O pacote NuGet Aspose.OCR e suas extensões GPU (`Aspose.OCR.Extensions`).  
4. Um PNG de exemplo (`input.png`) colocado em uma pasta que você pode referenciar a partir do seu projeto.  

Se algum desses lhe for desconhecido, não se preocupe — indicaremos alternativas onde for relevante.

---

## Etapa 1 – Instalar Aspose OCR e Extensões GPU

Primeiro as coisas. Sem as bibliotecas corretas, o resto do código não compilará.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

O pacote `Aspose.OCR.Extensions` traz os binários nativos CUDA necessários para a aceleração GPU.  
*Dica profissional:* Se você estiver em uma máquina sem GPU, ainda pode compilar o projeto; basta definir `PreferGpu = false` mais tarde.

---

## Etapa 2 – Carregar o PNG que Você Deseja Processar

Agora realmente **executamos OCR em PNG** carregando‑o em um `Bitmap`. Esta etapa é simples, mas vale uma observação rápida: `Bitmap` espera um caminho de arquivo, então certifique‑se de que o caminho esteja correto em relação ao seu executável.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Se o PNG for incomumente grande (por exemplo, > 5000 px de lado), talvez você queira redimensioná‑lo primeiro para evitar esgotar a memória GPU. É aí que a opção **definir limite de memória GPU** se torna útil mais adiante.

---

## Etapa 3 – Criar e Configurar o Motor OCR para Uso da GPU

Aqui está o coração do tutorial: configurar o motor OCR para **reconhecer texto de imagem** usando a GPU. Duas propriedades são essenciais:

- `GpuDevice` – seleciona qual dispositivo CUDA usar.  
- `GpuMemoryLimitMb` – limita a quantidade de memória GPU que o motor pode alocar.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Por que definir um limite de memória?** Algumas GPUs compartilham memória com a tela ou executam várias cargas de trabalho simultaneamente. Ao limitar a alocação, você evita falhas por falta de memória, especialmente ao processar muitos PNGs em paralelo.

---

## Etapa 4 – Definir Opções de Reconhecimento (Idioma & Preferência de GPU)

O objeto `RecognitionOptions` informa ao motor qual idioma procurar e se deve **preferir GPU** mesmo para imagens pequenas. Para a maioria dos documentos em inglês isso é suficiente, mas você pode trocar `Language.English` por outras localidades suportadas.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Se você precisar **extrair texto de imagem** em um idioma diferente do inglês, basta mudar o enum `Language`. A biblioteca suporta dezenas de idiomas nativamente.

---

## Etapa 5 – Executar o OCR e Recuperar o Resultado

Com tudo configurado, a chamada final é uma única linha que realmente **executa OCR em PNG** e retorna um objeto de resultado rico.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

O `OcrResult` contém não apenas texto simples (`ocrResult.Text`), mas também pontuações de confiança, caixas delimitadoras e até a imagem original com palavras destacadas — útil se precisar depurar ou visualizar a extração.

**Saída esperada** (para um PNG de exemplo que diz “Hello World”):

```
=== OCR Output ===
Hello World
```

Se o texto aparecer confuso, verifique se o PNG não está corrompido e se o limite de memória GPU não está muito baixo para o tamanho da imagem.

---

## Etapa 6 – Lidando com Casos de Borda e Dicas de Boas Práticas

### GPUs com Pouca Memória

Se você encontrar uma exceção como `CudaException: out of memory`, diminua `GpuMemoryLimitMb` ou divida o PNG em blocos antes do processamento. O tiling pode ser feito com `Graphics.DrawImage` em um clone de `Bitmap`.

### Vários PNGs em Lote

Ao processar uma pasta de PNGs, reutilize a mesma instância de `OcrEngine` — inicializá‑la uma única vez economiza trocas de contexto da GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Recuar para CPU

Se uma GPU não estiver disponível, basta definir `PreferGpu = false`. O motor recairá automaticamente para a CPU sem alterações no código.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Exemplo Completo Funcionando

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Ele inclui todas as etapas acima, além de algumas verificações de segurança.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Salve o arquivo como `Program.cs`, execute `dotnet run`, e você deverá ver o texto extraído impresso no console.

---

## Conclusão

Acabamos de demonstrar como **executar OCR em PNG** usando as extensões GPU do Aspose OCR, como **reconhecer texto de imagem**, e como **extrair texto de imagem** enquanto controla o **definir limite de memória GPU**. Ao configurar `GpuDevice` e `GpuMemoryLimitMb` você mantém sua aplicação rápida e estável, mesmo em GPUs modestas.

A partir daqui você pode:

- Experimentar com outros idiomas (`Language.French`, `Language.Spanish`).  
- Integrar a etapa OCR em um pipeline maior de processamento de documentos.  
- Adicionar pós‑processamento como verificação ortográfica ou extração de entidades para refinar o texto bruto.  

Lembre‑se, o essencial não é apenas o código, mas entender por que cada configuração importa. Quando você souber como **definir limite de memória GPU** e quando recair para a CPU, construirá soluções OCR que escalam de forma elegante.

Tem dúvidas sobre um tamanho específico de PNG, TIFFs de várias páginas ou solução de erros de GPU? Deixe um comentário abaixo, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}