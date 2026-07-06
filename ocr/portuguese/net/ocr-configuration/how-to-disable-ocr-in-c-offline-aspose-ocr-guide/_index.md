---
category: general
date: 2026-04-11
description: Aprenda como desativar o OCR no Aspose OCR para C# para executar offline,
  extrair texto de imagem sem internet e carregar a imagem corretamente para o OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: pt
og_description: Como desativar o OCR no Aspose OCR para C# e executá‑lo offline, extrair
  texto de imagens sem precisar de internet e carregar a imagem para OCR facilmente.
og_title: Como desativar OCR em C# – Guia offline de OCR da Aspose
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Como desativar OCR em C# – Guia offline de OCR da Aspose
url: /pt/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Desativar OCR em C# – Guia Offline do Aspose OCR

Já se perguntou **como desativar OCR** quando você precisa de uma solução realmente offline? Talvez esteja construindo um aplicativo desktop seguro que não pode depender de uma conexão de rede, ou simplesmente queira evitar downloads inesperados. De qualquer forma, a boa notícia é que o Aspose OCR permite desligar o download automático de recursos, apontar para uma pasta local e manter tudo on‑premises. Neste tutorial você também verá como **extrair texto de imagem** e **carregar imagem para OCR** corretamente, sem contratempos.

Vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra cada passo — desde a inicialização do engine até a impressão do texto japonês reconhecido. Sem documentação externa, sem mágica oculta; apenas código C# puro que você pode inserir no seu projeto hoje. Ao final, você entenderá por que desativar o recurso de download automático é importante, como definir o caminho dos recursos e quais armadilhas evitar.

## Pré‑requisitos

- .NET 6.0 (ou qualquer versão recente do .NET) instalado na sua máquina.  
- Pacote NuGet Aspose.OCR for .NET (`Install-Package Aspose.OCR`).  
- Uma pasta que já contenha os recursos de idioma que você precisa (por exemplo, o modelo japonês).  
- Um arquivo de imagem (`japan_doc.png`) que você deseja processar com OCR.  

Se estiver faltando os pacotes de idioma, baixe‑os uma única vez no portal da Aspose, descompacte‑os em uma pasta como `AsposeOCRResources` e pronto. Nenhum download adicional ocorrerá depois que você desativar o recurso de download automático.

![Como desativar OCR offline](/images/how-to-disable-ocr.png "ilustração de como desativar OCR")

## Etapa 1 – Criar a Instância do OCR Engine  

A primeira coisa a fazer é instanciar `OcrEngine`. Pense neste objeto como o cérebro que lerá sua imagem.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Por que isso importa:** Sem um engine você não pode configurar nada. O objeto contém todas as definições, incluindo a flag crucial que indica à biblioteca se ela pode acessar a internet.

## Etapa 2 – Desativar o Download Automático de Recursos  

Por padrão, o Aspose OCR tenta buscar arquivos de idioma ausentes em tempo real. Para manter tudo offline, altere o interruptor `AutoDownloadResources` para `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Dica de especialista:** Desligar isso não só garante privacidade, como também acelera a primeira execução de reconhecimento, pois o engine não perderá tempo verificando atualizações.

## Etapa 3 – Apontar para a Sua Pasta Local de Recursos  

Agora informe ao engine onde os pacotes de idioma pré‑baixados estão armazenados. Este é o caminho que você configurou nos pré‑requisitos.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **O que pode dar errado?** Se o caminho estiver errado ou o arquivo de idioma necessário estiver ausente, o engine lançará uma `ResourceNotFoundException`. Verifique a ortografia da pasta e se o modelo japonês (`jpn.traineddata`) está presente.

## Etapa 4 – Selecionar o Modelo de Idioma Local  

Escolha o idioma que realmente está disponível no disco. No nosso exemplo usamos japonês, mas você pode trocar `Language.Japanese` por qualquer outro idioma que tenha baixado.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Caso extremo:** Alguns idiomas exigem dicionários adicionais (por exemplo, chinês). Certifique‑se de que esses arquivos auxiliares também estejam na mesma pasta de recursos.

## Etapa 5 – Carregar a Imagem para OCR  

Aqui é onde **carregamos a imagem para OCR**. O método `ImageStream.FromFile` lê o arquivo para um stream que o Aspose pode processar.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Dica:** Formatos suportados incluem PNG, JPEG, BMP e TIFF. Se precisar lidar com PDFs, converta cada página para imagem primeiro.

## Etapa 6 – Executar o Processo de Reconhecimento  

Agora o engine realmente lê os pixels e tenta transformá‑los em texto.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Por que esta etapa pode ser lenta:** OCR consome muita CPU, especialmente para imagens de alta resolução. Se o desempenho for crítico, considere reduzir a escala da imagem antes do reconhecimento.

## Etapa 7 – Exibir o Texto Extraído  

Por fim, **extraímos texto de imagem** e o imprimimos no console.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Executar o programa deve exibir os caracteres japoneses que estavam em `japan_doc.png`. Se tudo estiver configurado corretamente, você verá um bloco limpo de texto Unicode no seu console.

### Saída Esperada

```
これはサンプルの日本語テキストです。
```

(Seu resultado real dependerá do conteúdo da imagem.)

## Armadilhas Comuns & Como Evitá‑las  

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Arquivo de idioma ausente** | `AutoDownloadResources` está false, então o engine não pode buscá‑lo. | Verifique se `ResourcesPath` aponta para a pasta que contém `jpn.traineddata`. |
| **Caminho da imagem incorreto** | `ImageStream.FromFile` lança `FileNotFoundException`. | Use caminhos absolutos ou garanta que o diretório de trabalho esteja configurado corretamente. |
| **Formato de imagem não suportado** | Aspose lê apenas determinados formatos. | Converta sua imagem para PNG ou JPEG antes de chamar `FromFile`. |
| **Falha por falta de memória em imagens grandes** | OCR carrega a imagem inteira na memória. | Redimensione ou divida a imagem em blocos, ou aumente o limite de memória do processo. |

## Expandindo o Exemplo  

- **Processamento em lote:** Percorra um diretório de imagens, chame o mesmo código de reconhecimento e grave cada resultado em um arquivo `.txt` separado.  
- **Idiomas diferentes:** Substitua `Language.Japanese` por `Language.English` (ou outro) após colocar os arquivos de recurso correspondentes.  
- **Pré‑processamento personalizado:** Use Aspose.Imaging para corrigir inclinação ou melhorar o contraste antes do OCR, obtendo maior precisão.

## Conclusão  

Agora você sabe **como desativar OCR** no Aspose OCR para C# e executá‑lo completamente offline. Ao definir `AutoDownloadResources` como `false`, apontar o engine para uma pasta local de recursos e **carregar imagem para OCR** corretamente, você pode **extrair texto de imagem** sem jamais tocar na internet. Essa abordagem é ideal para ambientes seguros, pipelines de CI ou qualquer cenário onde o acesso à rede seja limitado.

Pronto para o próximo passo? Experimente processar uma pasta inteira de PDFs escaneados, teste diferentes pacotes de idioma ou integre o resultado do OCR em um banco de dados pesquisável. A configuração offline que você construiu hoje é uma base sólida para qualquer fluxo de trabalho de processamento de documentos on‑premises.

Boa codificação, e sinta‑se à vontade para deixar um comentário se encontrar algum obstáculo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}