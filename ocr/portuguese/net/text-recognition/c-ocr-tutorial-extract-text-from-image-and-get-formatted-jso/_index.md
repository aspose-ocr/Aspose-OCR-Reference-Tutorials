---
category: general
date: 2026-01-13
description: tutorial de OCR em C# que mostra como extrair texto de uma imagem, carregar
  a imagem para OCR e formatar a saída JSON usando Aspose OCR. Aprenda a serializar
  objetos para JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: pt
og_description: Tutorial de OCR em C# que orienta você a extrair texto de imagem,
  carregar a imagem para OCR e formatar a saída JSON com Aspose OCR.
og_title: tutorial de OCR em C# – Extrair Texto e Formatar JSON
tags:
- OCR
- C#
- JSON
title: Tutorial de OCR em C# – Extrair Texto de Imagem e Obter JSON Formatado
url: /pt/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Extrair Texto de Imagem e Formatar Saída JSON

Já se perguntou como **extrair texto de imagem** em um projeto C# sem lidar com processamento de pixels de baixo nível? Esse é o problema que este *c# ocr tutorial* resolve. Em apenas alguns minutos você verá como **carregar imagem para ocr**, executar Aspose OCR e **formatar saída json** para que possa alimentar os dados diretamente na sua API ou banco de dados.

Vamos percorrer cada linha de código, explicar por que cada parte importa e até mostrar o JSON exato que você deve esperar. Ao final, você terá um aplicativo console pronto‑para‑executar que transforma um PNG de nota fiscal em JSON limpo e indentado. Sem enrolação, apenas uma solução prática que você pode inserir em qualquer projeto .NET 6+.

## O que este tutorial c# ocr cobre

- Instalar o pacote NuGet Aspose.OCR  
- Carregar um arquivo de imagem para processamento OCR  
- Reconhecer texto em inglês (ou qualquer idioma suportado)  
- **Serializar o resultado OCR para JSON** com impressão formatada  
- Exibir o JSON no console e salvá‑lo, se desejar  

Você só precisa de um entendimento básico de C# e de um SDK .NET recente. Nada mais. Se você está curioso sobre como **extrair texto de imagem** para faturas, recibos ou formulários escaneados, continue lendo.

---

## Etapa 1: Configurar o Ambiente do tutorial c# ocr

Antes de escrever qualquer código, certifique‑se de que tem as ferramentas corretas:

1. **.NET 6 SDK ou posterior** – você pode baixá‑lo no site da Microsoft.  
2. **Visual Studio 2022** (a edição Community funciona bem) ou qualquer editor de sua preferência.  
3. **Pacote NuGet Aspose.OCR** – execute `dotnet add package Aspose.OCR` na pasta do seu projeto.

> **Dica profissional:** Se você estiver usando um pipeline CI, adicione a referência do pacote ao seu `.csproj` para que a compilação o restaure automaticamente.

## Etapa 2: Carregar Imagem para OCR

O primeiro passo real em nosso tutorial é obter a imagem que você deseja processar. Aspose OCR funciona com formatos comuns como PNG, JPEG e TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Por que isso importa:** Carregar a imagem como um `OcrImage` fornece ao motor acesso aos dados de bitmap e a informações de DPI, o que melhora a precisão do reconhecimento. Pular esta etapa ou fornecer um arquivo corrompido causará uma exceção em tempo de execução.

## Etapa 3: Extrair Texto da Imagem

Agora realmente executamos o motor OCR. O método `Recognize` retorna um rico objeto `OcrResult` contendo o texto bruto, pontuações de confiança e detalhes de layout.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Caso de borda:** Se precisar processar um documento multilíngue, chame `Recognize` duas vezes com valores diferentes de `OcrLanguage` e concatene os resultados. O motor é thread‑safe, então você pode paralelizar lotes grandes.

## Etapa 4: Serializar Objeto para JSON – Formatar Saída JSON

O objeto `OcrResult` é uma classe C# simples, o que significa que podemos passá‑lo para `System.Text.Json`. Ao habilitar `WriteIndented`, a saída torna‑se legível por humanos.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **O que você obtém:** Uma string JSON bem indentada que inclui o texto reconhecido, a confiança e o layout da página. Isso é perfeito para logs, envio a um serviço web ou armazenamento em um banco de dados NoSQL.

## Etapa 5: Exibir e (Opcionalmente) Salvar o JSON Formatado

Finalmente, exibimos o JSON no console. Você também pode gravá‑lo em um arquivo com `File.WriteAllText`, se preferir.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Saída esperada no console (truncada para brevidade):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Se o motor OCR não encontrar nenhum texto, o campo `Text` será uma string vazia e `Confidence` será `0`. Isso indica que você deve verificar a qualidade da imagem.

## Etapa 6: Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo que você pode copiar‑colar em um novo aplicativo console:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Execute o programa (`dotnet run` a partir da pasta do projeto) e veja o console imprimir uma representação JSON bem formatada da sua fatura escaneada.

## Armadilhas Comuns & Dicas (Extras do tutorial c# ocr)

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Campo `Text` vazio** | Imagem com baixo contraste ou rotacionada. | Pré‑processar a imagem (aumentar contraste, corrigir inclinação) ou usar `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Binaries nativos do Aspose OCR ausentes. | Certifique‑se de que o pacote NuGet foi restaurado corretamente e que a arquitetura de tempo de execução (x64/x86) corresponde ao seu SO. |
| **Atraso de desempenho em PDFs grandes** | OCR processa cada página sequencialmente. | Paralelizar criando instâncias separadas de `OcrEngine` por página (o motor é thread‑safe). |
| **JSON muito grande** | Você está serializando todos os detalhes, incluindo caixas delimitadoras. | Use um DTO que contenha apenas `Text` e `Confidence` antes da serialização. |

> **Lembre‑se:** O objetivo deste tutorial é mostrar um fluxo limpo, de ponta a ponta. Você pode sempre reduzir o JSON ou adicionar mais metadados posteriormente.

## Conclusão

Você acabou de concluir um **c# ocr tutorial** que carrega uma imagem, **extrai texto de imagem** e produz um **formato json output** ao **serializar objeto para json**. As etapas são simples, o código está pronto para executar e o JSON está perfeitamente indentado para consumo downstream.

Qual é o próximo passo? Experimente trocar `OcrLanguage.English` por `OcrLanguage.French` ou alimentar uma pasta de recibos em um loop. Você também pode explorar salvar o JSON diretamente no Azure Blob Storage ou enviá‑lo a um modelo de aprendizado de máquina.

Se encontrar algum obstáculo, verifique se o caminho da imagem está correto e se a licença do Aspose OCR (caso possua) está carregada antes de chamar `Recognize`. Boa codificação, e que seus resultados OCR sejam sempre nítidos! 

--- 

*Imagem ilustrando o fluxo OCR (texto alternativo: "diagrama do tutorial c# ocr mostrando carregar imagem, reconhecer texto, serializar para JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}