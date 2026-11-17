---
category: general
date: 2026-04-26
description: Como fazer OCR em lote dos seus documentos e extrair texto de digitalizações
  em Python. Aprenda o processamento em lote passo a passo com OcrEngine para saída
  em JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: pt
og_description: Como fazer OCR em lote dos seus arquivos digitalizados e extrair texto
  das digitalizações em um único script. Código completo, dicas e tratamento de casos
  extremos.
og_title: Como fazer OCR em lote – Guia rápido de Python
tags:
- OCR
- Python
- Automation
title: Como fazer OCR em lote – Extraia texto de digitalizações de forma eficiente
url: /pt/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote – Extrair texto de digitalizações de forma eficiente

Já se perguntou **como fazer OCR em lote** em uma montanha de PDFs digitalizados sem perder a sanidade? Você não está sozinho—desenvolvedores perguntam constantemente: *“Como posso extrair texto de digitalizações de uma só vez?”* A boa notícia é que algumas linhas de Python podem transformar essa tarefa tediosa em um pipeline suave e automatizado.

Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que **extrai texto de digitalizações**, salva os resultados como JSON e fornece uma rápida verificação de sanidade ao final. Sem serviços externos, sem mágica—apenas Python puro, a classe `OcrEngine` e um pouco de manipulação de pastas.

## O que você vai levar

- Um script totalmente funcional que **faz OCR em lote** em qualquer pasta de imagens.
- Explicações claras de *por que* cada linha existe, não apenas *o que* ela faz.
- Dicas para lidar com pastas vazias, arquivos que não são imagens e lotes grandes.
- Uma forma de verificar se a saída JSON realmente contém o texto extraído.

### Pré‑requisitos (o mínimo indispensável)

| Requisito | Por que importa |
|-----------|-----------------|
| Python 3.8+ | Sintaxe moderna e dicas de tipo |
| Biblioteca `OcrEngine` (ou um wrapper compatível) | Funcionalidade central de OCR |
| Um diretório com arquivos de imagens digitalizadas (PNG, JPG, TIFF) | Dados de entrada |
| Permissão de escrita para a pasta de saída | Salvar resultados JSON |

Se você já tem isso, ótimo—vamos começar.

![fluxo de batch OCR](image-placeholder.png){alt="fluxo de batch OCR"}

## Etapa 1 – Inicializar o Motor de OCR (como fazer batch OCR)

Antes de podermos processar qualquer coisa, precisamos de uma instância do motor de OCR. Pense nele como o “cérebro” que lerá cada imagem e gerará texto. Inicializá‑lo uma única vez e reutilizá‑lo ao longo de todo o lote é o padrão mais eficiente.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Por que reutilizar a mesma instância?**  
> Criar um novo motor para cada arquivo carregaria repetidamente modelos pesados na memória, desacelerando drasticamente o lote. Uma única instância mantém o modelo na RAM e permite processar milhares de imagens sem uma queda perceptível de desempenho.

## Etapa 2 – Apontar para a Pasta de Digitalizações (extrair texto de digitalizações)

Suas digitalizações estão em algum lugar no disco. Vamos dizer ao script onde encontrá‑las. Usar caminhos absolutos evita surpresas de “arquivo não encontrado” quando o script é iniciado a partir de um diretório de trabalho diferente.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Dica profissional:**  
> Se você estiver no Windows, barras (`/`) funcionam perfeitamente com `os.path.abspath`, então não é necessário escapar as barras invertidas.

## Etapa 3 – Escolher Onde os Resultados JSON Devem Ir

Provavelmente você quer uma pasta organizada para os resultados de OCR. Manter a saída separada da origem facilita a limpeza posterior ou a alimentação do JSON em outro pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Por que criar a pasta programaticamente?**  
> Garante que o script não falhe se o diretório estiver ausente, e `exist_ok=True` torna a operação idempotente—execute o script várias vezes sem erros.

## Etapa 4 – Executar o Processo em Lote (como fazer batch OCR)

