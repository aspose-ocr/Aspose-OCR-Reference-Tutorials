---
category: general
date: 2026-05-25
description: reconhecer texto de imagem usando Aspose OCR em C#. Aprenda como carregar
  a imagem para OCR, definir o idioma do OCR, criar o mecanismo OCR e extrair texto
  de um TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: pt
og_description: Reconheça texto de imagem usando Aspose OCR em C#. Este tutorial mostra
  como criar o mecanismo OCR, carregar a imagem para OCR, definir o idioma do OCR
  e extrair texto de um TIFF.
og_title: reconheça texto de imagem com Aspose OCR – Guia Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Reconheça texto de imagem com Aspose OCR – Guia Completo em C#
url: /pt/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem com Aspose OCR – Guia Completo em C#

Já precisou **reconhecer texto de imagem** mas não sabia qual biblioteca ofereceria velocidade e precisão? Você não está sozinho. Em muitos projetos de processamento de faturas ou arquivamento, o maior ponto crítico é obter texto limpo e pesquisável a partir de arquivos TIFF sem escrever um analisador personalizado.

A verdade é que o Aspose OCR para .NET torna todo esse fluxo muito simples. Neste guia vamos percorrer tudo o que você precisa — instalar o pacote, **criar o motor OCR**, carregar um TIFF, definir o idioma do OCR e, finalmente, **extrair texto de TIFF**. Ao final, você terá um aplicativo console pronto‑para‑executar que pode **reconhecer texto de imagem** em um piscar de olhos.

## Pré‑requisitos

- .NET 6.0 ou superior (o código funciona também com .NET Core e .NET Framework)
- Visual Studio 2022 (ou qualquer IDE de sua preferência)
- Pacote NuGet Aspose.OCR (suporte a GPU requer o add‑on `Aspose.OCR.Gpu`)
- Uma GPU com suporte a CUDA se você quiser velocidade extra (opcional, mas recomendado)

> **Dica de especialista:** Se você não tem uma GPU, basta omitir a linha `GpuDevice` que o motor retornará automaticamente ao uso da CPU.

## Etapa 1: Instalar Aspose OCR e Criar o Motor OCR

Primeiro, adicione os pacotes necessários via NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Agora podemos **criar o motor OCR**. Este objeto é o coração do processo; ele contém configurações como o dispositivo de execução e limites de memória.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Por que isso importa:** Ao vincular o motor a uma GPU você reduz drasticamente o tempo necessário para **reconhecer texto de imagem**, especialmente em lotes grandes de TIFFs de alta resolução.

## Etapa 2: Carregar Imagem para OCR

Em seguida, precisamos **carregar a imagem para OCR**. O Aspose.OCR trabalha com `System.Drawing.Image`, portanto qualquer formato suportado pelo GDI+ (incluindo TIFF multipágina) funciona.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Se você estiver lidando com um TIFF multipágina, pode percorrer as páginas usando `image.SelectActiveFrame`, mas na maioria dos cenários uma única chamada já basta.

## Etapa 3: Definir o Idioma do OCR

O motor não sabe magicamente qual idioma está sendo escaneado. **Defina o idioma do OCR** antes de executar o reconhecedor; caso contrário, você receberá muita saída corrompida.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Sabia que?** Trocar de idioma em tempo de execução é barato — você pode até processar um documento com múltiplos idiomas alterando essa propriedade entre as páginas.

## Etapa 4: Executar o Reconhecimento – Reconhecer Texto de Imagem

Agora a parte divertida: realmente **reconhecer texto de imagem**. O método `Recognize` devolve uma string simples com todos os caracteres detectados.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Se precisar de pontuações de confiança ou caixas delimitadoras, pode usar a sobrecarga que retorna um objeto `OcrResult`, mas para a maioria das tarefas de extração a string simples é suficiente.

## Etapa 5: Extrair Texto de TIFF (e lidar com arquivos multipágina)

Quando a fonte é um TIFF contendo várias páginas, você desejará repetir as etapas 2‑4 para cada quadro. Aqui está um loop rápido que **extrai texto de TIFF** página por página:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

O código acima imprime o texto extraído para cada página, facilitando o encaminhamento dos resultados para um banco de dados ou um índice de busca.

## Etapa 6: Exibir ou Persistir o Texto Extraído

Por fim, vamos **exibir o texto extraído** e, opcionalmente, gravá‑lo em um arquivo para processamento posterior.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Executar o programa deve exibir os caracteres reconhecidos e criar `extracted_text.txt` ao lado do seu TIFF de origem.

---

## Perguntas Frequentes & Casos de Borda

- **E se minha GPU não for detectada?**  
  Remova a linha `GpuDevice`; o motor mudará automaticamente para o modo CPU. O desempenho será mais lento, mas os resultados permanecem precisos.

- **Posso processar arquivos PNG ou JPEG?**  
  Claro — `Image.FromFile` funciona com qualquer formato suportado pelo System.Drawing, então você pode **carregar a imagem para OCR** independentemente da extensão.

- **Como lidar com digitalizações de baixa resolução?**  
  Aumente `ocrEngine.PreprocessOptions.Dpi` antes de chamar `Recognize`. DPI maior fornece mais pixels ao motor, melhorando a precisão.

- **Existe um limite para o tamanho do TIFF?**  
  A propriedade `GpuMemoryLimit` limita o uso da GPU. Se o limite for atingido, o motor recairá para a CPU nas páginas restantes.

---

## Conclusão

Agora você tem um trecho completo, pronto para produção, que **reconhece texto de imagem** usando Aspose OCR em C#. O tutorial abordou como **criar o motor OCR**, **carregar a imagem para OCR**, **definir o idioma do OCR** e **extrair texto de TIFF** — tudo aproveitando a aceleração por GPU para velocidade.

A partir daqui, você pode:

- Experimentar diferentes idiomas (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, etc.).
- Integrar a saída em um índice ElasticSearch pesquisável.
- Adicionar pós‑processamento (correção ortográfica, limpeza com regex) para melhorar a qualidade dos dados.

Teste em seu próprio lote de faturas, ajuste os limites de memória e veja o desempenho do OCR decolar. Boa codificação!

## Tutoriais Relacionados

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}