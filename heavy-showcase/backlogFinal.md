# Backlog  pour Éco-conception
## Repo miroir (Brief #2) : heavy-showcase/Édition Territoriale / Collectif Horizon
## Catégorie : Site institutionnel

## US-01 · Priorité P1 

**Contexte**
En tant que visiteur public, je veux accéder au fil d'actualités afin de consulter les différentes chroniques territoriales sans attendre un chargement long.

**Objectif**
Réduire le poids du fil d'actualités chargé en une seule fois  ce qui permet de limiter la consommation réseau côté terminal utilisateur.

**Bonnes pratiques éco-conception ciblées (issues du Brief #1)**
- BP1 — Lazy loading : ne charger que les articles visibles dans le viewport
- BP3 — Pagination côté serveur : ne renvoyer que les N premiers articles au premier appel

**KPI associé**
- Nombre de requêtes initiales ≤ 5
- LCP (Largest Contentful Paint) < 2,5 s
- Gain EcoIndex attendu : +10 pts minimum

**écran concerné**
page Accueil: section fil d'actualités

**Critère de réussite**
Le fil d'actualités se charge sans bloquer le rendu de la page. Seuls les articles visibles dans le viewport sont chargés au premier appel.

**Niveau de priorité**
p1 car ceci a un impact direct sur la consommation réseau et énergétique côté terminal



## US-02 · Priorité P1 

**Contexte**
En tant que visiteur, je veux consulter les dernières chroniques affichées de la plus récente à la plus ancienne afin de trouver les dernières publications sans chercher.

**Objectif**
Corriger l'ordre d'affichage (tri date DESC) et réduire le payload JSON retourné, éviter tout traitement superflu côté client.

**Bonnes pratiques éco-conception ciblées**
- BP2: Réduire le poids JS : déplacer le tri côté serveur plutôt que côté client (moins de calcul terminal)
- BP3: Pagination : ne renvoyer que les champs nécessaires à la liste. 

**KPI associé**
- Chroniques affichées en ordre décroissant (la plus récente en premier)
-Optimisation du payload JSON : -30 % de données échangées vs baseline, réduisant la consommation de ressources (bande passante, énergie serveur et client).
- Aucune requête de tri supplémentaire côté client

**Repo / écran concerné**
page Chroniques/ section Dernières publications

**Critère de réussite**
La chronique la plus récente apparaît systématiquement en première position. Le payload ne contient que les champs nécessaires à l'affichage de la liste.

**Niveau de priorité**
P1 Correction fonctionnelle et gain environnemental combinés


## US-03 · Priorité P2 

**Contexte**
En tant que visiteur cherchant à contacter l'équipe, je veux accéder à la page Contact sans que le chargement soit ralenti par une image hero volumineuse et décorative ou video.

**Objectif**
Supprimer ou optimiser le visuel hero lourd présent sur la page Contact.

**Bonnes pratiques éco-conception ciblées**
- BP5 — Suppression assets décoratifs : supprimer le hero si aucune valeur informative
- BP4 — Conversion WebP/AVIF + attribut loading="lazy" si image conservée
- BP1 — Lazy loading : ne pas charger l'image si elle n'est pas dans le viewport initial

**KPI associé**
- Poids total page Contact < 500 Ko (vs baseline à mesurer)
- Image hero ≤ 80 Ko si conservée
- Gain EcoIndex attendu : +8 pts

**Repo / écran concerné**
Page Contact/section hero droite

**Critère de réussite**
La page Contact passe sous 500 Ko de données transférées. L'image décorative est soit supprimée, soit remplacée par une version optimisée.

**Niveau de priorité**
P2, gain mesurable, effort faible, aucune régression fonctionnelle
