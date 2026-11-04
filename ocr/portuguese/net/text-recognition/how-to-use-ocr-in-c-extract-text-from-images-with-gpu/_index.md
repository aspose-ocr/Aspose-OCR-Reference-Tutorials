---
category: general
date: 2026-02-13
description: Aprenda a usar OCR em C# para extrair texto de arquivos de imagem, habilitar
  o processamento GPU e converter digitalizações em texto rapidamente.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: pt
og_description: Como usar OCR em C#? Este guia mostra como extrair texto de arquivos
  de imagem, habilitar o processamento GPU e converter digitalizações em texto.
og_title: Como usar OCR em C# – Extrair texto de imagens com GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Como usar OCR em C# – Extrair texto de imagens com GPU
url: /pt/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR em C# – Extrair Texto de Imagens com GPU

Já se perguntou **como usar OCR** para extrair texto de um documento escaneado sem esforço? Você não está sozinho—os desenvolvedores perguntam constantemente: “Como posso extrair texto de arquivos de imagem de forma eficiente?” A boa notícia é que com Aspose.OCR você pode fazer exatamente isso, e ainda pode **ativar o processamento por GPU** para um aumento de velocidade perceptível em hardware compatível.

Neste tutorial, percorreremos um exemplo completo, de ponta a ponta, que mostra **como usar OCR**, como **extrair texto de imagem**, como **converter escaneamento em texto**, e o que fazer se a GPU não estiver disponível. Ao final, você terá um aplicativo de console C# pronto‑para‑executar que imprime o texto reconhecido e informa se a GPU foi realmente usada.

## O que você precisará

- .NET 6 SDK ou posterior (o código funciona também com .NET Core)  
- Visual Studio 2022 ou qualquer editor de sua preferência  
- Pacote Aspose.OCR para .NET (disponível via NuGet)  
- Um arquivo de imagem de alta resolução (por exemplo, `highres_scan.tif`) para teste  

Nenhuma configuração complicada necessária—apenas alguns comandos NuGet e você está pronto para começar.

## Etapa 1: Instalar Aspose.OCR e Preparar o Projeto

Primeiro de tudo. Você precisa trazer a biblioteca OCR para o seu projeto. Abra um terminal na pasta da solução e execute:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Isso cria um novo projeto de console chamado **OcrDemo** e adiciona o pacote NuGet `Aspose.OCR`. A biblioteca contém a classe `OcrEngine` que usaremos.

> **Dica profissional:** Se você estiver em uma máquina com GPU dedicada, certifique‑se de que o driver gráfico mais recente esteja instalado; caso contrário, a biblioteca reverterá automaticamente para o modo CPU.

## Etapa 2: Escrever o Código OCR Completo

Agora abra `Program.cs` e substitua seu conteúdo pelo seguinte. Cada linha está comentada para que você veja *por que* fazemos o que fazemos.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Por que isso funciona

- **ProcessingMode = Gpu** indica ao mecanismo que tente a GPU primeiro. A biblioteca abstrai as chamadas de baixo nível CUDA/OpenCL, portanto você não precisa gerenciar contextos de dispositivo manualmente.  
- **IsGpuEnabled** é um booleano que confirma se o caminho da GPU teve sucesso. Se você vir `false`, o mecanismo recaiu para a CPU automaticamente—não há motivo para pânico.  
- **RecognizeImage** realiza todo o trabalho pesado: carrega a imagem, executa o modelo OCR e devolve o resultado em texto puro. Não é necessário pré‑processar manualmente o bitmap, a menos que você tenha requisitos especiais (por exemplo, correção de inclinação). 

## Etapa 3: Executar o Aplicativo e Verificar a Saída

Compile e execute:

```bash
dotnet run
```

Se tudo estiver configurado corretamente, você verá algo como:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Se a GPU não estiver disponível, a primeira linha mostrará `GPU used: False`, mas o texto extraído ainda aparecerá—graças à reversão elegante.

> **Pergunta comum:** *E se minha imagem for JPEG em vez de TIFF?*  
> O método `RecognizeImage` aceita qualquer formato suportado pelo `System.Drawing` do .NET (JPEG, PNG, BMP, etc.). Basta mudar a extensão do arquivo em `imagePath`.

## Etapa 4: Opcional – Ajustar Configurações para Melhor Precisão

Aspose.OCR oferece alguns ajustes que você pode modificar:

| Configuração | O que faz | Quando usar |
|--------------|-----------|-------------|
| `ocrEngine.Language` | Força um idioma específico (ex.: `OcrLanguage.English`) | Se você souber o idioma do documento |
| `ocrEngine.PageSegMode` | Controla como o mecanismo divide páginas em blocos | Para layouts de múltiplas colunas |
| `ocrEngine.DetectOrientation` | Rotaciona automaticamente texto que não está na posição correta | Scans que podem estar de cabeça para baixo |

Você pode definir essas propriedades antes de chamar `RecognizeImage`. Por exemplo:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Etapa 5: Visualizar o Fluxo (Imagem com Texto Alternativo)

Abaixo está um diagrama simples que ilustra **como usar OCR** com aceleração opcional por GPU. Não é necessário para o código executar, mas ajuda a visualizar o panorama geral.

![Diagrama mostrando como usar OCR com processamento por GPU](/images/ocr-gpu-flow.png)

*Texto alternativo:* *Diagrama mostrando como usar OCR com processamento por GPU, destacando a reversão para CPU quando necessário.*

## Casos de Borda & Solução de Problemas

1. **Out‑of‑Memory na GPU** – Imagens muito grandes podem exceder a memória da GPU. Nesse caso, a biblioteca reverterá automaticamente para a CPU. Você pode redimensionar a imagem previamente para manter o uso de memória baixo.  
2. **Formato de Imagem Não Suportado** – Se `RecognizeImage` lançar *NotSupportedException*, verifique a extensão do arquivo e assegure que a imagem não esteja corrompida. Converter para PNG costuma resolver o problema.  
3. **Baixas Pontuações de Confiança** – Quando o resultado do OCR contém muitos caracteres ilegíveis, considere pré‑processamento (binarização, remoção de ruído) ou mudar para um escaneamento de maior resolução.  

## Conclusão: O que alcançamos

Acabamos de cobrir **como usar OCR** em um aplicativo de console C#, demonstrar como **extrair texto de arquivos de imagem**, e mostrar como **ativar o processamento por GPU** para resultados mais rápidos. Agora você sabe como **converter escaneamento em texto**, verificar se a GPU foi realmente utilizada e ajustar algumas configurações para cenários de casos extremos.

### Próximos passos

- Tente alimentar a saída em um **índice de busca** (por exemplo, Elasticsearch) para que seus PDFs escaneados se tornem pesquisáveis.  
- Experimente o **processamento em lote**—percorrer uma pasta de imagens e gravar cada resultado em um arquivo `.txt`.  
- Combine OCR com **APIs de tradução** para traduzir automaticamente documentos escaneados em idiomas estrangeiros.  

Tem mais perguntas? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}