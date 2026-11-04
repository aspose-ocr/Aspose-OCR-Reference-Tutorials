---
category: general
date: 2026-07-18
description: Execute OCR em imagem usando Aspose OCR em Python. Aprenda a extrair
  texto simples da imagem, aplicar pós‑processamento de IA e obter resultados limpos
  rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: pt
lastmod: 2026-07-18
og_description: Execute OCR em imagem com Aspose OCR e Python. Este tutorial mostra
  como extrair texto simples de uma imagem e aumentar a precisão usando um pós‑processador
  de IA.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Execute OCR em Imagem – Guia Completo de Python com Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Execute OCR em imagem com Aspose AI – Tutorial completo em Python
url: /pt/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem com Aspose AI – Tutorial Completo em Python

Já se perguntou como **executar OCR em arquivos de imagem** sem lidar com APIs de baixo nível? Você não está sozinho. Em muitos projetos—processamento de faturas, digitalização de recibos ou a digitalização de documentos antigos—obter texto limpo e pesquisável a partir de uma foto é o primeiro, e muitas vezes o mais difícil, passo.

Neste guia vamos percorrer um exemplo prático que não só **executa OCR em imagem**, mas também mostra como **extrair texto simples de imagem** usando o motor OCR da Aspose, e então refinar o resultado com um pequeno pós‑processador de IA. Ao final você terá um script pronto para rodar, uma compreensão clara de cada parte e algumas dicas para evitar armadilhas comuns.

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="Saída de console ao executar OCR em imagem mostrando texto original e texto aprimorado por IA"}

## O que você precisará

Antes de mergulharmos, certifique‑se de que você tem:

- Python 3.8+ instalado (o código funciona no Windows, macOS e Linux).
- Uma licença ativa do Aspose OCR for Python ou um teste gratuito (o pacote é `aspose-ocr` no PyPI).
- Um arquivo de imagem de exemplo (por exemplo, uma fatura ou recibo escaneado) salvo localmente.
- Opcional: uma máquina com GPU habilitada se você pretender mudar a configuração `gpu_layers` mais tarde.

É só isso—nenhum motor OCR pesado, nenhuma chamada externa à nuvem, apenas um único `pip install` e algumas linhas de código.

## Etapa 1: Instalar o Pacote Aspose OCR

Abra um terminal e execute:

```bash
pip install aspose-ocr
```

O pacote traz o motor OCR central mais o namespace leve `aspose.ocr` que usaremos ao longo do tutorial.

## Etapa 2: Importar as Classes Necessárias

Começamos importando as duas classes principais: `AsposeAI` para o pós‑processamento aprimorado por IA e `OcrEngine` para a extração real de texto.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Por que isso importa*: `OcrEngine` faz o trabalho pesado de reconhecer glifos, enquanto `AsposeAI` nos permite conectar lógica personalizada—como capitalizar cada palavra—sem reescrever o núcleo do OCR.

## Etapa 3: Criar uma Instância AsposeAI (Logger Opcional)

Se quiser logs detalhados, pode passar um logger personalizado, mas o padrão funciona bem na maioria dos casos.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Etapa 4: Ajustar o Modelo Subjacente (Opcional)

O Aspose OCR vem com um modelo de idioma padrão, mas você pode apontá‑lo para um repositório HuggingFace ou forçar a execução na CPU. Abaixo habilitamos downloads automáticos e selecionamos o modelo pequeno `gpt2`—apenas para ilustrar os ajustes disponíveis.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Dica de especialista:** Se você possui uma GPU compatível com CUDA, aumente `gpu_layers` para `1` ou `2` para obter um ganho de velocidade perceptível.

## Etapa 5: Registrar um Pós‑Processador Simples

Nosso objetivo é **extrair texto simples de imagem** e então deixá‑lo mais apresentável. Aqui está uma função pequena que capitaliza cada palavra. Você pode substituí‑la por correção ortográfica, detecção de idioma ou até mesmo uma chamada completa a um LLM.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

O dicionário `custom_settings` permite que você passe parâmetros extras mais tarde—útil quando evoluir o processador.

## Etapa 6: Carregar uma Imagem e Executar OCR

Agora finalmente **executamos OCR em imagem**. Recuperaremos duas versões de saída:

1. **Texto simples** – uma string bruta sem informações de layout.
2. **Texto estruturado** – consciente de layout, preservando colunas e tabelas.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Por que ambos?** `plain_text` é perfeito para buscas rápidas, enquanto `structured_text` brilha quando você precisa reconstruir tabelas ou manter o alinhamento de colunas.

## Etapa 7: Aprimorar as Saídas OCR com o Pós‑Processador de IA

Com os resultados do OCR em mãos, os passamos para `AsposeAI.run_postprocessor`. É aqui que a função `capitalize_words` definida anteriormente é executada.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Se mais tarde você decidir trocar o pós‑processador por algo mais sofisticado—por exemplo, um corretor gramatical—basta substituir a função na Etapa 5 e o restante do pipeline permanece idêntico.

## Etapa 8: Ver os Resultados

Vamos imprimir tudo lado a lado para que você possa comparar o OCR bruto com a versão aprimorada por IA.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Saída Esperada

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Observe como o pós‑processador de IA transformou palavras totalmente minúsculas em palavras capitalizadas, tornando o texto muito mais legível. Você pode aplicar qualquer transformação que desejar—isto é apenas uma prova de conceito.

## Etapa 9: Liberar Recursos

O Aspose carrega arquivos de modelo pesados na memória. Quando terminar, libere‑os para evitar vazamentos de memória, especialmente em serviços de longa duração.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Perguntas Frequentes & Casos de Borda

| Pergunta | Resposta |
|----------|----------|
| **Posso executar OCR em várias imagens em um loop?** | Absolutamente. Basta instanciar `OcrEngine` uma única vez, chamar `load_image` dentro do loop e reutilizar a mesma instância `AsposeAI` para o pós‑processamento. |
| **E se a imagem for de baixa resolução?** | Pré‑procese com OpenCV (por exemplo, `cv2.resize` e `cv2.threshold`) antes de enviá‑la ao `OcrEngine`. |
| **Preciso de uma GPU?** | Não é obrigatório. O modo padrão CPU funciona bem para a maioria dos documentos. Defina `ai.config.gpu_layers` > 0 apenas se você tiver uma GPU compatível e precisar de velocidade. |
| **Como extrair texto simples de imagem em outros idiomas?** | Altere `ocr_engine.language = "fr"` (ou qualquer código ISO‑639‑1) antes de chamar `recognize`. O mesmo pós‑processador ainda será executado, mas você pode precisar de lógica específica para o idioma. |

## Script Completo Funcionando

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Salve este arquivo como `run_ocr_on_image.py`, substitua o caminho de exemplo pelo caminho da sua imagem real e execute `python run_ocr_on_image.py`. Você deverá ver a saída antes/depois exatamente como no exemplo acima.

## Conclusão

Executamos com sucesso **OCR em arquivos de imagem** usando o Aspose OCR, demonstramos como **extrair texto simples de imagem** e mostramos uma forma leve de melhorar a legibilidade com um pós‑processador de IA. O padrão central—OCR

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extrair Texto de Imagem – Otimização de OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}