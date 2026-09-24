---
date: 2026-02-25
description: Aprenda como extrair texto de imagens usando Aspose.OCR para .NET. Este
  guia orienta você na preparação de retângulos para o reconhecimento de imagens OCR
  e na melhoria da precisão.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Como extrair texto de uma imagem preparando retângulos no OCR
url: /pt/net/ocr-optimization/prepare-rectangles/
weight: 11
---

 "Testado com:".

**Author:** Aspose -> "Autor:".

Then closing shortcodes.

Now produce final content.

Be careful to keep markdown formatting exactly.

Let's write.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prepare Retângulos no Reconhecimento de Imagem OCR

## Introdução

Optical Character Recognition (OCR) é essencial para converter conteúdo visual em texto pesquisável e editável. Neste tutorial você **extrairá texto de imagem** preparando retângulos personalizados que focam o motor OCR em regiões específicas. Usando Aspose.OCR for .NET, percorreremos cada passo — desde a configuração do seu projeto até a obtenção do texto reconhecido — para que você possa integrar funcionalidade poderosa de imagem‑para‑texto em suas aplicações .NET.

## Respostas Rápidas
- **O que significa “extrair texto de imagem”?** Significa converter os caracteres visuais de uma foto em sequências legíveis por máquina.  
- **Qual biblioteca ajuda com isso no .NET?** Aspose.OCR for .NET.  
- **Preciso de licença para desenvolvimento?** Um trial gratuito funciona para testes; uma licença é necessária para produção.  
- **Posso direcionar áreas específicas?** Sim, definindo retângulos que limitam o escopo do OCR.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## O que é “extrair texto de imagem” com retângulos?
Quando você define zonas retangulares em uma imagem, o motor OCR processa apenas essas zonas. Isso melhora a precisão, reduz o tempo de processamento e permite ignorar fundos ruidosos ou seções irrelevantes.

## Por que preparar retângulos antes do OCR?
- **Focar no conteúdo relevante:** Ignorar cabeçalhos, rodapés ou gráficos decorativos.  
- **Aumentar desempenho:** Regiões menores significam reconhecimento mais rápido.  
- **Melhorar precisão:** Menos ruído visual gera resultados mais limpos.

## Por que isso importa em projetos do mundo real
Muitos documentos empresariais — recibos, faturas, carteiras de identidade — possuem layouts mistos onde apenas certas partes contêm texto valioso. Ao usar retângulos, você pode extrair apenas os campos necessários, reduzindo drasticamente o trabalho de pós‑processamento e aumentando a confiabilidade geral da sua cadeia de automação.

## Casos de uso comuns
- **Automação de entrada de dados:** Capturar campos específicos de formulários escaneados.  
- **Verificações de conformidade:** Isolar e validar blocos de texto legal.  
- **Indexação de conteúdo:** Indexar apenas o título ou legenda de uma imagem para mecanismos de busca.  

## Pré-requisitos

- Familiaridade com C# e desenvolvimento .NET.  
- Biblioteca Aspose.OCR for .NET instalada – você pode baixá‑la **[aqui](https://releases.aspose.com/ocr/net/)**.  
- Uma imagem de exemplo (por exemplo, `sample.png`) que contenha o texto que você deseja extrair.

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

Especifique onde seus arquivos de imagem estão localizados e crie uma instância do motor OCR.

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

- **Coordenadas de retângulo incorretas:** Certifique‑se de que os valores `X`, `Y`, `Width` e `Height` mapeiam corretamente para a região desejada.  
- **Qualidade da imagem:** Imagens de baixa resolução podem gerar resultados ruins de OCR; considere pré‑processamento (por exemplo, binarização).  
- **Resultados vazios:** Verifique se os retângulos realmente contêm texto; caso contrário, o motor retornará strings vazias.

## Solução de Problemas e Melhores Práticas

| Sintoma | Causa Provável | Solução |
|---------|----------------|--------|
| Nenhuma saída ou strings vazias | Retângulos fora dos limites da imagem | Verifique novamente as dimensões da imagem e as coordenadas dos retângulos |
| Caracteres corrompidos | Baixo contraste ou ruído | Aplique limpeza de imagem (tons de cinza, limiar) antes do OCR |
| Desempenho lento em arquivos grandes | Muitos retângulos ou imagem muito grande | Divida a imagem ou reduza a quantidade de retângulos quando possível |

## Conclusão

Agora você aprendeu como **extrair texto de imagem** preparando retângulos personalizados com Aspose.OCR for .NET. Essa técnica oferece controle granular sobre o processamento OCR, ajudando a construir recursos de extração de texto mais rápidos e precisos em suas aplicações.

## Perguntas Frequentes

**Q:** Posso usar Aspose.OCR for .NET com outros frameworks .NET?  
**A:** Sim, Aspose.OCR for .NET é compatível com diversos frameworks .NET.

**Q:** Existe um trial gratuito disponível para Aspose.OCR for .NET?  
**A:** Absolutamente! Você pode acessar o trial gratuito **[aqui](https://releases.aspose.com/)**.

**Q:** Como obtenho suporte para Aspose.OCR for .NET?  
**A:** Visite o **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** para suporte dedicado.

**Q:** Posso obter uma licença temporária para fins de teste?  
**A:** Sim, você pode adquirir uma licença temporária **[aqui](https://purchase.aspose.com/temporary-license/)**.

**Q:** Onde encontro a documentação para Aspose.OCR for .NET?  
**A:** A documentação está disponível **[aqui](https://reference.aspose.com/ocr/net/)**.

---

**Última Atualização:** 2026-02-25  
**Testado com:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}