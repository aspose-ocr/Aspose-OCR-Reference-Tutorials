---
category: general
date: 2026-06-28
description: Como fazer OCR em lote usando Python. Aprenda a fazer OCR em múltiplas
  imagens, extrair texto de PNG e converter imagem em texto com um tutorial completo
  de OCR em Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: pt
og_description: Como fazer OCR em lote no Python explicado na primeira frase. Siga
  este tutorial de OCR em Python para extrair texto de arquivos PNG de forma eficiente.
og_title: Como fazer OCR em lote no Python – Guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Como fazer OCR em lote no Python – Guia completo passo a passo
url: /pt/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em Python – Guia completo passo a passo

Já se perguntou **como fazer OCR em lote** em uma pilha de páginas escaneadas sem escrever um loop que bloqueia sua UI? Você não é o único. Processar dezenas de arquivos PNG um a um pode parecer assistir a tinta secar, especialmente quando cada imagem leva um segundo ou dois para decodificar.  

Neste tutorial vamos mostrar uma maneira limpa e não‑bloqueante de **OCR de múltiplas imagens** de uma vez, **extrair texto de PNG** arquivos, e **converter imagem em texto** usando um motor OCR moderno em Python. Ao final você terá um script pronto‑para‑executar que pode inserir em qualquer projeto – perfeito para um rápido *tutorial de OCR em python* ou um job em lote de nível produção.

## O que você vai construir

- Inicializar um motor OCR e definir seu idioma para Latim (ou qualquer idioma que você precisar).  
- Fornecer uma lista de caminhos de imagens (PNG no nosso exemplo) ao motor.  
- Iniciar uma operação em lote que retorna um objeto semelhante a Future.  
- Obter todos os resultados simultaneamente com um pool de threads, mantendo sua thread principal livre.  
- Imprimir o texto reconhecido para cada página, devidamente separado.

Sem mágica oculta, apenas Python puro e uma biblioteca OCR de terceiros (usaremos o pacote fictício `pyocr` para ilustração).  

**Pré-requisitos**  
- Python 3.8+ instalado.  
- Familiaridade básica com funções Python e `concurrent.futures`.  
- Acesso a uma biblioteca OCR que exponha a classe `OcrEngine` (por exemplo, `pip install pyocr`).  

Se você ainda não tem algum deles, instale agora – é mais fácil do que parece.

---

## Como fazer OCR em lote em Python – Conceitos principais

Antes de mergulharmos no código, vamos responder ao “porquê” de cada etapa.

1. **Por que definir o idioma?**  
   A precisão do OCR dispara quando o motor sabe quais caracteres esperar. Latim funciona para Inglês, Francês, Espanhol, etc. Mude para `Language.Japanese` ou `Language.Arabic` se necessário.

2. **Por que usar uma operação em lote?**  
   Uma chamada em lote permite que o motor agende o trabalho internamente, frequentemente aproveitando threads nativas ou aceleração por GPU. Ela retorna um manipulador que você pode consultar depois, o que significa que não bloqueia enquanto cada imagem é processada.

3. **Por que um ThreadPoolExecutor?**  
   O objeto Future que recebemos de volta é *preguiçoso* – ele só começa a obter resultados quando solicitamos. Ao passar um pool de threads para `getAll`, permitimos que o Python recupere o texto de cada página em paralelo, reduzindo drasticamente o tempo total de execução.

4. **Por que enumerar os resultados?**  
   A ordem dos resultados corresponde à ordem dos caminhos de entrada, então podemos rotular com segurança o número de cada página.

Entender esses “porquês” ajuda a adaptar o padrão a outras bibliotecas ou a conjuntos de dados maiores.

## Etapa 1: Instalar e importar os pacotes necessários

