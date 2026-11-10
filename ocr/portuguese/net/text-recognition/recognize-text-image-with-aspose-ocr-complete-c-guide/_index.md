---
category: general
date: 2026-06-22
description: Aprenda a reconhecer imagens de texto e extrair imagens de texto de faturas
  OCR de alta resolução usando o Aspose OCR. Inclui configuração de idioma OCR e aceleração
  por GPU.
draft: false
keywords:
- recognize text image
- extract text image
- high resolution ocr
- process invoice ocr
- set ocr language
language: pt
og_description: reconheça imagens de texto usando Aspose OCR em C#. Este tutorial
  mostra como extrair texto de imagens de faturas de alta resolução, definir o idioma
  do OCR e melhorar o desempenho.
og_title: Reconheça imagem de texto com Aspose OCR – Guia Completo em C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  headline: recognize text image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Learn how to recognize text image and extract text image from high
    resolution OCR invoices using Aspose OCR. Includes set OCR language and GPU acceleration.
  name: recognize text image with Aspose OCR – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code also works on .NET Framework 4.7+). -
      A valid Aspose.OCR NuGet package (free trial works fine). - A high‑resolution
      image of an invoice (e.g., `high_res_invoice.png`). - Basic familiarity with
      C# and Visual Studio or your favorite IDE.'
  - name: 1. Image Quality Matters
    text: Even the fastest GPU can’t fix a blurry scan. Aim for at least **300 dpi**
      for invoices; lower resolutions cause missed characters. If you can’t control
      the source, consider pre‑processing with a sharpening filter before sending
      the image to Aspose.
  - name: 2. Memory Consumption on Very Large Files
    text: A 5000 × 7000 pixel PNG can consume several hundred megabytes of RAM. If
      you hit `OutOfMemoryException`, split the invoice into pages or downscale slightly
      (e.g., to 250 dpi) before OCR.
  - name: 3. Fallback to CPU When GPU Fails
    text: If the GPU driver crashes, Aspose will silently revert to CPU. To ensure
      you’re always using the GPU, check `ocrEngine.ProcessingMode` after initialization
      and log a warning if it isn’t `ProcessingMode.Gpu`.
  - name: 4. Multi‑Language Documents
    text: 'When an invoice contains both English and Spanish, you can enable **multiple
      languages**:'
  type: HowTo
tags:
- Aspose OCR
- C#
- Image Processing
title: Reconheça imagem de texto com Aspose OCR – Guia Completo em C#
url: /pt/net/text-recognition/recognize-text-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto em imagem com Aspose OCR – Guia Completo em C#

Já precisou **recognize text image** mas os resultados ficaram borrados ou extremamente lentos? Você não está sozinho. Seja escaneando uma fatura em alta‑resolução ou extraindo dados de um contrato digitalizado, obter uma saída limpa e confiável é fundamental. Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que **recognize text image** a partir de um arquivo de alta‑resolução, **extract text image**, e ainda **set OCR language** para a melhor precisão — tudo aproveitando a aceleração por GPU.

Também vamos incluir alguns truques extras: como **process invoice OCR** de forma eficiente, por que você pode querer **high resolution OCR**, e o que fazer quando a GPU não está disponível. Ao final, você terá um único programa C# que transforma um PNG embaçado em texto pesquisável num piscar de olhos.

## O que você vai aprender

- Como criar uma instância `OcrEngine` com Aspose OCR.  
- Habilitar **GPU acceleration** para **high resolution OCR** ultra‑rápido.  
- Usar **set OCR language** para definir o idioma (por exemplo, English).  
- **Extract text image** de um arquivo de fatura em alta‑resolução.  
- Medir o tempo de processamento para comprovar os ganhos de desempenho.  
- Tratar cenários de fallback quando a GPU não está presente.

### Pré‑requisitos

- .NET 6.0 SDK ou superior (o código também funciona no .NET Framework 4.7+).  
- Um pacote Aspose.OCR válido no NuGet (a versão de avaliação funciona).  
- Uma imagem de alta‑resolução de uma fatura (ex.: `high_res_invoice.png`).  
- Familiaridade básica com C# e Visual Studio ou sua IDE favorita.

---

## Etapa 1: Instalar Aspose.OCR e preparar o projeto

Primeiro, adicione a biblioteca Aspose OCR ao seu projeto. Abra um terminal na pasta da solução e execute:

```bash
dotnet add package Aspose.OCR
```

> **Dica:** Mantenha o pacote sempre atualizado; versões mais recentes melhoram o suporte a GPU e os modelos de idioma.

Crie um novo aplicativo console caso ainda não tenha um:

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
```

Agora você tem um ambiente limpo para **recognize text image**.

## Etapa 2: Inicializar o OCR Engine (ativar GPU)

O coração do processo é o `OcrEngine`. Por padrão ele roda na CPU, mas para **high resolution OCR** em grandes escaneamentos de faturas a GPU pode reduzir segundos do tempo de execução.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Enable GPU processing – dramatically speeds up high‑resolution OCR
    ProcessingMode = ProcessingMode.Gpu
};
```

> **Por que GPU?** Uma imagem de alta‑resolução pode conter milhões de pixels. A GPU processa esses pixels em paralelo, transformando um trabalho de 5 segundos na CPU em uma operação de menos de um segundo na maioria das placas gráficas modernas.