Agora o ponto central: dizer ao `ocr_engine` para percorrer cada arquivo em `input_dir`, executar OCR e gravar JSON em `output_dir`. O parâmetro `format="json"` indica ao motor que ele deve serializar o resultado de forma estruturada, que ferramentas downstream adoram.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### O que está acontecendo nos bastidores?

1. **Descoberta de arquivos** – O motor escaneia `input_folder` recursivamente, ignorando arquivos ocultos.
2. **Validação de arquivos** – Apenas extensões de imagem suportadas (`.png`, `.jpg`, `.tif`, etc.) são enviadas ao modelo OCR.
3. **Execução do OCR** – Cada imagem é enviada ao motor OCR; texto, pontuações de confiança e dados de layout são capturados.
4. **Serialização JSON** – O resultado é escrito em um arquivo com o mesmo nome base, porém com extensão `.json`, em `output_folder`.

> **Tratamento de casos extremos:**  
> - **Pasta vazia:** O motor registra “No files found” e retorna graciosamente.  
> - **Imagem corrompida:** Ele ignora o arquivo, registra uma entrada de erro em `batch_errors.log` e continua.  
> - **Lote enorme (10k+ arquivos):** O uso de memória permanece baixo porque cada imagem é processada independentemente.

## Etapa 5 – Confirmar que a Conversão Terminou

Uma simples instrução `print` fornece feedback imediato no console. Para pipelines de produção você pode substituir isso por uma chamada de logging ou uma notificação por e‑mail.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Quando você vir essa linha, pode inspecionar com segurança a pasta `json_output`. Cada arquivo JSON terá aproximadamente este formato:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Agora você pode alimentar esses arquivos JSON em um banco de dados, um índice de busca ou qualquer ferramenta de análise downstream.

## Perguntas Frequentes (e respostas rápidas)

**Q: E se eu precisar processar PDFs em vez de imagens?**  
A: Converta cada página PDF em uma imagem primeiro (por exemplo, usando `pdf2image`) e coloque os arquivos PNG/JPG resultantes em `input_dir`. A lógica de OCR em lote permanece inalterada.

**Q: Posso mudar o formato de saída para texto simples?**  
A: Claro. Substitua `format="json"` por `format="txt"` e o motor escreverá um arquivo `.txt` contendo apenas o texto extraído.

**Q: Minhas digitalizações estão em várias subpastas—o script recursará?**  
A: Sim. `batch_process` percorre a árvore de diretórios por padrão. Se você quiser uma saída plana, defina `flatten=True` (se a biblioteca suportar) ou pós‑procese os nomes dos JSON.

**Q: Como lidar com scripts não latinos?**  
A: Inicialize `OcrEngine` com um parâmetro de idioma, por exemplo, `OcrEngine(lang="spa+eng")`. O loop em lote em si não precisa de alterações.

## Dicas Profissionais & Armadilhas Comuns

- **Tamanho do lote importa:** Se notar picos de CPU, reduza a velocidade do processo com um simples `time.sleep(0.1)` entre arquivos.
- **Logging:** Troque a chamada `print` pelo módulo `logging` do Python para capturar timestamps e níveis de erro.
- **Colisões de nomes de arquivo:** Se duas digitalizações compartilharem o mesmo nome base mas estiverem em subpastas diferentes, os arquivos JSON sobrescreverão uns aos outros. Anexe um hash do caminho relativo ao nome de saída para evitar isso.
- **Vazamentos de memória:** Alguns back‑ends OCR mantêm recursos nativos alocados. Chame `ocr_engine.close()` ao final do seu script se a biblioteca oferecer um método de limpeza.

## Script Completo – Pronto para Copiar & Colar

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Saída esperada no console**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Você pode verificar o JSON abrindo qualquer arquivo em `json_output` com um editor de texto ou carregando-o no Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Você deverá ver o texto OCR‑extraído bruto impresso no console.

## Conclusão

Acabamos de cobrir **como fazer OCR em lote** em um diretório inteiro de imagens digitalizadas e **extrair texto de digitalizações** em arquivos JSON limpos e legíveis por máquina. A abordagem é deliberadamente simples: configure o motor uma vez, aponte para uma pasta e deixe a biblioteca fazer o trabalho pesado. A partir daqui você pode:

- Conectar o JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}