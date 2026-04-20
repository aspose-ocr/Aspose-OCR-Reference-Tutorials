---
category: general
date: 2026-02-14
description: Carregue o arquivo de imagem e extraia o texto do recibo usando o motor
  Aspose OCR GPU. Aprenda a definir a memória máxima da GPU, configurar a memória
  da GPU e executar OCR na imagem de forma eficiente.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: pt
og_description: Carregue o arquivo de imagem e extraia o texto do recibo usando o
  motor OCR GPU da Aspose. Este guia mostra como definir a memória máxima da GPU e
  executar OCR na imagem em C#.
og_title: Carregar arquivo de imagem e extrair texto de recibo com OCR GPU em C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Carregar arquivo de imagem e extrair texto de recibo com OCR GPU em C#
url: /pt/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carregar Arquivo de Imagem e Extrair Texto de Recibo com OCR GPU em C#

Já precisou **load image file** e extrair o texto exato de um recibo, mas ficou preso na etapa de OCR? Você não está sozinho. Em muitos aplicativos do mundo real—rastreadores de despesas, sistemas de inventário ou até bots simples de escaneamento de recibos—a capacidade de ler rapidamente a imagem de um recibo pode ser um divisor de águas.  

A boa notícia? Com o motor acelerado por GPU da Aspose.OCR você pode **load image file**, **set max GPU memory** e **run OCR on image** tudo em algumas linhas organizadas de C#. A seguir, vamos percorrer todo o processo, desde a configuração da GPU até a impressão do texto simples extraído.

## O que você aprenderá

* **Load image file** do disco usando `ImageStream` da Aspose.
* **Configure GPU memory** para que o motor nunca consuma mais RAM do que você permite.
* **Run OCR on image** e extraia cada caractere de um recibo.
* Lide com armadilhas comuns—como erros de out‑of‑memory ou digitalizações borradas.
* Verifique a saída e ajuste as configurações para melhor precisão.

Sem serviços externos, sem truques obscuros—apenas código puro em C# que você pode inserir em qualquer projeto .NET 6+.

---

## Pré-requisitos

Antes de mergulharmos, certifique-se de que você tem:

* .NET 6 SDK ou posterior instalado.
* Uma licença válida do Aspose.OCR (ou você pode usar o modo de avaliação gratuito).
* Os pacotes NuGet `Aspose.OCR` e `Aspose.OCR.Gpu` adicionados ao seu projeto.
* Uma imagem de recibo de exemplo (`receipt.png`) pronta no disco.

Se algum desses lhe for desconhecido, faça uma pausa e instale os pacotes:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

É isso—nenhuma biblioteca nativa extra é necessária porque o suporte a GPU está incorporado diretamente no pacote NuGet.

---

## Carregar Arquivo de Imagem e Preparar o Motor GPU

A primeira coisa que você deve fazer é **load image file** em um `ImageStream`. Esse objeto abstrai os detalhes do sistema de arquivos e fornece ao motor OCR uma representação limpa, em memória.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Por que isso importa:**  
*Loading the image file* via `ImageStream.FromFile` garante que o motor veja os dados de pixel exatos, preservando DPI e profundidade de cor. Pular esta etapa ou fornecer um stream corrompido fará com que o OCR perca caracteres ou lance exceções.

> **Dica profissional:** Se você estiver lidando com arquivos enviados por usuários, envolva a chamada `FromFile` em um bloco try‑catch e valide o tamanho do arquivo primeiro. Imagens grandes podem estourar a memória da GPU se você não tiver **configured GPU memory** corretamente.

---

## Definir Memória Máxima da GPU para Desempenho Ótimo

Recursos de GPU são preciosos, especialmente em servidores compartilhados ou laptops com VRAM limitada. A propriedade `MaxDeviceMemory` informa à Aspose quanto da memória da GPU pode ser alocada com segurança.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Quando você **set max GPU memory**, o motor automaticamente recairá para o processamento por CPU se não conseguir atender à solicitação—evitando falhas. Esta é a maneira mais segura de **configure GPU memory** sem codificar limites específicos do dispositivo.

**Quando ajustar:**  
* Se você notar `OutOfMemoryException` durante o processamento em lote pesado, diminua o limite.  
* Se seus recibos forem de alta resolução (300 DPI+), aumente para 2 GB para manter a velocidade alta.

---

## Executar OCR na Imagem para Extrair Texto do Recibo

Agora a parte divertida—realmente **run OCR on image** e extrair o texto do recibo. O método `Recognize` retorna um objeto `OcrResult` que contém a propriedade `Text` com a saída em texto simples.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

O console exibirá algo como:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Por que isso funciona:**  
O motor GPU executa um modelo de deep‑learning que foi treinado em uma variedade de layouts de documentos. Ao fornecer uma imagem limpa e carregada corretamente, você dá ao modelo a melhor chance de **extract text from receipt** com precisão.

---

## Verificar a Saída e Armadilhas Comuns

Mesmo com um motor poderoso, OCR não é mágica. Aqui estão algumas coisas para ficar atento:

| Problema | Causa | Correção |
|----------|-------|----------|
| Caracteres embaralhados | Baixo contraste ou imagem borrada | Pré‑processar com `ImageProcessor` da Aspose para aumentar o contraste |
| Linhas ausentes | Imagem recortada demais | Garanta que o recibo caiba totalmente dentro dos limites da imagem |
| Erros de falta de memória | `MaxDeviceMemory` muito baixo para o tamanho da imagem | Aumente `MaxDeviceMemory` ou reduza a escala da imagem primeiro |
| Idioma errado | Recibo contém texto não‑inglês | Defina `gpuEngine.Language = OcrLanguage.Spanish;` (ou o apropriado) |

Se você encontrar algum desses, a solução rápida é redimensionar a imagem para menos de 2000 px no lado mais longo—isso reduz drasticamente a pressão sobre a GPU sem sacrificar a legibilidade na maioria dos recibos.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo, pronto para compilar. Substitua o caminho do arquivo pela localização do seu próprio recibo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Saída esperada no console** (seu recibo será diferente, é claro):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Execute o programa com `dotnet run`. Se você vir o texto impresso, parabéns—você **load image file**, **set max GPU memory**, e **run OCR on image** com sucesso para **extract text from receipt**.

---

## Perguntas Frequentes

**Q: Isso funciona em máquinas sem GPU dedicada?**  
A: Sim. Aspose.OCR recairá graciosamente para o modo CPU se nenhuma GPU compatível for detectada. Você ainda poderá **load image file** e **run OCR on image**, apenas um pouco mais devagar.

**Q: Posso processar vários recibos em lote?**  
A: Absolutamente. Envolva o código de reconhecimento em um loop `foreach`, mas lembre‑se de reutilizar a mesma instância `GpuEngine`—isso evita reinicializar os recursos da GPU para cada arquivo.

**Q: E se meu recibo estiver em um idioma diferente do inglês?**  
A: Defina o idioma antes de chamar `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Próximos Passos e Tópicos Relacionados

Agora que você dominou o básico, considere explorar:

* **Fine‑tuning OCR accuracy** – experimente `gpuEngine.RecognitionOptions` como `EnableDeskew` ou `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}