Se a máquina alvo não possuir uma GPU compatível, o Aspose reverte automaticamente para o modo CPU. Você pode detectar esse fallback assim:

```csharp
if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
{
    Console.WriteLine("GPU not available – using CPU fallback.");
}
```

## Etapa 3: **set OCR language** – escolha o dicionário correto

O Aspose OCR vem com idiomas principais; o inglês é o padrão, mas você pode defini‑lo explicitamente. Isso importa porque o modelo de idioma influencia a segmentação de caracteres e as buscas no dicionário.

```csharp
// Step 3: Explicitly set the language to English (core language)
ocrEngine.Language = OcrLanguage.English;
```

> **Caso extremo:** Se precisar ler uma fatura em francês, basta substituir `OcrLanguage.English` por `OcrLanguage.French`. A mesma chamada **set OCR language** funciona para qualquer idioma suportado.

## Etapa 4: **recognize text image** – alimente uma fatura de alta‑resolução

Agora vamos realmente **recognize text image**. Aponte o engine para um PNG (ou TIFF) de alta‑resolução que você deseja processar. O caminho pode ser absoluto ou relativo; apenas garanta que o arquivo exista.

```csharp
// Step 4: Recognize the image and capture the result
string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

O objeto `OcrResult` contém tanto o texto extraído quanto informações de tempo, que exibiremos a seguir.

## Etapa 5: **extract text image** – exiba resultados e tempo de processamento

Por fim, imprima o texto OCR e o tempo gasto. Este é o momento de verificar se **process invoice OCR** foi executado como esperado.

```csharp
// Step 5: Output processing time and extracted text
Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(ocrResult.Text);
Console.WriteLine("=== Extracted Text End ===");
```

Executar o programa deve gerar algo como:

```
GPU OCR time: 312 ms
=== Extracted Text Start ===
Invoice #12345
Date: 2024‑04‑15
Total: $1,250.00
...
=== Extracted Text End ===
```

Pronto — seu fluxo **extract text image** está concluído.

---

## Bônus: lidando com armadilhas comuns

### 1. Qualidade da imagem importa

Mesmo a GPU mais rápida não corrige um escaneamento borrado. Mire em pelo menos **300 dpi** para faturas; resoluções menores provocam perda de caracteres. Se não puder controlar a origem, considere pré‑processar com um filtro de nitidez antes de enviar a imagem ao Aspose.

### 2. Consumo de memória em arquivos muito grandes

Um PNG de 5000 × 7000 pixels pode consumir várias centenas de megabytes de RAM. Se ocorrer `OutOfMemoryException`, divida a fatura em páginas ou reduza levemente a escala (ex.: para 250 dpi) antes do OCR.

### 3. Fallback para CPU quando a GPU falha

Se o driver da GPU travar, o Aspose reverte silenciosamente para a CPU. Para garantir que está sempre usando a GPU, verifique `ocrEngine.ProcessingMode` após a inicialização e registre um aviso caso não seja `ProcessingMode.Gpu`.

### 4. Documentos multilíngues

Quando uma fatura contém inglês e espanhol, você pode habilitar **multiple languages**:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

O engine tentará reconhecer caracteres de qualquer um dos idiomas configurados.

---

## Exemplo completo funcional

Abaixo está o **complete, runnable program** que incorpora todas as etapas discutidas. Copie‑e‑cole em `Program.cs`, substitua o caminho da imagem e pressione **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance and enable GPU acceleration
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu // Fast high‑resolution OCR
        };

        // Verify GPU availability (optional but helpful)
        if (ocrEngine.ProcessingMode != ProcessingMode.Gpu)
        {
            Console.WriteLine("GPU not detected – falling back to CPU processing.");
        }

        // Step 3: Set the OCR language (set OCR language for better accuracy)
        ocrEngine.Language = OcrLanguage.English; // Change as needed

        // Step 4: Recognize text from a high‑resolution invoice image
        string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // Step 5: Display processing time and the extracted text
        Console.WriteLine($"GPU OCR time: {ocrResult.ProcessingTimeMs} ms");
        Console.WriteLine("=== Extracted Text Start ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("=== Extracted Text End ===");
    }
}
```

**Saída esperada** (os tempos variam conforme o hardware):

```
GPU OCR time: 287 ms
=== Extracted Text Start ===
Invoice #98765
Date: 2024‑03‑22
Amount Due: $2,340.00
...
=== Extracted Text End ===
```

Teste com diferentes faturas para observar como o tempo de processamento permanece abaixo de meio segundo em uma GPU modesta.

---

## Conclusão

Você acabou de aprender como **recognize text image** usando Aspose OCR, **extract text image** de uma fatura em alta‑resolução e **set OCR language** para resultados ótimos — tudo aproveitando a aceleração por GPU para **high resolution OCR**. O código apresentado está pronto para produção, inclui lógica de fallback e pode ser estendido para lidar com PDFs multipágina, diferentes idiomas ou até fluxos de câmera em tempo real.

Próximos passos? Experimente:

- Converter o texto extraído em um objeto JSON de fatura estruturado.  
- Adicionar pré‑processamento de imagem (deskew, binarização) para melhorar a precisão em escaneamentos de baixa qualidade.  
- Integrar a chamada OCR em uma API ASP.NET Core para que seu serviço web processe faturas sob demanda.

Tem dúvidas sobre **process invoice OCR** ou precisa de ajuda para ajustar os pacotes de idioma? Deixe um comentário abaixo e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}