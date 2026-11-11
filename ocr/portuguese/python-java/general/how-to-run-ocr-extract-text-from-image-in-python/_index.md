---
category: general
date: 2026-03-26
description: Como executar OCR em um arquivo PNG e extrair texto da imagem com um
  dicionário personalizado para melhorar a precisão do OCR. Aprenda a carregar a imagem
  para OCR rapidamente.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: pt
og_description: Como executar OCR em um arquivo PNG e extrair texto da imagem com
  dicionário personalizado para melhorar a precisão do OCR. Guia passo a passo.
og_title: Como Executar OCR – Extrair Texto de Imagem em Python
tags:
- OCR
- Python
- Image Processing
title: Como Executar OCR – Extrair Texto de Imagem em Python
url: /pt/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR – Extrair Texto de Imagem em Python

Já se perguntou **como executar OCR** em uma fatura escaneada ou uma captura de tela e obter texto limpo e pesquisável? Você não está sozinho. Em muitos projetos o gargalo é simplesmente carregar a imagem para OCR e então convencer o motor a entender palavras específicas do domínio.  

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que **extrai texto de imagens**, mostra como **reconhecer texto de arquivos PNG** e ainda demonstra truques para **melhorar a precisão do OCR** com dicionários personalizados e caracteres especiais. Ao final, você terá um script autônomo que pode inserir em qualquer base de código Python.

## O que Você Precisa

- Python 3.8+ (o código usa type hints, mas funciona em versões anteriores do 3.x)
- A biblioteca `ocr` que vem com o motor OCR que você está direcionando (instale via `pip install ocr‑engine` – substitua pelo nome real do pacote)
- Um arquivo de imagem (`input.png`) que você deseja processar
- Opcional: um arquivo de texto simples (`invoice_terms.txt`) com palavras específicas do domínio, uma por linha

Sem dependências externas pesadas, sem chaves de API na nuvem, apenas um motor OCR local.

---

## Etapa 1: Instalar e Importar a Biblioteca OCR

Primeiro, certifique-se de que o pacote OCR está instalado. Se você estiver usando o pacote hipotético `ocr-engine`, execute:

```bash
pip install ocr-engine
```

Agora importe as classes que você precisará:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Dica profissional:** Se você estiver em um ambiente virtual, ative-o antes de instalar para manter seu Python global limpo.

## Etapa 2: Criar uma Instância do Motor OCR

Criar um objeto de motor é o ponto de entrada para toda tarefa de OCR. Pense nisso como ligar o hardware do scanner via software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Por que isso importa: o motor mantém configurações como pacotes de idioma, modos de reconhecimento e quaisquer recursos personalizados que você anexará mais tarde. Sem ele, você não pode **carregar imagem para OCR** ou executar o pipeline de reconhecimento.

## Etapa 3: Carregar a Imagem que Você Deseja Reconhecer

Aqui realmente **carregamos a imagem para OCR**. O método `Imaging.Image.load()` lê o arquivo e o converte para o formato bitmap interno que o motor espera.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Se você tem um JPEG ou TIFF, o mesmo método funciona — basta mudar a extensão. O motor detecta automaticamente o formato.

> **Caso extremo:** Imagens muito grandes (acima de 5 MP) podem causar picos de memória. Considere redimensionar com Pillow antes de carregar se você encontrar problemas de desempenho.

## Etapa 4: Fornecer um Dicionário Personalizado para Aumentar a Precisão

A maioria dos motores OCR vem com modelos de idioma genéricos. Para faturas, recibos ou documentos legais você frequentemente verá palavras perdidas. Fornecer uma lista de palavras personalizada diz ao motor “estes termos são legítimos, trate‑os como corretos”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Entradas típicas podem ser:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Adicionar esses melhora a métrica **melhorar a precisão do OCR** drasticamente — especialmente para símbolos não‑ASCII.

## Etapa 5: Adicionar Caracteres Especiais Não Cobertos pelo Conjunto Padrão

Se seu domínio usa símbolos como o sinal de Euro (€) ou o Ø escandinavo, você pode adicioná‑los explicitamente:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

O motor agora tratará esses glifos como válidos durante a fase de reconhecimento, reduzindo a chance de saída “lixo”.

## Etapa 6: Executar o Processo OCR e Recuperar o Texto

Finalmente, invoque o reconhecedor e obtenha o resultado em texto simples. A chamada `recognize()` retorna um objeto rico; precisamos apenas da string bruta para a maioria dos casos de uso.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Saída esperada** (truncada para brevidade):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Se a saída parecer confusa, verifique novamente se seu dicionário personalizado e caracteres especiais foram carregados corretamente.

---

## Visão Geral Visual

![diagrama de como executar OCR](ocr-workflow.png){alt="diagrama de como executar OCR"}

O diagrama acima ilustra o fluxo desde o carregamento de uma imagem até a obtenção de texto limpo, destacando onde você pode inserir dicionários personalizados e conjuntos de caracteres.

---

## Perguntas Frequentes & Armadilhas

### Isso funciona com PDFs de várias páginas?

Sim — basta converter cada página para PNG (usando `pdf2image` ou similar) e alimentá‑las sequencialmente na mesma instância `ocr_engine`. O motor processa cada imagem independentemente, então você obterá uma lista de strings que pode concatenar.

### E se a imagem estiver rotacionada?

A maioria dos motores OCR modernos detecta automaticamente a orientação, mas você pode forçar uma rotação com:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Como lidar com idiomas diferentes do inglês?

Troque o modelo de idioma antes de carregar a imagem:

```python
ocr_engine.set_language("de")  # German
```

Certifique‑se de que o pacote de idioma correspondente está instalado.

---

## Script Completo – Pronto para Copiar & Colar

Abaixo está o programa completo, pronto para executar após você substituir os caminhos de placeholder.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Execute‑o com:

```bash
python run_ocr.py
```

Você deverá ver o texto extraído impresso no console. A partir daí, pode escrevê‑lo em um arquivo, inseri‑lo em um banco de dados ou passá‑lo para pipelines de NLP subsequentes.

---

## Recapitulação & Próximos Passos

Cobremos **como executar OCR** em um PNG, como **extrair texto de imagem**, e mostramos maneiras práticas de **reconhecer texto de PNG** enquanto **melhoramos a precisão do OCR** com dicionários e caracteres personalizados.  

Em seguida, considere:

- **Processamento em lote:** Percorrer um diretório de imagens.
- **Pós‑processamento:** Use regex para extrair números de fatura ou datas.
- **Integração:** Conectar o script a uma API Flask para serviços OCR sob demanda.

Se você está curioso sobre tópicos mais avançados, confira tutoriais sobre **carregar imagem para OCR** com pré‑processamento OpenCV, ou mergulhe em modelos OCR baseados em deep‑learning como Tesseract 4+ com camadas LSTM.

---

### Continue Experimentando!

Tente substituir o `invoice_terms.txt` por uma lista de terminologia médica, adicionar caracteres gregos ou alimentar o motor com uma foto de baixa resolução para ver até onde a precisão pode chegar. Quanto mais você mexer, melhor entenderá as compensações entre pré‑processamento, vocabulários personalizados e configurações do motor.

Feliz codificação, e que seus resultados de OCR sejam sempre nítidos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}