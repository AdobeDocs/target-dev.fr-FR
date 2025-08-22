---
title: Présentation de l’API de diffusion Adobe Target
description: Présentation de l’API de diffusion Adobe Target
keywords: api de diffusion
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Présentation de l’API de diffusion

Le [!DNL Adobe Target Delivery API] est basé sur REST. Cette documentation décrit les ressources qui constituent le [!DNL Adobe Target] [!DNL Delivery API]. Les méthodes HTTP sont utilisées pour exécuter des opérations sur ces ressources.

À l’aide de [!UICONTROL Adobe Target's Delivery API], vous pouvez :

* Diffusez des expériences sur le web, y compris les SPA et les canaux mobiles, ainsi que sur des appareils IoT non basés sur un navigateur, tels qu’une télévision connectée, un kiosque ou un écran numérique en magasin.
* Diffusez des expériences à partir de n’importe quelle plateforme ou application côté serveur pouvant effectuer des appels HTTP/s.
* Proposez des expériences cohérentes et personnalisées à un utilisateur, quel que soit le canal ou les appareils qu’il a utilisés dans votre entreprise.
* Mettez en cache les expériences d’un utilisateur au sein d’une session de votre serveur afin d’éviter plusieurs appels d’API et d’obtenir ainsi de meilleures performances.
* Intégrez de manière transparente des produits [!DNL Adobe Experience Cloud] tels que [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] et [!DNL Experience Cloud ID Service] côté serveur.

>[!IMPORTANT]
>
>Soyez prudent lors de la mise à jour de vos [!DNL Recommendations] [!UICONTROL Catalog] via le [!DNL Delivery API]. Le [!DNL Delivery API] est public. Évitez donc de l’utiliser pour remplir les éléments cliquables de votre catalogue de recommandations. Vous risquez ainsi d’introduire du contenu non validé et de polluer votre catalogue.
>
>Bonnes pratiques :
>
>Utilisez le [!DNL Delivery API] uniquement pour mettre à jour les attributs de catalogue qui :
>* Changez fréquemment (par exemple, le prix, le niveau des stocks).
>* Suivez un format prédéfini qui peut être facilement validé sur votre site web.
>* Ne l’utilisez pas pour ajouter ou modifier des éléments cliquables ou tout autre contenu non vérifié.
>
>Si nécessaire, vous pouvez demander au service clientèle de désactiver les mises à jour du catalogue via l’API de diffusion.

Pour plus d’informations, voir la documentation [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

>[!NOTE]
>
>Vous pouvez toujours accéder à la documentation de l’API [héritée /v1/mbox et /v2/batchmbox](https://developers.adobetarget.com/api/legacy-api/index.html). Toutefois, les fonctionnalités seront développées dans l’API de diffusion (comme documenté ici) qui ne seront pas rétroportées dans les API héritées.
