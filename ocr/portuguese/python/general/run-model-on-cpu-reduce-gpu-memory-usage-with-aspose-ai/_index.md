---
category: general
date: 2026-06-22
description: Execute o modelo na CPU e aprenda a reduzir o uso de memória da GPU configurando
  camadas de GPU no Aspose AI. Guia passo a passo com trechos de código.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: pt
og_description: Execute o modelo na CPU e reduza o consumo de memória da GPU configurando
  as camadas da GPU. Tutorial completo para configuração do modelo Aspose AI.
og_title: Executar modelo na CPU – Reduzir uso de memória da GPU
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Executar modelo na CPU – Reduzir o uso de memória da GPU com Aspose AI
url: /pt/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar Modelo na CPU – Reduzir Uso de Memória da GPU com Aspose AI

Já se perguntou como **executar modelo na CPU** quando seu servidor não tem GPU disponível? Ou talvez você esteja enfrentando erros de falta de memória em uma GPU modesta e precise **reduzir o uso de memória da GPU** sem sacrificar muito desempenho. Neste guia vamos percorrer exatamente isso: anexar um pós‑processador, inicializar o Aspose AI na CPU e ajustar o número de camadas da GPU para manter a pegada de memória mínima.

Cobriremos tudo, desde a primeira linha de código até a validação de que o modelo realmente está usando a configuração solicitada. Ao final, você será capaz de **executar modelo na CPU**, **limitar camadas da GPU** e **configurar camadas da GPU** para qualquer carga de trabalho — sem mágica, apenas Python puro.

## Pré‑requisitos

- Python 3.8+ instalado (o código usa type hints, mas funciona em versões mais antigas)
- Pacote `asposeai` (instale via `pip install asposeai`)
- Familiaridade básica com conceitos de inferência de redes neurais (não é preciso PhD, só curiosidade)
- Opcional: uma máquina com GPU habilitada para testar a diferença entre execuções na CPU e na GPU

Se estiver faltando algum desses itens, instale o SDK primeiro; o restante do tutorial assume que a importação funciona.

![Diagrama ilustrando como executar modelo na CPU em vez da GPU](run-model-on-cpu-diagram.png)

## Etapa 1: Anexar o Pós‑Processador de Verificação Ortográfica (Sem Configurações Personalizadas)

Antes de pensar em CPU ou GPU, vamos conectar o pós‑processador de verificação ortográfica que o Aspose AI fornece. É uma boa prática anexar pós‑processadores logo no início, para que façam parte de cada chamada de inferência.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Por que isso importa:* Pós‑processadores são executados **depois** que o modelo produz os tokens brutos. Ao configurá‑los agora, você garante que qualquer texto gerado — seja na CPU ou na GPU — seja limpo automaticamente. É um passo pequeno que evita bugs posteriores.

## Etapa 2: Executar Modelo na CPU – Inicializar Aspose AI Sem GPU

Agora vem o núcleo do tutorial: dizer ao Aspose AI para **executar modelo na CPU**. O SDK expõe `AsposeAIModelConfig`, onde o parâmetro `gpu_layers` controla quantas camadas permanecem na GPU. Definir `0` força toda a rede para a CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*O que está acontecendo nos bastidores?* Quando `gpu_layers=0`, o runtime aloca todos os tensores na memória do host. Isso elimina a necessidade de drivers CUDA, permitindo que o script rode em praticamente qualquer servidor. O trade‑off é menor taxa de transferência, mas para jobs em lote ou protótipos de baixa latência a simplicidade costuma superar a velocidade bruta.

## Etapa 3: Limitar Camadas da GPU para Reduzir Uso de Memória da GPU

