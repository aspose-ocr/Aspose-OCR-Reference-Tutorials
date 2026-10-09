---
category: general
date: 2026-02-25
description: reconheça texto de imagem rapidamente usando OCR acelerado por GPU. aprenda
  a definir o modo GPU, carregar a imagem para OCR e extrair texto de TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: pt
og_description: reconheça texto de imagem instantaneamente usando OCR acelerado por
  GPU. Tutorial passo a passo em C# cobrindo como definir o modo GPU, carregar a imagem
  para OCR e extrair texto de TIFF.
og_title: Reconheça texto de imagem com OCR acelerado por GPU – Guia C#
tags:
- Aspose OCR
- C#
- GPU computing
title: Reconhecer texto de imagem usando OCR acelerado por GPU em C#
url: /pt/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem usando OCR acelerado por GPU em C#

Já precisou **reconhecer texto de imagem** mas sua CPU não aguentava um escaneamento de alta resolução? Você não está sozinho. Em muitos projetos reais — pense em digitalização de faturas ou arquivamento de jornais antigos — um único arquivo TIFF pode travar seu pipeline por minutos. A boa notícia? Aspose.OCR permite que você ative um interruptor e delegue o trabalho pesado à sua GPU, transformando uma operação lenta em quase instantânea.

Neste tutorial vamos percorrer todo o processo: como **definir o modo GPU**, como **carregar a imagem para OCR** e como **extrair texto de arquivos TIFF**. Ao final, você terá um exemplo autônomo, pronto para produção, que pode ser inserido em qualquer projeto .NET 6+.

## Prerequisites

Antes de mergulharmos, certifique-se de que você tem:

- .NET 6 SDK (ou superior) instalado.  
- Visual Studio 2022 ou qualquer editor de sua preferência.  
- O pacote NuGet Aspose.OCR (`Aspose.OCR`) adicionado ao seu projeto.  
- Uma GPU que suporte DirectX 11 ou superior (a maioria das GPUs modernas se enquadra).  
  *Se você não possui uma GPU, ainda pode executar o código com `GpuMode.Auto` — a biblioteca reverterá automaticamente para a CPU.*

> **Dica profissional:** Verifique se o driver da sua GPU está atualizado; drivers desatualizados podem causar erros obscuros de inicialização.

## Step 1 – Create the OCR engine and set GPU mode

A primeira coisa que você precisa é uma instância de `OcrEngine`. Esse objeto contém toda a configuração, inclusive se o motor deve usar a GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Por que isso importa:** Habilitar o modo GPU move o pré‑processamento de imagem intensivo em computação (binarização, remoção de ruído, etc.) para a placa gráfica. Em uma RTX 3060 de médio alcance, você pode observar um **aceleração de 3‑5×** comparado ao processamento puro por CPU.

## Step 2 – Load image for OCR (TIFF example)

Aspose.OCR aceita muitos formatos, mas TIFF é comum para documentos escaneados porque preserva qualidade sem perdas. Use `ImageStream.FromFile` para ler o arquivo na memória.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Caso extremo:** Alguns arquivos TIFF contêm várias páginas. `ImageStream.FromFile` lerá apenas a primeira página. Se precisar processar todas as páginas, itere sobre `ImageInfo.Pages` e alimente cada uma ao motor separadamente.

## Step 3 – Perform the recognition

Agora que o motor está configurado e a imagem carregada, chame `Recognize()`. O método retorna um objeto `OcrResult` contendo o texto puro e metadados adicionais.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**E se o texto aparecer embaralhado?**  
- Certifique‑se de que a imagem está em orientação legível (gire se necessário).  
- Ajuste opções de pré‑processamento, como `ocrEngine.Config.DeskewEnabled = true;`.  
- Para documentos multilíngues, defina `ocrEngine.Config.Language = Language.English;` ou o enum apropriado.

## Step 4 – Verify the output and handle errors

Uma implementação robusta verifica resultados nulos e captura exceções potenciais (por exemplo, drivers de GPU ausentes).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Por que envolver em try/catch?** A inicialização da GPU pode lançar `DllNotFoundException` se as bibliotecas nativas necessárias não estiverem presentes. O bloco catch oferece um caminho de degradação elegante.

## Full, runnable example

Juntando tudo, aqui está um programa completo que você pode compilar e executar agora. Substitua o caminho do arquivo por um TIFF real em sua máquina.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Saída esperada**

Se o TIFF contiver texto legível em inglês, você verá algo como:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Se a imagem estiver em branco ou ilegível, o console aconselhará a verificar o arquivo de origem.

## Common questions & variations

| Question | Answer |
|----------|--------|
| **Posso processar JPEG ou PNG em vez de TIFF?** | Absolutamente. `ImageStream.FromFile` funciona com qualquer formato suportado pelo Aspose.OCR (PNG, JPEG, BMP, etc.). |
| **E se eu tiver várias páginas em um único TIFF?** | Percorra `ImageInfo.Pages` e atribua cada página a `ocrEngine.Image` antes de chamar `Recognize()`. |
| **Preciso de licença para Aspose.OCR?** | Uma avaliação gratuita funciona para até 100 páginas. Para produção, adquira uma licença para remover a marca d'água de avaliação. |
| **Como altero o modelo de idioma?** | Defina `ocrEngine.Config.Language = Language.Spanish;` (ou qualquer enum suportado). |
| **Existe como obter pontuações de confiança?** | Ative `ocrEngine.Config.EnableConfidence = true;` e inspecione `result.Confidence` por linha. |

## Conclusion

Agora você sabe como **reconhecer texto de imagem** usando um pipeline **OCR acelerado por GPU** em C#. Ao **definir o modo GPU**, **carregar a imagem para OCR** e **extrair texto de arquivos TIFF**, você construiu uma solução rápida e escalável pronta para cargas de trabalho reais.

Próximos passos? Experimente encadear este código com um gerador de PDF para criar PDFs pesquisáveis, ou alimente as strings extraídas em um pipeline de processamento de linguagem natural. Você também pode experimentar `GpuMode.Auto` para tornar seu aplicativo adaptável a ambientes sem GPU.

Happy coding, and may your OCR runs be lightning‑quick! 

![recognize text from image example](https://example.com/ocr-demo.png "recognize text from image using GPU‑accelerated OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}