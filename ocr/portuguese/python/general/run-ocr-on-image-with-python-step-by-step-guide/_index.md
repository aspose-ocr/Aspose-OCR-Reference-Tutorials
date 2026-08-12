---
category: general
date: 2026-08-12
description: Execute OCR em imagem usando Python e Aspose AI para extrair texto da
  imagem e melhorar a precisão do OCR com um pós-processador de verificação ortográfica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: pt
lastmod: 2026-08-12
og_description: Execute OCR em imagem no Python e extraia instantaneamente o texto
  da imagem, aprimorando a precisão do OCR com o pós‑processamento de IA da Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Execute OCR em imagem com Python – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Execute OCR em imagem com Python – guia passo a passo
url: /pt/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em imagem com Python – guia passo a passo

Se você precisa **executar OCR em imagem** arquivos em Python, este guia o conduz por todo o fluxo de trabalho. Você aprenderá como **extrair texto de imagem**, aplicar **correção de texto OCR** e **melhorar a precisão do OCR** com apenas algumas linhas de código.

Processar documentos digitalizados, recibos ou capturas de tela frequentemente gera texto ruidoso. Ao anexar um pós‑processador de verificação ortográfica, você pode transformar a saída bruta do OCR em conteúdo limpo e pesquisável sem mudar para uma ferramenta separada. Este tutorial cobre tudo o que você precisa — desde o carregamento da imagem até a exibição do resultado corrigido.

## Pré-requisitos

* Python 3.9 ou mais recente instalado.
* Acesso aos pacotes Python Aspose.OCR e Aspose.AI (ou seus equivalentes de código aberto).
* Uma imagem de exemplo (por exemplo, `sample.png`) colocada em um diretório conhecido.
* Familiaridade básica com funções Python e código orientado a objetos.

Você pode instalar as bibliotecas necessárias com pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv .venv`) para manter as dependências isoladas.

## Etapa 1: Executar OCR em imagem – criar a instância do motor

O primeiro passo é criar um objeto `OcrEngine`. Este objeto encapsula a configuração do motor OCR e fornece métodos para manipulação e reconhecimento de imagens.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Criar o motor uma única vez e reutilizá‑lo em várias imagens reduz a sobrecarga de inicialização e garante configurações consistentes ao longo da sessão.

## Etapa 2: Carregar imagem para OCR

Antes que o reconhecimento possa ocorrer, o motor deve saber qual imagem analisar. O método `load_image` aceita um caminho de arquivo ou um fluxo binário.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Por que isso importa:** Carregar a imagem corretamente é a base para um OCR preciso. Fornecer uma imagem de alta resolução (300 dpi ou mais) geralmente **melhora a precisão do OCR** porque o motor pode distinguir os caracteres com mais clareza.

## Etapa 3: Extrair texto de imagem – realizar reconhecimento básico

Com a imagem carregada, você pode chamar `recognize()` para obter um objeto de resultado. O resultado contém o texto bruto, pontuações de confiança e, opcionalmente, caixas delimitadoras para cada palavra.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Neste ponto você executou **OCR em imagem** com sucesso e extraiu os caracteres brutos. Contudo, o texto pode conter erros ortográficos, especialmente em digitalizações de baixa qualidade.

## Etapa 4: Correção de texto OCR – anexar um verificador ortográfico pós‑processamento

Aspose AI fornece um pipeline de pós‑processamento flexível. Ao conectar um verificador ortográfico personalizado, você pode corrigir erros típicos de OCR (por exemplo, “l” vs. “1”, “O” vs. “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Como o verificador ortográfico funciona:** `MySpellChecker` deve implementar um método `process(text: str) -> str`. Dentro dele, você pode usar bibliotecas como `pyspellchecker` ou `symspellpy` para substituir sequências de palavras improváveis por alternativas validadas por dicionário.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Etapa 5: Exibir texto OCR original e corrigido

Finalmente, compare as saídas bruta e corrigida. Isso ajuda a verificar se a **correção de texto OCR** realmente **melhorou a precisão do OCR** para seu caso de uso.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Saída esperada

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

A linha corrigida mostra que o verificador ortográfico substituiu reconhecimentos errôneos comuns do OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Etapa 6: Melhorar a precisão do OCR – checklist de boas práticas

Mesmo com pós‑processamento, você pode aumentar a qualidade base do motor OCR:

| Item da checklist | Por que ajuda |
|-------------------|---------------|
| **Use imagens de alta resolução (≥300 dpi)** | Mais dados de pixel reduzem a ambiguidade de caracteres. |
| **Converta imagens coloridas para escala de cinza** | Remove ruído de croma que pode confundir o motor. |
| **Aplique correção de inclinação da imagem** | Endireita texto inclinado, evitando erros de quebra de linha. |
| **Defina idioma/localidade explicitamente** | Orienta o reconhecedor para o conjunto de caracteres correto. |
| **Habilite modelo de linguagem** (se a biblioteca suportar) | Fornece previsões contextuais, melhorando ainda mais a **precisão do OCR**. |

Você pode implementar essas etapas de pré‑processamento com Pillow ou OpenCV antes de enviar a imagem para `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Script completo executável

Juntando tudo, o script a seguir está pronto para copiar‑colar em um arquivo chamado `run_ocr.py` e executar.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Executar o script imprime o texto original e corrigido, confirmando que você executou com sucesso **OCR em imagem**, **extraiu texto de imagem** e **melhorou a precisão do OCR** através da **correção de texto OCR**.

## Conclusão

Agora você sabe como **executar OCR em imagem** arquivos em Python, extrair o texto bruto e aplicar um verificador ortográfico pós‑processamento para obter resultados mais limpos. Seguindo o checklist para **melhorar a precisão do OCR**, você pode adaptar este fluxo de trabalho para recibos, faturas, carteiras de identidade ou qualquer documento digitalizado.

### O que vem a seguir?

* Explore **dicionários específicos de idioma** para OCR multilíngue.
* Integre o pipeline a um banco de dados ou índice de busca (por exemplo, Elasticsearch) para tornar o texto extraído pesquisável.
* Substitua o verificador ortográfico simples por um modelo de linguagem neural (por exemplo, correção baseada em GPT) para ainda mais precisão.

Sinta‑se à vontade para experimentar diferentes técnicas de pré‑processamento de imagem, diferentes pós‑processadores ou motores OCR alternativos. O padrão central — **executar OCR em imagem → extrair texto de imagem → correção de texto OCR → melhorar a precisão do OCR** — permanece o mesmo, proporcionando uma base robusta para qualquer projeto de digitalização de documentos.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter imagem em texto: extrair texto de imagem usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extrair texto de imagem com Aspose OCR – Guia passo a passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair texto de imagem – otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}