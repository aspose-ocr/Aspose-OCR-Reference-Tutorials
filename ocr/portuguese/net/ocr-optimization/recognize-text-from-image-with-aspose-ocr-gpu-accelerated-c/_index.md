---
category: general
date: 2026-01-13
description: Aprenda a reconhecer texto a partir de imagens e extrair texto de recibos
  rapidamente usando o Aspose OCR. Inclui etapas de carregamento de imagem para OCR
  e definição do ID do dispositivo GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: pt
og_description: reconheça texto de imagem instantaneamente com o Aspose OCR. siga
  este guia passo a passo para carregar a imagem para OCR, definir o ID do dispositivo
  GPU e extrair texto do recibo.
og_title: reconhecer texto de imagem – Guia completo de C# acelerado por GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Reconheça texto de imagem com Aspose OCR – Tutorial C# Acelerado por GPU
url: /pt/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem – Guia completo C# acelerado por GPU

Já precisou **reconhecer texto de imagem** e achou a versão CPU dolorosamente lenta? Talvez você esteja tentando **extrair texto de recibos** e a latência esteja matando a experiência do usuário. A boa notícia é que você não precisa se contentar com desempenho lento — o pacote GPU do Aspose OCR pode turbinar o processo, e o código tem apenas algumas linhas.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **carregar imagem para OCR**, configurar a GPU com **definir ID do dispositivo GPU**, e finalmente obter o resultado em texto simples. Ao final, você terá um snippet pronto para usar que funciona em qualquer máquina Windows ou Linux moderna com uma placa NVIDIA compatível.

---

## O que você precisará

- **.NET 6+** (ou .NET Framework 4.7.2+) – a API funciona com ambos.
- Pacote NuGet **Aspose.OCR** **mais** o add‑on **Aspose.OCR.Gpu**.
- Uma GPU NVIDIA com pelo menos 2 GB de VRAM (a demonstração limita o uso a 1 GB).
- Uma imagem de exemplo, por exemplo, um recibo escaneado (`receipt.jpg`).

Se já tem um projeto, basta executar `dotnet add package Aspose.OCR` e `dotnet add package Aspose.OCR.Gpu`. Nenhuma biblioteca nativa extra é necessária; o SDK inclui os binários CUDA necessários.

---

## Implementação passo a passo

### ## Como reconhecer texto de imagem usando Aspose OCR e GPU

Abaixo está o **programa completo e autocontido**. Copie‑e‑cole em um novo projeto de console e pressione `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Dica profissional:** Se sua máquina tem várias GPUs, altere `DeviceId` para `1`, `2`, etc., para escolher a placa menos ocupada. O SDK lançará uma clara `GpuDeviceNotFoundException` se o ID estiver fora do intervalo.

### ### Passo 1: Carregar imagem para OCR

A chamada `OcrImage.FromFile` faz mais do que apenas ler um bitmap — ela pré‑processa a imagem (deskew, binarização) com base em heurísticas internas. Por isso **carregar imagem para OCR** é uma etapa separada: você pode trocar por um `MemoryStream` se sua imagem estiver em um banco de dados.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Se precisar **reconhecer texto de imagem** que já está na memória:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Passo 2: Definir ID do dispositivo GPU e limites de memória

Recursos de GPU são finitos. Ao expor `DeviceId` e `MaxMemoryMb`, a Aspose permite que você **defina ID do dispositivo GPU** com segurança, evitando que um processo monopolize toda a placa.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Se ultrapassar o limite de memória, o motor automaticamente transbordará para a RAM do sistema, o que é mais lento, mas evita falhas.

### ### Passo 3: Extrair texto do recibo (reconhecer texto de imagem)

O método `Recognize` faz o trabalho pesado. Você pode passar qualquer idioma suportado pelo Aspose OCR; para recibos, o inglês funciona na maioria das vezes, mas você também pode adicionar `OcrLanguage.Spanish` ou um pacote de idioma customizado.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Saída esperada** (exemplo):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Variações comuns & casos de borda

| Situação | O que mudar | Por quê |
|-----------|----------------|-----|
| **Múltiplos recibos em uma imagem** | Chamar `ocrEngine.Recognize` em cada região recortada (usar `OcrImage.Crop`) | Melhora a precisão porque o motor vê uma área menor e mais limpa. |
| **Digitalizações de baixa resolução (<150 dpi)** | Pré‑escalar com `receiptImage.Resize(2.0)` antes do reconhecimento | Maior densidade de pixels fornece mais dados para a GPU. |
| **Recibos não‑inglês** | Passar `OcrLanguage.French` (ou um `.traineddata` customizado) | Modelos específicos de idioma reduzem falsos positivos. |
| **GPU indisponível** | Recuar para `OcrEngine` (CPU) dentro de um bloco try‑catch | Garante que o app continue funcionando em servidores sem GPU. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Dicas para OCR pronto para produção

- **Processamento em lote:** Envolva o loop de reconhecimento em `Parallel.ForEach`, mas limite o grau de paralelismo ao número de streams de GPU que você pode alocar (geralmente 1‑2 por placa).
- **Higiene de memória:** Libere objetos `OcrImage` prontamente (`receiptImage.Dispose()`), especialmente ao processar milhares de recibos.
- **Log:** Capture `ocrResult.Confidence` para cada linha; baixa confiança pode acionar um fluxo de revisão manual.
- **Segurança:** Ao lidar com recibos sensíveis, garanta que os arquivos de imagem sejam armazenados em pastas temporárias criptografadas e apagados após o processamento.

---

## Conclusão

Agora você tem um **exemplo completo e executável** que demonstra como **reconhecer texto de imagem** com a aceleração GPU do Aspose OCR, **carregar imagem para OCR**, **definir ID do dispositivo GPU**, e finalmente **extrair texto de recibos** em poucos passos concisos. O código está pronto para copiar‑e‑colar, e as explicações fornecem contexto suficiente para adaptá‑lo a cenários multilinguísticos, multi‑GPU ou de alta taxa de transferência.

Pronto para o próximo desafio? Experimente alimentar um stream de vídeo ao vivo em `GpuOcrEngine` para escaneamento de recibos em tempo real, ou integre o resultado a uma API de contabilidade. O céu é o limite quando você combina OCR rápido em GPU com um design C# limpo.

*Feliz codificação, e que seu OCR seja sempre veloz!* 

![reconhecer texto de imagem demonstração captura de tela](placeholder-image.png "exemplo de reconhecer texto de imagem")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}