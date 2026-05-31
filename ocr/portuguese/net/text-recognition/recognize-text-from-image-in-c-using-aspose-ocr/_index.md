---
category: general
date: 2026-05-31
description: Aprenda a reconhecer texto a partir de imagens em C# com Aspose OCR,
  incluindo como extrair texto de arquivos TIFF e carregar imagens para OCR de forma
  eficiente.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: pt
og_description: Guia passo a passo para reconhecer texto de imagem com Aspose OCR,
  abordando a extração de TIFF e o carregamento adequado da imagem para OCR.
og_title: reconhecer texto de imagem em C# usando Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: reconhecer texto de imagem em C# usando Aspose OCR
url: /pt/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem em C# usando Aspose OCR

Já precisou **reconhecer texto de imagem** mas não sabia por onde começar em C#? Você não está sozinho—muitos desenvolvedores encontram essa barreira ao lidar com documentos escaneados ou TIFFs de várias páginas. Neste guia, vamos percorrer um exemplo completo, pronto‑para‑executar que **reconhece texto de imagem** usando a biblioteca Aspose OCR, e também mostraremos como **extrair texto de tiff** e a melhor forma de **carregar imagem para OCR** sem perder a cabeça.

Cobriremos tudo, desde a instalação do pacote NuGet até o manuseio de aceleração GPU e fallback para CPU quando necessário. Ao final deste tutorial você terá um aplicativo console que imprime o texto reconhecido e o tempo de processamento—sem peças faltando, sem referências vagas.

## O que você vai construir

- Um simples aplicativo console .NET que carrega uma imagem (incluindo TIFF de várias páginas)  
- Um motor OCR configurado para uso de GPU, com fallback elegante para CPU  
- Extração de texto simples da imagem, impresso no console  
- Informações de tempo para que você possa ver o impacto de desempenho da GPU vs. CPU  

**Pré‑requisitos**

- .NET 6 SDK ou superior (o código funciona com .NET Core e .NET Framework)  
- Familiaridade básica com C# e linha de comando  
- Acesso à internet para baixar o pacote NuGet Aspose.OCR  

Se você tem isso, vamos mergulhar.

![Código C# para reconhecer texto de imagem usando Aspose OCR](image.png "Código C# para reconhecer texto de imagem usando Aspose OCR")

## Etapa 1 – Reconhecer texto de imagem: Configurar o motor OCR

Primeiro de tudo, precisamos de uma instância `OcrEngine`. O Aspose OCR permite escolher o dispositivo de processamento—GPU para velocidade, CPU como rede de segurança. O motor também aceita uma dica de limite de memória, o que pode ser útil em máquinas compartilhadas.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Por que isso importa:**  
Escolher `OcrDevice.Gpu` pode reduzir segundos do tempo de reconhecimento para imagens grandes, especialmente TIFFs de várias páginas. O `GpuMemoryLimit` impede que seu aplicativo consuma toda a memória GPU em uma estação de trabalho compartilhada.

## Etapa 2 – Carregar imagem para OCR (com suporte a TIFF)

Agora alimentamos o motor com uma imagem. `ImageStream.FromFile` da Aspose aceita **qualquer** formato que a biblioteca suporte—TIFF, PNG, JPEG, o que for. Esta etapa atende diretamente ao requisito de **carregar imagem para OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Dica profissional:** Se você estiver trabalhando com um TIFF de várias páginas, a Aspose trata automaticamente cada página como um quadro separado, e o motor as processará sequencialmente. Nenhum código extra necessário.

## Etapa 3 – Executar o reconhecimento e **extrair texto de tiff**

Com o motor preparado e a imagem carregada, iniciamos a operação OCR. O método `Recognize` retorna um `OcrResult` que contém o texto simples, pontuações de confiança e detalhes de tempo.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Tratamento de casos extremos:**  
Se a GPU não estiver disponível, `engine.Recognize()` ainda funciona porque o motor muda silenciosamente para CPU. Você pode verificar `engine.Device` após o reconhecimento se precisar registrar qual dispositivo foi realmente usado.

## Etapa 4 – Recuperar o texto simples reconhecido

Extrair o texto é simples—basta ler a propriedade `Text`. É aqui que finalmente **extraímos texto de tiff** (ou qualquer outra imagem) e o apresentamos ao usuário.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Você verá os caracteres brutos, com quebras de linha preservadas como aparecem na imagem de origem. Para uma saída mais estruturada (como JSON ou CSV), você pode explorar `result.Regions` e `result.Lines`, mas o texto simples costuma ser suficiente para scripts rápidos.

## Etapa 5 – Medir o tempo de processamento e lidar com fallback de GPU

Desempenho importa, especialmente ao processar dezenas de páginas. A propriedade `ProcessingTime` informa exatamente quanto tempo o OCR levou, independentemente de ter sido executado na GPU ou CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Por que isso importa:**  
Se você notar que o tempo está inflando, pode ser necessário ajustar `GpuMemoryLimit` ou mudar explicitamente para CPU (`Device = OcrDevice.Cpu`). Por outro lado, um resultado em menos de um segundo em um TIFF grande indica que sua aceleração GPU está fazendo o trabalho.

## Exemplo completo, pronto‑para‑executar

Copie o código abaixo para um novo projeto console (`dotnet new console -n OcrDemo`) e execute `dotnet add package Aspose.OCR`. Em seguida, substitua `YOUR_DIRECTORY/sample_multi_page.tif` pelo caminho da sua imagem.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Saída esperada (truncada para brevidade):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Se sua máquina não possuir uma GPU capaz, o tempo decorrido pode ser alguns segundos a mais, mas o texto ainda será extraído corretamente.

## Perguntas frequentes & Armadilhas

- **E se a imagem for enorme (mais de 10 MB)?**  
  Reduza sua resolução antes de enviá‑la ao motor, ou aumente `GpuMemoryLimit` se houver VRAM suficiente.  
- **Posso processar várias imagens em um loop?**  
  Claro. Basta reutilizar a mesma instância `OcrEngine` e atribuir um novo `ImageStream` a cada iteração.  
- **Preciso liberar algum recurso?**  
  `OcrEngine` implementa `IDisposable`. Envolva‑a em um bloco `using` para gerenciamento limpo de recursos, especialmente ao trabalhar com recursos de GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **E quanto a idiomas diferentes do inglês?**  
  Defina `engine.Language = OcrLanguage.Spanish` (ou qualquer idioma suportado) antes de chamar `Recognize()`.  

## Conclusão

Agora você tem uma solução completa, de ponta a ponta, que **reconhece texto de imagem** em C# usando Aspose OCR. O tutorial abordou como **carregar imagem para OCR**, como **extrair texto de tiff** e como medir desempenho enquanto lida elegantemente com fallback de GPU.

A partir daqui, você pode:

- Experimentar diferentes formatos de imagem (BMP, PDF) para ver como a Aspose os trata.  
- Mergulhar em `result.Regions` para obter dados de caixas delimitadoras se precisar de layout‑aware


## O que você deve aprender a seguir?

- [Como usar Aspose para reconhecer imagem a partir de stream em OCR de reconhecimento de imagem](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extrair texto de imagem – Otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Extrair texto de imagem – Reconhecer linha com Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}