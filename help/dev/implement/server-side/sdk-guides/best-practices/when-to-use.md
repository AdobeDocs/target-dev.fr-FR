---
source-git-commit: 5c66ee5c8dd5fe60eaeed10fdb9bb6dcee000c89
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---
# Quand utiliser la prise de décision sur l’appareil par rapport à la périphérie

## Tenir compte des cas d’utilisation lors de la décision d’utiliser la prise de décision sur l’appareil

![image alternative](assets/comparison.jpeg)

La principale différence entre *on-device* prise de décision et prise de décision Edge : la prise de décision sur les appareils exécute les décisions localement sur vos serveurs, tandis que les décisions Edge sont prises sur le réseau Adobe Target Edge. La prise de décision sur appareil doit être utilisée pour toute activité A/B ou XT qui doit être diffusée sur des pages à fort trafic, où les performances affectent considérablement les indicateurs clés de performance de votre entreprise, tels que la conversion, les recettes et la rétention. Supposons, par exemple, que votre équipe marketing exécute des campagnes publicitaires pour attirer des prospects vers votre page d’accueil. L’exécution de campagnes publicitaires sur les réseaux d’éditeurs nécessite un paiement. Par conséquent, tout prospect qui parvient sur votre page d’accueil se traduit par un montant en dollars. En même temps, supposons que vous exécutiez des expériences A/B pour déterminer quelle image à forte identification capte le mieux l’attention de votre consommateur. Si la diffusion de ces expériences A/B prend 2 secondes supplémentaires, il est fort probable que le consommateur s’impatiente et rebondit. Voilà vos investissements marketing et vos expériences A/B ! Il est difficile de perdre cette perspective durement acquise, car toute opportunité de convertir cette perspective en client fidèle ou fidèle est désormais perdue. Par conséquent, l’exécution d’une activité de prise de décision sur l’appareil pour ce cas d’utilisation peut éviter tout impact négatif que la latence peut introduire.

D’un autre côté, la prise de décision Edge nécessite un appel de blocage réseau pour récupérer une expérience, mais peut s’avérer très bénéfique, puisque les données en temps réel et le ML peuvent être utilisés pour rendre l’expérience de l’utilisateur final extrêmement attrayante. Un appel de blocage de réseau introduit une latence supplémentaire lors de la diffusion de l’expérience ; toutefois, dans certains cas, ce compromis peut s’avérer judicieux. Prenons l’exemple d’un scénario dans lequel un client parcourt votre catalogue de produits et suppose qu’il accède à une page de détails du produit. Si cette page affiche une liste de produits recommandés, ainsi que le produit actuellement consulté par le client, cela peut améliorer l’engagement, puis la conversion et les recettes. Bien que l’affichage de la liste de produits recommandée de cette manière nécessite une décision anticipée influencée par l’algorithme ML Adobe Target (ce qui signifie qu’il y a une latence ajoutée), cette latence ajoutée n’est pas suffisamment significative pour que l’utilisateur final puisse rebondir. En outre, une liste de produits recommandée se traduit par un taux de conversion plus élevé. Par conséquent, dans ce cas, une décision de périphérie offre à votre entreprise la valeur la plus élevée.

## Fonctionnalités prises en charge

En plus d’évaluer vos cas d’utilisation et vos objectifs commerciaux, passez en revue les fonctionnalités de prise de décision sur les appareils [prend](../on-device-decisioning/supported-features.md) avant de décider s’il faut utiliser la prise de décision sur l’appareil ou la prise de décision sur les périphériques. Actuellement, la prise de décision Edge prend en charge tous les types d’activité, le ciblage des audiences et les méthodes d’attribution.