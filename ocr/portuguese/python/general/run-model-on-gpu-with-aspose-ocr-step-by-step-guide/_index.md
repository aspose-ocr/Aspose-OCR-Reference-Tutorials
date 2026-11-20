---
category: general
date: 2026-03-26
description: Execute o modelo na GPU usando Aspose OCR. Aprenda como baixar o repositório
  do Hugging Face, definir camadas de GPU, importar o Aspose OCR e carregar o modelo
  Qwen2.5 em minutos.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: pt
og_description: Execute o modelo na GPU com Aspose OCR. Este tutorial mostra como
  baixar um repositório do Hugging Face, definir camadas da GPU, importar o Aspose
  OCR e carregar o modelo Qwen2.5.
og_title: Execute o modelo na GPU com Aspose OCR – Guia Completo
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: Execute o modelo na GPU com Aspose OCR – Guia passo a passo
url: /pt/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar modelo na GPU com Aspose OCR – Tutorial Completo

Já se perguntou como **executar modelo na GPU** sem lutar com código CUDA de baixo nível? Você não está sozinho. Muitos desenvolvedores encontram um obstáculo quando precisam acelerar um modelo de linguagem grande, mas ainda desejam a simplicidade de uma biblioteca de alto nível. A boa notícia? Aspose OCR vem com um motor de IA fácil de usar que pode buscar um modelo diretamente do Hugging Face, quantizá‑lo e mover as primeiras doze camadas para sua GPU — tudo em poucas linhas de Python.

Neste guia percorreremos todo o processo: **baixar repositório Hugging Face**, **importar Aspose OCR**, configurar **camadas GPU**, e finalmente **carregar o modelo Qwen2.5**. Ao final você terá um motor OCR pronto para uso que já está rodando na sua placa de vídeo, e entenderá por que cada configuração importa.

## O que você precisará

- Python 3.9 ou mais recente (o código usa type hints e f‑strings)
- Uma GPU compatível com CUDA (opcional, mas recomendada para velocidade)
- Acesso à internet para baixar o modelo do Hugging Face
- O pacote `asposeocr` (`pip install asposeocr`)  

Nenhuma outra dependência externa é necessária — Aspose OCR cuida do trabalho pesado para você.

## Etapa 1: Baixar repositório Hugging Face e importar Aspose OCR

A primeira coisa que você precisa fazer é garantir que os arquivos do modelo estejam disponíveis localmente. O `AsposeAIModelConfig` da Aspose OCR pode buscar automaticamente um repositório do Hugging Face, então você não precisa clonar nada manualmente.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**Por que isso importa:** Importar o pacote lhe dá acesso à classe `AsposeAI`, que encapsula o modelo transformer subjacente. O objeto `AsposeAIModelConfig` é onde você indica ao motor *onde* obter o modelo e *como* tratá‑lo (por exemplo, quantização, alocação de GPU).

> **Dica profissional:** Se você estiver atrás de um proxy corporativo, defina a variável de ambiente `HTTPS_PROXY` antes de executar o script — Aspose OCR respeita as configurações padrão de proxy do Python.

## Etapa 2: Definir camadas GPU para desempenho ideal

Executar um modelo em uma GPU não é um interruptor binário “ligado/desligado”. Você pode decidir quantas das primeiras camadas transformer devem permanecer na GPU enquanto o restante recai para a CPU. Essa abordagem híbrida é útil quando a memória da sua GPU é limitada.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**Por que 20 camadas?** O modelo Qwen2.5‑3B possui 32 blocos transformer. Alocar as primeiras 20 para a GPU lhe dá um ganho sólido de velocidade enquanto mantém o uso de memória sob controle em uma placa de 12 GB. Sinta‑se à vontade para ajustar `gpu_layers` de acordo com seu hardware — definir como `0` força execução apenas na CPU, enquanto `32` tenta colocar tudo na GPU (o que pode causar OOM em placas modestas).

## Etapa 3: Criar o motor de IA e carregar o modelo Qwen2.5

