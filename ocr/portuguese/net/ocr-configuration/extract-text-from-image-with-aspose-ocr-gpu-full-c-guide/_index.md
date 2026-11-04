---
category: general
date: 2026-04-06
description: Extraia texto de imagem usando Aspose OCR GPU em C#. Aprenda a carregar
  a imagem a partir de um arquivo e definir o limite de memória da GPU neste guia
  passo a passo.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: pt
og_description: Extraia texto de imagem usando Aspose OCR GPU em C#. Aprenda a carregar
  a imagem a partir de um arquivo e definir o limite de memória da GPU neste guia
  passo a passo.
og_title: Extrair Texto de Imagem com Aspose OCR GPU – Guia Completo em C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Extrair texto de imagem com Aspose OCR GPU – Guia completo em C#
url: /pt/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem com Aspose OCR GPU – Guia Completo em C#

Já precisou **extrair texto de imagem** mas ficou travado no ponto em que o desempenho importava? Você não está sozinho—muitos desenvolvedores encontram o mesmo obstáculo quando o OCR se torna um gargalo. Neste tutorial vamos mostrar exatamente como extrair texto de imagem usando o runtime GPU do Aspose OCR, carregar a imagem a partir de um arquivo e até definir um limite de memória GPU para um controle de recursos mais rigoroso.

Vamos percorrer um exemplo completo, pronto‑para‑executar em C#, explicar por que cada linha importa e apontar armadilhas comuns que você pode encontrar. Ao final, você terá uma base sólida para construir pipelines de OCR rápidos e escaláveis que rodam na GPU.

## O que este Guia Cobre

- **Pré‑requisitos**: .NET 6+ (ou .NET Framework 4.6+), pacote NuGet Aspose.OCR, um driver de GPU compatível.  
- **Código passo‑a‑passo** que carrega uma imagem a partir de um arquivo, configura o motor Aspose OCR GPU e extrai o texto.  
- **Por que** você pode querer definir um limite de memória GPU e como fazer isso com segurança.  
- **Tratamento de casos de borda**: imagens de baixa resolução, GPU ausente e solução de problemas de pontuações de confiança.  
- **Próximos passos**: processamento em lote, integração com ASP.NET Core e troca de volta para CPU, se necessário.

> **Dica profissional:** Se não tiver certeza se sua GPU está sendo usada, verifique o monitor de atividade da GPU (por exemplo, NVIDIA‑SMI) enquanto o OCR roda. Você verá um pico no uso de memória que corresponde ao limite que você definiu.

---

![Diagrama mostrando o fluxo de extração de texto de imagem usando o motor Aspose OCR GPU](extract-text-from-image-aspose-ocr-gpu.png "extrair texto de imagem usando Aspose OCR GPU")

## Etapa 1: Inicializar o Motor Aspose OCR para Processamento GPU

A primeira coisa que você precisa é de uma instância `OcrEngine` que saiba que deve ser executada na GPU. A Aspose fornece um objeto limpo `OcrEngineSettings` onde você pode especificar o runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Por que isso importa:** Por padrão o Aspose OCR recorre à CPU, o que é aceitável para imagens pequenas, mas pode ser dolorosamente lento para fotos de alta resolução. Definir explicitamente `Runtime = OcrRuntime.Gpu` transfere o trabalho pesado para a placa gráfica, proporcionando um aumento de velocidade perceptível.

## Etapa 2: (Opcional) Definir um Limite de Memória GPU

Se você estiver rodando em uma estação de trabalho compartilhada ou em um contêiner com recursos de GPU limitados, pode limitar a quantidade de memória que o motor OCR consome. Isso previne falhas por falta de memória e mantém outros processos satisfeitos.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Quando usar:**  
- **Ambientes multi‑tenant** onde vários serviços compartilham a mesma GPU.  
- **Pipelines CI/CD** que alocam uma quantidade fixa de memória GPU por job.  

Se você omitir esta linha, a Aspose usará toda a memória que precisar, o que é aceitável em uma estação de trabalho dedicada.

## Etapa 3: Carregar Imagem a partir de Arquivo

Agora precisamos trazer a foto para a memória. O Aspose OCR trabalha com `System.Drawing.Image`, então usaremos `Image.FromFile`. Certifique‑se de que o caminho aponta para um arquivo real; caso contrário, uma exceção será lançada.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Por que carregar a partir de arquivo importa:** Muitos desenvolvedores tentam alimentar um array de bytes diretamente, o que funciona, mas adiciona uma etapa de conversão desnecessária. Usar `Image.FromFile` é direto, e a instrução `using` garante que o manipulador do arquivo seja liberado rapidamente.

## Etapa 4: Executar OCR e Recuperar o Resultado

Com o motor configurado e a imagem carregada, finalmente podemos extrair o texto. O método `Recognize` retorna um `OcrResult` contendo tanto o texto bruto quanto uma pontuação de confiança.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Entendendo a saída:**  
- `Confidence` é um valor entre 0 e 1. Uma confiança de 0,95 (ou 95 %) geralmente indica que o OCR está perfeito.  
- `Text` contém quebras de linha como aparecem na imagem, o que é útil para processamento posterior.

## Etapa 5: Verificar Saída e Tratar Casos de Borda

### Verificando Níveis de Confiança

Se a confiança cair abaixo, digamos, 80 %, você pode querer voltar ao processamento por CPU ou aplicar pré‑processamento de imagem (por exemplo, binarização).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Lidando com GPU Ausente

Nem toda máquina possui uma GPU compatível. A Aspose lançará uma `OcrException` se não conseguir inicializar o runtime GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Imagens de Alta Resolução

Imagens muito grandes (por exemplo, > 4000 px de largura) podem consumir muita memória GPU. Se você atingir o limite definido anteriormente, a Aspose truncará o processamento. Nesses casos, redimensione a imagem primeiro:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Exemplo Completo Funcional

Abaixo está o programa completo que você pode copiar‑colar em um novo projeto de console. Ele inclui todas as etapas, tratamento de erros e lógica opcional de fallback.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Saída Esperada

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Se a confiança cair abaixo do limiar, você verá as mensagens adicionais de fallback para CPU.

---

## Conclusão

Agora você sabe **como extrair texto de imagem** usando o motor GPU do Aspose OCR, como **carregar imagem a partir de arquivo** e por que pode querer **definir limite de memória GPU** para cargas de trabalho de produção. O exemplo acima é uma solução totalmente funcional e digna de citação que pode ser inserida em qualquer projeto .NET.

O que vem a seguir? Considere:

- **Processamento em lote**: percorrer uma pasta de imagens e gravar os resultados em um CSV.  
- **Integração ASP.NET Core**: expor um endpoint de API que aceita uma imagem enviada e devolve o texto OCR.  
- **Ajuste de desempenho**: experimentar diferentes valores de `GpuMemoryLimit` e monitorar a utilização da GPU para encontrar o ponto ideal.

Sinta‑se à vontade para adaptar o código ao seu cenário—seja construindo um pipeline de digitalização de documentos, um app de tradução em tempo real ou um serviço de escaneamento de recibos. Os fundamentos permanecem os mesmos: inicializar o motor GPU, gerenciar a memória com sabedoria e sempre verificar a confiança.

Tem perguntas ou encontrou algum problema? Deixe um comentário abaixo e vamos solucionar juntos. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}