---
category: general
date: 2026-11-20
description: Execute OCR em imagem com o Aspose OCR e, em seguida, extraia o texto
  da imagem usando o pós‑processador de IA incorporado. Aprenda um fluxo de trabalho
  completo em Python em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: pt
lastmod: 2026-11-20
og_description: Realize OCR em imagem com Aspose OCR, depois extraia o texto da imagem
  via pós‑processamento de IA. Siga este guia passo a passo em Python.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Realizar OCR em imagem e extrair texto da imagem usando Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Realize OCR em imagem e extraia texto da imagem com Aspose
url: /pt/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on image and extract text from image with Aspose

Se você precisa **perform OCR on image** arquivos em Python, este guia mostra uma solução completa de ponta a ponta. Usando Aspose OCR junto com o post‑processador Aspose AI, você pode de forma confiável **extract text from image** arquivos e melhorar a saída bruta de OCR com um modelo de linguagem leve.

Neste tutorial você vai:

* Configurar o motor Aspose OCR.
* Executar OCR para **extract text from image**.
* Opcionalmente configurar um modelo de IA para pós‑processamento.
* Registrar uma função de pós‑processador personalizada.
* Produzir texto aprimorado e liberar recursos.

As etapas funcionam com qualquer imagem raster (PNG, JPEG, BMP) e requerem apenas o pacote `aspose-ocr`.

## Pré-requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| Python 3.8+ | Requerido pelo Aspose SDK. |
| `aspose-ocr` pip package | Fornece `AsposeOCR`, `AsposeAI` e classes de configuração de modelo. |
| Um arquivo de imagem (por exemplo, `sample_image.png`) | A fonte que você **perform OCR on image**. |
| Opcional: suporte a GPU | Se você planeja executar um modelo maior em uma GPU, defina `gpu_layers` adequadamente. |

Instale o SDK com:

```bash
pip install aspose-ocr
```

## Etapa 1: Perform OCR on image

A primeira operação é ler a imagem e obter o texto bruto. Esta é a etapa central **perform OCR on image**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Por que isso funciona:** `AsposeOCR.recognize_image` executa um modelo pré‑treinado de reconhecimento óptico de caracteres que é otimizado para velocidade e precisão em fontes comuns. O método retorna uma string Unicode simples, que é a base para qualquer processamento adicional.

> **Dica profissional:** Se a imagem contiver múltiplos idiomas, defina `ocr_engine.language = "eng+spa"` (ou qualquer código ISO‑639‑2 suportado) antes de chamar `recognize_image`.

## Etapa 2: Initialise the AI post‑processor

Aspose AI fornece uma camada de pós‑processamento leve que pode limpar erros de OCR, corrigir pontuação ou aplicar lógica de negócios personalizada.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Por que você precisa disso:** OCR bruto frequentemente reconhece erroneamente caracteres (por exemplo, “0” vs “O”). A etapa de IA refina a saída, tornando o resultado **extract text from image** mais confiável para tarefas subsequentes, como indexação ou análise.

## Etapa 3: (Optional) Configure the AI model

Você pode apontar o processador para um modelo específico do Hugging Face, habilitar downloads automáticos ou forçar a execução na CPU. Esta etapa é opcional, mas útil quando você deseja comportamento determinístico.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Explicação:**  
* `allow_auto_download` economiza a gestão manual de modelos.  
* `hugging_face_repo_id` seleciona um modelo; `gpt2` é um bom compromisso entre tamanho e qualidade para correção de texto curto.  
* `gpu_layers` controla quantas camadas do transformer rodam na GPU; `0` força execução puramente na CPU, o que é seguro em todas as máquinas.

## Etapa 4: Register a custom post‑processing function

Aspose AI permite que você conecte qualquer callable que recebe a string OCR bruta e retorna uma versão transformada. Abaixo está um exemplo simples que converte tudo para maiúsculas.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Quando personalizar:** Use uma função personalizada quando precisar de limpeza específica de domínio, como remover identificadores confidenciais, normalizar datas ou aplicar correções baseadas em regex. O modelo de IA será executado *depois* desta função, permitindo combinar regras determinísticas com melhorias probabilísticas.

## Etapa 5: Enhance the OCR result using the AI post‑processor

Agora execute o pipeline completo: o texto OCR bruto é primeiro passado pela sua função personalizada, depois pelo modelo de IA, e finalmente você recebe a saída refinada.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**O que você deve ver:**  
Se a imagem original continha “Hello world”, o console pode exibir:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

Em um cenário real, o modelo de IA corrigiria erros ortográficos, adicionaria pontuação ausente ou reformataria quebras de linha, fornecendo um resultado **extract text from image** mais limpo, pronto para armazenamento ou análise.

## Etapa 6: Release resources when finished

Tanto o motor OCR quanto o pós‑processador de IA alocam recursos nativos. Liberá‑los explicitamente evita vazamentos de memória, especialmente em serviços de longa duração.

```python
# Clean up native resources
ai_processor.free_resources()
```

Se você também instanciou `ocr_engine` com um backend pesado, poderia chamar `ocr_engine.dispose()` (se disponível) da mesma forma.

## Variações comuns e casos de borda

| Situação | Ajuste recomendado |
|-----------|------------------------|
| **PDFs grandes com muitas páginas** | Iterar sobre cada página, chamar `recognize_image` para cada página rasterizada e agregar os resultados. |
| **Ambiente com GPU habilitada** | Defina `model_config.gpu_layers` para o número de camadas que você deseja na GPU (por exemplo, `4`). Certifique‑se de que os drivers CUDA estejam instalados. |
| **Texto não‑inglês** | Altere `ocr_engine.language` para o código de idioma apropriado e, se necessário, selecione um modelo Hugging Face específico para o idioma. |
| **Digitalizações muito ruidosas** | Pré‑processar a imagem com OpenCV (reduzir ruído, limiar) antes de chamar `recognize_image`. |
| **Necessidade de manter a capitalização original** | Substitua a função `my_post_processor` por uma operação nula ou uma regra mais sutil em vez de `text.upper()`. |

## Exemplo completo em funcionamento

Juntando tudo, aqui está um script único que você pode executar como está (substitua `YOUR_DIRECTORY/sample_image.png` pelo caminho real do seu arquivo):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Executar este script imprime tanto a saída OCR bruta quanto a versão aprimorada por IA, demonstrando como você pode **perform OCR on image** arquivos e de forma confiável **extract text from image** em um fluxo de trabalho único e reproduzível.

## Conclusão

Agora você sabe como **perform OCR on image** arquivos com Aspose OCR, e então **extract text from image** usando o post‑processador de IA incorporado. O tutorial abordou:

* Inicializando o motor OCR.  
* Executando OCR para obter texto bruto.  
* (Opcionalmente) configurando um modelo leve do Hugging Face.  
* Adicionando um

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}