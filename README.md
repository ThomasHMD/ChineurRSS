# Chineur RSS

Flux RSS statique du **Chineur de Livres Photo**.

Généré chaque lundi à 00h10 (Europe/Paris) par un workflow n8n qui :
1. interroge la base Notion `Ma bibliothèque`,
2. sélectionne 10 livres en promo (réduction ≥ 25%, visibles dans le Chineur),
3. reconstruit `feed.xml` et le pousse sur la branche `main`.

Le fichier est ensuite servi par GitHub Pages à l'URL :

```
https://thomashmd.github.io/ChineurRSS/feed.xml
```

C'est cette URL qui est consommée par Metricool pour programmer automatiquement les publications sociales.

## Pourquoi un fichier statique ?

L'ancien système exposait un webhook n8n que Metricool polait en boucle (plusieurs fois par heure). Chaque appel déclenchait l'exécution d'un workflow complet (Notion + code + réponse) et faisait tourner 4 services Railway pour rien. Le passage à un fichier statique élimine 100% de ces exécutions inutiles.
