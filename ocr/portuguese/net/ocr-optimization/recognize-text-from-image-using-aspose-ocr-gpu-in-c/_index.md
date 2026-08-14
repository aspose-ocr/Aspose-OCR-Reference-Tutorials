---
category: general
date: 2026-02-20
description: Reconheça texto de imagem rapidamente com a aceleração GPU do Aspose
  OCR. Aprenda como extrair texto de uma digitalização em C# com um exemplo completo
  e executável.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: pt
og_description: reconheça texto de imagem com aceleração GPU. Este tutorial mostra
  como extrair texto de uma digitalização em C# usando Aspose OCR, completo com código
  e dicas.
og_title: Reconheça texto de imagem usando Aspose OCR GPU – Guia C#
tags:
- Aspose
- OCR
- C#
- GPU
title: reconhecer texto de imagem usando Aspose OCR GPU em C#
url: /pt/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

We need to translate the tutorial text.

Let's go section by section.

First three shortcodes lines remain unchanged.

Then heading "# recognize text from image using Aspose OCR GPU in C#" translate to Portuguese: "# reconhecer texto de imagem usando Aspose OCR GPU em C#". Keep same case? We'll translate.

Then paragraph.

We'll translate each paragraph.

Make sure to keep code block placeholders unchanged.

Also tables.

Translate table content but keep structure.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem usando Aspose OCR GPU em C#

Já precisou **reconhecer texto de uma imagem** mas o arquivo era enorme e sua CPU travava? Talvez você tenha tentado uma biblioteca OCR simples e ela demorou uma eternidade, ou os resultados foram incompletos. A boa notícia? Com a aceleração por GPU do Aspose OCR você pode transformar um TIFF escaneado gigantesco em texto limpo e pesquisável em segundos.

Neste guia vamos percorrer um exemplo completo, pronto para copiar‑e‑colar, que mostra como **extrair texto de arquivos de digitalização** em uma máquina com GPU habilitada. Sem referências vagas, apenas o código que você precisa, por que cada linha importa e alguns detalhes para evitar dores de cabeça.

## O que você vai precisar

- **.NET 6+** (ou .NET Framework 4.7+ – a API funciona da mesma forma)
- Pacote NuGet **Aspose.OCR for .NET** (versão 23.12 ou superior)
- Uma **GPU** com suporte a CUDA (opcional, mas muito mais rápida)
- Uma imagem escaneada de alta resolução (por exemplo, `large_doc.tif`)

Se você não tem uma GPU, o motor retornará automaticamente ao uso da CPU – então ainda pode executar o exemplo, apenas um pouco mais devagar.

## Etapa 1 – Instalar o pacote Aspose.OCR

Abra seu terminal ou o Console do Gerenciador de Pacotes e execute:

```bash
dotnet add package Aspose.OCR
```

Ou, na UI do NuGet do Visual Studio, procure por **Aspose.OCR** e clique em *Install*. Isso traz a biblioteca OCR principal mais o assembly opcional de aceleração por GPU.

> **Dica de especialista:** Depois de instalar, verifique a pasta `packages` para `Aspose.OCR.Acceleration.dll`. Ele é necessário para o suporte à GPU; se você estiver em um servidor sem interface gráfica, pode omiti‑lo e o código ainda compilará.

## Etapa 2 – Inicializar o motor OCR acelerado por GPU

A classe `GpuOcrEngine` detecta automaticamente qualquer GPU compatível. Se houver mais de um dispositivo, você pode escolher um específico, mas a maioria dos desenvolvedores deixa que ele decida.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Por que isso importa:** Inicializar o motor GPU uma única vez mantém a sobrecarga baixa. Se você criar e destruir o motor repetidamente dentro de um loop, perderá os ganhos de desempenho.

## Etapa 3 – Carregar sua imagem escaneada de alta resolução

