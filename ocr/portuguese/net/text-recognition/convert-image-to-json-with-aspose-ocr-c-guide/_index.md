---
category: general
date: 2026-01-15
description: Converter imagem para JSON usando Aspose OCR em C#. Aprenda como extrair
  texto da imagem, obter caixas delimitadoras em JSON e reconhecer imagem de recibo.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: pt
og_description: Converter imagem para JSON usando Aspose OCR em C#. Guia passo a passo
  para extrair texto da imagem, reconhecer imagem de recibo e obter caixas delimitadoras
  em JSON.
og_title: Converter imagem para JSON com o guia Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Converter imagem para JSON com o guia Aspose OCR C#
url: /pt/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter Imagem para JSON com Guia Aspose OCR C# 

Já precisou **converter imagem para JSON** mas não tinha certeza de qual biblioteca poderia fornecer tanto o texto bruto quanto as coordenadas exatas das palavras? Você não está sozinho. Muitos desenvolvedores encontram esse obstáculo ao tentar extrair texto de arquivos de imagem—especialmente recibos—enquanto também precisam de um payload JSON legível por máquina para processamento posterior.

Neste tutorial vamos percorrer um **exemplo completo de Aspose OCR C#** que mostra como extrair texto de uma imagem, reconhecer imagem de recibo e gerar **caixas delimitadoras JSON** para cada palavra. Ao final, você terá um aplicativo console pronto‑para‑executar que imprime uma string JSON formatada que pode ser enviada a qualquer API, banco de dados ou pipeline de análise.

> **O que você levará consigo**  
> • Um projeto C# totalmente funcional que **converte imagem para JSON**  
> • Entendimento de por que habilitamos `IncludeBoundingBoxes` (é a chave para `json bounding boxes`)  
> • Dicas para lidar com diferentes formatos de imagem e idiomas  

Vamos começar.

---

## O que você precisará

Antes de mergulharmos no código, certifique‑se de que tem os pré‑requisitos a seguir instalados:

- **.NET 6.0 SDK** (ou qualquer versão posterior) – o código tem como alvo .NET 6, mas funciona também no .NET Framework 4.7+ .  
- **Aspose.OCR for .NET** pacote NuGet – você pode adicioná‑lo via `dotnet add package Aspose.OCR`.  
- Uma imagem de recibo de exemplo (`receipt.jpg`) colocada em uma pasta que você possa referenciar a partir do seu projeto.  
- Visual Studio 2022, VS Code ou qualquer IDE de sua preferência.

Nenhum outro serviço externo é necessário; tudo roda localmente.

---

## Converter Imagem para JSON – Visão geral

A ideia central é simples: carregar uma imagem, dizer ao Aspose OCR para reconhecer o inglês (ou qualquer idioma suportado), solicitar a inclusão de caixas delimitadoras e, por fim, obter o resultado em formato **JSON**. A biblioteca faz todo o trabalho pesado — OCR, análise de layout e serialização JSON.

Aqui está um diagrama de alto nível do fluxo (imagine uma imagem pequena):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Esse pequeno diagrama captura todo o pipeline que implementaremos.

---

## Etapa 1: Configurar o Projeto e Instalar o Aspose OCR

Primeiro, crie um novo projeto console e adicione o pacote Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Dica profissional:** Se estiver usando o Visual Studio, clique com o botão direito no projeto → *Manage NuGet Packages* → procure por **Aspose.OCR** e instale a versão estável mais recente (atualmente 23.12).

---

## Etapa 2: Carregar a Imagem que Você Deseja Reconhecer

Usaremos o método `OcrImage.FromFile` para ler a imagem do recibo. Certifique‑se de que o caminho aponta para um arquivo real; caso contrário, você receberá uma `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Se sua imagem estiver ao lado do `.csproj`, você pode simplesmente usar `"receipt.jpg"`.

---

## Etapa 3: Configurar as Opções de OCR para Caixas Delimitadoras JSON

A mágica acontece quando habilitamos `OutputFormat = OutputFormat.Json` **e** `IncludeBoundingBoxes = true`. O primeiro indica ao Aspose que serializa o resultado como JSON, enquanto o segundo adiciona `x`, `y`, `width` e `height` para cada palavra — exatamente o que você precisa para `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Você também pode ajustar `ocrOptions.Dpi` ou `ocrOptions.Language` se precisar de resolução maior ou de um idioma diferente.

