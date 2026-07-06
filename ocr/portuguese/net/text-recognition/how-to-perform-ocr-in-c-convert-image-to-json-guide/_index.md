---
category: general
date: 2026-02-17
description: Como realizar OCR em C# e converter imagem para JSON rapidamente. Siga
  este tutorial de OCR em C# para extrair texto de imagens e salvar o layout como
  JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: pt
og_description: Como fazer OCR em C#? Este guia mostra como converter uma imagem em
  JSON, extrair texto de uma imagem em C# e carregar um arquivo de imagem para OCR.
og_title: Como executar OCR em C# – Converter imagem para JSON
tags:
- OCR
- C#
- Aspose
title: Como Realizar OCR em C# – Guia de Conversão de Imagem para JSON
url: /pt/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em C# – Guia de Conversão de Imagem para JSON

Já se perguntou **como realizar OCR** em um recibo, nota fiscal ou qualquer documento escaneado usando C#? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam extrair texto *e* preservar o layout sem gastar horas escrevendo analisadores personalizados.  

Neste tutorial vamos percorrer um **c# ocr tutorial** completo que mostra exatamente como realizar OCR, **converter imagem para json**, e salvar o resultado para análise posterior. Ao final, você terá um aplicativo console pronto‑para‑executar que carrega um arquivo de imagem em C#, extrai o texto e grava um arquivo JSON detalhado contendo coordenadas, pontuações de confiança e o texto bruto.

## Pré‑requisitos — O Que Você Precisa

- .NET 6 SDK ou superior (o código funciona também em .NET Core)  
- Visual Studio 2022 ou qualquer editor de sua preferência  
- Uma licença Aspose OCR (você pode começar com uma avaliação gratuita)  
- Uma imagem de exemplo, por exemplo, `receipt.png`, colocada em uma pasta que você possa referenciar  

É só isso—nenhum pacote NuGet extra além do `Aspose.OCR`. Se você tem esses itens, está pronto para começar.

## Como Realizar OCR e Obter Saída JSON

O núcleo de **como realizar OCR** com Aspose é simples: crie um `OcrEngine`, forneça a ele um fluxo de imagem, chame `Recognize` e, em seguida, serialize o `OcrResult` para JSON. Vamos detalhar passo a passo.

### Etapa 1: Instalar o Pacote NuGet Aspose OCR

Abra seu terminal na pasta do projeto e execute:

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Use a flag `--version` para travar na versão estável mais recente (por exemplo, `23.9.0`). Isso mantém sua compilação reproduzível.

### Etapa 2: Criar o Esqueleto do Projeto Console

Se ainda não tem um projeto, crie um:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Agora você tem um arquivo `Program.cs` pronto para o código que **carregará o arquivo de imagem c#** e iniciará o processo de OCR.

### Etapa 3: Escrever o Código Completo de OCR‑para‑JSON

Abaixo está o programa completo, pronto‑para‑executar. Copie‑e‑cole em `Program.cs`. Cada linha está comentada para que você veja *por que* cada parte é importante.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### O Que o Código Faz

| Etapa | Por que é importante |
|------|----------------------|
| **Initialize OcrEngine** | Configura o idioma padrão (Inglês) e prepara os modelos internos. |
| **Load image file** | Usar `ImageStream.FromFile` garante que a imagem seja lida no formato esperado pelo Aspose. |
| **Recognize** | O trabalho pesado—análise de pixels, segmentação de caracteres e consulta ao dicionário. |
| **ToJson** | Produz uma saída estruturada que inclui caixas delimitadoras, confiança e texto bruto. |
| **WriteAllText** | Persiste o JSON para que você possa compartilhá‑lo com outros serviços. |
| **Console.WriteLine** | Fornece feedback imediato—útil ao executar a partir de um terminal. |

> **Atenção:** Se sua imagem for grande, considere redimensioná‑la primeiro para melhorar velocidade e uso de memória. Aspose fornece métodos `Resize` que podem ser chamados em `ImageStream`.

### Etapa 4: Executar a Aplicação e Verificar a Saída

No terminal:

```bash
dotnet run
```

Você deverá ver:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Abra `receipt.json` em qualquer editor; você encontrará algo como:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Esse JSON captura **extract text image c#** mais metadados de layout, perfeito para processamento posterior.

## Converter Imagem para JSON – Além do Básico

Agora que você sabe **como realizar OCR**, vamos explorar algumas variações que podem ser necessárias em projetos reais.

### Manipulando Múltiplas Páginas

Se sua fonte for um PDF ou TIFF de várias páginas, basta percorrer cada página:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Personalizando Idioma e Precisão

Aspose suporta mais de 40 idiomas. Para mudar para espanhol:

```csharp
ocrEngine.Language = Language.Spanish;
```

Você também pode ajustar `ocrEngine.Settings` para habilitar **auto‑rotate**, **remoção de ruído** ou **correção baseada em dicionário**—tudo isso melhora a qualidade do JSON obtido.

### Salvando JSON em Formato Legível

Se preferir JSON indentado para melhor leitura:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Carregar Arquivo de Imagem C# – Armadilhas Comuns e Dicas

Ao **carregar o arquivo de imagem c#**, você pode encontrar:

- **Arquivo não encontrado** – Garanta que o caminho seja absoluto ou use `Path.Combine` com `Environment.CurrentDirectory`.  
- **Formato não suportado** – Aspose lida com PNG, JPEG, BMP, TIFF e PDF. Para formatos RAW, converta‑os primeiro.  
- **Pressão de memória por arquivo grande** – Use `ImageStream.FromFile(path, maxSizeInKB)` para reduzir a escala ao carregar.

Resolver esses problemas cedo evita exceções enigmáticas mais tarde no pipeline de OCR.

## Extrair Texto da Imagem C# – Verificando Resultados

Depois de ter o JSON, talvez você queira apenas o texto puro:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Este trecho demonstra **extract text image c#** sem os detalhes de layout—útil para buscas rápidas ou registro de logs.

---

![Diagrama mostrando o fluxo de trabalho de OCR – como realizar OCR, converter imagem para JSON e extrair texto da imagem c#](/images/ocr-workflow.png "como realizar OCR workflow")

*Texto alternativo da imagem: "diagrama do fluxo de trabalho de OCR ilustrando converter imagem para JSON e extrair texto da imagem c#"*  

*(A imagem é um placeholder; substitua por um diagrama real ao publicar.)*

---

## Conclusão

Cobremos **como realizar OCR** em C# do início ao fim, mostramos como **converter imagem para JSON**, e explicamos as nuances de **carregar arquivo de imagem c#** e **extrair texto da imagem c#**. O exemplo de código completo está pronto para ser inserido em qualquer projeto .NET, e a saída JSON fornece tanto o texto bruto quanto dados precisos de layout para análises posteriores.

O que vem a seguir? Experimente alimentar o JSON em um banco de dados, visualizar caixas delimitadoras em uma UI, ou encadear múltiplas execuções de OCR para processamento em lote. Você também pode experimentar outros recursos da Aspose, como reconhecimento de escrita manual ou detecção de códigos de barras—ambos se encaixam naturalmente no mesmo pipeline.

Se encontrar algum obstáculo, revise as dicas de solução de problemas na seção “Carregar Arquivo de Imagem C#”, ou explore a documentação extensa da Aspose para configurações avançadas. Boa codificação e aproveite a transformação de imagens em dados estruturados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}