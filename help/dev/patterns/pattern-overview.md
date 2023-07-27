---
title: Présentation des modèles d’implémentation
description: Comprendre comment utiliser les modèles d’implémentation
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c4b9dfed19e5e4a56bfeae26c4310b997a2d617e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Présentation des modèles d’implémentation

[!DNL Adobe Target] les modèles d’implémentation vous aident à comprendre et à créer l’architecture suivante pour votre [!DNL Target] implémentation.

Cliquez sur l’image pour passer en mode plein écran.

![Diagramme d’architecture Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Notez que les nombres dans l’image n’indiquent pas la séquence des opérations :

1. SDK côté client pour [!DNL Adobe Target] et [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] appel
1. Appel d’acquisition ECID
1. API de mise à jour des profils en masse et [!DNL Customer Attributes] Service (CA)
1. Ingestion des données de profil des sources de données du client vers [!DNL Target] banque de profils
1. Collecter les données de profil/comportement et décider quelle expérience présenter à l’utilisateur final
1. Rendu des expériences sur la page
1. at.js effectue le rendu des expériences sur la page

Chaque motif se compose de différentes parties. Chaque partie correspond à une exigence de mise en oeuvre critique pour votre [!DNL Target] implémentation.

Chaque partie est expliquée sur une page distincte de ce guide. Par exemple, la variable [!DNL Target] Le modèle d’implémentation contient les pages suivantes :

* Initialisation du SDK
* Enrichir le profil
* Expériences de rendu
* Notifier [!DNL Target]

