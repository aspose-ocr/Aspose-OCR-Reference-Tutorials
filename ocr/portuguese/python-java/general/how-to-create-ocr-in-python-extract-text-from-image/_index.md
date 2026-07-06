---
category: general
date: 2026-04-26
description: Como criar OCR de forma rápida e confiável. Aprenda a extrair texto de
  imagens, carregar a imagem para OCR e executar OCR em PNG com um dicionário personalizado.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: pt
og_description: Como criar OCR em Python e extrair texto de uma imagem. Este guia
  mostra como carregar a imagem para OCR, executar OCR em PNG e usar um dicionário
  personalizado.
og_title: Como criar OCR em Python – Extração rápida de texto
tags:
- OCR
- Python
- Image Processing
title: Como criar OCR em Python – Extrair texto de imagem
url: /pt/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar OCR em Python – Guia Passo a Passo

Já se perguntou **como criar OCR** que possa ler seus PDFs escaneados, capturas de tela ou notas manuscritas? Você não está sozinho. Em muitos projetos do mundo real precisamos *extrair texto de imagem* de arquivos, mas os motores prontos‑para‑uso frequentemente tropeçam em palavras específicas de domínio.  

Neste tutorial você verá um exemplo completo e executável que carrega uma imagem para OCR, aplica um dicionário personalizado e, finalmente, **executa OCR em arquivos PNG**. Ao final, você será capaz de extrair texto de qualquer imagem e adaptar o motor ao seu próprio vocabulário.

## O Que Este Tutorial Abrange

Vamos percorrer cada passo que você precisa:

* Instalar o pequeno, porém poderoso, pacote `aocr` (ou qualquer biblioteca compatível).  
* Configurar um **dicionário personalizado** para que termos como `aspocorp` ou `licensekey` sejam reconhecidos.  
* **Carregar uma imagem para OCR**, seja PNG, JPEG ou uma página de PDF escaneada.  
* Executar o processo de OCR e imprimir o resultado.  

Sem links externos de documentação, apenas uma solução autocontida que você pode copiar‑colar e executar hoje.

### Pré‑requisitos

* Python 3.8 ou superior (o código usa f‑strings).  
* Familiaridade básica com a linha de comando – você digitará alguns comandos `pip install`.  
* Um arquivo de imagem (`technical_doc.png` no exemplo) colocado em algum local que você possa referenciar.  

Se você atender a esses três itens, está pronto para começar.  

---

## Passo 1: Instalar a Biblioteca de OCR

Primeiro, precisamos de um motor de OCR que suporte um objeto de configuração programável. O pacote `aocr` é um wrapper leve em torno de um motor OCR nativo e funciona bem para demonstrações.

```bash
# Install the library (run once)
pip install aocr
```

> **Dica de especialista:** Se você estiver no Windows e encontrar um erro de compilação, experimente `pip install aocr‑binary`, que fornece wheels pré‑compilados.

### Por Que Instalar Esta Biblioteca?

`aocr` nos dá acesso direto a um objeto `config` onde podemos injetar um **dicionário personalizado**. Esse é o ingrediente secreto para melhorar a precisão em vocabulários de nicho.

---

## Passo 2: Criar a Instância do Motor OCR & Adicionar um Dicionário Personalizado

Agora iniciamos o motor e informamos quais palavras ele deve tratar como conhecidas.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Por Que um Dicionário Personalizado Importa

Modelos OCR padrão são treinados em corpora genéricos. Quando o modelo vê “aspocorp”, ele pode dividir em “aspo corp” ou até omitir letras. Ao fornecer uma lista personalizada, direcionamos o reconhecedor para a grafia exata que precisamos, reduzindo drasticamente o esforço de pós‑processamento.

---

## Passo 3: Carregar a Imagem Que Você Deseja Processar

É aqui que **carregamos a imagem para OCR**. O método `Image.load` aceita uma string de caminho e determina automaticamente o tipo de arquivo.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Caso extremo:** Se sua fonte for um PDF de várias páginas, converta cada página para PNG primeiro (por exemplo, com `pdf2image`) e alimente‑as uma a uma ao motor.

