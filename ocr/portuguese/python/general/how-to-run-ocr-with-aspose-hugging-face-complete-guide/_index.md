---
category: general
date: 2026-04-29
description: Aprenda a executar OCR nas suas digitalizações, usar o modelo Hugging
  Face automaticamente e reconhecer texto das digitalizações com o Aspose OCR em minutos.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: pt
og_description: Como executar OCR em digitalizações usando Aspose OCR, baixar automaticamente
  um modelo do Hugging Face e obter texto limpo e pontuado.
og_title: Como executar OCR com Aspose e Hugging Face – Guia completo
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Como Executar OCR com Aspose e Hugging Face – Guia Completo
url: /pt/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR com Aspose & Hugging Face – Guia Completo

Já se perguntou **como executar OCR** em uma pilha de documentos escaneados sem passar horas ajustando configurações? Você não está sozinho. Em muitos projetos, os desenvolvedores precisam **reconhecer texto de escaneamentos** rapidamente, mas tropeçam em downloads de modelos e no pós‑processamento.  

Boa notícia: este tutorial mostra uma solução pronta‑para‑usar que **usa um modelo Hugging Face**, baixa‑o automaticamente e adiciona pontuação para que a saída pareça ter sido escrita por um humano. Ao final, você terá um script que processa cada imagem em uma pasta e gera um arquivo `.txt` limpo ao lado de cada escaneamento.

## O que Você Precisa

- Python 3.8+ (o código usa f‑strings, então versões mais antigas não funcionam)
- `aspose-ocr` pacote (instale via `pip install aspose-ocr`)
- Acesso à internet para o download do modelo na primeira vez  
- Uma pasta de escaneamentos de imagem (`.png`, `.jpg` ou `.tif`)

É isso—sem binários extras, sem ajustes manuais de modelo. Vamos mergulhar.

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

## Etapa 1: Importar Classes do Aspose OCR & Configurar o Ambiente

Começamos importando as classes necessárias da biblioteca Aspose OCR. Importar tudo de uma vez mantém o script organizado e facilita a identificação de dependências ausentes.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Por que isso importa*: `OcrEngine` faz o trabalho pesado, enquanto `AsposeAI` nos permite conectar um large language model para um pós‑processamento mais inteligente. Se você pular a importação, o resto do código nem vai compilar—então não se esqueça dela.

## Etapa 2: Configurar um Modelo Hugging Face Compatível com GPU  

Agora informamos ao Aspose onde buscar o modelo e quantas camadas devem ser executadas na GPU. O parâmetro `allow_auto_download="true"` cuida da parte de **download automático do modelo** para você.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Dica de especialista**: Se você não tem uma GPU, defina `gpu_layers=0`. O modelo usará a CPU, que é mais lenta mas ainda funciona.

### Por que Escolher um Modelo Hugging Face?

Hugging Face hospeda uma enorme coleção de LLMs prontos‑para‑usar. Ao apontar para `Qwen/Qwen2.5-3B-Instruct-GGUF`, você obtém um modelo compacto, ajustado por instruções, que pode adicionar pontuação, corrigir espaçamento e até corrigir pequenos erros de OCR. Essa é a essência de **usar modelo hugging face** na prática.

## Etapa 3: Inicializar o Motor de IA e Habilitar o Pós‑Processamento de Pontuação  

O motor de IA não serve apenas para chats sofisticados—aqui anexamos um *adicionador de pontuação* que limpa a saída bruta do OCR.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*O que está acontecendo?* A chamada `set_post_processor` registra um pós‑processador embutido que roda após o OCR terminar. Ele recebe a string bruta e insere vírgulas, pontos e letras maiúsculas onde cabem, tornando o texto final muito mais legível.

## Etapa 4: Criar o Motor OCR e Anexar o Motor de IA  

Conectar o motor de IA ao motor OCR nos fornece um único objeto que pode ler caracteres e aprimorar o resultado.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Se você pular esta etapa, o OCR ainda funcionará, mas perderá o aprimoramento de pontuação—então a saída parecerá um fluxo de palavras.

## Etapa 5: Processar Cada Imagem em uma Pasta  

Aqui está o coração do tutorial. Percorremos cada imagem, executamos OCR, aplicamos o pós‑processador e gravamos o texto limpo em um arquivo `.txt` ao lado.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### O que Esperar

Executar o script imprime algo como:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Cada linha informa a pontuação de confiança (uma verificação rápida) e cria `invoice_001.png.txt`, `receipt_2024.tif.txt`, etc., contendo texto pontuado e legível por humanos.

### Casos Limite & Variações

- **Escaneamentos não‑ingleses**: Troque o `hugging_face_repo_id` para um modelo multilíngue (ex.: `microsoft/Multilingual-LLM-GGUF`).
- **Grandes lotes**: Envolva o loop em um `concurrent.futures.ThreadPoolExecutor` para processamento paralelo, mas fique atento aos limites de memória da GPU.
- **Pós‑processamento customizado**: Substitua `"punctuation_adder"` pelo seu próprio script se precisar de limpeza específica de domínio (ex.: remover números de fatura).

## Etapa 6: Limpar Recursos  

Quando o trabalho termina, liberar recursos evita vazamentos de memória, especialmente importante se você estiver executando isso dentro de um serviço de longa duração.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Negligenciar esta etapa pode deixar memória da GPU ocupada, o que sabotaria execuções subsequentes.

## Recapitulação: Como Executar OCR de Ponta a Ponta  

Em apenas algumas linhas, demonstramos **como executar OCR** em uma pasta de escaneamentos, **usar um modelo Hugging Face** que se baixa automaticamente na primeira vez, e **reconhecer texto de escaneamentos** com pontuação adicionada automaticamente. O script completo está pronto para copiar‑colar, ajustar seus caminhos e executar.

## Próximos Passos & Tópicos Relacionados  

- **Pós‑processamento em lote**: Explore `ocr_engine.run_batch_postprocessor` para um manuseio em massa ainda mais rápido.  
- **Modelos alternativos**: Experimente a família `openai/whisper` se precisar de speech‑to‑text junto ao OCR.  
- **Integração com bancos de dados**: Armazene o texto extraído no SQLite ou Elasticsearch para arquivos pesquisáveis.  

Sinta‑se à vontade para experimentar—troque o modelo, ajuste `gpu_layers`, ou adicione seu próprio pós‑processador. A flexibilidade do Aspose OCR combinada com o hub de modelos da Hugging Face torna isso uma base versátil para qualquer projeto de digitalização de documentos.

---

*Feliz codificação! Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação do Aspose OCR para opções de configuração mais avançadas.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}