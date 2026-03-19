---
category: general
date: 2026-03-18
description: Extrair texto de PNG usando Python e Aspose OCR. Aprenda como carregar
  a imagem para OCR, executar OCR em vários arquivos e realizar OCR em lote de imagens
  com reconhecimento de imagem paralelo.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: pt
og_description: Extraia texto de PNG com Aspose OCR em Python. Este tutorial mostra
  como carregar a imagem para OCR, processar OCR em vários arquivos e executar OCR
  em lote de imagens usando reconhecimento de imagem paralelo.
og_title: Extrair texto de PNG – Guia de OCR Paralelo
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extrair texto de PNG – Guia de OCR Paralelo para Reconhecimento de Imagens
  em Lote
url: /pt/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto de PNG – Guia de OCR Paralelo para Reconhecimento de Imagens em Lote

Já precisou **extrair texto de arquivos PNG** mas ficou travado no ponto em que uma única imagem leva uma eternidade para ser processada? Você não está sozinho. Em muitos projetos do mundo real—pense em scanners de faturas, digitalizadores de recibos ou ferramentas de arquivamento—velocidade importa, e processar cada PNG um‑por‑um simplesmente não funciona.  

Neste guia vamos percorrer uma solução completa, pronta‑para‑executar que **carrega imagem para OCR**, executa **ocr multiple files** em um modo de **batch OCR images**, e aproveita **parallel image recognition** com o módulo `threading` do Python. Ao final, você terá um script que extrai texto de qualquer número de PNGs em segundos, não minutos.

## O que você precisará

- Python 3.8 ou mais recente (a sintaxe mostrada funciona também em 3.10+).  
- O pacote Aspose OCR for Java/​Python (`aspose-ocr`). Você pode instalá‑lo via `pip`.  
- Uma pasta com alguns arquivos PNG que deseja processar.  
- Uma quantidade modesta de RAM—cada thread mantém uma pequena instância do motor OCR, então até um laptop pode iniciar dezenas de workers.

Sem serviços externos, sem chaves de nuvem e sem arquivos de configuração misteriosos. Apenas código Python puro que você pode copiar‑colar e executar.

## Por que extrair texto de PNG em paralelo?

Processar um PNG é intensivo em CPU: o motor OCR executa uma série de algoritmos de análise de imagem que consomem os dados de pixel. Quando você tem dez, vinte ou cem imagens, o tempo total de execução é essencialmente a soma de cada execução individual.  

Ao criar uma thread para cada arquivo, deixamos o sistema operacional agendar esses trabalhos pesados de CPU simultaneamente. Em uma máquina multi‑core isso costuma reduzir — ou até dividir — o tempo de relógio. O trade‑off é um consumo de memória ligeiramente maior, mas para a maioria dos jobs em lote o ganho de velocidade vale a pena.

> **Dica profissional:** Se você estiver lidando com centenas de megabytes de imagens, considere usar `concurrent.futures.ProcessPoolExecutor` em vez de `threading`. Processos fornecem paralelismo verdadeiro no interpretador CPython limitado pelo GIL, ao custo de um pouco mais de overhead.

## Etapa 1: Instalar Aspose OCR para Python

Primeiro de tudo—vamos colocar a biblioteca OCR no seu sistema.

```bash
pip install aspose-ocr
```

Essa única linha baixa os binários mais recentes do Aspose OCR e suas ligações para Python. Se você encontrar um erro de permissão, tente adicionar `--user` ou usar um ambiente virtual.

## Etapa 2: Carregar imagem para OCR – a função de trabalho

Agora definimos a rotina principal que será executada em cada thread. Ela **carrega imagem para OCR**, executa o reconhecimento e imprime uma pré‑visualização do texto extraído.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Alguns pontos a observar:

- **Por que um novo `OcrEngine` por thread?** O motor mantém buffers internos; compartilhar uma única instância causaria condições de corrida e saída corrompida.  
- **Por que remover quebras de linha?** Quando registramos no console isso mantém a linha organizada.  
- **Tratamento de erros?** Em produção você envolveria o corpo em um `try/except` e talvez registraria em um arquivo—algo que abordaremos mais adiante.

## Etapa 3: Listar os arquivos PNG que você deseja processar

Você poderia codificar a lista, mas uma abordagem mais flexível é escanear um diretório. Abaixo listamos manualmente três arquivos para clareza; substitua os caminhos pela sua própria pasta.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Se você preferir uma descoberta automática:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Essa pequena alteração permite que você **extraia texto de PNG** em massa sem tocar no código fonte a cada vez.

## Etapa 4: Configurar OCR de múltiplos arquivos com OCR em lote de imagens

Agora criamos uma thread para cada imagem. Este é o coração do padrão de **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

A compreensão de lista mantém o código conciso, e cada objeto `Thread` armazena a função alvo e seu argumento (`image_path`).  

> **Nota lateral:** O módulo `threading` do Python usa threads nativas do SO, então em um laptop de 4‑cores você normalmente verá até quatro threads realmente executando ao mesmo tempo; o restante será agendado conforme os núcleos ficarem livres.

## Etapa 5: Executar reconhecimento de imagem em paralelo

Iniciar os workers é simples: iterar sobre a lista e chamar `start()`. Depois disso esperamos cada thread terminar usando `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Quando o script terminar, você verá uma série de linhas como:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Essa saída confirma que cada PNG foi processado e o texto extraído está disponível para tratamento posterior (por exemplo, salvar em um banco de dados ou alimentar um pipeline de NLP).

## Etapa 6: Verificar os resultados e lidar com casos extremos

### Verificando resultados vazios

Às vezes uma imagem está muito ruidosa, ou o motor OCR falha ao detectar caracteres. Uma verificação rápida pode salvar você de erros posteriores.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limitando o número de threads concorrentes

Se você executar isso em uma VM modesta, criar centenas de threads pode sobrecarregar o escalonador. Você pode limitar a concorrência com um semáforo:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Salvando resultados em um arquivo

Em vez de imprimir, você pode querer um CSV com o nome do arquivo e o texto extraído:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Certifique-se de abrir o CSV **uma única vez** fora da função de thread para evitar condições de corrida; o escritor do módulo `csv` é thread‑safe para gravações simples.

## Exemplo completo em funcionamento

Juntando tudo, aqui está um script único que você pode colocar em um arquivo chamado `batch_ocr.py` e executar:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}