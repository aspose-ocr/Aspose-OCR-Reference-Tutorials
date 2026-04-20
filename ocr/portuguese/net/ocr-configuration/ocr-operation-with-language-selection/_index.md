---
date: 2026-02-25
description: Aprenda como extrair texto de imagens em C# usando Aspose.OCR para .NET.
  Este guia passo a passo mostra OCR multilíngue, seleção de idioma e dicas práticas.
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: Extrair texto de imagem em C# com seleção de idioma usando Aspose.OCR
url: /pt/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

 any markdown links: keep same.

Check for any code fences: there are none except placeholders.

We need to translate "Extract image text C# with language selection using Aspose.OCR" etc.

Let's translate.

Be careful with "step-by-step in order - do not skip sections". Provide full translation.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR

## Introdução

Se você precisa **extrair texto de imagem C#** de fotos e PDFs em uma aplicação .NET, o Aspose.OCR para .NET oferece uma solução rápida, precisa e sensível ao idioma. Neste tutorial vamos percorrer um exemplo do mundo real que demonstra o reconhecimento de imagem OCR com seleção de idioma, para que você possa obter texto multilíngue de imagens com apenas algumas linhas de código. Ao final, você verá como é fácil integrar OCR em seus projetos C# e por que essa abordagem é uma escolha sólida para cargas de trabalho de produção.

## Respostas rápidas
- **O que o Aspose.OCR faz?** Ele reconhece texto impresso e manuscrito em imagens e devolve o texto extraído.  
- **Posso escolher o idioma?** Sim – você pode especificar qualquer idioma suportado, como English, German, Spanish, Chinese, etc.  
- **Preciso de licença para desenvolvimento?** Um trial gratuito funciona para avaliação; uma licença é necessária para uso em produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **A correção de inclinação é automática?** Você pode habilitar `AutoSkew` e ajustar a configuração `SkewAngle`.  

## O que é “extrair texto de imagem C#”?

Extrair texto de imagem em C# significa usar uma biblioteca para ler o conteúdo visual de uma imagem (PNG, JPEG, TIFF, etc.) e convertê‑lo em texto pesquisável e editável. O Aspose.OCR fornece essa capacidade localmente, sem enviar dados a serviços externos, o que mantém seu fluxo de trabalho seguro e em conformidade.

## Por que escolher Aspose.OCR para tarefas de OCR?

- **Alta precisão** em múltiplas fontes e qualidades de imagem.  
- **Seleção de idioma integrada** elimina a necessidade de pacotes de idioma externos.  
- **API simples** que se integra de forma limpa a projetos C# existentes, facilitando **extrair texto de imagem C#**.  
- **Sem dependências externas** – tudo roda localmente, mantendo seus dados seguros.  

## Pré‑requisitos

Antes de mergulharmos no código, certifique‑se de que você tem os seguintes pré‑requisitos:

- Aspose.OCR para .NET: Garanta que a biblioteca Aspose.OCR esteja instalada. Você pode baixá‑la na [página de download do Aspose.OCR para .NET](https://releases.aspose.com/ocr/net/).

- Ambiente de desenvolvimento: Configure um ambiente de trabalho com uma aplicação .NET. Se ainda não fez isso, consulte a [documentação](https://reference.aspose.com/ocr/net/) para instruções detalhadas.

## Importar namespaces

Em sua aplicação .NET, comece importando os namespaces necessários:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Etapa 1: Inicializar Aspose.OCR

Comece inicializando uma instância da classe Aspose.OCR. Isso prepara o uso dos recursos de OCR dentro da sua aplicação.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Etapa 2: Especificar o caminho da imagem

Em seguida, defina o caminho da imagem que você deseja processar com OCR. Certifique‑se de que a imagem esteja acessível pela sua aplicação.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Etapa 3: Reconhecer a imagem com seleção de idioma

Agora vem a operação principal de OCR. Utilize a biblioteca Aspose.OCR para reconhecer texto da imagem especificada. Ajuste as configurações de reconhecimento, incluindo a seleção de idioma, para refinar o processo de **extrair texto de imagem C#**.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Etapa 4: Imprimir e exibir os resultados

Após a operação de OCR, imprima e exiba os resultados, incluindo o texto reconhecido, áreas, avisos e a representação em JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Problemas comuns e dicas

- **Seleção de idioma incorreta** – Se a saída parecer corrompida, verifique se a propriedade `Language` corresponde ao idioma da imagem de origem.  
- **Imagens inclinadas** – Habilite `AutoSkew` ou ajuste manualmente `SkewAngle` para melhorar a precisão em digitalizações inclinadas.  
- **Arquivos grandes** – Processar imagens grandes em partes ou reduzir a resolução antes de enviá‑las ao `RecognizeImage` ajuda a economizar memória.  

## Perguntas frequentes

**Q: O Aspose.OCR é adequado para reconhecimento de texto multilíngue?**  
A: Sim, o Aspose.OCR suporta vários idiomas, oferecendo flexibilidade para tarefas de OCR multilíngue.

**Q: Posso ajustar finamente as configurações de OCR para características específicas da imagem?**  
A: Absolutamente! Ajuste parâmetros como ângulo de inclinação, reconhecimento de linhas e detecção de áreas para otimizar o OCR em diferentes cenários.

**Q: Onde posso encontrar suporte adicional ou discussões da comunidade?**  
A: Visite o [fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para suporte e discussões com a comunidade.

**Q: Existe um trial gratuito disponível?**  
A: Sim, explore o [trial gratuito](https://releases.aspose.com/) para experimentar os recursos do Aspose.OCR.

**Q: Como posso comprar o Aspose.OCR para .NET?**  
A: Para comprar, acesse a [página de compra](https://purchase.aspose.com/buy).

## Conclusão

Parabéns! Você aprendeu **como extrair texto de imagem C#** com seleção de idioma usando Aspose.OCR para .NET. Este tutorial mostrou como configurar o motor OCR, selecionar o idioma apropriado e lidar com os resultados, proporcionando uma base sólida para construir recursos de extração de texto multilíngue em suas aplicações.

---

**Última atualização:** 2026-02-25  
**Testado com:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}