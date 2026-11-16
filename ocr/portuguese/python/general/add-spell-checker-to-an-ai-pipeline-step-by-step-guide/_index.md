---
category: general
date: 2026-08-12
description: Adicione verificador ortográfico ao seu pipeline de IA e aprenda como
  definir o pós-processador, adicionar pós-processamento e aplicar a verificação ortográfica
  em Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add spell checker
- add post processing
- use post processor
- apply spell checking
- how to set post processor
language: pt
lastmod: 2026-08-12
og_description: Adicione verificador ortográfico ao seu pipeline de IA. Este guia
  mostra como configurar o pós-processador, adicionar pós-processamento e aplicar
  a verificação ortográfica em poucos minutos.
og_image_alt: Diagram illustrating how to add spell checker as a post processor in
  an AI pipeline
og_title: Adicionar verificador ortográfico a um pipeline de IA – tutorial completo
  em Python
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  headline: Add spell checker to an AI pipeline – step‑by‑step guide
  type: TechArticle
- description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  name: Add spell checker to an AI pipeline – step‑by‑step guide
  steps:
  - name: Why this works
    text: '* **`SpellChecker`** encapsulates the logic for detecting and correcting
      misspelled tokens. * **`set_post_processor`** tells the pipeline to invoke the
      supplied object after the primary model finishes inference. * The configuration
      dictionary lets you customize behavior (language, custom dictionarie'
  - name: What the wrapper does
    text: 1. **Runs the original inference** and captures the raw output. 2. **Detects
      the appropriate entry point** (`process` method or callable) on the supplied
      processor. 3. **Calls the processor** with the result and any options you provided.
  - name: Handling edge cases
    text: '| Situation | Recommended approach | |----------------------------------------|--------------------------------------------------------------------|
      | Input contains domain‑specific terms | Provide a custom dictionary via the
      `options` parameter. | | Processor raises an exception | Wrap the call in '
  type: HowTo
tags:
- AI pipeline
- Python
- post‑processing
title: Adicionar verificador ortográfico a um pipeline de IA – guia passo a passo
url: /pt/python/general/add-spell-checker-to-an-ai-pipeline-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar verificador ortográfico a um pipeline de IA – guia passo a passo

Se você precisa **adicionar verificador ortográfico** a um pipeline de IA, este tutorial mostra exatamente como fazer isso. Você verá como definir um pós‑processador, adicionar pós‑processamento e aplicar a verificação ortográfica com a menor quantidade de código possível.

O guia cobre tudo, desde a instalação da biblioteca personalizada de verificação ortográfica até a sua integração em um pipeline existente. Ao final do artigo você poderá executar um exemplo completo de ponta a ponta que corrige erros de ortografia no texto gerado.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.9 ou superior instalado.  
* Um objeto de pipeline de IA que suporte pós‑processamento (por exemplo, um `TransformerPipeline` da biblioteca `transformers`).  
* Acesso ao pacote `my_spellchecker` ou a qualquer módulo de verificação ortográfica compatível.

Você não precisa de conhecimento profundo sobre os detalhes internos do pipeline; os passos abaixo tratam de todas as integrações necessárias.

## Como adicionar verificador ortográfico como pós‑processador

A ideia central é criar uma instância da classe de verificação ortográfica e registrá‑la no pipeline usando o método `set_post_processor`. Esse método aceita o objeto do processador e um dicionário de configuração opcional.

```python
# Step 1: Import the custom spell checker class
from my_spellchecker import SpellChecker

# Step 2: Create an instance of the spell checker
spell_checker = SpellChecker()

# Step 3: Attach the spell checker as a post‑processor to the AI pipeline,
#         providing any necessary options (e.g., language)
ai.set_post_processor(spell_checker, {"lang": "en"})
```

### Por que isso funciona

* **`SpellChecker`** encapsula a lógica para detectar e corrigir tokens com erros ortográficos.  
* **`set_post_processor`** informa ao pipeline que ele deve invocar o objeto fornecido após o modelo principal concluir a inferência.  
* O dicionário de configuração permite personalizar o comportamento (idioma, dicionários personalizados, etc.) sem alterar o código do processador.

## Adicionando pós‑processamento ao seu pipeline de IA

Se o seu pipeline ainda não expõe um método `set_post_processor`, você pode estendê‑lo por herança ou usando uma função wrapper. A seguir, um wrapper genérico que funciona com qualquer pipeline chamável.

```python
def add_post_processor(pipeline, processor, options=None):
    """
    Registers a post‑processor on a generic pipeline.
    """
    def wrapped(*args, **kwargs):
        # Run the original pipeline
        result = pipeline(*args, **kwargs)
        # Apply the post‑processor if it implements `process`
        if hasattr(processor, "process"):
            return processor.process(result, **(options or {}))
        # Fallback: assume processor is a callable
        return processor(result, **(options or {}))

    return wrapped

# Example usage with a Hugging Face pipeline
from transformers import pipeline as hf_pipeline

# Create the base pipeline (e.g., text generation)
base = hf_pipeline("text-generation", model="gpt2")

# Wrap it with the spell‑checking post processor
ai = add_post_processor(base, spell_checker, {"lang": "en"})
```

### O que o wrapper faz

1. **Executa a inferência original** e captura a saída bruta.  
2. **Detecta o ponto de entrada adequado** (`process` method ou callable) no processador fornecido.  
3. **Chama o processador** com o resultado e quaisquer opções que você tenha passado.  

Esse padrão permite **usar pós‑processadores** que não foram originalmente projetados para o pipeline, oferecendo total flexibilidade para adicionar verificação ortográfica ou qualquer outra lógica personalizada.

## Usando um pós‑processador para verificação ortográfica

Uma vez que o processador esteja anexado, você pode chamar o pipeline como de costume. A etapa de verificação ortográfica é executada automaticamente após o modelo gerar o texto.

```python
# Generate text that may contain spelling errors
raw_output = ai("Write a short paragraph about climate change.")

print("Raw output:", raw_output)
print("Corrected output:", ai.last_result)  # Assuming the wrapper stores the final result
```

**Saída esperada (exemplo):**

```
Raw output: ['Climte change is a global issue that affects all nations.']
Corrected output: ['Climate change is a global issue that affects all nations.']
```

Observe como a palavra escrita incorretamente *“Climte”* se transforma em *“Climate”* após a execução do verificador ortográfico. Isso demonstra que a etapa **apply spell checking** funciona de forma transparente.

### Lidando com casos extremos

| Situação                                 | Abordagem recomendada                                                |
|------------------------------------------|----------------------------------------------------------------------|
| Entrada contém termos específicos de domínio | Forneça um dicionário personalizado via o parâmetro `options`.      |
| Processador gera uma exceção             | Envolva a chamada em um bloco `try/except` e retorne o resultado bruto como fallback. |
| Vários pós‑processadores são necessários | Encadeie‑os aninhando chamadas `add_post_processor` ou criando um processador composto. |

## Como definir opções do pós‑processador dinamicamente

Pode ser necessário mudar o idioma ou as configurações de dicionário em tempo de execução. O método `set_post_processor` pode ser chamado novamente com uma nova configuração, sobrescrevendo a anterior.

```python
# Switch to French spell checking
ai.set_post_processor(spell_checker, {"lang": "fr"})
```

Chamar o método uma segunda vez **how to set post processor** substitui a configuração antiga, garantindo que gerações subsequentes utilizem o novo modelo de idioma.

## Dica profissional: testando sua integração de verificação ortográfica

Testes automatizados garantem que o verificador ortográfico continue funcional após alterações no código.

```python
import unittest

class TestSpellCheckerIntegration(unittest.TestCase):
    def test_correction(self):
        result = ai("The qick brown fox.")
        self.assertIn("quick", result[0].lower())

if __name__ == "__main__":
    unittest.main()
```

Executar este teste confirma que a etapa **add spell checker** modifica corretamente a saída.

## Resumo

Este guia mostrou como **add spell checker** a um pipeline de IA, como **add post processing**, e como **use post processor** para **apply spell checking**. Você aprendeu a **how to set post processor** opções, lidar com casos extremos e validar a integração com testes unitários.

A partir daqui você pode:

* Estender o padrão para outras tarefas de pós‑processamento, como filtragem de profanidade ou análise de sentimento.  
* Explorar os recursos avançados da biblioteca `my_spellchecker`, como sugestões contextuais.  
* Combinar múltiplos pós‑processadores para pipelines de saída mais ricas.

Experimente diferentes configurações e compartilhe suas descobertas com a comunidade. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais, com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Improve OCR Accuracy with Spell Checking in Images](/ocr/english/net/ocr-optimization/result-correction-with-spell-checking/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}