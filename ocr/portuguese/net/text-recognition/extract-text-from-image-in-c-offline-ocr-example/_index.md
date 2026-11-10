---
category: general
date: 2026-02-09
description: Extrair texto de imagem usando OCR offline em C#. Um exemplo completo
  de OCR em C# mostra como carregar a imagem para OCR, reconhecer texto cirílico e
  extrair texto de passaporte.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: pt
og_description: Extraia texto de imagem com OCR offline em C#. Aprenda um exemplo
  passo a passo de OCR em C# que carrega uma imagem para OCR, reconhece texto cirílico
  e extrai texto de um passaporte.
og_title: Extrair Texto de Imagem em C# – Guia de OCR Offline
tags:
- OCR
- C#
- Aspose
title: Extrair Texto de Imagem em C# – Exemplo de OCR Offline
url: /pt/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em C# – Exemplo de OCR Offline

Já precisou **extrair texto de imagem** mas ficou preso em APIs dependentes de rede? Você não está sozinho. Muitos desenvolvedores esbarram na parede quando o serviço de OCR tenta baixar pacotes de idioma em tempo de execução, especialmente em ambientes restritos.

Neste guia vamos percorrer um **c# ocr example** que funciona totalmente offline, carrega uma imagem para OCR e reconhece texto cirílico de um passaporte. Ao final você terá um programa pronto‑para‑executar que imprime o conteúdo em texto puro de qualquer imagem suportada diretamente no console.

## O que você vai aprender

- Como configurar o Aspose.OCR para processamento offline.  
- O código exato para **carregar imagem para OCR** a partir do disco.  
- Como configurar o motor para **reconhecer texto cirílico**.  
- Um **c# ocr example** completo, pronto para copiar‑colar, que extrai texto de uma foto no estilo de passaporte.  

Nenhuma experiência prévia com Aspose é necessária; apenas o SDK .NET 6 (ou superior) e o Visual Studio 2022 (ou VS Code) são suficientes.

---

![Extrair texto de imagem usando Aspose OCR em foto de passaporte](/images/ocr-passport.jpg "extrair texto de imagem")

## Etapa 1: Configurar o Projeto para Extrair Texto de Imagem

Antes de escrever qualquer código, certifique‑se de que o pacote NuGet Aspose.OCR foi adicionado ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Use a flag `--version` para travar na versão estável mais recente (por exemplo, `13.9.0`). Isso garante compatibilidade com .NET 6.

Criar um novo aplicativo de console é tão simples quanto:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Agora você tem uma base limpa onde iremos **extrair texto de imagem** sem nunca tocar na internet.

## Etapa 2: Carregar Imagem para OCR – Lendo a Foto do Passaporte

A primeira coisa que o motor de OCR precisa é um bitmap ou stream que represente a foto. No nosso cenário vamos **carregar imagem para OCR** a partir de um arquivo local chamado `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Por que isso importa:** Fornecer um stream em vez de um `Bitmap` bruto permite que o Aspose faça a detecção de formato internamente, reduzindo código boilerplate e possíveis bugs.

## Etapa 3: Configurar o Modo Offline e Escolher o Idioma Cirílico

O Aspose.OCR pode baixar modelos de idioma sob demanda, mas isso anula o objetivo de uma solução offline. Desative chamadas de rede e indique explicitamente ao motor qual idioma usar.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Caso de borda:** Se mais tarde precisar reconhecer caracteres latinos no mesmo documento, basta adicionar `OcrLanguage.English` ao array. O motor lidará automaticamente com detecção multilíngue.

## Etapa 4: Executar o Motor de OCR e Reconhecer Texto Cirílico

Agora realmente **reconhecemos texto de imagens no estilo passaporte**. O método `Recognize` devolve um objeto de resultado rico contendo o texto puro, pontuações de confiança e caixas delimitadoras.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Saída Esperada no Console

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Se o resultado parecer corrompido, verifique se a imagem fonte está nítida e se o pacote de idioma `OfflineMode` para Cirílico está presente na pasta de instalação do Aspose (geralmente `\Aspose.OCR\resources\languages`).

## Exemplo Completo de OCR em C# – Código Fonte Integral

Abaixo está o **c# ocr example** na íntegra. Copie‑cole para `Program.cs` e execute `dotnet run`. Tudo que você precisa para **extrair texto de imagem** está aqui.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Executando o Exemplo

```bash
dotnet run
```

Você deverá ver o console imprimir os detalhes do passaporte em cirílico. Esse é o momento em que você sabe que seu pipeline de **extrair texto de imagem** funciona.

## Armadilhas Comuns & Como Corrigi‑las

| Sintoma | Causa Provável | Solução |
|---------|----------------|---------|
| `PlainText` vazio | Modelo de idioma errado ou imagem muito escura | Garanta que o pacote de idioma `OfflineMode` inclua `Cyrillic` e aumente o contraste da imagem |
| `System.DllNotFoundException` | Binaries nativos do Aspose OCR ausentes | Reinstale o pacote NuGet ou copie o `Aspose.OCR.Native.dll` para a pasta de saída |
| Desempenho lento em imagens grandes | O motor processa resolução completa | Reduza a imagem para ≤ 1500 px de largura antes de enviá‑la ao `ImageStream` |
| Caracteres estranhos | Imagem rotacionada incorretamente | Use `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` antes de criar o stream |

## Próximos Passos – Expandindo o Workflow de OCR Offline

- **Carregar imagem para OCR** a partir de um `MemoryStream` ao lidar com arquivos enviados em ASP.NET Core.  
- Alternar para **reconhecer texto de passaporte** em modo batch percorrendo uma pasta de digitalizações de passaporte.  
- Combinar o resultado com **expressões regulares** para extrair campos como número do passaporte ou data de nascimento.  
- Experimentar `ocrEngine.Configuration.UseParallelProcessing = true` para ganhos de velocidade em múltiplos núcleos.

---

### Conclusão

Acabamos de mostrar como **extrair texto de imagem** usando um pipeline de OCR C# totalmente offline. O curto e autocontido **c# ocr example** carrega uma imagem, configura o motor para **reconhecer texto cirílico** e imprime os dados do passaporte extraídos — tudo sem uma única requisição de rede.

Sinta‑se à vontade para ajustar o código, adicionar mais idiomas ou conectar a saída a um banco de dados. O céu é o limite depois que você domina o básico de carregar uma imagem para OCR e reconhecer texto de uma foto no estilo de passaporte.

Tem perguntas ou quer compartilhar suas próprias adaptações? Deixe um comentário abaixo e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}