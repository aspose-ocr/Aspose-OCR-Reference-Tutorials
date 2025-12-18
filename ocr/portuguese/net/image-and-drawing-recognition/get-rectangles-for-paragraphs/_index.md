---
date: 2025-12-17
description: Aprenda a extrair retângulos para parágrafos em imagens OCR usando Aspose.OCR
  para .NET – o guia definitivo sobre como extrair retângulos e coordenadas de parágrafos.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Como Extrair Retângulos para Parágrafos no Reconhecimento de Imagens OCR
url: /pt/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Extrair Retângulos para Parágrafos no Reconhecimento de Imagens OCR

## Introdução

Bem-vindo ao nosso guia abrangente sobre **how to extract rectangles** para parágrafos no reconhecimento de imagens OCR com Aspose.OCR para .NET. Se você deseja melhorar seu pipeline de processamento de documentos, extrair os limites dos parágrafos e automatizar a extração de dados, está no lugar certo. Vamos percorrer cada passo — desde a configuração do ambiente até a impressão das coordenadas dos retângulos — para que você possa começar a usar os resultados do OCR imediatamente.

## Respostas Rápidas
- **O que significa “extract rectangles”?** Ele retorna as caixas delimitadoras (x, y, largura, altura) das áreas de texto detectadas.  
- **Qual método da API fornece os retângulos?** `AsposeOcr.GetRectangles` com `AreasType.PARAGRAPHS`.  
- **Preciso de uma licença para desenvolvimento?** Uma avaliação gratuita funciona para testes; uma licença comercial é necessária para produção.  
- **Posso processar várias imagens de uma vez?** Sim — faça um loop sobre sua lista de imagens e chame `GetRectangles` para cada arquivo.  
- **Quais formatos são suportados?** PNG, JPEG, TIFF, BMP e muitos outros.

## O que é “how to extract rectangles” em OCR?

Na terminologia de OCR, extrair retângulos significa identificar os limites geométricos que envolvem cada parágrafo ou linha de texto dentro de uma imagem. Essas coordenadas permitem que você destaque, recorte ou analise mais detalhadamente seções específicas de um documento escaneado.

## Por que extrair coordenadas de parágrafos?
- **Processamento pós‑processamento preciso** – você pode alimentar cada retângulo em fluxos de trabalho subsequentes (por exemplo, tradução, redação).  
- **UI/UX aprimorado** – sobreponha caixas delimitadoras na imagem original para mostrar aos usuários onde o texto foi encontrado.  
- **Automação em lote** – localize e isole rapidamente parágrafos em grandes conjuntos de documentos.

## Pré-requisitos

- Conhecimento básico de C# e desenvolvimento .NET.  
- Um ambiente de desenvolvimento com Aspose.OCR para .NET instalado – você pode baixá-lo [aqui](https://releases.aspose.com/ocr/net/).  
- Familiaridade com conceitos de processamento de imagem e por que OCR é essencial para extrair texto de arquivos escaneados.

## Importar Namespaces

No seu arquivo C#, importe os namespaces necessários para que as classes OCR estejam disponíveis:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Etapa 1: Configurar o Diretório do Documento

Defina a pasta que contém as imagens que você deseja analisar:

```csharp
string dataDir = "Your Document Directory";
```

## Etapa 2: Inicializar a Instância AsposeOcr

Crie um objeto `AsposeOcr` – isso lhe dá acesso a todas as funções OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Etapa 3: Especificar o Caminho da Imagem

Aponte para o arquivo de imagem exato que você deseja processar:

```csharp
string fullPath = dataDir + "sample.png";
```

## Etapa 4: Reconhecer a Imagem e Obter Retângulos de Parágrafos

Chame o método `GetRectangles`. Definir `detect_areas` como `true` indica ao motor que retorne retângulos de **parágrafo**:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Etapa 5: Imprimir Resultados

Exiba as coordenadas para que você possa ver as **coordenadas de extração de parágrafo** que foram detectadas:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Problemas Comuns e Soluções

| Problema | Motivo | Correção |
|----------|--------|----------|
| Nenhum retângulo retornado | Qualidade da imagem muito baixa ou `AreasType` incorreto | Garanta que a imagem esteja nítida e use `AreasType.PARAGRAPHS`. |
| Coordenadas com deslocamento de um | Incompatibilidade de escala DPI | Defina o DPI correto ao carregar a imagem ou use `api.Config.Dpi`. |
| Exceção de licença | Executando sem uma licença válida em produção | Aplique uma licença temporária ou permanente via `api.SetLicense`. |

## Perguntas Frequentes

**P: O Aspose.OCR é compatível com diferentes formatos de imagem?**  
R: Sim, o Aspose.OCR suporta PNG, JPEG, TIFF, BMP e muitos outros formatos comuns.

**P: Posso usar o Aspose.OCR para processamento em lote de várias imagens?**  
R: Absolutamente! Percorra uma coleção de caminhos de arquivos e chame `GetRectangles` para cada imagem.

**P: Existe uma avaliação gratuita disponível para Aspose.OCR para .NET?**  
R: Sim, você pode experimentar uma avaliação gratuita [aqui](https://releases.aspose.com/).

**P: Como posso obter uma licença temporária para o Aspose.OCR?**  
R: Você pode adquirir uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).

**P: Onde posso encontrar suporte adicional e discussões relacionadas ao Aspose.OCR?**  
R: Acesse o [fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para suporte da comunidade e discussões.

## Conclusão

Neste tutorial, mostramos **how to extract rectangles** para parágrafos usando Aspose.OCR para .NET, percorremos cada trecho de código e explicamos como interpretar as coordenadas retornadas. Ao integrar essas etapas em sua aplicação, você pode extrair de forma confiável os limites dos parágrafos, aprimorar fluxos de trabalho de documentos e criar soluções OCR mais inteligentes.

---

**Última atualização:** 2025-12-17  
**Testado com:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}