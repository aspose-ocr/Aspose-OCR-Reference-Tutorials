---
category: general
date: 2026-03-17
description: Tutorial de OCR em C# – descubra como extrair texto de arquivos de imagem,
  ler texto de fotos WebP e converter imagem em texto usando um OcrEngine simples.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: pt
og_description: Tutorial de OCR em C# mostra como extrair texto de arquivos de imagem,
  ler texto de fotos WebP e converter imagem em texto com algumas linhas de código.
og_title: Tutorial de OCR em C# – Extraia Texto de Imagens em Minutos
tags:
- C#
- OCR
- Image Processing
title: 'Tutorial de OCR em C#: Extrair Texto de Imagens (WebP, Foto) – Guia Rápido'
url: /pt/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Extrair Texto de Imagens (WebP, Foto)

Já precisou **extrair texto de arquivos de imagem** mas não sabia por onde começar em C#? Talvez você tenha uma captura de tela em WebP, um JPEG de um recibo ou uma página de PDF escaneada e queira apenas as palavras contidas nela. Neste **c# OCR tutorial** vamos percorrer um exemplo completo, pronto‑para‑executar, que lê texto de uma foto, lida com WebP e outros formatos modernos, e converte a imagem em texto simples — tudo em poucas linhas.

**Qual é o benefício?** Você poderá transformar qualquer imagem contendo texto em strings pesquisáveis, inseri‑las em bancos de dados ou enviá‑las para pipelines de IA subsequentes. Sem mágica, apenas um motor OCR sólido, algumas APIs .NET e explicações claras do “porquê” de cada passo.

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que tem:

- **.NET 6 SDK** (ou superior). O código abaixo compila com .NET 6+ e roda no Windows, Linux ou macOS.
- **Visual Studio 2022** ou qualquer editor de sua preferência (VS Code funciona bem).
- O pacote NuGet **`Microsoft.Windows.SDK.Contracts`** (fornece `Windows.Media.Ocr`). Instale com:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Um arquivo de imagem que você deseja processar – para este tutorial usaremos uma foto **WebP** chamada `photo.webp` colocada em uma pasta chamada `YOUR_DIRECTORY`.

> Dica de especialista: Se você estiver em uma plataforma não‑Windows, pode substituir o `OcrEngine` por uma biblioteca multiplataforma como **Tesseract**. O código ao redor permanece praticamente o mesmo.

## Etapa 1: Configurar um Projeto de Tutorial OCR em C#

Primeiro, crie um novo aplicativo de console. Abra um terminal e execute:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Adicione o pacote necessário (conforme mostrado acima) e abra o projeto em sua IDE. Essa estrutura nos dá uma base limpa para o **c# OCR tutorial**.

## Etapa 2: Importar Namespaces e Preparar a Imagem

Precisamos de alguns directives `using` para que o compilador saiba onde encontrar `OcrEngine`, `SoftwareBitmap` e os auxiliares de carregamento de imagem.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Por que esses namespaces?**  
> `Windows.Media.Ocr` contém a classe `OcrEngine` que realmente realiza o reconhecimento. `Windows.Graphics.Imaging` nos permite decodificar a imagem (incluindo WebP) em um `SoftwareBitmap` que o motor entende. Os auxiliares `System.IO` e `Windows.Storage.Streams` facilitam o carregamento de arquivos.

Agora, carregue a imagem. O decodificador interno pode lidar com WebP, HEIF, PNG, JPEG e mais, então você pode **ler texto de WebP** sem plugins adicionais.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Caso extremo:** Se sua imagem já for preto‑e‑branco, pode pular a etapa de conversão. A conversão para tons de cinza traz um pequeno ganho de desempenho e costuma melhorar o reconhecimento em fotos ruidosas.

## Etapa 3: Executar o Motor OCR – Reconhecer Texto da Foto

Aqui está o coração do **c# OCR tutorial**. Criamos uma instância de `OcrEngine`, alimentamos o bitmap e extraímos o texto reconhecido.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**O que está acontecendo?**  
- `TryCreateFromUserProfileLanguages()` seleciona o(s) idioma(s) configurados no perfil do usuário Windows, que normalmente cobrem Inglês, Espanhol, etc. Se precisar de um idioma específico, use `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` executa o trabalho pesado em uma thread em segundo plano, retornando um `OcrResult` que contém a string bruta, caixas delimitadoras de palavras e pontuações de confiança.
- Por fim, imprimimos `ocrResult.Text`, fornecendo o resultado do **converter imagem em texto** que você pode encaminhar para onde desejar.

## Etapa 4: Exemplo Completo e Executável

Juntando tudo, aqui está um programa autocontido que você pode copiar‑colar em `Program.cs`. Ele compila, executa e imprime o texto extraído de `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Saída Esperada

Se `photo.webp` contiver a frase “Hello, world! This is a test.” você verá algo como:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

As quebras de linha exatas dependem do layout da imagem fonte, mas o resultado do **extrair texto de imagem** será sempre uma string simples que você pode manipular posteriormente.

## Perguntas Frequentes & Casos de Borda

### Isso funciona com outros formatos de imagem?

Com certeza. O decodificador usado (`BitmapDecoder`) detecta automaticamente JPEG, PNG, BMP, GIF, **WebP**, HEIF e mais. Portanto, você pode **ler texto de WebP**, JPEG ou até mesmo TIFF sem mudar o código.

### E se o motor OCR retornar baixa confiança?

Você pode inspecionar `ocrResult.Lines` e cada `OcrWord` para obter um `ConfidenceScore`. Se a pontuação estiver abaixo de um limiar (ex.: 0.6), considere:

- Pré‑processar a imagem (aumentar contraste, nitidez, corrigir inclinação).
- Usar uma imagem de origem com resolução maior.
- Trocar para uma biblioteca dedicada como **Tesseract** para suporte multilíngue.

### Como lidar com múltiplos idiomas na mesma imagem?

Crie instâncias separadas de `OcrEngine` para cada idioma e execute‑as sequencialmente, ou use uma biblioteca que suporte detecção de idiomas mistos. Para o motor interno, você pode passar um objeto `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Posso executar isso no Linux/macOS?

A API `Windows.Media.Ocr` é exclusiva do Windows. Em plataformas não‑Windows, substitua a seção OCR por **Tesseract** (via `Tesseract.Net.SDK`). O código de carregamento e pré‑processamento permanece idêntico, de modo que o restante deste **c# OCR tutorial** ainda se aplica.

## Dicas de Especialista para Melhor Precisão

- **Redimensione** imagens grandes para no máximo 2000 px no lado maior – motores OCR funcionam mais rápido em tamanhos moderados.
- **Remova ruído** usando um desfoque gaussiano simples se a foto estiver granulada.
- **Corrija inclinação** do bitmap se o texto não estiver perfeitamente horizontal; `SoftwareBitmap` pode ser rotacionado antes de ser passado ao `OcrEngine`.
- **Cache** a instância `OcrEngine` se estiver processando muitas imagens em lote; criá‑la repetidamente gera sobrecarga.

## Tópicos Relacionados para Explorar

- **Converter imagem em texto** usando **Tesseract** para projetos multiplataforma.
- **Extrair texto de PDF** renderizando cada página como imagem primeiro.
- **OCR em lote**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}