---
category: general
date: 2026-02-09
description: Como usar o Aspose OCR com aceleração GPU em C#. Aprenda a reconhecer
  texto de JPG, extrair texto de imagem e habilitar a GPU em apenas alguns minutos.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: pt
og_description: Como usar o Aspose OCR com GPU em C#. Este guia mostra como reconhecer
  texto de JPG e extrair texto de imagem usando aceleração GPU.
og_title: Como usar o Aspose OCR com GPU – Guia completo de programação
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: Como usar o Aspose OCR com GPU – Guia passo a passo
url: /pt/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Aspose OCR com GPU – Guia de Programação Completo

Já precisou processar uma pilha de notas fiscais escaneadas em um instante, mas a CPU não aguentava? Esse é um ponto de dor clássico quando você está tentando **how to use aspose** para OCR em escala. Neste tutorial vamos guiá‑lo através de um exemplo do mundo real que mostra **how to use aspose** para reconhecer texto de arquivos jpg, extrair texto de imagem e aproveitar ao máximo sua GPU.

Pense nisso como um passo‑a‑passo de intervalo de café — sem enrolação, apenas os trechos que você pode copiar‑colar no Visual Studio e ver a mágica acontecer. Ao final você terá um aplicativo console C# autônomo que roda em qualquer máquina Windows moderna com GPU NVIDIA ou AMD.

![how to use aspose OCR with GPU](/images/aspose-gpu-example.png)

## O Que Você Precisa

- **.NET 6.0** (ou superior) – o código tem como alvo o .NET 6, mas funciona com .NET 5 e .NET Framework 4.8 com pequenos ajustes.
- **Aspose.OCR for .NET** pacote NuGet – instale‑o via `dotnet add package Aspose.OCR`.
- Uma **máquina com GPU habilitada** – o tutorial mostra como **how to enable gpu** e **how to set gpu** limites de memória, mas o código recairá graciosamente para CPU se nenhuma GPU compatível for encontrada.
- Uma imagem como `invoice_01.jpg` colocada em uma pasta que você possa referenciar.

Tem tudo isso? Ótimo, vamos mergulhar.

## Como Usar Aspose OCR com GPU – Configuração Inicial

A primeira coisa que você deve fazer é criar uma instância do motor OCR e instruí‑lo a usar a GPU. Esta etapa é crucial porque, sem a flag, o Aspose usará o processamento por CPU por padrão, o que anula o objetivo do nosso ganho de desempenho.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**Por que isso importa:** Habilitar a GPU move os kernels pesados de processamento de imagem para o processador gráfico, que pode ser 10‑20× mais rápido que a CPU para imagens grandes. O `GpuMemoryLimit` funciona como válvula de segurança; definir 1024 MB funciona para a maioria das placas de médio alcance enquanto mantém o aplicativo responsivo.

> **Dica de especialista:** Se você executar o aplicativo em uma máquina sem GPU compatível, o Aspose reverterá automaticamente para o modo CPU e registrará um aviso. Sem travamentos, apenas uma execução mais lenta.

## Reconhecer Texto de JPG – Carregando a Imagem

Agora que o motor está pronto, precisamos alimentá‑lo com uma imagem. O exemplo usa um JPEG porque **recognize text from jpg** é um cenário comum para notas fiscais, recibos e passaportes.

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**Por que verificamos o arquivo:** Um arquivo ausente é a causa mais frequente de erros em tempo de execução em demonstrações rápidas. Ao tratá‑lo logo, você mantém o tutorial amigável para iniciantes.

## Extrair Texto da Imagem – Executando o Motor OCR

Com a imagem em mãos, o próximo passo é realmente executar o processo OCR. É aqui que o Aspose faz o trabalho pesado e devolve um objeto `OcrResult` que contém o texto puro, pontuações de confiança e até caixas delimitadoras, caso você precise delas mais tarde.

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**O que você verá:** O console imprime os caracteres brutos que o Aspose detectou. Para uma nota fiscal limpa, você pode obter algo como:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

Se a saída parecer confusa, provavelmente você precisará ajustar a qualidade da imagem ou habilitar opções adicionais de pré‑processamento (ex.: deskew, binarização). Esses detalhes estão fora do escopo deste guia rápido, mas são documentados na referência da API do Aspose.

## Como Habilitar GPU – Configurando o Motor

Você pode estar se perguntando **how to enable gpu** para o Aspose se perdeu a primeira etapa. A resposta é simplesmente alternar a flag `UseGpu` no objeto de configuração do motor, como mostrado anteriormente. Aqui está um trecho condensado que você pode inserir em qualquer projeto existente:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

Nos bastidores, o Aspose carrega bibliotecas nativas CUDA/OpenCL que correspondem ao seu hardware. Se o runtime não conseguir localizá‑las, ele registra um aviso e recua para CPU. Nenhuma etapa extra de instalação é necessária na maioria das configurações Windows.

## Como Definir GPU – Ajustando o Uso de Memória

Às vezes você encontrará um erro “out of memory” em uma GPU de baixo custo. É aí que **how to set gpu** limites de memória se torna útil. A propriedade `GpuMemoryLimit` aceita um inteiro que representa megabytes.

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**Quando ajustar:** Se você estiver processando muitas imagens em paralelo, diminua o limite para evitar que a placa fique saturada. Por outro lado, em uma estação de trabalho com 8 GB de VRAM você pode aumentar com segurança para 4096 MB para processamento em lote mais rápido.

## Exemplo Completo e Executável

A seguir está o programa completo que você pode copiar para um novo projeto console (`dotnet new console`). Ele inclui todas as partes que discutimos, além de um pequeno tratamento de erros para torná‑lo robusto.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**Saída esperada:** Após executar `dotnet run`, o console imprimirá o texto bruto extraído de `invoice_01.jpg`. Se a imagem contiver texto impresso claro, o resultado deverá ser quase idêntico ao documento original.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Correção Rápida |
|----------|------------------|-----------------|
| **GPU não detectada** | Drivers CUDA ausentes ou GPU não suportada | Instale o driver mais recente da NVIDIA/AMD; verifique com `nvidia-smi` ou equivalente |
| **Erro de falta de memória** | `GpuMemoryLimit` muito alto para a placa | Reduza o limite para 512 MB ou menos |
| **Saída confusa** | JPG de baixa resolução ou compressão pesada | Use uma imagem fonte de maior qualidade ou habilite `ocrEngine.Preprocessing.Deskew = true` |
| **`ocrResult` nulo** | Falha ao carregar o fluxo da imagem | Verifique o caminho do arquivo e assegure que o arquivo não esteja bloqueado |

Abordar esses pontos antecipadamente economiza tempo de caça a rastreamentos de pilha crípticos depois.

## Próximos Passos

Agora que você dominou **how to use aspose** para OCR rápido, pode explorar:

- **Processamento em lote** – percorrer um diretório de JPGs e gravar cada resultado em um arquivo `.txt`.
- **Extração estruturada** – usar `ocrResult.Regions` para obter caixas delimitadoras e extrair campos específicos como números de nota fiscal.
- **Modo híbrido CPU/GPU** – usar CPU para imagens pequenas e mudar para GPU apenas em arquivos grandes, equilibrando velocidade e memória.

Todas essas extensões se baseiam na mesma fundação que você acabou de montar, e são tópicos perfeitos para sua próxima aventura tutorial.

---

*Feliz codificação! Se encontrar algum obstáculo, deixe um comentário abaixo ou avise nos fóruns da comunidade Aspose. A GPU está pronta — vamos tornar o OCR relâmpago.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}