---

## Etapa 4: Executar o Reconhecimento – Extrair Texto da Imagem

Agora chamamos `Recognize`. O método retorna um objeto `OcrResult` que contém a string JSON, o texto bruto e mais informações.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Se precisar lidar com outros idiomas, substitua `Language.English` por `Language.Spanish`, `Language.French`, etc. O Aspose oferece suporte a mais de 30 idiomas nativamente.

---

## Etapa 5: Exibir o Resultado – Seu Payload JSON

Por fim, imprimimos o JSON no console. Em um aplicativo real, você provavelmente gravaria isso em um arquivo ou enviaria para um serviço.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Executar o programa deve gerar um documento JSON semelhante ao trecho abaixo.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Observe como cada palavra agora carrega sua **caixa delimitadora JSON** — perfeito para alimentar uma sobreposição de UI ou um analisador downstream.

---

## Exemplo Completo Funcionando

Abaixo está o programa completo, pronto para copiar e colar. Sem partes ocultas, sem chamadas externas — apenas C# puro.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Fique atento a:**  
> • **Erros de caminho de arquivo** – verifique duas vezes a localização da imagem.  
> • **Pacote NuGet ausente** – assegure‑se de que `Aspose.OCR` está referenciado.  
> • **Formatos de imagem não suportados** – use JPEG, PNG, BMP ou TIFF para obter os melhores resultados.

---

## Perguntas Frequentes & Casos de Borda

### Posso converter uma **página PDF** para JSON em vez de um JPEG?

Sim. Converta a página PDF para uma imagem primeiro (por exemplo, usando `Aspose.PDF`), depois alimente essa imagem ao mesmo pipeline OCR. A saída JSON será idêntica porque a etapa OCR trabalha apenas com dados rasterizados.

### E se o recibo estiver borrado?

Aumente o DPI em `ocrOptions`. Por exemplo:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Um DPI maior pode aumentar o uso de memória, então equilibre qualidade e desempenho.

### Preciso de **múltiplos idiomas** no mesmo recibo (ex.: Inglês + Espanhol).

Você pode passar um array de idiomas:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

O Aspose tentará reconhecer cada idioma na ordem especificada.

### Como escrevo o JSON em um arquivo?

Basta substituir a linha `Console.WriteLine` por:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Agora você tem um arquivo persistente que pode ser enviado a outros serviços.

---

## Resumo Visual

![exemplo de conversão de imagem para json](convert-image-to-json.png "exemplo de conversão de imagem para json")

*A captura de tela mostra a saída do console com o payload JSON após a execução da demonstração.*

---

## Conclusão

Acabamos de mostrar como **converter imagem para JSON** usando Aspose OCR em C#. Ao configurar `OutputFormat` e `IncludeBoundingBoxes`, você pode **extrair texto de imagem**, **reconhecer imagem de recibo** e obter caixas delimitadoras **JSON** precisas para cada palavra. O código completo e executável está no snippet acima, pronto para ser inserido em qualquer projeto .NET agora mesmo.

O que vem a seguir? Experimente alimentar o JSON em um visualizador front‑end que destaque cada palavra, ou envie os dados para um modelo de machine‑learning que classifique itens de linha em recibos. Você também pode testar outros idiomas, configurações de DPI mais altas ou processar múltiplas imagens em lote dentro de um loop.

Se encontrar algum obstáculo, lembre‑se das dicas sobre caminhos de arquivo, DPI e arrays de idiomas. Sinta‑se à vontade para deixar um comentário ou abrir uma issue no repositório GitHub que criar para esta demonstração. Feliz codificação e aproveite para transformar imagens em JSON estruturado!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}