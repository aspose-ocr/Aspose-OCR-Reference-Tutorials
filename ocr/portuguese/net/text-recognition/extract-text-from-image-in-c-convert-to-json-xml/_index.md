---
category: general
date: 2026-04-26
description: Extraia texto de imagem em C# usando Aspose.OCR e aprenda como converter
  a imagem para formatos JSON e XML em minutos.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: pt
og_description: Extraia texto de imagem em C# com Aspose.OCR. Aprenda passo a passo
  como converter o resultado para JSON e XML instantaneamente.
og_title: Extrair texto de imagem em C# – Converter para JSON e XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Extrair texto de imagem em C# – Converter para JSON e XML
url: /pt/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto de imagem em C# – Converter para JSON & XML

Já precisou **extrair texto de imagem** em um projeto .NET, mas ficou preso na pergunta “como eu realmente obtenho os dados?” Você não está sozinho. Em muitas aplicações reais—pense em processamento de faturas, digitalização de recibos ou verificação de crachás—extrair os caracteres brutos de uma foto é o primeiro passo crucial.  

A boa notícia? Com Aspose.OCR você pode fazer isso em poucas linhas e, em seguida, **converter a imagem para JSON** ou **converter a imagem para XML** para sistemas downstream. Neste guia vamos percorrer o código completo, pronto‑para‑executar, explicar por que cada parte importa e mostrar alguns truques para evitar armadilhas comuns.

---

## O que você precisará

- **.NET 6+** (qualquer SDK recente funciona; o exemplo tem como alvo o .NET 6)
- **Aspose.OCR for .NET** pacote NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Um arquivo de imagem (PNG, JPG, etc.) que contenha texto legível; usaremos `invoice.png` como exemplo.
- Um editor de código—Visual Studio, VS Code ou Rider—o que preferir.

É só isso. Nenhum motor OCR extra, nenhum serviço externo, apenas um único pacote NuGet.

---

## Etapa 1: Configurar o mecanismo OCR – Como extrair texto de imagem

Primeiro criamos uma instância de `OcrEngine` e apontamos para o arquivo de imagem. Essa etapa é a base; sem uma imagem carregada corretamente o mecanismo não consegue reconhecer nada.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Por que isso importa:**  
- `OcrEngine` encapsula todo o pré‑processamento de imagem de baixo nível (binarização, correção de inclinação).  
- Carregar a imagem via `ImageStream.FromFile` garante que o mecanismo leia os bytes exatos, preservando DPI e profundidade de cor—ambos podem afetar a precisão do reconhecimento.  

> **Dica profissional:** Se suas imagens de origem estiverem em um stream (por exemplo, enviadas via API web), use `ImageStream.FromStream(yourStream)` em vez de `FromFile`.

---

## Etapa 2: Informar ao mecanismo qual idioma esperar – extrair texto de imagem com precisão

Aspose.OCR suporta muitos alfabetos. Especificar o idioma correto reduz o conjunto de caracteres e aumenta a precisão.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Por que:**  
Ao definir `Language.Latin`, o mecanismo OCR ignora glifos cirílicos ou asiáticos, reduzindo falsos positivos. Se mais tarde precisar lidar com documentos multilíngues, pode mudar para `Language.Multilingual` ou combinar idiomas.

---

## Etapa 3: Executar o processo de reconhecimento – extrair texto de imagem em uma chamada

Agora realmente reconhecemos o texto. O método `Recognize` devolve um objeto `RecognitionResult` que contém o texto bruto, pontuações de confiança e até dados de layout.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Por que:**  
Chamar `Recognize` uma única vez basta porque o mecanismo realiza internamente pré‑processamento, segmentação e classificação de caracteres. A propriedade `Text` fornece uma representação em string simples, ideal para logs ou validações rápidas.

---

## Etapa 4: Converter o resultado para JSON – converter imagem para json facilmente

Muitos serviços modernos preferem payloads JSON. Aspose.OCR oferece o método conveniente `ToJson` que serializa todo o `RecognitionResult`, incluindo valores de confiança e caixas delimitadoras.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Por que você pode querer JSON:**  
- **Interoperabilidade:** Aplicações front‑end (React, Angular) podem consumir o JSON diretamente.  
- **Depuração:** O JSON inclui a confiança por caractere, permitindo sinalizar palavras de baixa confiança para revisão manual.  

> **Caso de borda:** Se seu sistema downstream precisar apenas do texto simples, você pode extrair `recognitionResult.Text` e envolvê‑lo em um objeto JSON customizado ao invés do payload completo da Aspose.

---

## Etapa 5: Converter o resultado para XML – converter imagem para xml para sistemas legados

Algumas empresas ainda dependem de esquemas XML para troca de dados. O método `ToXml` espelha `ToJson`, mas gera XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Por que XML:**  
- **Validação de esquema:** Você pode definir um XSD que corresponda à estrutura emitida pela Aspose, garantindo conformidade contratual.  
- **Integração:** Sistemas ERP ou de gestão documental mais antigos costumam analisar XML nativamente.

---

## Exemplo completo – Código tudo‑em‑um

Abaixo está o programa completo que une tudo. Copie‑e‑cole em um novo projeto console (`dotnet new console`) e execute.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Saída esperada (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

Os arquivos JSON e XML conterão uma estrutura mais rica, por exemplo:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Perguntas comuns & casos de borda

### E se a imagem estiver borrada ou rotacionada?
Aspose.OCR corrige automaticamente a inclinação da maioria das imagens, mas em casos extremos você pode pré‑processar com `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Aumentar um pouco o contraste (`ImageProcessor.AdjustContrast`) também pode melhorar a pontuação de confiança.

### Posso extrair texto de PDFs?
Sim—converta cada página do PDF em uma imagem primeiro (por exemplo, usando Aspose.PDF ou uma biblioteca gratuita como PDFium) e então alimente essas imagens ao mesmo fluxo OCR.

### Como lidar com múltiplos idiomas em um documento?
Defina `ocrEngine.Language = Language.Multilingual;` ou combine idiomas específicos:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Esteja ciente de que conjuntos de idiomas mais amplos podem

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}