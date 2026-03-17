---
category: general
date: 2026-03-17
description: Extraia texto de PNG usando Aspose OCR em C#. Aprenda a ler texto de
  imagem, processar OCR de recibos e criar um motor OCR com aceleração GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: pt
og_description: Extraia texto de PNG usando Aspose OCR. Este guia mostra como ler
  texto de uma imagem, processar OCR de recibos e criar um mecanismo OCR de forma
  eficiente.
og_title: Extrair texto de PNG – Ler texto de imagem com OCR
tags:
- OCR
- CSharp
- Aspose
title: Extrair texto de PNG – Ler texto de imagem com OCR
url: /pt/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PNG – Ler Texto de Imagem com OCR

Já precisou **extrair texto de PNG** mas não sabia qual biblioteca ofereceria resultados confiáveis? Você não está sozinho—desenvolvedores perguntam constantemente: “Como leio texto de arquivos de imagem como recibos sem escrever uma rede neural personalizada?” A boa notícia é que o Aspose OCR faz o trabalho pesado para você, e ainda é possível ativar a GPU para ganhar velocidade.

Neste tutorial vamos percorrer tudo que você precisa para **processar OCR de recibos**, desde a instalação do pacote NuGet até a criação de um motor OCR que entende seu arquivo PNG. Ao final, você terá um aplicativo console autônomo que lê a imagem de um recibo, imprime o texto reconhecido e mostra como ajustar o motor para diferentes cenários. Sem documentação externa, apenas código puro e explicações claras.

## Pré‑requisitos

- .NET 6.0 SDK (ou qualquer versão recente do .NET)  
- Visual Studio 2022 ou VS Code com extensões C#  
- Uma GPU NVIDIA suportada com o driver mais recente (opcional, mas recomendado para modo GPU)  
- O pacote **Aspose.OCR** NuGet (`dotnet add package Aspose.OCR`)  

Se você não tem GPU, ainda pode executar o exemplo em modo CPU—basta pular as linhas de configuração da GPU.

## Etapa 1: Instalar Aspose.OCR e Configurar o Projeto

Primeiro, crie um novo projeto console e adicione a biblioteca Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Por que isso importa: o pacote `Aspose.OCR` inclui o motor OCR, carregadores de imagem e suporte opcional à GPU. Instalá‑lo via NuGet garante que você obtenha a versão estável mais recente (em março 2026 é a 23.10).

## Etapa 2: Importar Namespaces e Criar o Motor OCR

Agora abra **Program.cs** e adicione as diretivas `using` necessárias. Em seguida, instancie o motor.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Dica:** Se encontrar `System.DllNotFoundException` em máquinas sem GPU, basta comentar as duas linhas que definem `EngineMode` e `GpuDeviceId`. O motor reverte automaticamente para CPU.

## Etapa 3: Carregar a Imagem PNG da Qual Você Quer Extrair Texto

Aspose OCR pode ler imagens diretamente de um caminho de arquivo, de um stream ou até de um array de bytes. Para esta demonstração, carregaremos uma imagem de recibo local.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Observe como protegemos contra a falta do arquivo. Em aplicativos reais, provavelmente exibirá uma mensagem amigável ao usuário em vez de simplesmente encerrar.

## Etapa 4: Executar o Reconhecimento OCR

A extração real do texto ocorre com uma única chamada de método. O motor devolve um objeto `OcrResult` que contém a string bruta, pontuações de confiança e informações de layout.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Por que verificamos `ocrResult.Text`: às vezes um PNG de baixa qualidade gera uma string vazia, e é melhor avisar o usuário do que não produzir saída silenciosamente.

## Etapa 5: Exibir o Texto Reconhecido

Por fim, imprima a string extraída no console. Você também pode gravá‑la em um arquivo, banco de dados ou enviá‑la para outro serviço.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Ao executar o programa (`dotnet run`), você deverá ver algo como:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Essa é a **solução completa para extrair texto de arquivos PNG** com Aspose OCR, e você acabou de aprender como **ler texto de imagens** que se parecem com recibos.

## Opcional: Ajuste Fino do Motor OCR (Avançado)

Se precisar de maior precisão para fontes específicas ou fundos ruidosos, considere ajustar estas configurações:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Essas alterações são especialmente úteis quando você **processa OCR de recibos** em trabalhos em lote onde algumas digitalizações não são perfeitas.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| **Driver da GPU ausente** | O motor tenta carregar CUDA mas não encontra a DLL. | Instale o driver NVIDIA mais recente ou troque para modo CPU removendo a linha `EngineMode.Gpu`. |
| **Caminho de imagem incorreto** | `ImageStream.FromFile` lança exceção se o arquivo não for encontrado. | Sempre valide o caminho (veja a Etapa 3) ou use `Path.Combine` para segurança multiplataforma. |
| **Baixa confiança em recibos borrados** | O motor OCR não consegue diferenciar os caracteres. | Ative `EnableImagePreprocessing` e, opcionalmente, aumente o DPI da imagem antes de enviá‑la ao motor. |
| **Vazamento de memória em serviços de longa execução** | Cada `OcrEngine` mantém recursos não gerenciados. | Libere o motor após o uso: `using var ocrEngine = new OcrEngine();` |

## Exemplo Completo (Copiar‑Colar)

Abaixo está o **programa inteiro** que você pode colar em `Program.cs`. Ele inclui todos os ajustes opcionais comentados para fácil ativação.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Salve, execute `dotnet run` e verá o conteúdo do recibo impresso no console.

![exemplo de extração de texto de png](receipt.png "exemplo de extração de texto de png")

*A imagem acima mostra um exemplo de recibo PNG que o código pode processar.*

## Recapitulação

Cobremos como **extrair texto de arquivos PNG** usando Aspose OCR, demonstramos como **ler texto de imagens**, e percorremos um pipeline completo de **processamento OCR de recibos** que inclui aceleração opcional por GPU. Ao **criar seu próprio motor OCR**, você ganha controle total sobre configuração, desempenho e tratamento de erros.

## O Que Explorar a Seguir?

- **Processamento em lote**: Percorra um diretório de recibos PNG e grave cada resultado em um arquivo CSV.  
- **Integração com Azure Functions**: Transforme este aplicativo console em um endpoint serverless que aceita uploads de imagens.  
- **Suporte multilíngue**: Troque `Language.English` por `Language.Spanish` ou adicione dicionários personalizados.  
- **Pós‑processamento**: Use expressões regulares para extrair campos como valor total, data ou CNPJ da string OCR bruta.

Sinta‑se à vontade para experimentar—OCR é uma ferramenta surpreendentemente flexível quando você conhece os botões corretos. Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte a referência da API Aspose OCR para aprofundamentos.

Feliz codificação e aproveite para transformar aqueles teimosos recibos PNG em texto pesquisável!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}