Agora instanciamos o motor e alimentamos a configuração que acabamos de construir. A chamada explícita `initialize` é opcional — Aspose OCR será inicializado de forma preguiçosa no primeiro uso — mas chamá‑la antecipadamente torna a verificação de prontidão mais clara.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**O que acontece nos bastidores?**  
1. Aspose OCR contata o Hugging Face, baixa o arquivo GGUF (se ainda não estiver em cache).  
2. O arquivo é convertido para um formato que o runtime interno entende.  
3. Os primeiros blocos `gpu_layers` são movidos para a memória CUDA; o restante permanece na CPU.  
4. O motor marca a si mesmo como *initialized*, o que você pode consultar com `is_initialized()`.

## Etapa 4: Verificar se o modelo está pronto para rodar na GPU

Uma verificação rápida de sanidade salva você de erros de runtime crípticos mais tarde. O método `is_initialized()` retorna um Boolean, permitindo confirmar que o download, a conversão e a alocação na GPU foram bem‑sucedidos.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

Quando tudo ocorre sem problemas, você deverá ver:

```
AI ready: True
```

Se você obtiver `False`, verifique novamente se seus drivers CUDA estão atualizados e se a GPU tem memória livre suficiente para as 20 camadas solicitadas.

## Opcional: Executar uma inferência rápida de OCR para ver a GPU em ação

Embora o foco do tutorial seja carregar o modelo, a maioria dos leitores logo desejará realmente executar OCR. Aqui está um exemplo mínimo que processa uma imagem local (`sample.png`) e imprime o texto detectado.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**Por que executar isso agora?** Porque a primeira inferência costuma disparar a compilação JIT dos kernels CUDA. Se você cronometrar a chamada com `time.perf_counter()`, notará que a segunda execução é dramaticamente mais rápida — um sinal claro de que o modelo está realmente executando na GPU.

## Armadilhas comuns e como corrigi‑las

| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| `RuntimeError: CUDA out of memory` | `gpu_layers` definido alto demais para sua placa | Diminua `gpu_layers` (ex.: para 12) ou troque para quantização `int8` (já feita). |
| `OSError: Unable to download repository` | Falta de internet ou proxy bloqueando | Defina as variáveis de ambiente `HTTPS_PROXY`/`HTTP_PROXY` ou baixe o arquivo GGUF manualmente e aponte `hugging_face_repo_id` para um caminho local. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | Uso de versão mais antiga do `asposeocr` | Atualize via `pip install --upgrade asposeocr`. |
| `False` de `is_initialized()` | Incompatibilidade de driver CUDA | Verifique se `nvidia-smi` mostra a versão do driver compatível com seu toolkit CUDA. |

## Resumo visual

![Run model on GPU diagram](run-model-on-gpu.png "Diagram showing model download, GPU layer allocation, and inference flow")

*Alt text:* *diagrama de execução do modelo na GPU ilustrando o download de um repositório Hugging Face, a definição das camadas GPU e a execução do modelo Qwen2.5 via Aspose OCR.*

## Recapitulação – O que conseguimos

- **Imported Aspose OCR** and its AI helper classes.  
- **Downloaded a Hugging Face repo** automatically, thanks to `allow_auto_download`.  
- **Set GPU layers** (`gpu_layers=20`) to off‑load the most compute‑intensive parts to the graphics card.  
- **Loaded the Qwen2.5‑3B‑Instruct model** with int8 quantization, dramatically shrinking memory use.  
- **Verified** that the engine is ready (`is_initialized()` returns `True`).  

## Próximos passos e tópicos relacionados

1. **Experiment with different quantizations** (`float16`, `bfloat16`) to see the trade‑off between speed and accuracy.  
2. **Scale up to larger models** (e.g., Qwen2.5‑7B) by adjusting `gpu_layers` and ensuring you have enough VRAM.  
3. **Batch OCR processing**: feed a list of image paths to `ocr_engine.recognize_images()` for higher throughput.  
4. **Integrate with FastAPI** to expose a REST endpoint that runs OCR on incoming files—perfect for microservices.  

Se você está interessado em ajustes de GPU mais avançados, confira o guia oficial de desempenho do Aspose OCR ou a documentação do CUDA Toolkit para variáveis de ambiente como `CUDA_VISIBLE_DEVICES`.

*Feliz codificação! Se este tutorial ajudou você a colocar um modelo rodando na GPU, deixe um comentário ou compartilhe suas próprias adaptações. Quanto mais experimentamos juntos, mais rápido a comunidade aprende.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}