---
category: general
date: 2026-06-22
description: Exécutez le modèle sur le CPU et apprenez à réduire l’utilisation de
  la mémoire GPU en configurant les couches GPU dans Aspose AI. Guide étape par étape
  avec des extraits de code.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: fr
og_description: Exécutez le modèle sur le CPU et réduisez la consommation de mémoire
  GPU en configurant les couches GPU. Tutoriel complet pour la configuration du modèle
  Aspose AI.
og_title: Exécuter le modèle sur le CPU – Réduire l'utilisation de la mémoire GPU
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
title: Exécuter le modèle sur le CPU – Réduire l'utilisation de la mémoire GPU avec
  Aspose AI
url: /fr/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter le modèle sur le CPU – Réduire l’utilisation de la mémoire GPU avec Aspose AI

Vous êtes‑vous déjà demandé comment **exécuter le modèle sur le CPU** lorsque votre serveur ne possède pas de GPU ? Ou peut‑être vous luttez contre des erreurs de manque de mémoire sur un GPU modeste et devez **réduire l’utilisation de la mémoire GPU** sans sacrifier trop de vitesse. Dans ce guide, nous allons passer en revue exactement cela : attacher un post‑processus, initialiser Aspose AI sur le CPU, et ajuster le nombre de couches GPU afin de garder une empreinte mémoire minime.

Nous couvrirons tout, depuis la toute première ligne de code jusqu’à la validation que le modèle utilise réellement la configuration que vous avez demandée. À la fin, vous serez capable de **exécuter le modèle sur le CPU**, **limiter les couches GPU**, et **configurer les couches GPU** pour n’importe quelle charge de travail—pas de magie, juste du Python pur.

## Prérequis

- Python 3.8+ installé (le code utilise des annotations de type mais fonctionne aussi avec des versions antérieures)
- `asposeai` package (installer via `pip install asposeai`)
- Familiarité de base avec les concepts d’inférence de réseaux de neurones (vous n’avez pas besoin d’un doctorat, juste de curiosité)
- Optionnel : une machine avec GPU pour tester le contraste entre les exécutions CPU et GPU

Si vous n’avez pas l’un de ces éléments, installez d’abord le SDK ; le reste du tutoriel suppose que l’import fonctionne.

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## Étape 1 : Attacher le post‑processus de vérification orthographique (aucun paramètre personnalisé requis)

Avant même de penser au CPU ou au GPU, connectons le post‑processus de vérification orthographique fourni avec Aspose AI. C’est une bonne habitude d’attacher les post‑processus tôt afin qu’ils fassent partie de chaque appel d’inférence.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Pourquoi c’est important :* Les post‑processus s’exécutent **après** que le modèle a produit les tokens bruts. En les connectant maintenant, vous garantissez que tout texte que vous générez ensuite—que ce soit sur CPU ou GPU—soit automatiquement nettoyé. C’est une petite étape qui évite les bugs en aval.

## Étape 2 : Exécuter le modèle sur le CPU – Initialiser Aspose AI sans GPU

Voici le cœur du tutoriel : dire à Aspose AI de **exécuter le modèle sur le CPU**. Le SDK expose `AsposeAIModelConfig`, où le paramètre `gpu_layers` contrôle le nombre de couches restant sur le GPU. Le régler à `0` force tout le réseau sur le CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Que se passe-t-il en coulisses ?* Lorsque `gpu_layers=0`, le runtime alloue tous les tenseurs en mémoire hôte. Cela élimine tout besoin de pilotes CUDA, rendant le script exécutable sur pratiquement n’importe quel serveur. Le compromis est un débit plus lent, mais pour les travaux par lots ou les prototypes à faible latence, la simplicité l’emporte souvent sur la vitesse brute.

## Étape 3 : Limiter les couches GPU pour réduire l’utilisation de la mémoire GPU

