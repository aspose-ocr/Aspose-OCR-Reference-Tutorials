---
category: general
date: 2026-03-26
description: reconheça texto de PNG e extraia dados de recibo usando Aspose OCR em
  C#. Converta a imagem para JSON‑L e processe o recibo com OCR em um exemplo completo.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: pt
og_description: reconheça texto de png e transforme recibos em JSON‑L com Aspose OCR
  em C#. Código completo passo a passo e dicas.
og_title: reconhecer texto de PNG – Guia Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Reconhecer texto de PNG – tutorial Aspose OCR C# JSON‑L
url: /pt/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de png – Guia completo Aspose OCR C# 

Já precisou **reconhecer texto de png** arquivos mas não tinha certeza de qual biblioteca forneceria resultados limpos, linha por linha? Você não está sozinho. Em muitos aplicativos de pequenas empresas o recibo está como uma imagem PNG, e extrair o valor, a data ou o nome do comerciante é um ponto de dor diário.  

A boa notícia? Com algumas linhas de C# e a biblioteca **Aspose OCR** você pode **extrair texto de receipt**, então **converter imagem para jsonl** para análises posteriores. Neste tutorial vamos percorrer todo o pipeline — carregar um PNG, executar OCR e gravar cada linha em um arquivo JSON‑L — para que você possa **processar receipt com OCR** imediatamente.

Vamos cobrir tudo que você precisa: pacotes NuGet necessários, um programa completo executável, explicações sobre por que cada passo importa e algumas dicas práticas que você vai apreciar quando os recibos ficarem bagunçados. Nenhuma documentação externa necessária; basta copiar‑colar, executar e adaptar.

---

## O que você aprenderá

- Como **reconhecer texto de png** usando `Aspose.OCR`.
- Como **extrair texto de receipt** de objetos de linha e capturar pontuações de confiança.
- Como **converter imagem para jsonl** para que cada linha de OCR se torne um objeto JSON separado.
- Como **processar receipt com OCR** de ponta a ponta, lidando com casos extremos como imagens vazias ou linhas de baixa confiança.
- Dicas para solucionar problemas comuns de OCR e melhorar a precisão.

### Pré-requisitos

- .NET 6.0 ou posterior (o código funciona também com .NET Core e .NET Framework).
- Visual Studio 2022 ou qualquer IDE de sua preferência.
- Uma licença válida do Aspose OCR (você pode começar com uma licença temporária gratuita da Aspose.com).
- Um recibo de exemplo salvo como `receipt.png` em uma pasta que você controla.

---

## Etapa 1: Reconhecer texto de png com Aspose OCR

A primeira coisa que precisamos é um `OcrEngine` inicializado. Esse objeto contém as configurações do motor OCR (idioma, modo de detecção, etc.). Por padrão ele usa inglês e detecta automaticamente o layout da página, o que funciona bem para a maioria dos recibos.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Por que isso importa:**  
`OcrEngine` é o componente que faz o trabalho pesado; criá‑lo uma vez e reutilizá‑lo em várias imagens reduz o consumo de memória. Se precisar de outro idioma (por exemplo, recibos em espanhol), você pode definir `ocrEngine.Language = OcrLanguage.Spanish;` antes de chamar `Recognize`.

---

## Etapa 2: Extrair texto das linhas do receipt

`OcrResult` contém uma coleção chamada `Lines`. Cada linha possui o texto bruto e uma pontuação de confiança (0‑100). Extrair esses dados lhe dá controle granular — você pode descartar linhas de baixa confiança ou marcá‑las para revisão manual.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Por que escapamos JSON:**  
O texto do receipt pode conter aspas (`"`) ou barras invertidas (`\`) que quebrariam uma string JSON ingênua. O método `EscapeJson` garante uma linha JSON válida.

**Como a saída se parece:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Cada linha é um registro separado, perfeito para streaming em um data lake ou alimentar um modelo de machine‑learning.

---

## Etapa 3: Converter imagem para JSONL – lidando com casos extremos

Ao processar um lote de recibos, algumas imagens podem estar em branco, corrompidas ou ter pontuações de confiança extremamente baixas. Vamos tornar o pipeline um pouco mais robusto.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Por que filtrar:**  
Recibos impressos em papel desbotado podem gerar caracteres estranhos com baixa confiança. Descartar tudo abaixo de 80 % geralmente remove o ruído mantendo os dados úteis.

---

## Etapa 4: Processar receipt com OCR – exemplo de ponta a ponta

Juntando tudo, aqui está o programa **completo, pronto‑para‑executar**. Substitua `YOUR_DIRECTORY` pela pasta que contém seu arquivo PNG.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Executando o código:**  
1. Abra um terminal na pasta do projeto.  
2. `dotnet add package Aspose.OCR` – instala a biblioteca.  
3. `dotnet run` – você deve ver a mensagem de sucesso e o arquivo `receipt.jsonl` aparecer.

**Resultado esperado:** Um arquivo JSON delimitado por linhas onde cada linha espelha uma linha do receipt, completo com pontuações de confiança. Agora você pode encaminhar esse arquivo para Power BI, Elastic ou qualquer ferramenta de análise que entenda JSON‑L.

---

## Armadilhas comuns e dicas avançadas

| Problema | Por que acontece | Correção rápida |
|----------|------------------|-----------------|
| **Blank output** | Caminho da imagem errado ou arquivo não é PNG. | Verifique o caminho, use `File.Exists(imagePath)`. |
| **Garbage characters** | DPI baixo ou PNG muito comprimido. | Use escaneamentos de pelo menos 300 dpi; evite compressão agressiva JPEG. |
| **Too many low‑confidence lines** | Receipt impresso em papel térmico desbotado. | Aumente o limiar `minConfidence` ou pré‑procese a imagem (contraste/limiar). |
| **JSON parsing errors** | Aspas não escapadas no texto do receipt. | Mantenha o helper `EscapeJson` ou troque para `System.Text.Json` para serialização robusta. |

**Dica avançada:** Se precisar extrair campos específicos (ex.: valor total), execute uma regex simples em cada `line.Text` depois de gerar o arquivo JSON‑L. Isso mantém o OCR separado da lógica de negócio e facilita a depuração.

---

## Expandindo a solução

- **Processamento em lote:** Envolva a lógica `Main` em um `foreach` sobre todos os arquivos PNG em um diretório.  
- **Suporte multilíngue:** Defina `ocrEngine.Language = OcrLanguage.Spanish;` (ou qualquer idioma suportado) antes de `Recognize`.  
- **Saída estruturada:** Em vez de JSON linha a linha, construa um objeto `Receipt` com propriedades `Date`, `Merchant`, `Total`, e então serialize uma única vez.  

Todas essas variações ainda **convert image to jsonl** no núcleo, então você pode trocar o consumidor downstream sem tocar na parte de OCR.

---

## Conclusão

Acabamos de mostrar como **reconhecer texto de png** usando Aspose OCR, **extrair texto de receipt** e **converter imagem para jsonl** para processamento posterior fácil. O programa C# completo e autocontido demonstra todo o fluxo de trabalho — desde carregar um PNG, lidar com casos extremos, até gravar um arquivo JSON‑L limpo — para que você possa imediatamente **processar receipt com OCR** em seus próprios projetos.

Experimente com alguns recibos de exemplo, ajuste o limiar de confiança e veja como rapidamente uma pilha ruidosa de imagens se transforma em dados estruturados prontos para análise. Quando estiver confortável, explore o processamento em lote ou adicione um pequeno modelo de ML para classificar categorias de despesa automaticamente.

Tem perguntas ou descobriu um ajuste inteligente? Deixe um comentário abaixo — feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}