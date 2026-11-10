---
category: general
date: 2026-06-06
description: reconhecer imagem de texto usando C# OCR – um exemplo passo a passo de
  OCR em C# que extrai texto de digitalizações e converte a digitalização em texto
  em minutos.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: pt
og_description: reconheça imagens de texto com C# OCR. Aprenda um exemplo prático
  de OCR em C# que extrai texto de digitalizações, converte digitalizações em texto
  e lida com imagens do mundo real.
og_title: Reconhecer texto em imagem no C# – Tutorial completo de OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Reconhecer texto em imagem no C# – Guia completo de OCR
url: /pt/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto em imagem em C# – Tutorial Completo de OCR

Já se perguntou como **reconhecer texto em imagem** diretamente de uma foto escaneada usando C#? Você não está sozinho. Seja digitalizando recibos antigos, extraindo dados de um cartão de visita ou simplesmente transformando um escaneamento de baixa resolução em texto editável, a capacidade de extrair texto de uma imagem é um truque útil que todo desenvolvedor deveria ter em sua caixa de ferramentas.

Neste guia, percorreremos um **c# ocr example** que carrega uma foto, executa reconhecimento óptico de caracteres e imprime o resultado no console. Ao final, você será capaz de **extrair texto de escaneamento**, **converter escaneamento em texto**, e ainda ajustar o processo para imagens ruidosas. Nenhum serviço de terceiros sofisticado é necessário — apenas a API integrada Windows.Media.Ocr (ou qualquer OcrEngine compatível) e algumas linhas de código.

## O que você vai aprender

* Como configurar um projeto C# para OCR.  
* O código exato necessário para **reconhecer texto em imagem**.  
* Dicas para lidar com escaneamentos de baixa resolução e documentos de várias páginas.  
* Formas de estender o exemplo em uma biblioteca reutilizável para seus próprios aplicativos.

### Pré‑requisitos

* .NET 6.0 ou posterior (a API funciona também em .NET 5+).  
* Visual Studio 2022 (a edição Community serve) ou qualquer IDE de sua preferência.  
* Uma imagem de exemplo, como `lowres_scan.jpg`, colocada em uma pasta que você possa referenciar.  
* Familiaridade básica com async/await — as chamadas de OCR são assíncronas na API do Windows.

> **Dica profissional:** Se você estiver em uma plataforma não Windows, troque o namespace `Windows.Media.Ocr` por uma biblioteca multiplataforma como TesseractSharp; a lógica ao redor permanece a mesma.

---

## Etapa 1: Configurar para **reconhecer texto em imagem** com um mecanismo OCR

Primeiro, precisamos de uma instância do mecanismo OCR. A classe `OcrEngine` é o ponto de entrada para qualquer operação **imagem para texto c#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Por que isso importa:** O mecanismo abstrai o trabalho pesado de reconhecimento de padrões. Ao criá‑lo explicitamente, ganhamos controle sobre as configurações de idioma, o que é essencial quando você quiser **extrair texto de escaneamento** em outros idiomas.

## Etapa 2: Carregar o arquivo de imagem – o núcleo de **converter escaneamento em texto**

Em seguida, lemos a imagem do disco e a transformamos em um `SoftwareBitmap`, o formato que o mecanismo OCR espera.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Por que fazemos isso:** Alimentar diretamente um fluxo de arquivo bruto ao OCR costuma gerar resultados ruins, especialmente com escaneamentos de baixa resolução. Converter para um `SoftwareBitmap` permite manipular DPI, profundidade de cor e até aplicar filtros antes do reconhecimento.

## Etapa 3: Executar a operação de **reconhecer texto em imagem**

Agora finalmente chamamos o método `RecognizeAsync` do mecanismo. É aqui que a mágica acontece.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**O que você verá:** Se `lowres_scan.jpg` contiver a frase “Hello World”, o console imprimirá:

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Esse é o **c# ocr example** completo em ação — apenas quatro etapas lógicas, mas cobre tudo, desde o carregamento do arquivo até a saída final.

## Etapa 4: Tratando casos extremos – Quando o escaneamento não está perfeito

Imagens do mundo real nem sempre são nítidas. Aqui estão alguns ajustes que você pode fazer sem reescrever todo o programa:

| Problema | Correção rápida |
|----------|-----------------|
| **DPI muito baixo (≤ 72)** | Redimensione o bitmap usando `BitmapTransform` antes do reconhecimento. |
| **Texto inclinado** | Aplique uma transformação de rotação (`SoftwareBitmap.Rotate`) para endireitar a página. |
| **Múltiplos idiomas** | Crie `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` e ajuste `engine.Language` conforme necessário. |
| **Arquivos grandes** | Processar a imagem em blocos (`engine.RecognizeAsync(tileBitmap)`) e concatenar os resultados. |

Essas adaptações garantem que sua rotina de **extrair texto de escaneamento** permaneça confiável mesmo ao lidar com recibos ruidosos ou fotos tiradas em ângulo.

## Etapa 5: Transformar o exemplo em um helper reutilizável (Opcional)

Se você pretende **converter escaneamento em texto** em várias partes de um aplicativo, encapsule a lógica em uma pequena classe utilitária:

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Agora basta chamar:

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Por que você vai adorar isso:** O helper isola a infraestrutura de OCR, permitindo que você se concentre na lógica de negócio — perfeito para um **c# ocr example** que será reutilizado em diversos projetos.

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*Texto alternativo:* **reconhecer texto em imagem** saída de um aplicativo console OCR em C#.

---

## Perguntas Frequentes

**P: Isso funciona no .NET Core em Linux?**  
R: O namespace `Windows.Media.Ocr` é exclusivo do Windows. No Linux ou macOS, troque-o por TesseractSharp ou IronOcr — ambos expõem um método similar `Engine.Recognize`, de modo que o código ao redor permanece praticamente inalterado.

**P: Quão precisa é a OCR integrada para notas manuscritas?**  
R: O reconhecimento de escrita à mão ainda é experimental. Para melhores resultados, use fontes impressas ou considere um serviço em nuvem como Azure Cognitive Services se precisar de alta precisão.

**P: Posso processar PDFs diretamente?**  
R: Não diretamente. Converta cada página do PDF em uma imagem primeiro (usando `PdfSharp` ou `Ghostscript`) e então alimente o bitmap ao mecanismo OCR.

---

## Conclusão

Agora você tem um **c# ocr example** completo e pronto para produção que pode **reconhecer texto em imagem**, **extrair texto de escaneamento** e **converter escaneamento em texto** em apenas algumas linhas de código. Ao entender o fluxo — criação do mecanismo, carregamento da imagem, reconhecimento assíncrono e tratamento do resultado — você pode adaptar o padrão a qualquer projeto C# que precise transformar fotos em strings pesquisáveis.

Pronto para o próximo passo? Experimente adicionar uma interface simples com WinForms ou WPF, teste diferentes idiomas ou conecte a saída a um banco de dados para arquivos pesquisáveis. O céu é o limite quando você domina técnicas de **imagem para texto c#**.

Bom código, e que seus escaneamentos estejam sempre nítidos!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Converter imagem em texto – Executar OCR em imagem a partir de URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Como extrair texto de imagem preparando retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}