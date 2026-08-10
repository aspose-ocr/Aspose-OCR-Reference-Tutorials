---
date: 2026-07-23
description: Aprenda como extrair texto de imagens usando Aspose.OCR for .NET, preparando
  retângulos para melhorar a precisão do OCR e converter imagens em texto de forma
  eficiente.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Prepare Retângulos no Reconhecimento de Imagens OCR
og_description: Extrair texto de imagem usando Aspose.OCR for .NET. Aprenda a preparar
  retângulos, aumentar a precisão do OCR e converter imagens em texto de forma eficiente.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Extrair Texto de Imagem com Retângulos – Guia OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Extrair Texto de Imagem com Retângulos – Guia OCR
url: /pt/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem com Retângulos – Guia de OCR

## Introdução

O Reconhecimento Óptico de Caracteres (OCR) permite que você **extraia texto de imagem** de arquivos, tornando-os pesquisáveis e editáveis. Neste tutorial, mostraremos como melhorar a precisão do OCR preparando retângulos personalizados que focam o motor nas zonas exatas que você precisa. Usando Aspose.OCR para .NET, você verá todo o fluxo de trabalho — desde a configuração do projeto até a recuperação das strings reconhecidas — para que possa incorporar uma conversão confiável de imagem‑para‑texto em qualquer aplicação .NET.

## Respostas Rápidas
- **O que significa “extrair texto de imagem”?** Converte caracteres visuais em uma foto em strings legíveis por máquina.  
- **Qual biblioteca lida com isso no .NET?** Aspose.OCR para .NET fornece um motor OCR completo.  
- **Preciso de uma licença para produção?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para implantação.  
- **Posso limitar o OCR a zonas específicas?** Sim — defina retângulos para focar apenas nas áreas que contêm texto útil.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## O que é “extrair texto de imagem” com retângulos?
O processo `extract text from image` lê caracteres dentro de zonas retangulares definidas, ignorando todo o resto. Ao limitar o OCR a essas zonas, você obtém maior precisão, processamento mais rápido e menos esforço de pós‑processamento. Essa abordagem isola o texto que você deseja enquanto descarta gráficos de fundo, elementos decorativos e outros ruídos visuais que podem confundir o motor OCR.

## Por que preparar retângulos antes do OCR?
Preparar retângulos permite concentrar o motor OCR nas partes mais relevantes de uma imagem, o que melhora tanto a velocidade quanto a precisão. Ao reduzir a área de análise, você diminui a quantidade de dados que o motor precisa examinar, resultando em resultados mais rápidos e menos erros de reconhecimento causados por ruído visual desnecessário.

- **Focar no conteúdo relevante:** Ignorar cabeçalhos, rodapés ou gráficos decorativos que confundiriam o motor.  
- **Aumentar desempenho:** Regiões menores exigem menos cálculos, reduzindo o tempo de execução em até 40 % em digitalizações grandes.  
- **Melhorar precisão:** Reduzir o ruído visual eleva as taxas de reconhecimento de caracteres de ~85 % para >95 % em documentos ruidosos.

## Por que isso importa em projetos reais
Muitos documentos empresariais — recibos, faturas, cartões de identidade — misturam texto com logotipos ou códigos de barras. Ao desenhar retângulos ao redor dos campos que você realmente precisa, você extrai apenas os dados valiosos, reduzindo drasticamente o trabalho de limpeza posterior e aumentando a confiabilidade dos fluxos de trabalho automatizados. Essa extração direcionada diminui o esforço de pós‑processamento e ajuda a manter a conformidade com os padrões de manuseio de dados.

## Casos de uso comuns
- **Automação de entrada de dados:** Extrair campos específicos de formulários escaneados ou recibos de despesas.  
- **Verificações de conformidade:** Isolar cláusulas legais ou declarações regulatórias para verificação.  
- **Indexação de conteúdo:** Indexar apenas o título ou a legenda de uma imagem para visibilidade em mecanismos de busca.

## Pré-requisitos

