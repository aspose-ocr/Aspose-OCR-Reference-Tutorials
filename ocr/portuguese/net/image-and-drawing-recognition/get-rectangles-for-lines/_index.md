---
date: 2025-12-17
description: Aprenda como obter retângulos de linhas OCR usando Aspose.OCR para .NET
  para reconhecer linhas de texto em imagens e extrair facilmente as coordenadas das
  linhas.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Obter Retângulos de Linhas OCR para Linhas de Texto da Imagem
url: /pt/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter Retângulos de Linhas OCR para Linhas de Texto em Imagem

## Introdução

Neste tutorial você descobrirá **como obter retângulos de linhas OCR** com Aspose.OCR para .NET. Ao final do guia você será capaz de **reconhecer linhas de texto em uma imagem** e **extrair coordenadas de linhas** para cada linha detectada — perfeito para processamento posterior, como análise de layout, extração de dados ou renderização personalizada.

## Respostas Rápidas
- **O que significa “obter retângulos de linhas OCR”?** Retorna as caixas delimitadoras de cada linha de texto detectada em uma imagem.  
- **Qual método da API é usado?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Preciso de licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Formatos de imagem suportados?** PNG, JPEG, BMP, TIFF e mais.  
- **Posso executar isso no .NET Core?** Sim, Aspose.OCR suporta totalmente .NET Core e .NET 5/6.

## Pré-requisitos

Antes de mergulhar no tutorial, certifique-se de que você tem os seguintes pré-requisitos configurados:

- Conhecimento básico de C# e desenvolvimento .NET.  
- Um ambiente de desenvolvimento integrado (IDE) como o Visual Studio.  
- Biblioteca Aspose.OCR para .NET instalada. Você pode baixá-la [aqui](https://releases.aspose.com/ocr/net/).  
- Uma imagem de exemplo contendo texto para reconhecimento OCR.

## Importar Namespaces

Certifique-se de que os namespaces necessários estejam importados no seu projeto. Adicione as linhas a seguir ao início do seu arquivo C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Agora, vamos dividir o processo de obtenção de retângulos para linhas no reconhecimento de imagem OCR em etapas fáceis de seguir.

## Etapa 1: Configurar o Diretório do Documento

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Substitua `"Your Document Directory"` pelo caminho real da pasta que contém sua imagem de exemplo.

## Etapa 2: Inicializar Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crie uma instância da classe `AsposeOcr` para acessar a funcionalidade OCR.

## Etapa 3: Especificar o Caminho da Imagem

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Defina o caminho completo da imagem na qual você deseja executar OCR.

## Etapa 4: Reconhecer a Imagem e Obter Retângulos

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

O método `GetRectangles` retorna uma lista de objetos `Rectangle`, cada um representando as coordenadas de uma linha de texto detectada. Este é o núcleo de **obter retângulos de linhas OCR**.

## Etapa 5: Imprimir Resultado

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Imprima as coordenadas das áreas detectadas no console. Você verá valores que poderá usar posteriormente para **extrair coordenadas de linhas** para processamento personalizado.

## Por que Usar Aspose.OCR para Retângulos de Linhas?

- **Alta precisão** – Algoritmos avançados detectam linhas mesmo em imagens ruidosas ou inclinadas.  
- **Multiplataforma** – Funciona no .NET Framework, .NET Core e .NET 5/6.  
- **Sem dependências externas** – Biblioteca .NET pura, sem DLLs nativas para distribuir.  
- **Saída rica** – Além de retângulos de linhas, você também pode recuperar palavras, caracteres e pontuações de confiança.

## Problemas Comuns e Soluções

| Problema | Solução |
|----------|---------|
| **Nenhum retângulo retornado** | Certifique-se de que a imagem contenha texto claro e horizontal e que `AreasType.LINES` esteja especificado. |
| **Coordenadas incorretas** | Verifique o DPI da imagem; imagens de baixa resolução podem causar limites imprecisos. |
| **Gargalo de desempenho em imagens grandes** | Redimensione a imagem para uma resolução razoável antes de chamar `GetRectangles`. |
| **Exceção de licença** | Use uma licença de teste para avaliação; aplique uma licença completa para produção para evitar limites de avaliação. |

## Perguntas Frequentes

**Q: Posso extrair palavras individuais em vez de linhas completas?**  
A: Sim, use `AreasType.WORDS` com o mesmo método `GetRectangles` para obter caixas delimitadoras ao nível de palavra.

**Q: A API suporta PDFs de várias páginas?**  
A: Converta cada página do PDF em uma imagem primeiro, então chame `GetRectangles` em cada imagem.

**Q: Como lidar com texto rotacionado?**  
A: Ative a opção de auto‑rotação nas configurações do OCR ou pré-rotacione a imagem antes do processamento.

**Q: Existe uma forma de obter pontuações de confiança para cada linha?**  
A: Após obter os retângulos, chame `api.RecognizeImage(...).Lines` para acessar objetos de linha que incluem valores de confiança.

**Q: Quais versões do .NET são compatíveis?**  
A: A biblioteca funciona com .NET Framework 4.5+, .NET Core 3.1+, e .NET 5/6.

## Conclusão

Parabéns! Você obteve com sucesso **retângulos de linhas OCR** para uma imagem usando Aspose.OCR para .NET. Com as caixas delimitadoras em mãos, você pode agora alimentar as coordenadas das linhas em fluxos de trabalho posteriores, como renderização personalizada, extração de dados ou análise de layout.

---

**Última atualização:** 2025-12-17  
**Testado com:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}