---
date: 2026-05-19
description: Apprenez comment extraire du texte à partir d'images en utilisant Aspose.OCR
  pour .NET, convertir l'image en document et améliorer la précision OCR dans vos
  applications.
keywords:
- extract text from images
- convert image to document
- improve ocr accuracy
- ocr image to txt
- save ocr as pdf
linktitle: Paramètres OCR
second_title: Aspose.OCR .NET API
title: Extraire du texte à partir d'images – Paramètres OCR avec Aspose.OCR
url: /fr/net/ocr-settings/
weight: 26
---

{{< blocks/products/pf/main-wrap-class >}}  
{{< blocks/products/pf/main-container >}}  
{{< blocks/products/pf/tutorial-page-section >}}  

# Extraire du texte à partir d'images – Paramètres OCR avec Aspose.OCR  

## Introduction  

Dans le monde numérique d'aujourd'hui, où tout évolue rapidement, **extraire du texte à partir d'images** est une capacité cruciale pour tout, de la traitement des factures aux archives consultables. Aspose.OCR pour .NET vous fournit un moteur puissant, prêt à l'emploi, capable de transformer n'importe quelle image en texte modifiable, PDF, DOCX ou fichiers texte brut. Dans ce guide, nous passerons en revue les paramètres OCR les plus courants, expliquerons *pourquoi* chacun d'eux est important, et vous montrerons comment les appliquer dans des scénarios réels afin d'améliorer la précision, la vitesse et la flexibilité de vos applications.  

## Réponses rapides  
- **Que signifie « extract text from images » ?** C’est le processus de reconnaissance des caractères dans les fichiers image et de les restituer sous forme de texte modifiable.  
- **Quelle bibliothèque gère cela le mieux sous .NET ?** Aspose.OCR pour .NET offre une précision leader du secteur et une prise en charge multilingue.  
- **Puis-je convertir le résultat OCR en PDF ou DOCX ?** Oui – le tutoriel « Save Result as Document » vous montre comment exporter en PDF, DOCX ou TXT en un seul appel.  
- **Comment accélérer l'OCR pour de gros lots ?** Augmentez le nombre de threads (voir « Set Threads Count ») pour exécuter la reconnaissance en parallèle.  
- **Le réglage fin est‑il possible ?** Absolument – vous pouvez définir les valeurs de seuil, créer une liste blanche des caractères autorisés, une liste noire des caractères ignorés, et charger des packs de langues pour des résultats optimaux.  

## Qu’est‑ce que « extract text from images » ?  

Il convertit la représentation visuelle des caractères en texte Unicode modifiable en analysant les motifs de pixels, en appliquant un prétraitement tel que la binarisation et la réduction du bruit, puis en utilisant des modèles de langue entraînés pour reconnaître chaque glyphe. Les chaînes résultantes peuvent être stockées, recherchées, indexées ou traitées davantage dans vos applications.  

## Pourquoi utiliser Aspose.OCR pour .NET ?  

Chargez la bibliothèque Aspose.OCR et vous obtenez instantanément la prise en charge de **plus de 50 formats d'entrée et de sortie** — y compris JPEG, PNG, BMP, TIFF, la conversion PDF‑vers‑image, et plus – ainsi que la capacité de traiter des fichiers jusqu'à **500 Mo** sans épuiser la mémoire. Le moteur offre **jusqu'à 98 % de précision** sur des scans propres et fournit un prétraitement intégré qui améliore les images à faible contraste ou bruitées pour obtenir des résultats quasi parfaits.  

## Enregistrer le résultat en document dans la reconnaissance d'image OCR  

`SaveResultAsDocument` enregistre la sortie OCR directement dans un fichier document.  

Lorsque vous appelez `ocrEngine.SaveResultAsDocument(outputPath, SaveFormat.Pdf)`, Aspose.OCR écrit le texte dans un PDF avec des calques de texte sélectionnables, permettant la recherche et la fonction copier‑coller sans aucun post‑traitement supplémentaire.  

## Définir le nombre de threads dans la reconnaissance d'image OCR  

Ajuster le pool de threads contrôle le nombre de pages d'image traitées simultanément.  

**Définition :** La propriété `ThreadsCount` détermine le nombre maximal de threads de travail OCR parallèles que le moteur va créer.  

Augmenter cette valeur de la valeur par défaut **1** à **4** (ou plus sur des serveurs multi‑cœurs) peut réduire le temps de traitement de **30‑70 %** pour de gros lots, tout en respectant la limite de mémoire que vous avez définie dans la configuration de votre application.  

## Définir la valeur de seuil dans la reconnaissance d'image OCR  

La binarisation convertit une image en niveaux de gris en un bitmap noir et blanc, ce qui est crucial pour les sources à faible contraste.  

**Définition :** La propriété `Threshold` définit le seuil de luminance (0‑255) utilisé lors de la binarisation.  

Pour un scan fané, un seuil de **180** donne souvent des contours de caractères plus nets, réduisant les faux positifs jusqu'à **15 %** par rapport au réglage automatique par défaut.  

## Spécifier les caractères autorisés dans la reconnaissance d'image OCR  

Parfois, vous n'avez besoin que d'un sous‑ensemble de caractères, comme les chiffres pour les numéros de série.  

**Définition :** La collection `AllowedCharacters` agit comme une liste blanche, limitant la reconnaissance aux caractères que vous spécifiez.  

En limitant le moteur à "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ", vous pouvez éliminer le bruit de la ponctuation et améliorer la précision des codes alphanumériques de **20 %**.  

## Spécifier les caractères ignorés dans la reconnaissance d'image OCR  

Inversement, vous pouvez vouloir ignorer les caractères qui apparaissent fréquemment comme du bruit.  

