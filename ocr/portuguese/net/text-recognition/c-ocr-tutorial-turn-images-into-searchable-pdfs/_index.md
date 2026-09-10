---
category: general
date: 2026-01-12
description: Tutorial de OCR em C# que mostra como reconhecer texto em imagem, extrair
  texto de imagem em C# e gerar um arquivo OCR de imagem para PDF com pontuações de
  confiança.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: pt
og_description: Aprenda um tutorial completo de OCR em C# para reconhecer imagens
  de texto, extrair texto de imagens em C# e criar um documento OCR de imagem para
  PDF com pontuações de confiança.
og_title: Tutorial de OCR em C# – Converter imagens em PDFs pesquisáveis
tags:
- OCR
- C#
- PDF
title: Tutorial de OCR em C# – Transforme imagens em PDFs pesquisáveis
url: /pt/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Transforme Imagens em PDFs Pesquisáveis

Já se perguntou como **reconhecer imagens de texto** em um projeto C# sem precisar procurar serviços de terceiros? Você não está sozinho. Em muitos aplicativos do mundo real — pense em scanners de faturas, rastreadores de recibos ou arquivos de documentos multilíngues — os desenvolvedores precisam de um mecanismo OCR confiável, on‑premise, que também forneça pontuações de confiança.  

Este **c# ocr tutorial** irá guiá‑lo por tudo que você precisa: desde carregar uma imagem, selecionar modelos de idioma, alternar a aceleração GPU, até salvar o resultado como um PDF pesquisável. Ao final, você terá um exemplo de código pronto‑para‑executar que extrai texto, relata a confiança do OCR e, opcionalmente, cria um arquivo *image to pdf ocr* — tudo em menos de um minuto de codificação.

## O que você vai construir

- Carregar uma imagem multilíngue (`sample_multi_lang.jpg` é usada como placeholder).  
- Escolher os modelos de idioma Árabe, Hindi e Russo (você pode adicionar mais).  
- Ativar o processamento GPU se sua máquina o suportar.  
- Obter o resultado bruto do OCR **com pontuações de confiança**.  
- Serializar o resultado em JSON formatado **ou** gravar um PDF pesquisável.  

Sem serviços web externos, sem mágica oculta — apenas Aspose.OCR para .NET, algumas linhas de C# e uma explicação clara do **porquê** cada linha importa.

## Pré‑requisitos

- .NET 6.0 ou superior (o código compila em .NET Core e .NET Framework).  
- Visual Studio 2022 (ou qualquer IDE que você prefira).  
- Uma licença Aspose.OCR para .NET (o trial gratuito funciona para testes).  
- Opcional: uma GPU compatível com CUDA se você quiser acelerar o reconhecimento.

> **Dica profissional:** Se você não tem uma GPU, basta definir `UseGpu = false` e o mecanismo retornará ao CPU sem nenhuma alteração de código.

## Etapa 1: Instale os Pacotes NuGet Necessários

Abra o **Package Manager Console** e execute:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

## Etapa 2: Configure a Estrutura do Projeto

Crie um novo projeto de console (`dotnet new console -n AsposeOcrDemo`) e substitua o `Program.cs` gerado pelo código abaixo.  
Toda a lógica reside dentro da classe `Program`; o único tipo extra é um pequeno método de extensão que formata o resultado do OCR para JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Por que este código funciona

1. **Alternância de GPU** – `GpuOcrEngine` utiliza núcleos CUDA; o operador ternário torna a troca simples.  
2. **Download automático de idioma** – `AutoDownloadResources = true` garante que os modelos Árabe, Hindi e Russo sejam baixados na primeira execução do aplicativo.  
3. **Pontuações de confiança** – `result.Words` contém um `Confidence` para cada palavra reconhecida; o método de extensão as formata em um objeto JSON limpo.  
4. **PDF pesquisável** – `result.Pdf` já é um PDF totalmente pesquisável, então apenas gravamos o array de bytes no disco. Nenhuma biblioteca extra é necessária.

## Etapa 6: Execute o Exemplo

Abra um terminal, navegue até a pasta do projeto e execute:

```bash
dotnet run
```

Se você escolheu a saída **JSON**, verá algo como:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Se você mudou para **PDF**, o console imprime o caminho e você encontrará um PDF pesquisável ao lado da imagem de origem.

## Perguntas Frequentes & Casos Limítrofes

- **E se um modelo de idioma não estiver disponível?**  
  O mecanismo OCR lança uma clara `ResourceNotFoundException`. Como definimos `AutoDownloadResources = true`, o modelo ausente é baixado automaticamente na primeira execução, portanto a exceção raramente aparece em produção.

- **Posso processar um lote de imagens?**  
  Absolutamente. Envolva a chamada `engine.Recognize` em um loop `foreach` sobre um diretório de arquivos. O mesmo `OcrResultExtensions` funciona para cada imagem.

- **Preciso de licença para GPU?**  
  Não. O trial gratuito funciona tanto para CPU quanto para GPU. Uma licença completa remove a marca d'água do trial e elimina as restrições de limite de páginas.

- **Quão precisas são as pontuações de confiança?**  
  As pontuações variam de 0.0 (sem confiança) a 1.0 (confiança perfeita). Na prática, tudo acima de 0.90 é confiável para processamento subsequente; você pode filtrar palavras com menor confiança se precisar de validação mais rigorosa.

## Etapa 7: Próximos Passos (Expanda seu Kit de Ferramentas OCR)

1. **Adicionar mais idiomas** – basta acrescentar `LanguageModel.French` (ou qualquer modelo suportado) ao array `Languages`.  
2. **Combinar OCR com conversão PDF/A** – Aspose.PDF pode incorporar a camada OCR em um documento compatível com PDF/A‑2b para arquivamento.  
3. **Integrar com Azure Functions** – envolva a lógica em um endpoint serverless para processar uploads em tempo real.  
4. **Ajustar finamente os limites de confiança** – use `result.Words.Where(w => w.Confidence < 0.85)` para sinalizar palavras incertas para revisão manual.

### TL;DR

Este **c# ocr tutorial** mostra como:

- Carregar uma imagem e selecionar múltiplos modelos de idioma.  
- Ativar a aceleração GPU com uma única flag booleana.  
- Recuperar resultados OCR **com pontuações de confiança** e serializá‑los para JSON.  
- Opcionalmente gravar um PDF pesquisável (**image to pdf ocr**).  

Tudo isso é possível com apenas algumas linhas, um trial gratuito do Aspose.OCR e o código acima. Experimente, ajuste a lista de idiomas e você terá um pipeline OCR pronto para produção em minutos.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}