---
category: general
date: 2026-04-26
description: como extrair OCR de imagens usando Python – um exemplo de OCR em Python
  que mostra como carregar a imagem para OCR e extrair texto de um recibo.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: pt
og_description: como extrair OCR de imagens usando Python. Aprenda um exemplo de OCR
  em Python, carregue a imagem para OCR e extraia texto de recibos em minutos.
og_title: como extrair OCR em Python – Guia Completo
tags:
- OCR
- Python
- Image Processing
title: como extrair OCR em Python – tutorial passo a passo
url: /pt/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como extrair ocr em Python – Guia Completo

Já se perguntou **como extrair OCR** de um recibo borrado ou de uma fatura escaneada? Você não está sozinho — desenvolvedores frequentemente esbarram em dificuldades quando precisam de texto limpo e legível por máquina a partir de imagens. A boa notícia? Com apenas algumas linhas de Python você pode transformar uma foto de um recibo em texto de alta confiança e pesquisável.

Neste tutorial, vamos percorrer um **exemplo de OCR em Python** que demonstra **como carregar imagem para OCR**, executar o motor e manter apenas os caracteres que atendem a um limite de confiança de 85 %. Ao final, você será capaz de **extrair texto de recibos** sem precisar vasculhar a documentação ou adivinhar parâmetros da API.

## O que você precisará

- Python 3.9 ou mais recente (a sintaxe que usamos funciona em 3.8+)
- O pacote `aocr` (ou qualquer biblioteca OCR que forneça uma classe `OcrEngine`). Instale‑o com:

```bash
pip install aocr
```

- Uma imagem de recibo de exemplo (`receipt.png`) colocada em uma pasta que você pode referenciar.
- Um editor de texto ou IDE — VS Code, PyCharm, ou até mesmo um notebook simples serve.

É isso. Sem frameworks pesados, sem serviços externos, apenas Python puro.

![Resultado de OCR de alta confiança – como extrair OCR de um recibo](/images/ocr-high-confidence.png)

*Texto alternativo da imagem: como extrair OCR de um recibo usando Python OCR*

## Etapa 1 – Criar a Instância do Motor OCR (como extrair OCR)

A primeira coisa que fazemos é iniciar um motor OCR. Pense nele como o cérebro que lerá os pixels para nós.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Por quê?** Instanciar `OcrEngine` fornece um novo objeto de configuração. Você pode ajustar posteriormente modelos de idioma, configurações de DPI ou etapas de pré‑processamento — tudo sem tocar no loop principal de processamento.

## Etapa 2 – Carregar a Imagem para OCR

Em seguida, apontamos o motor para a imagem que queremos analisar. É aqui que a palavra‑chave **carregar imagem para OCR** entra em ação.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Dica profissional:** Se sua imagem estiver em um diretório diferente, use `os.path.join` para construir um caminho independente de plataforma.

**Por que carregar a imagem desta forma?** O helper `Image.load` lê o arquivo em um formato que o motor entende, lidando automaticamente com formatos comuns (PNG, JPEG, TIFF). Pular esta etapa ou fornecer bytes brutos geraria um `ValueError`.

## Etapa 3 – Executar o Processo OCR

Agora realmente executamos o OCR. O método `process` retorna um objeto de resultado rico contendo símbolos reconhecidos, pontuações de confiança e caixas delimitadoras.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**O que `ocr_result` contém?** Na maioria das bibliotecas inclui:

- `text`: a string bruta concatenada.
- `symbol_confidences`: uma lista de tuplas `(char, confidence)`.
- `boxes`: coordenadas para cada caractere (útil para depuração visual).

Ter acesso à confiança por caractere é essencial para a próxima etapa.

## Etapa 4 – Manter Apenas Símbolos de Alta Confiança (≥ 85 %)

