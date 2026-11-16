---
category: general
date: 2026-07-05
description: Realize OCR em imagem usando Python. Aprenda como converter imagem em
  texto com Python, carregar a imagem para OCR e extrair texto cirílico da imagem
  em minutos.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: pt
og_description: Realize OCR em imagem no Python. Este guia mostra como converter imagem
  em texto usando Python, carregar a imagem para OCR e extrair texto cirílico da imagem
  rapidamente.
og_title: Realizar OCR em Imagem com Python – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Realize OCR em Imagem com Python – Guia Completo Passo a Passo
url: /pt/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em Imagem com Python – Guia Completo Passo a Passo

Já se perguntou como **perform OCR on image** arquivos sem entregá‑los a um serviço de terceiros? Você não está sozinho. Em muitos projetos—scanners de passaporte, digitalizadores de recibos ou ferramentas de arquivamento—obter texto bruto de uma foto é o primeiro obstáculo.  

Neste tutorial, vamos percorrer um exemplo prático que **converts image to text python** style, mostra como **load image for OCR**, e finalmente **extract Cyrillic text from image** usando a biblioteca open‑source `aocr`. Ao final, você será capaz de **recognize Cyrillic text** em qualquer imagem que você usar.

> **O que você levará consigo:** um script pronto‑para‑executar, explicações claras de cada passo e dicas para lidar com armadilhas comuns (como digitalizações borradas ou fontes inesperadas). Sem APIs externas, apenas Python puro.

---

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Python 3.8 ou mais recente instalado.
- Um terminal ou prompt de comando com o qual você se sinta confortável.
- O pacote `aocr` (instalável via `pip install aocr`).
- Um arquivo de imagem que contenha caracteres cirílicos (por exemplo, um passaporte russo escaneado).  

Se algum desses itens lhe for desconhecido, não entre em pânico—cada ponto será abordado brevemente ao longo do tutorial.

---

## Etapa 1: Perform OCR on Image – Configurando o Ambiente

A primeira coisa que precisamos é de um ambiente Python limpo onde a biblioteca OCR reside. Usar um ambiente virtual isola as dependências e evita conflitos de versões.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Por quê?**  
Um ambiente dedicado garante que o pacote `aocr` e seus binários nativos não interfiram em outros projetos. Também facilita a reprodutibilidade—alguém pode clonar seu repositório e executar o mesmo comando `pip install -r requirements.txt`.

> **Dica profissional:** Congele suas dependências com `pip freeze > requirements.txt` para sempre saber exatamente quais versões foram usadas.

---

## Etapa 2: Load Image for OCR – Importando e Preparando o Arquivo

Agora que a biblioteca está pronta, precisamos **load image for OCR**. O método `aocr.Image.from_file` lida com os formatos mais comuns (PNG, JPEG, TIFF). Veja como fazer:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**O que está acontecendo aqui?**  
`aocr.Image.from_file` lê os dados binários, decodifica‑os e os armazena em um objeto que o motor OCR pode entender. Se o arquivo não for encontrado, o Python lançará um `FileNotFoundError`, que você pode capturar depois se precisar de um tratamento de erro elegante.

> **Caso extremo:** Alguns scanners geram TIFFs de várias páginas. Nesse caso, você precisará dividir as páginas primeiro—`aocr` fornece `Image.from_tiff_pages()` para isso.

---

## Etapa 3: Configure the OCR Engine – Forçando o Reconhecimento de Cyrillic

Por padrão, muitos motores OCR tentam adivinhar o idioma, o que pode gerar saída confusa para scripts não‑latinos. Para **recognize Cyrillic text** de forma confiável, definimos explicitamente o idioma como “cyrillic”.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Por que forçar o idioma?**  
Caracteres cirílicos compartilham semelhanças visuais com letras latinas (ex.: “A” vs “А”). Informar ao motor que deve esperar cirílico reduz drasticamente o reconhecimento incorreto, especialmente em digitalizações de baixa resolução.

---

## Etapa 4: Perform OCR on Image – Executando o Reconhecimento

Com a imagem carregada e o motor ajustado, finalmente **perform OCR on image**. O método `recognize` retorna um objeto `OcrResult` contendo o texto extraído e as pontuações de confiança.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**O que `ocr_result` fornece?**  
- `text`: a string simples dos caracteres reconhecidos.  
- `confidence`: um float (0‑1) indicando a certeza geral.  
- `lines`: uma lista de objetos de linha caso você precise de controle granular.

> **Pergunta comum:** *E se o texto estiver de cabeça‑para‑baixo?*  
> `aocr` pode auto‑rotacionar imagens; basta definir `ocr_engine.auto_rotate = True` antes de chamar `recognize`.

---

## Etapa 5: Convert Image to Text Python – Pós‑processamento da Saída

A string bruta pode conter espaços em branco indesejados ou artefatos de quebras de linha. Para **convert image to text python** style, vamos limpá‑la com alguns passos simples:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Por que se preocupar?**  
Uma saída limpa é mais fácil de alimentar em pipelines posteriores—seja armazenando em um banco de dados, enviando para uma API de tradução ou executando buscas regex por números de passaporte.

---

## Etapa 6: Extract Cyrillic Text from Image – Unindo Tudo

Vamos agrupar tudo em uma única função reutilizável. Isso torna **extract Cyrillic text from image** um comando de uma linha em seus próprios projetos.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Resultado que você deve ver (exemplo):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Se a imagem estiver nítida e a fonte corresponder ao modelo OCR, você obterá uma transcrição quase perfeita.

## solução de problemas & Dicas

| Problema | Causa Provável | Correção |
|-------|--------------|-----|
| Garbled characters | Wrong language setting | Ensure `ocr_engine.language = "cyrillic"` |
| Empty output | Image too dark or low‑resolution | Preprocess with `opencv` to increase contrast |
| Wrong orientation | Image rotated 90° | Set `ocr_engine.auto_rotate = True` |
| Slow performance | Large image ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

![exemplo de perform OCR on image](ocr_example.png "exemplo de perform OCR on image")

*Texto alternativo: “exemplo de perform OCR on image mostrando código Python extraindo texto cirílico de um escaneamento de passaporte.”*

## Conclusão

Acabamos de **perform OCR on image** arquivos usando Python puro, aprendemos como **load image for OCR**, forçamos o motor a **recognize Cyrillic text**, e finalmente **extract Cyrillic text from image** com uma função auxiliar organizada. Todo o pipeline—desde a instalação do `aocr` até a limpeza do resultado—cabe em algumas dezenas de linhas de código e pode ser inserido em qualquer projeto que precise **convert image to text python** style.

## O que vem a seguir?

- **Processamento em lote:** Percorra uma pasta de digitalizações e armazene os resultados em SQLite.
- **Detecção de idioma:** Combine `langdetect` com `aocr` para alternar automaticamente entre Cyrillic e Latin.
- **Pré‑processamento avançado:** Use `opencv` para corrigir inclinação, remover ruído ou binarizar imagens para maior precisão.
- **Integração com FastAPI:** Exponha a função `extract_cyrillic_text` como um endpoint REST para aplicativos web.

Sinta‑se à vontade para experimentar—troque o idioma para “latin” para passaportes em inglês, ou tente um backend OCR diferente. Os conceitos permanecem os mesmos, e o código é flexível o suficiente para se adaptar.

Feliz codificação, e que suas imagens estejam sempre legíveis!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converter Imagem em Texto – Perform OCR on Image a partir de URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}