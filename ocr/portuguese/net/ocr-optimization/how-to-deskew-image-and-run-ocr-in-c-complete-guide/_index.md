---
category: general
date: 2026-03-07
description: Aprenda a corrigir a inclinação da imagem, aumentar o contraste e extrair
  texto de digitalizações usando o Aspose OCR. Execute OCR em uma imagem com um exemplo
  completo em C# e carregue a imagem para OCR facilmente.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: pt
og_description: Aprenda a corrigir a inclinação da imagem, aumentar o contraste e
  extrair texto de uma digitalização usando Aspose OCR em C#. Realize OCR na imagem
  com código passo a passo.
og_title: Como desinclinar a imagem e executar OCR em C# – Guia completo
tags:
- C#
- OCR
- Image Processing
title: Como Desinclinar Imagem e Executar OCR em C# – Guia Completo
url: /pt/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Desinclinar Imagem e Executar OCR em C# – Guia Completo

Se você já se perguntou **como desinclinar imagem** antes de executar OCR, está no lugar certo. Neste tutorial, vamos guiá-lo através do aumento de contraste, carregamento de uma imagem para OCR e, finalmente, **extrair texto da digitalização** com Aspose OCR.  

Seja digitalizando recibos antigos, limpando contratos escaneados ou simplesmente precisando de uma maneira confiável de ler texto de uma foto torta, os passos abaixo cobrem tudo o que você precisa. Sem enrolação — apenas um exemplo funcional que você pode copiar‑colar no Visual Studio.  

## O que Você Vai Conquistar

* Corrija a inclinação em até 30° (essa é a parte do **how to deskew image**).  
* Aumente o contraste da imagem para bordas de caracteres mais nítidas (**how to boost contrast**).  
* Carregue sua foto no motor OCR (**load image for OCR**).  
* Execute o processo de reconhecimento e **extract text from scan**.  

Tudo isso funciona com o pacote NuGet mais recente do Aspose.OCR .NET (v23.11 na data de escrita).  

---

![Exemplo de como desinclinar imagem](/images/deskew-example.png "como desinclinar imagem")

*A imagem acima mostra um documento escaneado antes e depois da desinclinação.*

## Pré-requisitos

* .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
* Visual Studio 2022 (ou qualquer IDE C# de sua preferência).  
* Pacote NuGet Aspose.OCR – instale via `dotnet add package Aspose.OCR`.  

É só isso. Sem serviços externos, sem chaves de API.

---

## Como Desinclinar Imagem com Aspose OCR

A primeira coisa que fazemos é criar um **ImageProcessingPipeline** e adicionar um `DeskewFilter`. O filtro detecta automaticamente o ângulo dominante da linha de texto e gira a imagem de volta à horizontal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Por que isso importa:**  
Um escaneamento inclinado confunde o motor OCR porque os caracteres não estão mais alinhados à linha de base. O `DeskewFilter` analisa o histograma da imagem, encontra o ângulo e a gira, melhorando drasticamente a precisão do reconhecimento.

> **Dica de especialista:** Se você souber que seus documentos nunca excedem uma inclinação de 15°, defina `MaxAngle = 15` para acelerar o processamento.

---

## Como Aumentar o Contraste para Melhor Reconhecimento

Depois de desinclinar, o próximo passo é fazer o texto se destacar. O `ContrastBoostFilter` estica a faixa de intensidade dos pixels, o que é especialmente útil para impressões desbotadas.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Por que ajuda:**  
Escaneamentos de baixo contraste produzem caracteres acinzentados que o binarizador pode interpretar como fundo. Aumentar o contraste deixa os pixels escuros mais escuros e os claros mais claros, proporcionando ao `BinarizationFilter` um canvas mais limpo.

---

## Executar OCR na Imagem – Carregando o Arquivo

Agora que a imagem está pré‑processada, precisamos **load image for OCR**. A Aspose oferece um auxiliar conveniente `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Se sua imagem estiver em um stream (por exemplo, enviada via API web), você pode usar `ImageStream.FromStream(yourStream)` em vez disso. O motor aceita BMP, JPEG, PNG, TIFF e muitos outros formatos.

---

## Executar o Processo de Reconhecimento e Extrair Texto da Digitalização

Com tudo conectado, chamar `Recognize()` faz o trabalho pesado. Após a chamada, o texto reconhecido está disponível via `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Saída esperada** (exemplo para uma fatura simples):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Se a saída parecer confusa, verifique novamente a ordem do pipeline — desinclinar primeiro, depois denoising, aumento de contraste e, por fim, binarização. Trocar a ordem pode degradar os resultados.

---

## Armadilhas Comuns e Casos de Borda

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Resultado vazio** | A imagem está muito escura ou muito clara para o método padrão de binarização. | Aumente `ContrastBoostFilter.Strength` ou troque para `BinarizationMethod.Otsu`. |
| **Texto parcial ausente** | Ainda há ruído após a redução de ruído. | Use `DenoiseLevel.Medium` para imagens mais suaves, ou adicione um segundo `DenoiseFilter`. |
| **Direção de rotação errada** | O documento tem orientação mista (por exemplo, uma foto de uma página rotacionada). | Defina manualmente `DeskewFilter.MaxAngle` mais baixo e pré‑rotacione a imagem com `ImageProcessor.Rotate`. |
| **Desaceleração de desempenho** | Grande lote de imagens de alta resolução. | Reduza a escala das imagens (`ImageProcessor.Resize`) antes do pipeline, ou processe em paralelo (`Parallel.ForEach`). |

---

## Exemplo Completo Funcionando (Pronto para Copiar‑Colar)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Salve isso como `Program.cs`, execute `dotnet run` e observe o console imprimir o resultado de **extract text from scan**.  

---

## Próximos Passos e Tópicos Relacionados

* **Batch processing** – Envolva a lógica acima em um loop para lidar com dezenas de arquivos.  
* **Custom language packs** – Se precisar ler scripts não latinos, carregue um modelo de idioma via `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF output** – Combine Aspose.PDF com OCR para incorporar texto pesquisável diretamente em um arquivo PDF.  
* **Performance tuning** – Experimente a ordem do `ImageProcessingPipeline`; às vezes denoising antes do deskew gera resultados mais rápidos em fotos ruidosas.  

Todos esses itens se baseiam nos conceitos centrais que abordamos: **how to deskew image**, **how to boost contrast**, **load image for OCR**, **perform OCR on image**, e finalmente **extract text from scan**.

---

## Conclusão

Acabamos de demonstrar uma forma completa e pronta para produção de **how to deskew image** e executar OCR em C#. Ao encadear um filtro de desinclinação, uma etapa de denoising, um aumento de contraste e um binarizador, você obtém uma entrada limpa que permite ao Aspose OCR extrair texto da digitalização de forma confiável.  

Teste o código, ajuste os parâmetros dos filtros para seus próprios documentos e verá como a precisão do reconhecimento melhora rapidamente. Tem dúvidas? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}