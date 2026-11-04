---
category: general
date: 2026-03-05
description: Como usar OCR em C# para extrair texto de uma imagem. Aprenda a converter
  imagem em texto, ler caracteres coreanos e carregar a imagem para OCR rapidamente.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: pt
og_description: Como usar OCR em C# e extrair instantaneamente texto de uma imagem.
  Este guia mostra como converter imagem em texto, ler caracteres coreanos e carregar
  a imagem para OCR.
og_title: Como usar OCR em C# – Extrair texto de uma imagem
tags:
- OCR
- C#
- Aspose
title: Como usar OCR em C# – Extrair texto de imagem
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR em C# – Extrair Texto de Imagem

Já se perguntou **como usar OCR** quando você tem uma captura de tela cheia de texto coreano e precisa da string simples de volta? Você não é o único coçando a cabeça com isso. Neste tutorial, vamos percorrer um exemplo completo, pronto‑para‑executar que **extrai texto de imagem**, **converte imagem em texto**, e ainda mostra como **ler caracteres coreanos** com Aspose.OCR.

Também abordaremos a etapa frequentemente negligenciada de **carregar imagem para OCR** para que você não encontre uma surpresa de “arquivo não encontrado” mais tarde. Ao final, você terá um programa autônomo que pode inserir em qualquer projeto .NET.

## O que você precisará

- .NET 6+ (ou .NET Framework 4.7.2 e posterior) – o código funciona em ambos.
- Aspose.OCR para .NET – você pode obter uma avaliação gratuita no site da Aspose.
- Uma imagem de exemplo (`korean_doc.png`) que contém texto coreano.
- Seu IDE favorito (Visual Studio, Rider, VS Code – o que preferir).

Nenhuma outra biblioteca de terceiros é necessária.

## Etapa 1: Configurar o Projeto e Adicionar Aspose.OCR

Primeiro, crie um novo aplicativo de console:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Em seguida, adicione o pacote NuGet Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se você tem um arquivo de licença, coloque‑o na raiz do projeto; caso contrário, a avaliação gratuita funcionará, mas adicionará uma marca d'água à saída.

## Etapa 2: Como usar OCR – Inicializar o Engine

Agora vamos escrever o código C#. A primeira coisa a fazer ao **como usar OCR** é instanciar o `OcrEngine`. Este objeto é o coração da biblioteca; ele contém todas as configurações que você precisará mais tarde.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Por que isso importa:** Sem uma instância adequada do engine você não pode definir o idioma, carregar imagens ou recuperar resultados. O engine também gerencia recursos internos, portanto criá‑lo uma vez e reutilizá‑lo é mais eficiente do que construir novos objetos repetidamente.

## Etapa 3: Escolher o Idioma – Ler Caracteres Coreanos

A próxima linha informa ao engine qual idioma procurar. Como nosso objetivo é **ler caracteres coreanos**, definimos `OcrLanguage.Korean`. Você pode trocar isso por Árabe, Tailandês, Gujarati, etc., dependendo do seu caso de uso.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Por que é importante:** A seleção de idioma melhora drasticamente a precisão. O engine OCR usa dicionários e modelos de caracteres específicos do idioma; alimentá‑lo com o idioma errado pode gerar saída confusa.

## Etapa 4: Carregar Imagem para OCR – Converter Imagem em Texto

Antes que o engine possa fazer qualquer trabalho, você precisa **carregar imagem para OCR**. O método `ImageStream.FromFile` lê o arquivo em um formato que o engine entende.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Se a imagem estiver em uma pasta diferente, basta ajustar o caminho. Lembre‑se de definir a *Build Action* do arquivo como “Copy if newer” para que o executável possa encontrá‑la em tempo de execução.

> **Armadilha comum:** Fornecer um caminho com barras invertidas (`\`) em um literal de string sem escapá‑las causará um erro de compilação. Use duas barras invertidas (`\\`) ou uma string verbatim (`@"C:\path\file.png"`).

## Etapa 5: Executar OCR – Extrair Texto da Imagem

Agora a parte pesada acontece. Chamar `Recognize()` executa o algoritmo OCR, e a propriedade `Text` fornece a string bruta.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Neste ponto você **extraiu texto de imagem** e efetivamente **converteu imagem em texto**. O resultado pode conter caracteres de nova linha se o layout original tinha quebras de linha.

## Etapa 6: Mostrar o Resultado – Verificar a Saída

Finalmente, vamos imprimir o resultado no console para que você possa verificar se funcionou.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Execute o programa:

```bash
dotnet run
```

### Saída Esperada

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Se você vir caracteres coreanos semelhantes à imagem, parabéns — você dominou **como usar OCR** com Aspose.OCR!

![diagrama de exemplo de como usar OCR](image.png)

*Texto alternativo da imagem: diagrama de exemplo de como usar OCR mostrando o fluxo de carregamento de uma imagem até a impressão do texto reconhecido.*

## Casos de Borda & Variações

### 1. Manipulando Múltiplas Páginas

Se você precisar **extrair texto de imagem** de arquivos que contêm várias páginas (por exemplo, um TIFF multipágina), faça um loop sobre cada página e chame `Recognize()` para cada instância de `ImageStream`.

### 2. Lidando com Digitalizações de Baixa Qualidade

Imagens de baixa resolução podem prejudicar a precisão. Antes de chamar `Recognize()`, você pode melhorar a imagem com as ferramentas de pré‑processamento da Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Alternando Idiomas em Tempo Real

Suponha que você tenha um documento com múltiplos idiomas. Você pode mudar `ocrEngine.Language` entre reconhecimentos:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Salvando o Resultado em um Arquivo

Se você preferir **converter imagem em texto** e armazená‑lo, basta escrever a string em um arquivo `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Perguntas Frequentes

- **Preciso de uma licença para executar este código?**  
  Não. A avaliação gratuita funciona bem para experimentação, mas adiciona uma marca d'água à saída. Uma licença comprada remove a marca d'água e desbloqueia o desempenho total.

- **Posso usar isso no Linux?**  
  Absolutamente. Aspose.OCR é multiplataforma; basta garantir que você tenha as dependências nativas necessárias (libgdiplus para .NET Core no Linux).

- **E se minha imagem estiver em um stream ao invés de um arquivo?**  
  Use `ImageStream.FromStream(yourStream)` – a API aceita qualquer `System.IO.Stream`.

## Conclusão

Nós guiamos você passo a passo através de **como usar OCR** em C# para **extrair texto de imagem**, **converter imagem em texto**, e **ler caracteres coreanos** enquanto carrega corretamente **imagem para OCR**. O exemplo completo e executável acima deve funcionar imediatamente, e as dicas extras fornecem um roteiro para cenários mais avançados.

Pronto para o próximo desafio? Experimente trocar por um idioma diferente, processar PDFs página por página, ou integrar a chamada OCR em uma API web para que os usuários possam enviar fotos e obter resultados de texto instantâneos. As possibilidades são infinitas, e agora você tem uma base sólida para construir.

Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}