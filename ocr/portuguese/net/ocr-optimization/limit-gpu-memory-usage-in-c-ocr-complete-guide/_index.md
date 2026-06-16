---
category: general
date: 2026-05-02
description: Limite o uso de memória da GPU ao executar OCR em imagem no C#. Aprenda
  como habilitar a aceleração da GPU, extrair texto de um recibo e dominar um tutorial
  de OCR em C#.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: pt
og_description: Limite o uso de memória da GPU ao executar OCR em imagens com C#.
  Este guia mostra como habilitar a aceleração GPU, extrair texto de um recibo e dominar
  um tutorial de OCR em C#.
og_title: Limitar o uso de memória da GPU em OCR C# – Guia Completo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Limitar o uso de memória da GPU em OCR C# – Guia Completo
url: /pt/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# limitar o uso de memória GPU em C# OCR – Guia Completo

Já precisou **limitar o uso de memória GPU** ao processar um lote de recibos? Você não é o único—os desenvolvedores frequentemente encontram erros de falta de memória quando a GPU é solicitada a manipular muitas imagens ao mesmo tempo. A boa notícia é que o Aspose.OCR permite limitar a pegada de memória **e** ativar a aceleração GPU em uma única linha de código.  

Neste tutorial, percorreremos uma solução prática, passo a passo, que mostra **como habilitar a aceleração GPU**, extrair texto de uma imagem de recibo de exemplo e manter o uso de RAM da GPU abaixo de 1 GB. Ao final, você terá um aplicativo de console C# pronto para executar, além de várias dicas que podem ser reutilizadas em qualquer cenário de **run OCR on image**.

## O que você precisará

- .NET 6.0 SDK ou posterior (o código também compila com .NET 5+)  
- Pacote NuGet Aspose.OCR para .NET (`Aspose.OCR`) – instale com `dotnet add package Aspose.OCR`  
- Uma GPU compatível com CUDA ou um dispositivo Windows compatível com DirectML  
- Uma imagem de recibo de exemplo (`receipt.jpg`) colocada em uma pasta que você possa referenciar  

É isso—nenhuma biblioteca nativa extra, sem cópias complicadas de DLLs. O Aspose abstrai o backend da GPU, permitindo que você se concentre na lógica de negócios.

## Etapa 1: Instalar o pacote NuGet Aspose.OCR

Primeiro de tudo. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.OCR
```

Isso obtém a versão estável mais recente (em maio 2026 é 23.11). O pacote inclui binários para CPU e GPU, portanto você não precisa baixar manualmente os runtimes CUDA ou DirectML—o Aspose detecta o que está disponível em tempo de execução.

> **Dica profissional:** Se você estiver direcionando um pipeline CI/CD, fixe a versão no seu `.csproj` para evitar atualizações inesperadas.

## Etapa 2: Criar o OCR Engine e **limitar o uso de memória GPU**

Agora vamos instanciar o `OcrEngine` e dizer explicitamente que ele não deve exceder 1 GB de memória GPU. Este é o núcleo do requisito de **limit GPU memory usage**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

Observe o comentário `// 👉 Limit GPU memory usage…`—essa linha é a resposta para a palavra‑chave principal. Ao definir `GpuMemoryLimitMb` você indica ao mecanismo de inferência subjacente que aloque no máximo a quantidade especificada, permitindo que vários trabalhos simultâneos coexistam sem sobrecarregar a GPU.

## Etapa 3: **Como habilitar a aceleração GPU** (e por que isso importa)

Você pode se perguntar, “Por que não ficar apenas com a CPU?” A resposta é velocidade. Em uma RTX 3080 moderna, o mesmo recibo é processado em menos de 200 ms contra 1,2 segundos em uma CPU de 4 núcleos.  

Habilitar a aceleração GPU é tão simples quanto mudar o enum `EngineMode`:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

O Aspose seleciona automaticamente o melhor backend:

| Backend Detectado | O que Faz |
|------------------|-----------|
| CUDA (NVIDIA)    | Usa kernels cuDNN para OCR, ideal para Windows/Linux com placas NVIDIA |
| DirectML (Windows) | Aproveita DirectX 12, funciona em GPUs AMD/Intel sem drivers adicionais |
| None (fallback)  | Recorre ao caminho otimizado de CPU |

Se nem CUDA nem DirectML estiverem presentes, o engine reverte silenciosamente para a CPU—sem falhas, apenas desempenho mais lento.

## Etapa 4: **Run OCR on image** e **extrair texto do recibo**

Com o engine configurado, alimentar uma imagem é simples. O método `RecognizeImage` aceita um caminho de arquivo, um `Stream` ou até um `Bitmap`. Aqui está a chamada mínima:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

Assumindo que o recibo contém:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Você deve ver uma saída semelhante a:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

Se o texto parecer confuso, verifique se a imagem tem alto contraste e está corretamente orientada—OCR funciona melhor com digitalizações limpas.

## Etapa 5: Verificar limites de memória e lidar com casos extremos

Após a primeira execução, você pode consultar quanta memória GPU o engine realmente usou:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

Se você planeja processar dezenas de recibos em paralelo, pode querer reduzir o limite para 512 MB e executar várias instâncias do engine. Apenas lembre-se de que cada instância respeita o mesmo limite global; a biblioteca limitará as alocações automaticamente.

> **Armadilha comum:** Definir o limite muito baixo (por exemplo, 100 MB) pode fazer com que o engine volte para a CPU durante a execução, resultando em desempenho inconsistente. Teste com uma carga de trabalho realista antes de fixar o valor.

## Exemplo completo em funcionamento

Abaixo está um programa de console completo, pronto para copiar e colar. Substitua `YOUR_DIRECTORY` pelo caminho real da sua imagem de recibo.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

Salve o arquivo, execute `dotnet run`, e você deverá ver o texto extraído do recibo impresso no console, junto com um pequeno relatório de consumo de memória GPU.

## Solução de Problemas & Perguntas Frequentes

**Q: Minha GPU não foi detectada—por quê?**  
A: Certifique‑se de que o driver NVIDIA mais recente (para CUDA) ou o Windows 10 1809+ (para DirectML) esteja instalado. Também verifique se as DLLs `Aspose.OCR` correspondem à arquitetura do seu processo (x64 recomendado).

**Q: A saída está vazia.**  
A: Verifique a qualidade da imagem—recibos borrados ou rotacionados geralmente precisam de pré‑processamento (correção de inclinação, binarização). O Aspose fornece `ImagePreprocessor` que pode ser inserido antes de `RecognizeImage`.

**Q: Posso executar isso no Linux?**  
A: Sim, contanto que você tenha uma GPU NVIDIA com CUDA 11+ instalado. O mesmo código funciona sem alterações.

## Conclusão

Cobrimos tudo o que você precisa para **limit GPU memory usage** enquanto **run OCR on image** usando Aspose.OCR em C#. Desde a instalação do pacote NuGet até a configuração do engine, habilitação da aceleração GPU e, finalmente, **extrair texto do recibo**, o guia oferece uma solução pronta para uso que é ao mesmo tempo econômica em memória e extremamente rápida.

Em seguida, você pode explorar tópicos mais avançados de **c# OCR tutorial**—como processamento em lote, pacotes de idioma personalizados ou integração dos resultados em um banco de dados. Experimente diferentes valores de `GpuMemoryLimitMb` para encontrar o ponto ideal para sua carga de trabalho e fique de olho no diagnóstico de memória usada para evitar surpresas.

Feliz codificação, e que sua GPU permaneça fria enquanto seu OCR permanece preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}