O Aspose OCR trabalha com `System.Drawing.Image`. Certifique‑se de que o caminho do arquivo aponta para uma imagem real; caso contrário, você receberá um `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Caso extremo:** Se a imagem for maior que 10 000 × 10 000 px, considere fazer down‑sampling primeiro. A memória da GPU é limitada, e tentar carregar um bitmap gigantesco pode gerar um `OutOfMemoryException`.

## Etapa 4 – Executar OCR com as configurações de idioma padrão (Latim)

O método `Recognize` devolve uma string simples. Você pode passar um objeto `OcrOptions` se precisar de outro idioma ou de pré‑processamento customizado.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Por que o padrão funciona:** A maioria dos documentos escaneados – contratos, notas fiscais, relatórios – está em alfabetos baseados no latim. Se precisar de cirílico, árabe ou chinês, defina `ocrEngine.Language = "ru"` (ou o código ISO apropriado) antes de chamar `Recognize`.

## Etapa 5 – Exibir ou persistir o texto extraído

Para uma verificação rápida, vamos apenas escrever o resultado no console. Em uma aplicação real você pode salvar em um banco de dados, em um arquivo `.txt` ou enviá‑lo para um índice de busca.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Saída esperada

Se `large_doc.tif` contiver um parágrafo simples como “Hello, world!”, você verá:

```
Hello, world!
```

Para digitalizações de várias páginas o motor concatena o texto na ordem de leitura. Você pode dividir depois usando quebras de linha (`\n`) se precisar separar as páginas.

## Lidando com armadilhas comuns

| Problema | Sintoma | Solução |
|----------|---------|---------|
| **Nenhuma GPU detectada** | `ocrEngine.Device` é `null` e o processamento está lento. | Instale o driver NVIDIA mais recente e o CUDA Toolkit (v11+). Verifique com `nvidia-smi`. |
| **Atrasos na coleta de lixo** | Picos de memória após processar muitas imagens. | Chame `scannedImage.Dispose()` após o OCR, ou envolva a imagem em um bloco `using`. |
| **Idioma errado** | Caracteres embaralhados para texto não‑latino. | Defina `ocrEngine.Language` para o código ISO 639‑1 correto antes de `Recognize`. |
| **Arquivos muito grandes** | `OutOfMemoryException`. | Reduza a resolução com `Image.GetThumbnailImage` ou divida a digitalização em blocos. |

## Exemplo completo, pronto para executar

Abaixo está o programa inteiro – incluindo diretivas `using`, tratamento de erros e um bloco `using` organizado para a imagem:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### O que este código faz

1. **Cria** um `GpuOcrEngine` que seleciona automaticamente a melhor GPU.
2. **Carrega** o TIFF alvo dentro de um bloco `using` para garantir a liberação.
3. **Chama** `Recognize` para converter o bitmap em uma string.
4. **Escreve** o resultado tanto no console quanto em um arquivo `.txt` ao lado da imagem original.
5. **Captura** qualquer exceção e exibe uma mensagem de erro amigável.

## Avançando – De “reconhecer texto de imagem” a pipelines de documentos em escala

Agora que você pode **extrair texto de arquivos de digitalização**, considere os próximos passos:

- **Processamento em lote:** Percorra uma pasta de TIFFs e agregue os resultados em um único índice pesquisável.
- **Detecção de idioma:** Use `ocrEngine.DetectLanguage()` (se disponível) para mudar de idioma automaticamente.
- **Pós‑processamento:** Passe a saída por um corretor ortográfico ou filtro regex para limpar artefatos de OCR.
- **Integração com Azure Cognitive Search:** Envie o texto extraído para um índice de nuvem pesquisável e obtenha buscas instantâneas.

Cada um desses itens se baseia no mesmo padrão central que você acabou de ver – inicializar uma vez, alimentar imagens, coletar texto.

## Conclusão

Você acabou de aprender como **reconhecer texto de imagem** usando o motor OCR acelerado por GPU da Aspose OCR em C#. O exemplo completo e executável mostra como configurar o motor, carregar uma digitalização de alta resolução, executar OCR e lidar com a saída. Seguindo as dicas e o tratamento de casos extremos acima, você evitará armadilhas comuns e obterá resultados confiáveis, seja em um laptop de desenvolvimento ou em um servidor de produção.

Pronto para transformar mais digitalizações em dados pesquisáveis? Experimente processar uma pasta inteira, teste idiomas não latinos ou alimente os resultados em um motor de busca full‑text. O céu é o limite, e o código que você acabou de escrever é a base sólida que você precisava.

Happy coding! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}