Se você tem uma GPU, mas ela está apertada de memória, pode **limitar camadas da GPU** em vez de mover tudo para a CPU. Mantendo apenas algumas camadas iniciais na GPU, ainda se beneficia da aceleração de hardware enquanto reduz drasticamente o consumo de memória.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Por que limitar camadas da GPU ajuda:* Modelos transformer modernos alocam a maior parte da memória por camada. Remover até algumas camadas da GPU pode liberar centenas de megabytes. Essa abordagem é perfeita para “jobs com restrição de memória” onde ainda se deseja um ganho de velocidade nas computações mais pesadas.

## Etapa 4: Configurar Camadas da GPU para Gerenciamento Flexível de Memória

Às vezes é preciso um controle mais granular — talvez você queira **configurar camadas da GPU** com base no tamanho específico do job. O SDK permite ler o número total de camadas do modelo e calcular um número seguro de camadas da GPU em tempo de execução.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Dica de especialista:* Quando rodar em um servidor compartilhado, consulte a memória de GPU disponível primeiro (`torch.cuda.get_device_properties(0).total_memory`) e ajuste `desired_gpu_layers` de acordo. Essa etapa extra garante que você nunca sobrecarregue a GPU, evitando crashes por OOM.

## Etapa 5: Verificar a Configuração e Testar a Inferência

Depois de definir a configuração, é prudente confirmar onde cada camada está alocada. O Aspose AI fornece um método diagnóstico que devolve um mapeamento de camadas para dispositivos.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Quando estiver satisfeito, execute uma inferência rápida para ver tudo em ação:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Se o script imprimir o texto esperado e o relatório de alocação corresponder à sua configuração, você conseguiu **executar modelo na CPU**, **reduzir uso de memória da GPU** e **configurar camadas da GPU** para o seu cenário.

## Armadilhas Comuns & Como Evitá‑las

| Sintoma | Causa Provável | Correção |
|---------|----------------|----------|
| Erro `CUDA out of memory` | Muitas camadas na GPU | Diminua `gpu_layers` ou troque para `gpu_layers=0` |
| Nenhuma saída de `ai.process` | Modelo não inicializado | Garanta que `ai.initialize` seja chamado **depois** de anexar os pós‑processadores |
| Inferência lenta na GPU | Todas as camadas ainda na CPU | Verifique se `gpu_layers` > 0 e se o mapa de dispositivos mostra uso da GPU |
| Erros ortográficos inesperados | Pós‑processador não anexado | Chame `set_post_processor` antes de `initialize` |

## Bônus: Alternar Entre CPU e GPU em Tempo Real

Como o SDK reinicializa o modelo a cada chamada de `initialize`, você pode alternar entre CPU e GPU sem reiniciar o script.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Basta chamar `switch_to_cpu()` quando precisar de uma execução de baixa memória, e `switch_to_gpu(12)` quando estiver pronto para acelerar.

## Conclusão

Percorremos um exemplo completo e prático de como **executar modelo na CPU**, **reduzir uso de memória da GPU**, **limitar camadas da GPU** e **configurar camadas da GPU** com Aspose AI. Os passos são simples:

1. Anexe os pós‑processadores necessários.  
2. Escolha uma configuração (`gpu_layers=0` para CPU puro, ou um número modesto para modo misto).  
3. Inicialize o modelo com essa configuração.  
4. Verifique a alocação e execute uma inferência de teste.  

Com essas técnicas, você pode manter seus pipelines de inferência leves, evitar crashes custosos por OOM e ainda extrair desempenho de uma GPU modesta quando disponível. Em seguida, explore estratégias de batching, quantização ou até mesmo off‑loading de partes do modelo para a CPU enquanto mantém as cabeças de atenção na GPU — cada um desses tópicos se baseia diretamente na fundação de **configurar camadas da GPU** que você acabou de dominar.

Tem dúvidas sobre uma arquitetura de modelo específica ou precisa de ajuda para ajustar a contagem de camadas para um

## O Que Você Deve Aprender a Seguir?

Os tutoriais abaixo abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Tutorial Aspose OCR – Reconhecimento Óptico de Caracteres](/ocr/english/)
- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Fazer OCR de Texto em Imagem com Idioma Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}