---
category: general
date: 2026-01-10
description: Como executar OCR rapidamente e extrair texto em árabe de uma imagem.
  Aprenda a converter imagem em texto, ler texto de PNG e veja como extrair texto
  com Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: pt
og_description: Como executar OCR em C# e extrair texto em árabe de uma imagem PNG.
  Este guia mostra como converter a imagem em texto e ler o texto de PNG passo a passo.
og_title: Como Executar OCR em C# – Extrair Texto Árabe de PNG
tags:
- OCR
- C#
- Aspose
title: Como Executar OCR em C# – Extrair Texto Árabe de PNG
url: /pt/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em C# – Extrair Texto Árabe de PNG

Já se perguntou **como executar OCR** em uma imagem que contém caracteres árabes? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando precisam **extrair texto árabe** de um PNG, mas não sabem qual biblioteca lidará com scripts da direita para a esquerda sem dor de cabeça.  

Neste tutorial, percorreremos tudo o que você precisa saber para **converter imagem em texto**, **ler texto de PNG**, e finalmente **como extrair texto** usando Aspose.OCR em um aplicativo console C# limpo. Ao final, você terá um programa pronto‑para‑executar que imprime a string árabe diretamente no seu terminal.

## O que Você Vai Aprender

- Instalar e referenciar o pacote NuGet Aspose.OCR.  
- Configurar o motor OCR para suporte ao idioma árabe.  
- Carregar uma imagem PNG e executar o processo de reconhecimento.  
- Recuperar e exibir o texto extraído.  
- Ajustar configurações para melhor precisão e lidar com armadilhas comuns.

Nenhuma experiência prévia com OCR é necessária, apenas um entendimento básico de C# e um ambiente de desenvolvimento .NET (Visual Studio, Rider ou a CLI `dotnet` serve).

---

## Como Executar OCR – Configurando Aspose OCR

### Etapa 1: Adicionar o Pacote NuGet Aspose.OCR

A primeira coisa que precisamos é a própria biblioteca OCR. Aspose.OCR é um produto comercial, mas oferece um teste gratuito que funciona perfeitamente para fins de aprendizado.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternativamente, abra o **NuGet Package Manager** no Visual Studio, procure por **Aspose.OCR** e clique em **Install**.

> **Dica profissional:** Se você planeja usar a biblioteca em um pipeline de CI, adicione a flag `-v` para travar a versão, por exemplo, `dotnet add package Aspose.OCR -v 23.10`.

### Etapa 2: Criar um Novo Projeto Console (se você ainda não tem um)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Agora você tem um arquivo `Program.cs` novo pronto para o nosso código.

---

## Extrair Texto Árabe – Escrevendo o Código OCR

Abaixo está o programa completo, pronto‑para‑executar. Salve-o como `Program.cs` (ou substitua o arquivo gerado automaticamente).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Por Que Cada Linha Importa

- **`OcrEngine`**: A classe central que coordena o carregamento de imagens, a seleção de idioma e o reconhecimento.  
- **`Language = OcrLanguage.Arabic`**: O árabe usa um script da direita para a esquerda e glifos únicos; definir o idioma informa ao motor para aplicar os modelos de caracteres corretos.  
- **`ImageStream.FromFile`**: Lida com PNG, JPEG, BMP e muitos outros formatos. Se precisar ler de um `MemoryStream` (por exemplo, um arquivo enviado), substitua esta chamada adequadamente.  
- **`Recognize()`**: Executa o trabalho pesado — análise de pixels, segmentação e classificação de caracteres.  
- **`ocrEngine.Text`**: A string Unicode final, pronta para processamento adicional, armazenamento ou exibição.

### Saída Esperada

Se `arabic_sample.png` contiver a frase “مرحبا بالعالم” (Hello World), o console imprimirá:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Se a saída parecer corrompida, verifique se a imagem está nítida, se o idioma está definido como Árabe e se a versão do motor OCR corresponde à documentação.

---

## Converter Imagem em Texto – Ajustando a Precisão

Embora as configurações padrão funcionem para a maioria das digitalizações limpas, imagens do mundo real frequentemente precisam de um pouco de atenção extra.

| Configuração | O que faz | Quando usar |
|--------------|-----------|-------------|
| `ocrEngine.Config.Preprocess = true` | Habilita binarização automática e remoção de ruído. | Documentos escaneados com sombras. |
| `ocrEngine.Config.Deskew = true` | Gira a imagem para corrigir inclinação leve. | Fotos tiradas em ângulo. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Trata a imagem inteira como um bloco único de texto. | Legendas simples ou rótulos de linha única. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Limita o reconhecimento apenas a caracteres árabes. | Reduz falsos positivos em páginas com múltiplos idiomas. |

Você pode adicionar estas linhas logo após criar o motor:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Ler Texto de PNG – Manipulando Diferentes Fontes de Imagem

Às vezes o PNG está armazenado em um banco de dados ou vem de uma requisição web. Aqui está uma variante rápida que lê de um `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

O resto do fluxo permanece idêntico, o que significa que **como extrair texto** permanece consistente independentemente da fonte.

---

## Como Extrair Texto – Opções Avançadas & Casos Limite

### 1. PDFs ou TIFFs de Múltiplas Páginas

Se você precisar fazer OCR em um documento de várias páginas, faça um loop sobre cada página:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Nota:** Você precisará do pacote `Aspose.PDF` para este trecho.

### 2. Detecção Automática de Idioma

Aspose.OCR também oferece detecção automática, mas é mais lenta. Se você não tem certeza se a imagem contém árabe ou outro script, habilite-a:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. Dicas de Performance

- **Reutilize o objeto `OcrEngine`** para múltiplas imagens; criar uma nova instância a cada vez adiciona sobrecarga.  
- **Execute em paralelo** somente se você tiver instâncias de motor separadas por thread — compartilhar uma única instância causa condições de corrida.

---

## Conclusão

Cobremos **como executar OCR** em C# do início ao fim, mostrando como **extrair texto árabe**, **converter imagem em texto**, **ler texto de PNG**, e responder **como extrair texto** em uma variedade de cenários. O código de exemplo está completo, autocontido e pronto para você colar em qualquer projeto console .NET.

Próximos passos? Experimente substituir `OcrLanguage.Arabic` por coreano ou cirílico sérvio para ver o poder multilíngue da biblioteca. Experimente as flags de pré‑processamento para melhorar a precisão em digitalizações ruidosas, ou integre a rotina OCR em uma API web para que os usuários possam enviar imagens e obter resultados de texto instantâneos.

Feliz codificação, e que seus resultados de OCR estejam sempre cristalinos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}