Um recibo frequentemente tem manchas, impressão fraca ou ruído de fundo. Ao filtrar símbolos de baixa confiança, melhoramos drasticamente a análise subsequente.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Por que 85 %?** Empiricamente, um limite em torno de 0.85 equilibra recall e precisão para a maioria dos recibos impressos. Se notar números ausentes, diminua o limite; se obter lixo, aumente‑o.

## Etapa 5 – Exibir o Texto Extraído de Alta Confiança

Finalmente, imprimimos (ou armazenamos) a string sanitizada. Este é o núcleo do nosso fluxo de trabalho de **extrair texto de recibos**.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

A saída típica se parece com:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Agora você pode alimentar essa string em um escritor CSV, um banco de dados ou qualquer pipeline de análise subsequente.

## Script Completo, Pronto‑para‑Executar

Abaixo está o trecho de código completo que você pode copiar‑colar em `ocr_receipt.py` e executar imediatamente.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Salve o arquivo, garanta que `receipt.png` exista, e execute:

```bash
python ocr_receipt.py
```

Você deverá ver o texto limpo do recibo impresso no console.

## Casos de Borda & Cenários de “E‑Se”

| Situação | Correção Sugerida |
|-----------|----------------|
| **Confiança muito baixa em todo o conjunto** | Pré‑processar a imagem: aumentar o contraste, converter para escala de cinza ou aplicar um filtro de redução de ruído (`cv2.GaussianBlur`). |
| **Caracteres não latinos** | Passe um modelo de idioma para `OcrEngine` (por exemplo, `ocr_engine.language = "spa"` para espanhol). |
| **Múltiplos recibos em uma imagem** | Execute OCR na imagem inteira, então divida o resultado usando expressões regulares que detectam `\\n\\n+` (quebras de linha duplas). |
| **Precisa também do texto OCR bruto** | Mantenha `ocr_result.text` junto com a versão filtrada para depuração. |

Essas variações garantem que seu conhecimento de **como usar OCR** escale além do caso mais simples.

## Armadilhas Comuns (E Como Evitá‑las)

- **Esquecer de instalar a biblioteca** – `pip install aocr` deve ser bem‑sucedido antes de importar.
- **Usar o separador de caminho errado** no Windows (`\` vs `/`). Use `os.path.join`.
- **Codificar rigidamente o limite de confiança** sem testar – sempre faça uma verificação visual rápida em alguns recibos primeiro.
- **Ignorar a normalização Unicode** – alguns recibos contêm caracteres de traço especiais; execute `unicodedata.normalize('NFKC', text)` se você pretende armazenar a saída.

## Próximos Passos – Indo Além do Básico

Agora que você sabe **como extrair OCR** de um único recibo, pode querer:

1. **Processar em lote uma pasta de recibos** – percorrer todos os arquivos PNG/JPG e gravar cada resultado em um CSV.
2. **Integrar com um banco de dados** – armazenar `high_confidence_text` no SQLite para buscas rápidas.
3. **Aplicar análise de linguagem natural** – use regex ou `dateutil` para extrair datas, totais e valores de impostos.
4. **Experimentar bibliotecas alternativas** – `pytesseract`, `easyocr`, ou serviços em nuvem (Google Vision, Azure OCR) se precisar de suporte multilíngue ou maior precisão.

Cada um desses tópicos incorpora naturalmente nossas palavras‑chave secundárias: *python ocr example*, *extract text from receipt*, *load image for ocr* e *how to use OCR*.

## Conclusão

Acabamos de percorrer um **exemplo de OCR em Python** completo que mostra **como extrair OCR** de texto a partir de uma imagem de recibo, filtrar símbolos de baixa confiança e gerar resultados limpos. As etapas são simples, o código é autocontido e a abordagem é flexível o suficiente para se adaptar a projetos maiores.

Experimente com seus próprios recibos, ajuste o limite de confiança e então escale para processamento em lote. Se encontrar peculiaridades — como um logotipo fraco ou uma fonte incomum — lembre‑se das dicas de casos de borda acima. Boa codificação, e que seus pipelines de OCR sejam sempre precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}