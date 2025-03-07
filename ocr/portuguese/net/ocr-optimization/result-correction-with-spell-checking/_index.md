---
title: Correção de resultados com verificação ortográfica no reconhecimento de imagem OCR
linktitle: Correção de resultados com verificação ortográfica no reconhecimento de imagem OCR
second_title: API Aspose.OCR .NET
description: Aumente a precisão do OCR com Aspose.OCR para .NET. Corrija a ortografia, personalize dicionários e obtenha reconhecimento de texto sem erros sem esforço.
weight: 13
url: /pt/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Correção de resultados com verificação ortográfica no reconhecimento de imagem OCR

## Introdução

No domínio do reconhecimento óptico de caracteres (OCR), obter resultados precisos é crucial para extrair informações significativas das imagens. Um desafio comum é lidar com palavras com erros ortográficos no processo de reconhecimento. Felizmente, Aspose.OCR for .NET oferece uma solução poderosa para aprimorar os resultados de OCR por meio da verificação ortográfica.

Este tutorial irá guiá-lo através do processo de correção de resultados com verificação ortográfica usando Aspose.OCR for .NET. Ao final, você estará equipado para melhorar a precisão do texto derivado de OCR, garantindo uma saída mais refinada e livre de erros.

## Pré-requisitos

Antes de mergulharmos na magia da verificação ortográfica, certifique-se de ter os seguintes pré-requisitos em vigor:

-  Biblioteca Aspose.OCR para .NET: Baixe e instale a biblioteca Aspose.OCR do[página de lançamento](https://releases.aspose.com/ocr/net/).

- Diretório de documentos: certifique-se de ter um diretório designado para seus documentos. Substitua “Seu diretório de documentos” nos trechos de código pelo caminho real.

## Importar namespaces

Vamos começar importando os namespaces necessários no seu projeto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Etapa 1: inicializar Aspose.OCR

Inicialize uma instância de Aspose.OCR para iniciar o processo de OCR.

```csharp
// O caminho para o diretório de documentos.
string dataDir = "Your Document Directory";

// Inicialize uma instância do AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Etapa 2: reconhecer a imagem

A seguir, reconheça o texto em uma imagem usando Aspose.OCR. Aqui está um trecho demonstrando esse processo:

```csharp
// Reconhecer imagem
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Etapa 3: antes da correção

Recupere o resultado do OCR antes da correção para comparar com a versão corrigida.

```csharp
// Obter resultado
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Etapa 4: após a correção

Aplique a verificação ortográfica para obter o resultado corrigido. O trecho de código a seguir ilustra esta etapa:

```csharp
// Obtenha resultado corrigido
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Etapa 5: palavras e sugestões com erros ortográficos

Obtenha uma lista de palavras com erros ortográficos junto com sugestões de correções usando o seguinte código:

```csharp
// Obtenha uma lista de palavras com erros ortográficos com sugestões
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Etapa 6: corrigir o texto do usuário

Corrija o texto específico fornecido pelo usuário usando a biblioteca Aspose.OCR:

```csharp
// Texto correto do usuário
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Passo 7: Correção com Dicionário do Usuário

Melhore ainda mais a correção incorporando um dicionário de usuário personalizado:

```csharp
// Obtenha o resultado corrigido com o dicionário do usuário
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Conclusão

Parabéns! Você navegou com sucesso pelos recursos de verificação ortográfica do Aspose.OCR for .NET. Este recurso permite refinar os resultados do OCR, garantindo precisão e eliminando erros.

## Perguntas frequentes

### Q1: Posso usar o Aspose.OCR para outros idiomas além do inglês?

A1: Sim, Aspose.OCR oferece suporte a vários idiomas. Ajuste as configurações de idioma de acordo.

### Q2: Como integro o Aspose.OCR ao meu projeto .NET?

 A2: Consulte o[documentação](https://reference.aspose.com/ocr/net/) para etapas de integração detalhadas.

### Q3: Existe uma versão de teste disponível para Aspose.OCR?

 A3: Sim, você pode explorar os recursos com o[versão de teste gratuita](https://releases.aspose.com/).

### P4: Posso fazer upload de um dicionário personalizado para verificação ortográfica?

A4: Com certeza! O tutorial demonstra como aprimorar a correção usando um dicionário fornecido pelo usuário.

### Q5: Onde posso procurar suporte para Aspose.OCR?

 A5: Visite o[Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para apoio e orientação da comunidade.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