**Définition :** La collection `IgnoredCharacters` est une liste noire qui indique au moteur OCR de supprimer les symboles correspondants pendant la reconnaissance.  

Supprimer les artefacts courants comme « # » ou « $ » lorsqu'ils ne font pas partie des données cibles réduit considérablement les taux de mauvaise reconnaissance, surtout dans les formulaires numérisés.  

## Travailler avec différentes langues dans la reconnaissance d'image OCR  

Aspose.OCR est fourni avec des packs de langues pour **plus de 30 scripts**, du latin au cyrillique, en passant par l'arabe et les caractères asiatiques.  

**Définition :** La propriété `Language` sélectionne le modèle de langue qui guide l'analyse de la forme des caractères.  

Charger le pack approprié (par ex., `ocrEngine.Language = Language.French`) augmente la précision sur les documents multilingues de **10‑25 %**, car le moteur applique des heuristiques spécifiques à chaque script.  

## Tutoriels des paramètres OCR  
### [Enregistrer le résultat en document dans la reconnaissance d'image OCR](./save-result-as-document/)  
Débloquez le potentiel d'Aspose.OCR pour .NET. Reconnaissez facilement du texte dans les images et enregistrez les résultats dans divers formats de documents.  
### [Définir le nombre de threads dans la reconnaissance d'image OCR](./set-threads-count/)  
Débloquez l'efficacité de l'OCR sous .NET. Définissez le nombre de threads sans effort avec Aspose.OCR. Améliorez la précision et la vitesse.  
### [Définir la valeur de seuil dans la reconnaissance d'image OCR](./set-threshold-value/)  
Explorez Aspose.OCR pour .NET, une solution OCR robuste. Définissez facilement des valeurs de seuil personnalisées. Améliorez la reconnaissance de texte dans vos applications.  
### [Spécifier les caractères autorisés dans la reconnaissance d'image OCR](./specify-allowed-characters/)  
Débloquez un OCR précis sous .NET avec Aspose.OCR. Reconnaissez facilement du texte à partir d'images. Téléchargez dès maintenant pour une expérience de développement transformative.  
### [Spécifier les caractères ignorés dans la reconnaissance d'image OCR](./specify-ignored-characters/)  
Explorez les capacités avancées d'OCR avec Aspose.OCR pour .NET. Efficace, précis et convivial pour les développeurs.  
### [Travailler avec différentes langues dans la reconnaissance d'image OCR](./working-with-different-languages/)  
Débloquez la magie de l'OCR multilingue avec Aspose.OCR pour .NET. Extrayez du texte sans effort dans diverses langues.  

## Comment extraire du texte d'images avec Aspose.OCR – Aperçu des paramètres communs  

Chargez votre moteur OCR, configurez les paramètres souhaités, et appelez `Recognize` – c’est le flux de travail principal en **moins de 10 lignes de code**. En maîtrisant les paramètres communs ci‑dessous, vous pouvez adapter le moteur pour la vitesse, la précision ou la prise en charge multilingue, selon les besoins de votre projet.  

| Paramètre | Objectif | Quand l'utiliser |
|-----------|----------|-------------------|
| **Save Result as Document** | Exporter la sortie OCR en PDF/DOCX/TXT | Lorsque vous avez besoin d'un document réutilisable et consultable |
| **Threads Count** | Contrôler le traitement parallèle | Lots importants ou applications critiques en termes de performance |
| **Threshold Value** | Ajuster la binarisation de l'image | Images à faible contraste ou bruitées |
| **Allowed Characters** | Liste blanche de symboles spécifiques | Données spécifiques au domaine (par ex., numéros de série) |
| **Ignored Characters** | Liste noire des symboles indésirables | Supprimer le bruit comme la ponctuation |
| **Language Packs** | Activer la reconnaissance multilingue | Documents contenant des scripts non latins |

## Questions fréquemment posées  

**Q : Puis‑je utiliser Aspose.OCR dans un projet .NET Core ?**  
R : Oui, Aspose.OCR pour .NET prend pleinement en charge .NET Core, .NET 5+ et .NET 6+ avec la même surface d’API.  

**Q : Comment améliorer la précision de l'OCR sur des images basse résolution ?**  
R : Augmentez la valeur `Threshold`, activez le pack `Language` approprié, et envisagez de spécifier `AllowedCharacters` pour limiter l'ensemble de caractères.  

**Q : Est‑il possible d'extraire du texte directement à partir de PDF ?**  
R : Bien qu'Aspose.OCR se concentre sur les fichiers image, vous pouvez d'abord convertir les pages PDF en images avec Aspose.PDF, puis exécuter l'OCR sur les images résultantes.  

**Q : Quelles licences sont requises pour une utilisation en production ?**  
R : Une licence commerciale Aspose.OCR est requise pour le déploiement ; un essai gratuit de 30 jours est disponible pour l'évaluation.  

**Q : Existe‑t‑il des limites de taille pour les images que je peux traiter ?**  
R : La bibliothèque gère confortablement les images jusqu'à **500 Mo** ; pour des fichiers plus volumineux, augmentez `ThreadsCount` et ajustez les paramètres de mémoire en conséquence.  

---  

**Dernière mise à jour :** 2026-05-19  
**Testé avec :** Aspose.OCR 24.11 for .NET  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Extraire du texte d'image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/net/ocr-optimization/)
- [Définir le nombre de threads pour améliorer la précision de l'OCR sous .NET](/ocr/net/ocr-settings/set-threads-count/)
- [Reconnaître le texte d'image avec Aspose OCR pour plusieurs langues](/ocr/net/ocr-settings/working-with-different-languages/)


{{< /blocks/products/pf/tutorial-page-section >}}  
{{< /blocks/products/pf/main-container >}}  
{{< /blocks/products/pf/main-wrap-class >}}