- Conhecimento básico de C# e desenvolvimento .NET.  
- Biblioteca Aspose.OCR para .NET instalada – faça o download **[aqui](https://releases.aspose.com/ocr/net/)** ou navegue por todas as versões **[aqui](https://releases.aspose.com/)**.  
- Uma imagem de exemplo (por exemplo, `sample.png`) que contém o texto que você deseja extrair.

## Importar Namespaces

As instruções `using` trazem o motor OCR e as classes de geometria para o escopo.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Etapa 1: Configurar seu Diretório de Documentos

Especifique a pasta que contém suas imagens e crie uma instância do motor OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Como extrair texto de imagem usando múltiplos retângulos
Carregue a imagem uma única vez, depois forneça uma lista de retângulos ao motor OCR. Cada retângulo define uma região de interesse, e o motor retorna uma string separada para cada região, permitindo que você manipule os campos individualmente e combine os resultados conforme necessário.

### Definir os retângulos

Objetos `Rectangle` descrevem as coordenadas X‑Y e o tamanho de cada zona que você deseja escanear.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Executar reconhecimento OCR

O método `RecognizeImage` processa a imagem usando a lista de retângulos fornecida e retorna o texto reconhecido para cada região.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Como extrair texto de imagem usando RecognitionSettings (Abordagem Alternativa)
Se você preferir uma chamada baseada em configurações, pode obter o mesmo resultado com `RecognitionSettings`. Esse objeto permite agrupar definições de retângulos junto com idioma, DPI e outras opções de OCR, proporcionando uma chamada de API limpa e de parâmetro único.

### Definir configurações de reconhecimento

`RecognitionSettings` permite agrupar a lista de retângulos e opções adicionais (por exemplo, idioma, DPI) em um único objeto.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Exibir texto reconhecido

Itere sobre as strings retornadas e exiba o texto de cada região.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problemas Comuns & Dicas

- **Coordenadas de retângulo incorretas:** Verifique se `X`, `Y`, `Width` e `Height` correspondem à área pretendida.  
- **Qualidade da imagem:** Imagens de baixa resolução ou altamente comprimidas degradam os resultados do OCR; considere pré‑processamento como binarização.  
- **Resultados vazios:** Certifique-se de que os retângulos realmente contenham texto legível; caso contrário, o motor retornará strings vazias.

## Solução de Problemas e Melhores Práticas

| Sintoma | Causa Provável | Solução |
|---------|----------------|--------|
| Nenhuma saída ou strings vazias | Retângulos fora dos limites da imagem | Verifique novamente as dimensões da imagem e as coordenadas dos retângulos |
| Caracteres ilegíveis | Baixo contraste ou ruído | Aplicar conversão para escala de cinza e limiarização antes do OCR |
| Desempenho lento em arquivos grandes | Muitos retângulos ou imagem muito grande | Divida a imagem ou reduza a quantidade de retângulos quando possível |

## Conclusão

Agora você sabe como **extrair texto de imagem** preparando retângulos personalizados com Aspose.OCR para .NET. Essa abordagem oferece controle preciso sobre o processamento OCR, proporcionando recursos de extração de texto mais rápidos e precisos para qualquer solução .NET.

## Perguntas Frequentes

**Q:** Posso usar Aspose.OCR para .NET com outros frameworks .NET?  
**A:** Sim, Aspose.OCR para .NET funciona com .NET Framework 4.5+, .NET Core 3.1+, e .NET 5/6/7.

**Q:** Existe uma versão de teste gratuita disponível?  
**A:** Absolutamente! Baixe a versão de teste **[aqui](https://releases.aspose.com/)**.

**Q:** Onde posso obter suporte para Aspose.OCR para .NET?  
**A:** Visite o **[fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** para assistência dedicada.

**Q:** Posso obter uma licença temporária para testes?  
**A:** Sim, uma licença temporária está disponível **[aqui](https://purchase.aspose.com/temporary-license/)**.

**Q:** Onde está a documentação oficial?  
**A:** A referência completa da API está localizada **[aqui](https://reference.aspose.com/ocr/net/)**.

---

**Última Atualização:** 2026-07-23  
**Testado Com:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriais Relacionados

- [Como Extrair Retângulos para Parágrafos no Reconhecimento de Imagem OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Como Fazer OCR em Imagem – Executar OCR em Imagem no Reconhecimento de Imagem OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Como Extrair Texto de Imagem Usando Aspose.OCR para .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}