Si vous avez un GPU mais qu’il manque de mémoire, vous pouvez **limiter les couches GPU** au lieu de tout déplacer vers le CPU. En ne conservant qu’un petit nombre de couches initiales sur le GPU, vous bénéficiez toujours de l’accélération matérielle tout en réduisant drastiquement la consommation de mémoire.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Pourquoi limiter les couches GPU aide :* Les modèles de type transformer modernes allouent la plupart de leur mémoire par couche. Supprimer même quelques couches du GPU peut libérer des centaines de mégaoctets. Cette approche est parfaite pour les « travaux contraints par la mémoire » où vous souhaitez toujours un gain de vitesse pour les calculs les plus lourds.

## Étape 4 : Configurer les couches GPU pour une gestion flexible de la mémoire

Parfois vous avez besoin d’une approche plus granulaire—peut‑être voulez‑vous **configurer les couches GPU** en fonction de la taille spécifique du travail. Le SDK vous permet de lire le nombre total de couches du modèle et de calculer un nombre sûr de couches GPU à l’exécution.

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

*Astuce :* Lorsque vous exécutez sur un serveur partagé, interrogez d’abord la mémoire GPU disponible (`torch.cuda.get_device_properties(0).total_memory`) et ajustez `desired_gpu_layers` en conséquence. Cette étape supplémentaire garantit que vous ne surchargez jamais le GPU, ce qui causerait autrement des plantages OOM.

## Étape 5 : Vérifier la configuration et tester l’inférence

Après avoir configuré, il est judicieux de revérifier où chaque couche réside. Aspose AI fournit une méthode de diagnostic qui renvoie une correspondance des couches aux appareils.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Une fois satisfait, lancez une inference rapide pour voir tout cela en action :

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Si le script affiche le texte attendu et que le rapport de placement correspond à votre configuration, vous avez réussi à **exécuter le modèle sur le CPU**, **réduire l’utilisation de la mémoire GPU**, et **configurer les couches GPU** pour votre scénario.

## Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `CUDA out of memory` erreur | Trop de couches GPU | Réduire `gpu_layers` ou passer à `gpu_layers=0` |
| Pas de sortie de `ai.process` | Modèle non initialisé | S'assurer que `ai.initialize` est appelé **après** avoir attaché les post‑processus |
| Inference lente sur le GPU | Toutes les couches restent encore sur le CPU | Vérifier que `gpu_layers` > 0 et que la carte des appareils montre l’utilisation du GPU |
| Erreurs d’orthographe inattendues | Post‑processus non attaché | Appeler `set_post_processor` avant `initialize` |

## Bonus : Basculer entre CPU et GPU à la volée

Comme le SDK ré‑initialise le modèle chaque fois que vous appelez `initialize`, vous pouvez basculer entre CPU et GPU sans redémarrer votre script.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Appelez simplement `switch_to_cpu()` lorsque vous avez besoin d’une exécution à faible mémoire, et `switch_to_gpu(12)` lorsque vous êtes prêt pour un gain de vitesse.

## Conclusion

Nous avons parcouru un exemple complet et pratique de comment **exécuter le modèle sur le CPU**, **réduire l’utilisation de la mémoire GPU**, **limiter les couches GPU**, et **configurer les couches GPU** avec Aspose AI. Les étapes sont simples :

1. Attacher les post‑processus requis.  
2. Choisir une configuration (`gpu_layers=0` pour un CPU pur, ou un nombre modeste pour le mode mixte).  
3. Initialiser le modèle avec cette configuration.  
4. Vérifier le placement et exécuter une inference de test.  

Armés de ces techniques, vous pouvez garder vos pipelines d’inférence légers, éviter les plantages coûteux d’OOM, et toujours extraire des performances d’un GPU modeste lorsqu’il est disponible. Ensuite, vous pourriez explorer les stratégies de batch, la quantisation, ou même le déchargement de parties du modèle vers le CPU tout en conservant les têtes d’attention sur le GPU—chacun de ces sujets s’appuie directement sur la base **configurer les couches GPU** que vous venez de maîtriser.

Des questions sur une architecture de modèle spécifique ou besoin d’aide pour ajuster le nombre de couches pour un

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Tutoriel Aspose OCR – Reconnaissance optique de caractères](/ocr/english/)
- [Extraire du texte d’une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment faire de l’OCR du texte d’image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}