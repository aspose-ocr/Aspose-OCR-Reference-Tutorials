---
category: general
date: 2026-03-13
description: Le tutoriel OCR en direct montre comment définir la langue OCR et détecter
  les flux vidéo de texte en temps réel à l'aide d'Aspose.OCR. Suivez le guide étape
  par étape.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: fr
og_description: Le tutoriel OCR en direct explique comment définir la langue OCR et
  détecter le texte dans les flux vidéo en utilisant Aspose.OCR Live en C#. Code complet
  inclus.
og_title: 'Tutoriel OCR en direct : Détection de texte en temps réel dans la vidéo'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Tutoriel OCR en direct : détecter du texte dans une vidéo avec C#'
url: /fr/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR en direct : détecter du texte dans une vidéo avec C#

Vous avez déjà eu besoin d’un **live OCR tutorial** qui fonctionne réellement sur un flux vidéo ? Peut‑être que vous créez une application de caméra intelligente ou une superposition de traduction en temps réel et que vous êtes bloqué sur « comment extraire le texte de chaque image ? ». La bonne nouvelle, c’est que vous n’avez pas besoin de réinventer la roue. Dans ce guide, nous parcourrons un exemple complet et exécutable qui **définit la langue OCR**, récupère des images d’une caméra, et **détecte du texte vidéo** en temps réel.

Nous utiliserons la classe `LiveOcr` d’Aspose.OCR, spécialement conçue pour les scénarios à faible latence. À la fin de cet article, vous disposerez d’une application console qui affiche le premier texte détecté puis se ferme — parfait comme point de départ pour des pipelines plus sophistiqués.

## Prérequis

- .NET 6.0 SDK (ou toute version récente de .NET)  
- Visual Studio 2022 ou VS Code (votre IDE préféré)  
- Package NuGet `Aspose.OCR` (installer via `dotnet add package Aspose.OCR`)  
- Une webcam ou toute source vidéo capable de fournir des images `Bitmap`

Aucune bibliothèque native supplémentaire n’est requise ; Aspose.OCR fournit tout ce dont vous avez besoin.

## Étape 1 : Installer Aspose.OCR et ajouter les espaces de noms

Avant d’écrire du code, assurez‑vous que la bibliothèque Aspose OCR est référencée. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ensuite, en haut de votre `Program.cs`, importez les espaces de noms que nous allons utiliser :

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Astuce :** Si vous utilisez Visual Studio, l’IDE suggérera automatiquement les instructions `using` après que vous ayez tapé les noms de classe.

## Étape 2 : Créer et configurer l’instance LiveOcr

Le cœur du tutoriel est l’objet `LiveOcr`. Nous devons lui indiquer quelle langue rechercher et, éventuellement, appliquer des filtres de pré‑traitement (comme le redressement) pour améliorer la précision.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

Pourquoi définir la langue ? Les moteurs OCR utilisent des dictionnaires et des modèles de caractères spécifiques à chaque langue ; spécifier l’anglais réduit les faux positifs et accélère la reconnaissance. Si vous avez besoin d’une autre langue, remplacez simplement `Language.English` par `Language.Spanish`, `Language.French`, etc.

## Étape 3 : Capturer des images depuis votre caméra

Dans un projet réel, vous remplaceriez la méthode factice `CaptureFrameFromCamera()` par une logique de capture réelle — peut‑être en utilisant `AForge.Video`, `OpenCvSharp` ou l’API Windows Media Capture. Pour les besoins de ce tutoriel, nous garderons la méthode abstraite, mais nous montrerons un exemple rapide avec `AForge`.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **Cas particulier :** Si la caméra n’est pas disponible, `CaptureFrameFromCamera` renverra `null`. Protégez toujours votre code de production contre cela.

## Étape 4 : Traiter chaque image jusqu’à ce qu’un texte soit trouvé

Nous bouclons maintenant sur un nombre fixe d’images (ou indéfiniment) et transmettons chaque bitmap à `LiveOcr.ProcessFrame`. Dès que nous obtenons une chaîne non vide, nous l’affichons et sortons de la boucle.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### Pourquoi une pause ?

`Thread.Sleep(30)` laisse le pilote de la caméra respirer et réduit l’utilisation du CPU. Dans des scénarios haute performance, vous pourriez le remplacer par un contrôleur de fréquence d’images plus sophistiqué.

## Étape 5 : Regrouper le tout dans une application console

En rassemblant le tout, voici le programme complet, prêt à copier‑coller. Enregistrez‑le sous le nom `Program.cs` dans un nouveau projet console (`dotnet new console`) et exécutez `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### Sortie attendue

Lorsque la caméra voit du texte anglais lisible (par exemple, une étiquette imprimée), vous verrez quelque chose comme :

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Si rien n’est visible, la boucle se terminera après 100 itérations et affichera « Live OCR session ended ». Vous pouvez augmenter le nombre d’itérations ou remplacer la boucle `for` par un `while (true)` pour une surveillance continue.

## Questions fréquentes & pièges

| Question | Réponse |
|----------|--------|
| **Puis-je traiter plusieurs langues simultanément ?** | Oui. Définissez `Language = Language.English | Language.Spanish;` (OU bit à bit) pour activer un dictionnaire multilingue. |
| **Que faire si mes images sont volumineuses et que l’OCR semble lent ?** | Réduisez la taille du bitmap avant d’appeler `ProcessFrame`. Exemple : `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Ai‑je besoin d’une licence pour Aspose.OCR ?** | Une licence d’évaluation temporaire fonctionne jusqu’à 30 jours. En production, achetez une licence pour supprimer le filigrane. |
| **Comment gérer le texte tourné ?** | Le `DeskewFilter` corrige déjà les petites rotations. Pour des angles extrêmes, ajoutez un `RotateFilter` au pipeline. |
| **Cette approche est‑elle thread‑safe ?** | Les instances `LiveOcr` ne sont pas thread‑safe. Créez‑en une par thread ou protégez l’accès avec un verrou. |

## Étendre le tutoriel

Maintenant que vous avez une base de **live OCR tutorial**, envisagez les étapes suivantes :

1. **Diffuser vers une UI** – afficher la vidéo en direct avec les résultats OCR superposés en utilisant `Windows Forms` ou `WPF`.  
2. **Traitement par lots** – acheminer les images dans une file d’attente et exécuter l’OCR sur un pool de travailleurs en arrière‑plan pour un débit plus élevé.  
3. **Détection de langue** – intégrer une bibliothèque d’identification de langue pour changer `LiveOcr.Language` à la volée.  
4. **Persister les résultats** – écrire les chaînes détectées dans une base de données ou un fichier CSV pour l’analyse.  

Chacune de ces extensions repose toujours sur les concepts de base que nous avons couverts : initialiser `LiveOcr`, **définir la langue OCR**, et **détecter des images vidéo contenant du texte** en temps réel.

---

### TL;DR

- Installez Aspose.OCR via NuGet.  
- Créez un objet `LiveOcr`, **définissez la langue OCR** (anglais dans l’exemple).  
- Capturez des images `Bitmap` depuis une caméra.  
- Parcourez les images, appelez `ProcessFrame`, et arrêtez‑vous dès qu’un texte apparaît.  
- Le programme complet ci‑dessus est prêt à être exécuté et constitue une base solide pour tout projet de détection de texte en temps réel.

Essayez‑le, ajustez le pipeline de pré‑traitement, et voyez votre application commencer à lire le monde image par image. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}