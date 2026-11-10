---
date: 2026-02-22
description: Aprenda a realizar análise de layout OCR reconhecendo linhas de texto
  em uma imagem e extraindo retângulos de linha usando Aspose.OCR para .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Análise de Layout OCR – Obter Retângulos de Linhas a partir de Imagens
url: /pt/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Análise de Layout OCR – Obter Retângulos de Linha a partir de Imagens

## Introdução

Neste tutorial você descobrirá **como obter retângulos de linha OCR** com Aspose.OCR para .NET. Ao final do guia você será capaz de **reconhecer linhas de texto em uma imagem** e **extrair as coordenadas das linhas** para cada linha detectada — ideal para processamento posterior, como **análise de layout OCR**, extração de dados ou renderização personalizada.

## Respostas Rápidas
- **O que significa “obter retângulos de linha OCR”?** Retorna as caixas delimitadoras de cada linha de texto detectada em uma imagem.  
- **Qual método da API é usado?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Preciso de licença?** Uma avaliação gratuita funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Formatos de imagem suportados?** PNG, JPEG, BMP, TIFF e outros.  
- **Posso executar isso no .NET Core?** Sim, Aspose.OCR oferece suporte total ao .NET Core e .NET 5/6.

## Pré‑requisitos

Antes de mergulhar no tutorial, certifique‑se de que você possui os seguintes pré‑requisitos:

- Conhecimento básico de C# e desenvolvimento .NET.  
- Um ambiente de desenvolvimento integrado (IDE) como o Visual Studio.  
- Biblioteca Aspose.OCR para .NET instalada. Você pode baixá‑la [aqui](https://releases.aspose.com/ocr/net/).  
- Uma imagem de exemplo contendo texto para reconhecimento OCR.

## Importar Namespaces

Garanta que os namespaces necessários estejam importados no seu projeto. Adicione as linhas a seguir ao topo do seu arquivo C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Agora, vamos dividir o processo de obtenção de retângulos para linhas no reconhecimento de imagem OCR em etapas fáceis de seguir.

## análise de layout ocr – Guia Passo a Passo

### Etapa 1: Configurar o Diretório do Seu Documento

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Substitua `"Your Document Directory"` pelo caminho real da pasta que contém sua imagem de exemplo.

### Etapa 2: Inicializar Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crie uma instância da classe `AsposeOcr` para acessar a funcionalidade OCR.

### Etapa 3: Especificar o Caminho da Imagem

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Defina o caminho completo da imagem na qual você deseja executar o OCR.

### Etapa 4: Reconhecer a Imagem e Obter Retângulos

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

O método `GetRectangles` retorna uma lista de objetos `Rectangle`, cada um representando as coordenadas de uma linha de texto detectada. Este é o núcleo de **obter retângulos de linha OCR** e permite **análise de layout OCR**.

### Etapa 5: Imprimir o Resultado

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Imprima as coordenadas das áreas detectadas no console. Você verá valores que poderão ser usados posteriormente para **extrair coordenadas de linha** para processamento personalizado.

## Por que usar Aspose.OCR para Retângulos de Linha?

- **Alta precisão** – Algoritmos avançados detectam linhas mesmo em imagens ruidosas ou inclinadas.  
- **Multiplataforma** – Funciona no .NET Framework, .NET Core e .NET 5/6.  
- **Sem dependências externas** – Biblioteca pura .NET, sem DLLs nativas para distribuir.  
- **Saída rica** – Além dos retângulos de linha, você também pode recuperar palavras, caracteres e pontuações de confiança.

## Problemas Comuns e Soluções

| Problema | Solução |
|----------|---------|
| **Nenhum retângulo retornado** | Verifique se a imagem contém texto claro e horizontal e se `AreasType.LINES` está especificado. |
| **Coordenadas incorretas** | Confirme o DPI da imagem; imagens de baixa resolução podem gerar limites imprecisos. |
| **Gargalo de desempenho em imagens grandes** | Redimensione a imagem para uma resolução razoável antes de chamar `GetRectangles`. |
| **Exceção de licença** | Use uma licença de avaliação para testes; aplique uma licença completa para produção e evite limites de avaliação. |

## Perguntas Frequentes

**P: Posso extrair palavras individuais em vez de linhas completas?**  
R: Sim, use `AreasType.WORDS` com o mesmo método `GetRectangles` para obter caixas delimitadoras ao nível de palavra.

**P: A API suporta PDFs de várias páginas?**  
R: Converta cada página do PDF em uma imagem primeiro, depois chame `GetRectangles` em cada imagem.

**P: Como lidar com texto rotacionado?**  
R: Ative a opção de auto‑rotação nas configurações do OCR ou pré‑roteie a imagem antes do processamento.

**P: Existe uma forma de obter pontuações de confiança para cada linha?**  
R: Após obter os retângulos, chame `api.RecognizeImage(...).Lines` para acessar objetos de linha que incluem valores de confiança.

**P: Quais versões do .NET são compatíveis?**  
R: A biblioteca funciona com .NET Framework 4.5+, .NET Core 3.1+ e .NET 5/6.

## Casos de Uso no Mundo Real

- **Análise de layout de documentos OCR** – Alimente os retângulos de linha em um motor de layout para reconstruir estruturas de colunas.  
- **Extração automática de dados** – Use as coordenadas para recortar linhas individuais para pipelines de NLP posteriores.  
- **Renderização personalizada** – Sobreponha caixas delimitadoras na imagem original para verificação visual ou sobreposições de UI.  

## Conclusão

Parabéns! Você obteve com sucesso **retângulos de linha OCR** para uma imagem usando Aspose.OCR para .NET. Com as caixas delimitadoras em mãos, agora você pode alimentar as coordenadas de linha em fluxos de trabalho posteriores, como renderização personalizada, extração de dados ou **análise de layout OCR**.

---

**Última atualização:** 2026-02-22  
**Testado com:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}