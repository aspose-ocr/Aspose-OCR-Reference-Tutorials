---
date: 2026-02-20
description: Aprenda a reconhecer retângulos de página usando Aspose.OCR para Java,
  extrair texto de imagens em projetos Java e siga este tutorial de Aspose OCR para
  Java para um OCR preciso.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Como reconhecer retângulos de página para reconhecimento de texto OCR no Aspose.OCR
url: /pt/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Reconhecer Retângulos de Página para Reconhecimento de Texto OCR no Aspose.OCR

Em pipelines modernos de automação de documentos, **recognize page rectangles** é a técnica chave que permite indicar ao motor OCR exatamente onde procurar. Ao limitar o Aspose.OCR às áreas que realmente contêm texto, você aumenta a velocidade, reduz o ruído e obtém resultados mais limpos. Neste tutorial percorreremos cada passo — configuração da biblioteca, licenciamento, definição de retângulos e, finalmente, chamada da API OCR — para que você possa extrair texto de qualquer imagem com confiança.

## Respostas Rápidas
- **Qual biblioteca lida com reconhecimento de texto OCR em Java?** Aspose.OCR for Java.  
- **Preciso de uma licença para uso em produção?** Sim — uma licença válida do Aspose.OCR desbloqueia todas as funcionalidades.  
- **Posso limitar o OCR a partes específicas de uma imagem?** Absolutamente; você define retângulos que delimitam as zonas-alvo.  
- **Quais são os principais pré‑requisitos?** JDK 17+, Aspose.OCR for Java e uma IDE Java.  
- **Esta abordagem é adequada para extrair texto de imagens?** Sim, é uma forma eficiente de **extract text image java** projects.

## O que é “recognize page rectangles”?
A expressão refere‑se à prática de fornecer uma lista de objetos `java.awt.Rectangle` ao motor OCR para que ele processe apenas essas regiões específicas de uma página. Essa abordagem focada reduz o tempo de processamento e melhora a precisão, especialmente em documentos complexos como faturas ou formulários.

## Por que Preparar Retângulos para o Reconhecimento de Texto OCR?
Definir retângulos foca o motor nas regiões que realmente contêm texto, o que:
* Reduz o tempo de processamento.  
* Melhora a precisão ao ignorar fundos ruidosos.  
* Permite extrair apenas os dados necessários — perfeito para formulários, faturas e recibos.  

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- **Java Development Kit (JDK)** – Aspose.OCR for Java funciona com JDK 17 ou superior. Baixe-o no site da Oracle.  
- **Aspose.OCR for Java library** – Obtenha o JAR mais recente na página oficial de download [aqui](https://releases.aspose.com/ocr/java/). Siga o guia de instalação [aqui](https://reference.aspose.com/ocr/java/).  
- **Ambiente de Desenvolvimento** – Qualquer IDE Java (IntelliJ IDEA, Eclipse, VS Code, etc.) serve.

## Importar Pacotes

No seu arquivo fonte Java, importe as classes necessárias do Aspose.OCR e as utilidades padrão do Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Importamos `java.awt.Rectangle` porque a API OCR espera retângulos que definem as regiões a serem escaneadas.*

## Etapa 1: Configurar a Licença

```java
SetLicense.main(null);
```

Chamar `SetLicense` ativa sua licença Aspose.OCR, removendo limites de avaliação e habilitando o reconhecimento completo de texto OCR.

## Etapa 2: Definir Diretório do Documento e Caminho da Imagem

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Substitua `"Your Document Directory"` pelo caminho absoluto onde sua imagem (`p.png`) está localizada. Esta é a imagem que será processada.

## Etapa 3: Criar Instância do Aspose.OCR

```java
AsposeOCR api = new AsposeOCR();
```

Instanciar `AsposeOCR` fornece acesso ao método `RecognizePage`, que realiza o OCR propriamente dito.

## Etapa 4: Preparar Retângulos com Texto

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Cada `Rectangle(x, y, width, height)` indica ao Aspose.OCR exatamente onde procurar texto. Ajuste as coordenadas para corresponder ao layout da sua imagem fonte.

## Etapa 5: Executar o Reconhecimento OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

A chamada `RecognizePage` processa apenas os retângulos definidos e devolve a string extraída. A saída no console permite verificar instantaneamente o resultado da **ocr text recognition**.

## Problemas Comuns e Dicas

| Problema | Causa | Solução |
|----------|-------|----------|
| **Nenhuma saída** | Coordenadas de retângulo ou caminho da imagem incorretos | Verifique o valor de `dataDir` e assegure‑se de que os retângulos realmente cobrem as regiões de texto. |
| **Caracteres estranhos** | Imagem de baixa resolução ou fonte não suportada | Use uma fonte de maior resolução ou aplique pré‑processamento de imagem (ex.: binarização). |
| **Licença não aplicada** | `SetLicense` não chamado antes do OCR | Garanta que `SetLicense.main(null);` seja executado antes de quaisquer chamadas de API. |
| **Desempenho lento** | Muitos retângulos grandes | Reduza o número de retângulos e mantenha‑os o mais ajustado possível ao texto. |

## Perguntas Frequentes

**P:** *O Aspose.OCR é compatível com outras linguagens de programação?*  
**R:** Sim, o Aspose.OCR também oferece suporte a .NET, C++ e Python. Consulte a documentação oficial para exemplos específicos de cada linguagem.

**P:** *Posso usar o Aspose.OCR em um projeto comercial?*  
**R:** Absolutamente. Adquira uma licença comercial através da [loja Aspose](https://purchase.aspose.com/buy).

**P:** *Existe uma versão de avaliação gratuita?*  
**R:** Sim, você pode baixar a versão de avaliação [aqui](https://releases.aspose.com/).

**P:** *Como obtenho uma licença temporária para avaliação?*  
**R:** Licenças temporárias são fornecidas pelo [portal de licenças temporárias da Aspose](https://purchase.aspose.com/temporary-license/).

**P:** *Onde posso obter suporte da comunidade?*  
**R:** Visite o [fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para perguntas, dicas e exemplos de código.

## Conclusão

Agora você aprendeu a **reconhecer retângulos de página** com Aspose.OCR para Java, configurar a licença, definir caminhos de imagem e — mais importante — preparar retângulos precisos para focar o OCR nas partes exatas da imagem que você precisa. Esta técnica é ideal para qualquer **aspose ocr java tutorial** que exija extração de texto precisa e de alto desempenho.

---

**Last Updated:** 2026-02-20  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}