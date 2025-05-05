---
keywords: implémentation, implémentation, configuration, configuration, attributs de profil de script
description: Récupérez des données dans  [!DNL Target]  à l’aide d’attributs de profil de script.
title: Comment obtenir des données dans  [!DNL Target] à l’aide d’attributs de profil de script ?
feature: Implementation
exl-id: ba11f1de-e68b-4505-8e3e-cd4d46ef59a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 74%

---

# Attributs de profil de script

Les attributs de profil de script sont des paires nom/valeur définies dans la solution [!DNL Adobe Target]. La valeur est déterminée grâce à l’exécution d’un fragment de code JavaScript sur le serveur de Target à chaque appel de serveur.

Les utilisateurs écrivent de petits fragments de code qui s’exécutent à chaque appel de mbox, avant l’évaluation de l’appartenance d’audience et de l’appartenance à une activité d’un visiteur.

## Format

Les attributs de profil de script sont créés dans la section Audiences de Target. Tout nom d’attribut est valide et la valeur est le résultat d’une fonction JavaScript écrite par l’utilisateur [!DNL Target]. Les noms d’attributs sont automatiquement précédés du préfixe « user. &quot; dans [!DNL Target] pour les distinguer des attributs de profil internes à la page.

Les fragments de code sont écrits dans le langage JavaScript Rhino et peuvent référencer des jetons et d’autres valeurs.

## Exemples de cas d’utilisation

* **Abandon de panier** : lorsque le visiteur accède au panier, définissez le script de profil sur 1. Lorsque le visiteur convertit, redéfinissez-le sur 0. Si la valeur = 1, le visiteur a un article dans le panier.
* **Nombre de visites** : à chaque nouvelle visite, incrémentez le compteur de 1 pour effectuer le suivi des visites récurrentes d’un visiteur sur le site.

## Avantages de la méthode

Ne nécessite aucune mise à jour du code de page.

S’exécute avant les décisions concernant l’appartenance d’audience et l’appartenance à une activité, ce qui signifie que les attributs de script de profil peuvent affecter l’appartenance sur un appel au serveur unique.

Peut être très robuste. Jusqu’à 2 000 instructions peuvent être exécutées par script.

## Avertissements

Exige la connaissance de JavaScript.

L’ordre d’exécution des scripts de profil ne peut être garanti, ils ne peuvent donc pas dépendre les uns des autres.

Peut être difficile à déboguer.

## Exemples de code

Les scripts de profil sont assez souples :

```
user.purchase_recency: var dayInMillis = 3600 * 24 * 1000; if (mbox.name == 'orderThankyouPage') {  user.setLocal('lastPurchaseTime', new Date().getTime()); } var lastPurchaseTime = user.getLocal('lastPurchaseTime'); if (lastPurchaseTime) {  return ((new Date()).getTime()-lastPurchaseTime)/dayInMillis; }
```

### Liens vers les informations pertinentes

[Attributs de script de profil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=fr#concept_8C07AEAB0A144FECA8B4FEB091AED4D2)