Primeiro, certifique‑se de que a biblioteca OCR está instalada. O exemplo usa um pacote genérico `pyocr`; substitua‑o pela biblioteca real que preferir (por exemplo, `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Agora importe tudo que precisamos.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Dica profissional:** Usar `Path` de `pathlib` torna seu script independente do SO e mais fácil de ler.

## Etapa 2: Criar o motor OCR e definir o idioma

Criar o motor é simples. Vamos fixá‑lo em Latim para esta demonstração.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

A chamada `setLanguage` é opcional para alguns motores, mas é um bom hábito. Ela informa ao modelo OCR para focar no conjunto de caracteres que você deseja, melhorando tanto a velocidade quanto a precisão.

## Etapa 3: Listar os arquivos de imagem a processar (Extrair texto de PNG)

Colete todos os arquivos PNG que você deseja converter. Usar `Path.glob` permite que você coloque uma pasta inteira sem precisar editar o script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Por que isso importa:** Ao ordenar a lista garantimos uma ordem determinística, que depois alinha cada resultado com o número correto da página.

## Etapa 4: Iniciar uma operação de OCR em lote (Converter imagem em texto)

Agora entregamos a lista ao motor. O método retorna um contêiner semelhante a Future que consultaremos depois.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Nos bastidores, o motor pode iniciar suas próprias threads de trabalho ou até mesmo um pipeline de GPU. Tudo que nos importa é que temos um manipulador (`batch_future`) que sabe como buscar os resultados individuais.

## Etapa 5: Recuperar todos os resultados simultaneamente (OCR de múltiplas imagens)

É aqui que realmente *processamos em lote* o trabalho. Ao fornecer um `ThreadPoolExecutor` para `getAll`, o texto de cada página é buscado em sua própria thread.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Você pode ajustar `max_workers` com base nos núcleos da CPU ou nas recomendações da biblioteca OCR. Mais workers ≠ sempre mais rápido – monitore o uso da CPU.

## Etapa 6: Exibir o texto reconhecido (Final do tutorial de OCR em Python)

Finalmente, imprima o texto de cada página. O objeto `Result` expõe `getText()` – ajuste se sua biblioteca usar um nome de método diferente.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Saída esperada (exemplo)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Se alguma imagem falhar, a maioria dos motores insere uma string vazia ou lança uma exceção – você pode envolver o loop em um bloco `try/except` para lidar com casos extremos de forma elegante.

## Script completo – pronto para executar

A seguir está o script completo e autônomo. Copie‑e cole em um arquivo chamado `batch_ocr.py`, ajuste `YOUR_DIRECTORY` e execute `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Salve, execute e observe o console se encher com o texto extraído. Simples, rápido e totalmente assíncrono.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Sem saída** – strings vazias | O motor OCR não encontrou nenhum texto (imagem muito ruidosa) | Pré‑processar imagens: binarizar, corrigir inclinação ou aumentar DPI |
| **FileNotFoundError** | Caminho de diretório errado ou arquivos PNG ausentes | Verifique novamente `YOUR_DIRECTORY` e assegure‑se de que os arquivos terminam com `.png` |
| **Uso alto de CPU** | `max_workers` definido muito alto para sua máquina | Reduza `max_workers` ou habilite aceleração GPU se suportada |
| **Texto Unicode corrompido** | O motor padrão está em um idioma diferente | Chame `engine.setLanguage(Language.Latin)` (ou o apropriado) antes do OCR em lote |

Resolver esses problemas cedo economiza horas de depuração.

## Expandindo o tutorial – próximos passos

- **OCR de múltiplas imagens** em outros formatos (JPEG, TIFF) – basta mudar o padrão glob.  
- **Extrair texto de PNG** e enviá‑lo para um índice de busca (por exemplo, Elasticsearch).  
- **Converter imagem em texto** para geração de PDF usando `reportlab` ou `PyPDF2`.  
- **Paralelizar entre máquinas** com `multiprocessing` ou uma fila de tarefas como Celery para conjuntos de dados massivos.  

Cada um desses tópicos se baseia naturalmente no **tutorial de OCR em python** que você acabou de concluir.

## Conclusão

Nós percorremos **como fazer OCR em lote** em uma coleção de arquivos PNG, demonstramos o poder de uma API orientada a lote e mostramos como **extrair texto de PNG** com uma abordagem baseada em pool de threads. O script completo acima está pronto para produção, e agora você tem uma base sólida para qualquer projeto Python intensivo em OCR.

Experimente, ajuste as configurações de idioma e talvez até substitua `pyocr` por `pytesseract` – o padrão permanece o mesmo. Tem dúvidas ou quer compartilhar um caso de uso interessante? Deixe um comentário e vamos continuar a conversa.

*Feliz codificação!*

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}