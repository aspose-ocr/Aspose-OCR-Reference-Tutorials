---
category: general
date: 2026-02-20
description: Aprenda a ler recibos em C# extraindo texto de imagens e convertendo
  para JSON. Código passo a passo usando Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: pt
og_description: Descubra como ler recibos em C# carregando um arquivo de imagem, extraindo
  texto com Aspose OCR e convertendo o resultado para JSON. Exemplo completo de código.
og_title: Como Ler Recibo em C# – Extrair Texto, Converter para JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Como Ler Recibo em C# – Guia Completo para Extrair Texto de Imagem
url: /pt/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

they are placeholders. The requirement says preserve all code blocks fenced. There are none besides placeholders. So fine.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Ler Recibo em C# – Guia Completo

Já se perguntou **how to read receipt** imagens programaticamente? Talvez você esteja construindo um aplicativo de controle de despesas e precise extrair itens de linha de uma foto de um recibo de supermercado. Na minha experiência, o maior ponto crítico é transformar aquele JPEG borrado em dados estruturados que você realmente pode usar. A boa notícia? Com algumas linhas de C# e Aspose OCR você pode **extract text from image**, então **convert image to JSON** de uma forma que parece quase mágica.

Neste tutorial você sairá com uma solução pronta‑para‑executar que **loads an image file C#**, executa OCR e gera um payload JSON detalhado. Sem serviços externos, sem chamadas REST complicadas — apenas código .NET puro que você pode inserir em qualquer projeto console ou ASP.NET. Ao final, você entenderá por que cada passo importa, como lidar com casos de borda comuns (como tamanhos de recibos não‑padrão) e como realmente se parece a saída JSON.

## O que você precisará

- **.NET 6.0 ou posterior** – o código usa `System.Drawing.Common` que é suportado no Windows, Linux e macOS.
- **Aspose.OCR for .NET** – você pode obter um pacote NuGet de avaliação gratuita (`Aspose.OCR`) ou usar uma cópia licenciada se já a possuir.
- Uma **imagem de recibo de exemplo** (`receipt.jpg`) colocada em algum local que seu aplicativo possa ler.
- Qualquer IDE que você prefira (Visual Studio, Rider, VS Code).  

É isso. Nenhuma configuração extra, nenhuma chave de API.

---

## Etapa 1 – Carregar o Arquivo de Imagem C# (Palavra‑chave Principal em Ação)

Antes que o motor OCR possa fazer sua mágica, você precisa colocar a imagem na memória. Esta é a clássica etapa “load image file C#” que muitos desenvolvedores ignoram.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Por que isso importa:**  
`Image.FromFile` lê o arquivo *uma vez* e mantém um manipulador aberto, o que é perfeito para uma passagem rápida de OCR. Se você estiver processando muitos recibos em um loop, considere usar `Image.FromStream` para evitar bloquear o arquivo.

> **Dica profissional:** Se você encontrar uma *FileNotFoundException*, verifique novamente o caminho e certifique‑se de que a imagem realmente está lá. Caminhos relativos também funcionam (`"./receipt.jpg"`), mas caminhos absolutos são mais seguros para trabalhos em produção.

## Etapa 2 – Criar e Configurar o Motor OCR

Aspose OCR vem com um `OcrEngine` pronto‑para‑uso. Você não precisa treinar um modelo; a biblioteca já sabe ler texto impresso, que é exatamente o que a maioria dos recibos usa.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Por que definimos essas opções:**  
`DetectOrientation` indica ao motor para girar automaticamente a imagem se o recibo foi escaneado de cabeça‑para‑baixo. Definir o idioma restringe o conjunto de caracteres, o que pode melhorar a precisão — especialmente quando você só precisa de dados alfanuméricos em inglês.

## Etapa 3 – Reconhecer a Imagem e Converter para JSON

Agora vem a parte divertida: **extract text from image** e **convert image to JSON** em uma única chamada.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

O método `RecognizeToJson` retorna uma estrutura JSON rica que inclui:

- `Text`: o texto concatenado simples.
- `Lines`: um array de objetos de linha com coordenadas.
- `Words`: cada palavra com pontuações de confiança.
- `Regions`: caixas delimitadoras para blocos de texto detectados.

Você pode desserializar esse JSON em um objeto C# se precisar de acesso tipado, mas para muitos cenários imprimir o JSON bruto já é suficiente.

## Etapa 4 – Saída do JSON (ou Armazená‑lo)

Vamos ver a saída e discutir o que fazer com ela.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Exemplo de Saída

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**O que fazer a seguir?**  
Analise o array `Lines` para extrair o valor `Total`, ou envie o JSON para um serviço downstream que armazena lançamentos de despesas. Como o resultado já está em JSON, você pode conectá‑lo diretamente a qualquer banco de dados NoSQL, Azure Function ou fluxo do Power Automate.

## Etapa 5 – Lidando com Casos de Borda Comuns

Mesmo os melhores motores OCR tropeçam em algumas coisas. Abaixo estão cenários que você pode encontrar ao aprender **how to read receipt** imagens.

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **Recibo de baixa resolução (≤ 150 dpi)** | Aumente a escala da imagem primeiro usando `Bitmap` e `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Recibo girado ou inclinado** | Mantenha `DetectOrientation = true`. Para inclinação severa, pré‑procese com `Image.RotateFlip` ou uma biblioteca de terceiros como OpenCV. |
| **Fundo colorido (ex.: recibo sobre uma mesa)** | Converta para escala de cinza e aumente o contraste antes do OCR (`ImageAttributes`). |
| **Múltiplos recibos em uma foto** | Corte cada região de recibo manualmente ou use `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Arquivos grandes causando OutOfMemory** | Use declarações `using` para descartar objetos `Image` rapidamente, ou processe em partes. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

## Etapa 6 – Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa *completo* que você pode compilar agora mesmo. Ele inclui todas as etapas, diretivas `using` corretas e tratamento de erros elegante.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Execute:**  
`dotnet run` a partir da pasta do projeto. Se tudo estiver configurado corretamente, você verá o JSON impresso no console e salvo ao lado da sua imagem de recibo.

## Conclusão

Acabamos de cobrir **how to read receipt** imagens em C# do início ao fim. Ao carregar a imagem, configurar o Aspose OCR e chamar `RecognizeToJson`, você pode **extract text from image** e **convert image to JSON** com praticamente nenhum código boilerplate. A abordagem escala — de uma demonstração de recibo único a um processador em lote que lida com centenas de recibos por noite.

Próximos passos que você pode explorar:

- **Parse the JSON** para extrair datas, totais e itens de linha (use `System.Text.Json` ou `Newtonsoft.Json`).
- **Integrate with a database** (SQL, Cosmos DB) para armazenar registros de despesas automaticamente.
- **Add a UI** (WinForms, WPF ou Blazor) para que os usuários possam arrastar‑e‑soltar recibos.
- **Swap Aspose OCR** por outro motor (Tesseract, Microsoft Azure OCR) se a licença for um problema — apenas mantenha o mesmo padrão “load image file C#”.

Sinta‑se à vontade para experimentar, quebrar coisas e depois voltar aqui para um refresco. Se você encontrar algum problema, a comunidade (e os fóruns da Aspose) são ótimos lugares para perguntar. Feliz codificação, e aproveite transformar esses recibos de papel em dados limpos e pesquisáveis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}