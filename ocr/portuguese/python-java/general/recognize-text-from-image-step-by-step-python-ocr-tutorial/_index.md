---
category: general
date: 2026-03-26
description: Reconheça texto de imagem rapidamente aprendendo como carregar a imagem
  para OCR e extrair dados de uma região específica. Siga este guia prático.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: pt
og_description: reconheça texto de imagem em Python carregando uma imagem para OCR,
  definindo uma região de interesse e extraindo texto limpo. Aprenda todo o fluxo
  de trabalho.
og_title: Reconhecer texto de imagem – Guia completo de OCR em Python
tags:
- OCR
- Python
- Image Processing
title: Reconhecer texto a partir de imagem – Tutorial de OCR em Python passo a passo
url: /pt/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem – Guia Completo de OCR em Python

Já precisou **reconhecer texto de imagem** mas não sabia por onde começar? Talvez você tenha um formulário escaneado, um recibo ou uma captura de tela e queira apenas as palavras dentro de uma caixa específica. A boa notícia é que, com algumas linhas de Python, você pode carregar a imagem para OCR, focar em uma única região e extrair o texto exato que precisa — sem copiar manualmente.

Neste tutorial percorreremos todo o processo: carregar a imagem, definir uma região de interesse (ROI), executar o motor de OCR e imprimir o resultado. Ao final, você poderá incorporar este trecho em qualquer projeto que precise extrair texto de uma parte específica de uma imagem. Sem pipelines pesados de processamento de imagem, apenas código limpo e legível que funciona hoje.

## Pré‑requisitos

- Python 3.8+ instalado  
- O pacote `ocr` (ou qualquer biblioteca de OCR compatível) – instale com `pip install ocr-lib` (substitua pelo nome real do pacote que você usa)  
- Uma imagem PNG/JPEG que contenha o formulário que você deseja ler  
- Familiaridade básica com funções e classes em Python  

Se você já está confortável com isso, ótimo — pode pular adiante. Caso contrário, pegue um café rápido e certifique‑se de que os itens acima estejam prontos; os passos posteriores assumem que eles já estão configurados.

## Etapa 1: Criar uma Instância do Motor de OCR – Núcleo “reconhecer texto de imagem”

A primeira coisa que precisamos é um objeto que saiba como se comunicar com o motor de OCR. Pense nele como o cérebro que mais tarde **reconhecerá texto de imagem**.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Por que isso importa:** Inicializar o motor uma única vez permite reutilizar configurações (como pacotes de idioma) em várias imagens, o que melhora o desempenho e mantém o código organizado.

## Etapa 2: Carregar Imagem para OCR – Trazendo a Foto para a Memória

Agora realmente **carregamos a imagem para OCR**. A biblioteca fornece um método estático conveniente que lê o arquivo e devolve um objeto que o motor pode entender.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Dica profissional:** Se sua imagem for grande, considere redimensioná‑la antes de carregar. Imagens menores aceleram o OCR sem sacrificar a precisão para a maioria dos textos impressos.

## Etapa 3: Definir a Região de Interesse (ROI) do OCR

Frequentemente você não precisa da página inteira — apenas de uma caixa específica onde o usuário preencheu os dados. Definir uma **região de interesse do OCR** indica ao motor que ele deve ignorar todo o resto, reduzindo ruído e acelerando o processamento.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Por que focar na ROI?**  
> - **Velocidade:** O motor analisa menos pixels.  
> - **Precisão:** Gráficos de fundo fora da ROI podem confundir o reconhecimento de caracteres.  
> - **Simplicidade:** Você obtém uma string limpa que corresponde exatamente ao campo que lhe interessa.

## Etapa 4: Executar o Processo de OCR – O Momento da Verdade

Com tudo configurado, finalmente **reconhecemos texto de imagem** dentro da ROI definida.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Se o motor suportar múltiplas regiões, `ocr_result` conterá uma lista; no nosso caso de ROI única, ele será um objeto simples com o método `get_text()`.

## Etapa 5: Extrair e Imprimir o Texto – Obtendo a Saída Final

Agora extraímos a string simples do objeto de resultado e a exibimos. É aqui que você pode encaminhar a saída para um banco de dados, um arquivo CSV ou qualquer lógica subsequente.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Saída esperada** (exemplo para um campo de nome preenchido):

```
Text inside ROI:
 John Doe
```

Se o motor de OCR retornar espaços em branco extras ou quebras de linha, você pode limpá‑los com `.strip()` ou uma expressão regular.

## Tratamento de Casos de Borda Comuns

| Situação                               | O que fazer                                                               |
|----------------------------------------|---------------------------------------------------------------------------|
| **Imagem de baixa resolução**         | Aumente a escala com `Pillow` (`Image.resize`) antes de carregar.        |
| **Texto inclinado ou rotacionado**     | Aplique correção de rotação (`ocr.Imaging.Image.rotate`).                |
| **Múltiplos idiomas**                  | Defina o pacote de idioma no motor: `ocr_engine.set_language('eng+spa')`. |
| **Nenhuma ROI definida**               | Pule `add_region_of_interest`; o motor processará a imagem inteira.     |
| **Caracteres inesperados (ex.: vírgulas)** | Pós‑procese a string: `extracted_text.replace(',', '')`.                |

Essas dicas mantêm seu pipeline **carregar imagem para OCR** robusto mesmo quando o material de origem não é perfeito.

## Exemplo Completo – Copiar, Colar, Executar

Abaixo está o script completo que você pode colocar em um arquivo `.py` e executar. Ele inclui todas as importações, tratamento de erros e um pequeno helper que verifica se a imagem existe.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Executar este script imprime a string limpa da ROI, fornecendo um dado pronto para uso.

## Conclusão

Agora você tem um método claro, de ponta a ponta, para **reconhecer texto de imagem** ao primeiro **carregar imagem para OCR**, definir uma **região de interesse do OCR** precisa e, finalmente, extrair texto limpo. A abordagem funciona com qualquer biblioteca de OCR em Python que siga o padrão mostrado acima, e você pode facilmente estendê‑la para lidar com múltiplas ROIs, diferentes idiomas ou etapas de pré‑processamento.

Em seguida, você pode explorar:

- **Pré‑processamento de imagem para OCR** (limiarização, remoção de ruído) para melhorar a precisão em digitalizações ruidosas.  
- Usar o resultado **extrair texto da ROI** para popular um `pandas DataFrame` para análise em massa.  
- Migrar para um serviço de OCR baseado em nuvem (Google Vision, Azure Computer Vision) quando precisar de maior confiabilidade em escala.

Teste, ajuste as coordenadas do retângulo para combinar com seus próprios formulários e veja a automação assumir. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}