---
date: 2025-12-22
description: Aprenda como extrair texto de imagens usando Aspose.OCR para .NET. Este
  guia orienta você na preparação de retângulos para reconhecimento de imagem OCR
  e na melhoria da precisão.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Como extrair texto de imagem preparando retângulos no OCR
url: /pt/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preparar Retângulos no Reconhecimento Óptico de Caracteres (OCR)

## Introdução

O Reconhecimento Óptico de Caracteres (OCR) é essencial para converter conteúdo visual em texto pesquisável e editável. Neste tutorial você **extract text from image** preparando retângulos personalizados que focam o motor OCR em regiões específicas. Usando Aspose.OCR para .NET, percorreremos cada passo — desde a configuração do seu projeto até a obtenção do texto reconhecido — para que você possa integrar funcionalidade poderosa de imagem‑para‑texto em suas aplicações .NET.

## Respostas Rápidas
- **What does “extract text from image” mean?** Significa converter os caracteres visuais de uma imagem em cadeias legíveis por máquina.  
- **Which library helps with this in .NET?** Aspose.OCR for .NET.  
- **Preciso de uma licença para desenvolvimento?** Um teste gratuito funciona para testes; uma licença é necessária para produção.  
- **Posso direcionar áreas específicas?** Sim, definindo retângulos que limitam o escopo do OCR.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## O que é “extract text from image” com retângulos?
Quando você define zonas retangulares em uma imagem, o motor OCR processa apenas essas zonas. Isso melhora a precisão, reduz o tempo de processamento e permite ignorar fundos ruidosos ou seções irrelevantes.

## Por que preparar retângulos antes do OCR?
- **Focar no conteúdo relevante:** Ignorar cabeçalhos, rodapés ou gráficos decorativos.  
- **Aumentar o desempenho:** Regiões menores significam reconhecimento mais rápido.  
- **Melhorar a precisão:** Menos ruído visual resulta em resultados mais limpos.

## Prerequisites

- Familiaridade com C# e desenvolvimento .NET.  
- Aspose.OCR for .NET library installed – you can download it **[here](https://releases.aspose.com/ocr/net/)**.  
- Uma imagem de exemplo (por exemplo, `sample.png`) que contém o texto que você deseja extrair.

## Importar Namespaces

Primeiro, traga os namespaces necessários para o escopo:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Etapa 1: Configurar o Diretório do Documento

Especifique onde seus arquivos de imagem estão e crie uma instância do motor OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Como extrair texto de imagem usando múltiplos retângulos

### Etapa 2: Reconhecer Imagem com Múltiplos Retângulos

#### 2.1 Definir os retângulos

Crie uma lista de objetos `Rectangle` que delineiam as áreas que você deseja que o motor OCR escaneie.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Executar o reconhecimento OCR

Passe o caminho da imagem e a lista de retângulos para `RecognizeImage`. O método retorna uma coleção de strings — cada entrada corresponde a um retângulo.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Etapa 3: Reconhecer Imagem com Configurações de Reconhecimento (Abordagem Alternativa)

Se preferir usar `RecognitionSettings`, você pode obter o mesmo resultado com uma chamada de API ligeiramente diferente.

#### 3.1 Definir configurações de reconhecimento

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Exibir texto reconhecido

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problemas Comuns & Dicas

- **Coordenadas de retângulo incorretas:** Certifique-se de que os valores `X`, `Y`, `Width` e `Height` mapeiem corretamente para a região desejada.  
- **Qualidade da imagem:** Imagens de baixa resolução podem gerar resultados de OCR ruins; considere pré‑processamento (por exemplo, binarização).  
- **Resultados vazios:** Verifique se os retângulos realmente contêm texto; caso contrário, o motor retornará strings vazias.

## Conclusão

Agora você aprendeu como **extract text from image** preparando retângulos personalizados com Aspose.OCR para .NET. Esta técnica oferece controle detalhado sobre o processamento OCR, ajudando a criar recursos de extração de texto mais rápidos e precisos em suas aplicações.

## Frequently Asked Questions

**Q:** Posso usar Aspose.OCR para .NET com outros frameworks .NET?  
**A:** Sim, Aspose.OCR para .NET é compatível com vários frameworks .NET.

**Q:** Existe um teste gratuito disponível para Aspose.OCR para .NET?  
**A:** Absolutamente! Você pode acessar o teste gratuito **[here](https://releases.aspose.com/)**.

**Q:** Como obtenho suporte para Aspose.OCR para .NET?  
**A:** Visite o **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** para suporte dedicado.

**Q:** Posso obter uma licença temporária para fins de teste?  
**A:** Sim, você pode adquirir uma licença temporária **[here](https://purchase.aspose.com/temporary-license/)**.

**Q:** Onde posso encontrar a documentação para Aspose.OCR para .NET?  
**A:** A documentação está disponível **[here](https://reference.aspose.com/ocr/net/)**.

---

**Última atualização:** 2025-12-22  
**Testado com:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}