### Dicas para Melhor Qualidade de Imagem

* Mantenha a resolução em pelo menos 300 dpi.  
* Garanta que a imagem esteja na orientação correta; rotacione com `Pillow` se necessário.  
* Converta digitalizações coloridas para escala de cinza para reduzir ruído.

---

## Passo 4: Executar o Processo de OCR no Arquivo PNG

Com o motor configurado e a imagem carregada, finalmente **executamos OCR em PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

A chamada `process()` retorna um objeto que contém o texto reconhecido, pontuações de confiança e caixas delimitadoras para cada palavra.

---

## Passo 5: Exibir o Texto Reconhecido

A maneira mais simples de ver o que o motor encontrou é imprimir o atributo `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Saída Esperada

Se `technical_doc.png` contiver a frase *“The Aspocorp licensekey expires on 2025‑12‑31.”*, o console deverá exibir:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Observe como o dicionário personalizado manteve o nome da marca intacto—algo que um OCR padrão poderia ter corrompido.

---

## Exemplo Completo Funcionando (Pronto para Copiar‑Colar)

Abaixo está o script inteiro, pronto para ser salvo como `run_ocr.py`. Basta substituir o caminho placeholder pela localização da sua imagem.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Execute-o a partir do terminal:

```bash
python run_ocr.py
```

Você deverá ver o texto extraído impresso no console, exatamente como mostrado no exemplo anterior.

---

## Perguntas Frequentes (FAQ)

| Pergunta | Resposta |
|----------|----------|
| **Posso extrair texto de um PDF escaneado?** | Sim. Converta cada página para PNG (ou TIFF) primeiro, depois alimente as imagens ao mesmo script. |
| **E se minha imagem for JPEG em vez de PNG?** | O método `Image.load` suporta JPEG, BMP, TIFF e PNG nativamente. Basta mudar a extensão do arquivo. |
| **Como melhorar a precisão em digitalizações de baixo contraste?** | Pré‑procese com `Pillow` – aumente o contraste, aplique binarização ou use `opencv` para corrigir inclinação. |
| **Existe uma forma de obter pontuações de confiança para cada palavra?** | `ocr_result` inclui `words` – cada palavra tem um atributo `confidence` que você pode iterar. |
| **Posso executar isso em um servidor sem interface gráfica?** | Absolutamente. `aocr` não tem dependências de GUI, sendo perfeito para pipelines de CI. |

---

## Próximos Passos & Tópicos Relacionados

Agora que você sabe **como criar OCR** e **extrair texto de imagem**, considere explorar:

* **Técnicas de pré‑processamento** – `load image for OCR` é apenas o primeiro passo; use `opencv` para des‑ruído ou nitidez.  
* **Processamento em lote** – percorra um diretório de PNGs para gerar um arquivo pesquisável.  
* **Suporte multilíngue** – adicione pacotes de idioma ao motor se precisar ler documentos em francês ou alemão.  
* **Integração com Elasticsearch** – indexe o texto extraído para busca full‑text em ativos escaneados.  

Cada uma dessas extensões se baseia no padrão central que acabamos de cobrir, então a transição será tranquila.

---

## Conclusão

Em poucos minutos respondemos **como criar OCR** que extrai texto de arquivos de imagem de forma confiável, especialmente PNGs, e mostramos como **carregar imagem para OCR**, aplicar um **dicionário personalizado** e **executar OCR em PNG** sem serviços externos.  

Teste o script, ajuste o dicionário para combinar com seu próprio jargão, e você terá uma base sólida para qualquer projeto de digitalização de documentos.  

Se encontrou algum obstáculo, deixe um comentário abaixo—estamos felizes em ajudar. E não se esqueça de compartilhar suas histórias de sucesso; a comunidade aprende melhor com exemplos do mundo real.  

**Pronto para automatizar sua papelada?** Pegue o código, adapte-o e comece a transformar pixels em texto pesquisável hoje mesmo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}