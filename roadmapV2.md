# Roadmap v2 — Éco-conception eco-training-starters

> Dernière mise à jour : juin 2026

## Jalons Git

| Tag | Description | Commit | Statut |
|-----|-------------|--------|--------|
| `v0.1-baseline` | Premier commit — état initial du repo (heavy-showcase) | `4528212` | ✅ Atteint |
| `v0.2-cadrage` | Cadrage du projet, ajout du backlog initial (5 User Stories) | `dc40e54` | ✅ Atteint |
| `v1.0-impact` | Implémentation de 4,5/5 optimisations éco-conception (US-01, US-03, US-04, US-05 + partie US-02) | `df12eea` | ✅ Atteint |
| `v1.1-prod` | Finalisation US-02 — build de production + minification JS | — | 🔲 À venir |

---

## Vue d'ensemble des jalons

### ✅ v0.1-baseline → v0.2-cadrage
- Mise en place du repo miroir `heavy-showcase` (anti-patterns volontaires : images lourdes, autoplay, scripts tiers, absence de lazy loading)
- Connexion SonarQube pour l'analyse de qualité de code
- Rédaction du backlog initial (5 User Stories priorisées Haute, voir Backlog.md)

### ✅ v0.2-cadrage → v1.0-impact (cycle actuel)
Implémentation mesurée via Lighthouse Desktop (cache désactivé, mode `npm run dev`) :

| Métrique | Avant (v0.2) | Après (v1.0) | Gain |
|----------|--------------|---------------|------|
| Lighthouse Performance | 61 / 100 | 91–92 / 100 | +30 à +31 pts |
| FCP (First Contentful Paint) | 5,6 s | 1,0 s | −82% |
| LCP (Largest Contentful Paint) | ~10 s | 1,7–1,8 s | −82 à −83% |

**Statut des 5 User Stories** :
- ✅ **US-01** — Pagination du fil d'actualités (5 articles + bouton "charger plus")
- 🟡 **US-02** — Minification JS : partiellement traité (suppression du beacon analytics en bonus) ; minification réelle dépend du build de production, reportée
- ✅ **US-03** — Lazy loading sur toutes les images
- ✅ **US-04** — Tri serveur + payload API allégé
- ✅ **US-05** — Remplacement de l'image hero Contact par un bandeau CSS

---

## Re-priorisation pour le prochain cycle

À l'issue du jalon `v1.0-impact`, **US-02 reste ouverte** : les diagnostics Lighthouse "Minify JavaScript" (699 KiB) et "Reduce unused JavaScript" (660-702 KiB) persistent car les mesures ont été faites en mode développement, où Vite ne minifie pas le bundle.

### Jalon `v1.1-prod` (cible : +2 semaines) — priorité Haute
- [ ] Exécuter `npm run build` pour générer le bundle de production
- [ ] Servir le build de production (`npm run preview` ou équivalent)
- [ ] Mesurer Lighthouse sur le bundle de production
- [ ] Vérifier l'atteinte des cibles US-02 : Performance ≥ 75, JS -700 KiB
- [ ] Vérifier la conformité cache/compression (Gzip/Brotli) en conditions réelles

---

## Notes de tests

- **Outil de mesure** : Lighthouse Desktop (DevTools Chrome), cache désactivé
- **Environnement testé** : `npm run dev` (mode développement — Vite, bundle non minifié)
- **Pages testées** : Accueil (`/`), Actualités (`/news`), Contact (`/contact`)
- **Limite connue** : "Minify JavaScript" et "Reduce unused JavaScript" restent affichés en mode dev malgré les gains de Performance (+30 pts) ; ces diagnostics seront levés par le build de production (US-02, jalon v1.1-prod)
