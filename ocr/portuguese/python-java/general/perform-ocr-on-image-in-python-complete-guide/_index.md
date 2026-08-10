---
category: general
date: 2026-06-22
description: Realize OCR em uma imagem usando Python em apenas algumas linhas. Aprenda
  como carregar a imagem para OCR, reconhecer texto de um PNG e usar o motor de OCR
  de forma eficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: pt
og_description: Execute OCR em imagens rapidamente com Python. Este tutorial mostra
  como carregar a imagem para OCR, reconhecer texto de PNG e usar o motor de OCR com
  confiança.
og_title: Realize OCR em Imagem no Python – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Realize OCR em Imagem com Python – Guia Completo
url: /pt/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem no Python – Guia Completo

Já precisou **perform OCR on image** arquivos mas ficou travado na primeira linha de código? Você não está sozinho. Neste tutorial vamos mostrar exatamente como **load image for OCR**, configurar um **OCR engine** leve e, finalmente, **recognize text from PNG** com apenas alguns comandos.

Cobriremos tudo, desde a instalação da biblioteca até o ajuste da whitelist para que apenas dígitos e letras maiúsculas passem na varredura. Ao final, você terá um script pronto‑para‑executar que pode inserir em qualquer projeto—sem mistério, sem complicações extras.

## O que você aprenderá

- Como **use OCR engine** programaticamente em Python.  
- Os passos exatos para **load image for OCR** a partir de uma pasta local.  
- Por que e como restringir o reconhecimento a um conjunto de caracteres personalizado.  
- Como **recognize text from PNG** e lidar com o resultado de forma segura.  

**Pré-requisitos:** Python 3.7+ instalado, um terminal com o qual você se sinta confortável, e uma imagem (por exemplo, `serial-number.png`) que você deseja ler. Não é necessária experiência prévia com OCR.

---

## Executar OCR em Imagem – Inicializar o OCR Engine

A primeira coisa que você precisa fazer é criar uma instância do OCR engine. Pense no engine como o cérebro que analisará os pixels e os transformará em caracteres.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Por que isso importa:* Sem um engine não há nada para processar a imagem. A classe `OcrEngine` reúne todo o trabalho pesado—pré‑processamento, segmentação e classificação de caracteres—em um único objeto que você pode reutilizar.

---

## Carregar Imagem para OCR – Fornecer o Arquivo PNG

Agora que o engine existe, você precisa alimentá‑lo com a imagem que deseja ler. A biblioteca espera um objeto `ImageStream`, que pode ser criado diretamente a partir de um caminho de arquivo.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Dica profissional:* Mantenha a imagem em um formato de alto contraste (texto preto sobre fundo branco) e evite artefatos de compressão; eles podem atrapalhar o algoritmo de OCR.

---

## Restringir Caracteres – Whitelist de Dígitos e Letras Maiúsculas

Frequentemente você se importa apenas com um subconjunto de caracteres—por exemplo, um número de série que contém apenas A‑Z e 0‑9. Ao definir uma whitelist, você instrui o engine a ignorar todo o resto, o que melhora drasticamente a precisão.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*O que está acontecendo nos bastidores?* O engine cria um filtro que descarta qualquer glifo que não esteja presente na whitelist antes da fase final de classificação. Isso é especialmente útil quando a imagem contém ruído ou texto decorativo que você não precisa.

---

## Reconhecer Texto de PNG – Executar o Processo de OCR

Com o engine preparado e a imagem carregada, você pode finalmente **perform OCR on image**. A chamada `recognize()` executa todo o pipeline e retorna um objeto de resultado.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Se você está curioso sobre o desempenho, o método normalmente termina em algumas centenas de milissegundos para um PNG de 300 × 200 px em um laptop moderno.

---

## Saída e Verificação – Obter o Texto Reconhecido

O último passo é extrair o texto puro do objeto de resultado. Qualquer coisa que não corresponda à whitelist é descartada automaticamente, assim você obtém uma string limpa pronta para processamento adicional.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Saída típica:* `AB12C3D4E5` (supondo que a imagem contenha exatamente esse número de série).  

Se a saída estiver vazia ou distorcida, verifique novamente a qualidade da imagem e a whitelist; um erro comum é omitir acidentalmente caracteres necessários.

---

## Casos de Borda & Erros Comuns

| Situação | O que Verificar | Correção Sugerida |
|-----------|----------------|-------------------|
| **Arquivo não encontrado** | Erro de digitação no caminho ou arquivo ausente | Use `os.path.abspath` to verify the full path before calling `set_image`. |
| **Imagem de baixo contraste** | Texto se mistura com o fundo | Apply a simple threshold (`Pillow` or `OpenCV`) before feeding the image to the engine. |
| **Caracteres inesperados** | Whitelist muito restritiva | Add the missing characters to the whitelist string. |
| **Imagens grandes** | Reconhecimento lento | Resize the image to a maximum of 1024 px width; OCR quality usually stays high. |

---

## Script Completo – Pronto para Executar

Abaixo está o script completo e autônomo que une todas as partes. Salve‑o como `ocr_demo.py`, substitua `YOUR_DIRECTORY` pela pasta real e execute `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Saída esperada no console* (quando o PNG contém `SN12345`):

```
Recognized text: SN12345
```

---

## Conclusão

Agora você sabe exatamente como **perform OCR on image** arquivos em Python, desde **loading image for OCR** até **recognize text from PNG** e, finalmente, extrair um resultado limpo usando um **OCR engine** personalizável. A abordagem é direta, extensível e funciona pronto‑para‑usar na maioria das leituras de estilo número‑de‑série.

O que vem a seguir? Experimente trocar a whitelist por letras minúsculas, experimente diferentes formatos de imagem (JPEG, BMP) ou integre o script em um pipeline de processamento em lote. O mesmo padrão—engine → imagem → configurações → reconhecer → saída—vale para praticamente qualquer tarefa de OCR que você encontrar.

Tem perguntas ou uma imagem estranha que se recusa a cooperar? Deixe um comentário abaixo, e feliz codificação! 

![Diagrama ilustrando as etapas para executar OCR em imagem usando Python](https://example.com/ocr-flow.png "Diagrama mostrando como executar OCR em imagem com um motor OCR Python")


## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Converter Imagem para Texto – Executar OCR em Imagem a partir de URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Como Usar AspOCR: Pré‑processar Filtros de OCR de Imagem para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}