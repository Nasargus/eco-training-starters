# Backlog v2 — Éco-conception eco-training-starters

> Dernière mise à jour : juin 2026 — Tag associé : `v1.0-impact`

## Synthèse — 5 User Stories prioritaires

| ID | User Story | Page | Bonne Pratique (RGESN) | Cible / KPI | Priorité | Statut |
|----|------------|------|-------------------------|-------------|----------|--------|
| US-01 | Pagination/Lazy load fil d'actualités — charger sans bloquer le rendu initial | Accueil | RGESN 6.1/6.2 ; réduire requêtes/écran | Requêtes ≤ 15, LCP < 5 s | Haute | ✅ Fait |
| US-02 | Minification JavaScript — éliminer code mort et optimiser bundle | Accueil | RGESN 6.1 ; éliminer code mort, minify | JS -700 KiB, Performance ≥ 75 | Haute | 🟡 Partiel |
| US-03 | Lazy loading images — charger images uniquement au scroll | Accueil | RGESN 6.1/6.2 ; lazy load, compression | Images -800 Ko, LCP < 4 s | Haute | ✅ Fait |
| US-04 | Tri serveur + Allégement API — optimiser payload et tri date DESC | Actualités | RGESN 6.1 ; sobriété données, API | Payload -30%, transfert < 50 kB | Haute | ✅ Fait |
| US-05 | Suppression/Optimisation hero image — réduire poids Contact | Contact | RGESN Stratégie ; éliminer contenus non essentiels | Poids < 500 Ko, LCP < 3 s | Haute | ✅ Fait |

---

## Détail par User Story

### US-01 — Pagination / Lazy load fil d'actualités ✅
- **Fichier modifié** : `frontend/src/ShowcaseApp.tsx` (NewsPage)
- **Action réalisée** : ajout d'un état `visible` (PAGE_SIZE = 5), `articles.slice(0, visible)`, bouton "Charger plus d'articles"
- **Résultat mesuré** : LCP 10,15 s → ~1,7 s, Lighthouse Performance 61 → 91
- **Commit** : `df12eea`

### US-02 — Minification JavaScript 🟡 Partiel
- **Constat** : Lighthouse signale toujours 699 KiB de "Minify JavaScript" et 660-702 KiB de "Reduce unused JavaScript"
- **Cause** : les mesures sont faites en mode `npm run dev` (Vite ne minifie pas en développement)
- **Action réalisée en bonus** : suppression du `setInterval` envoyant une requête `/api/analytics/beacon` toutes les 4 secondes (code mort fonctionnel supprimé)
- **Action restante** : exécuter `npm run build` et mesurer Lighthouse sur le bundle de production pour valider la cible "Performance ≥ 75" et "JS -700 KiB"
- **Commit (partiel)** : `df12eea`
- **Reporté sur** : jalon `v1.1-prod`

### US-03 — Lazy loading images ✅
- **Fichier modifié** : `frontend/src/ShowcaseApp.tsx` (toutes les pages)
- **Action réalisée** : ajout de `loading="lazy"` + `width`/`height` sur toutes les balises `<img>` hors viewport initial
- **Résultat mesuré** : FCP 5,6 s → 1,0 s sur Accueil et Contact
- **Commit** : `df12eea`

### US-04 — Tri serveur + Allégement API ✅
- **Fichier modifié** : `backend/src/index.ts` (route `GET /api/articles`)
- **Action réalisée** : tri `.sort()` par `publishedAt` DESC + `.map()` ne retournant que 8 champs essentiels (suppression de `bodySections`, `tags`, `mediaGallery`)
- **Résultat** : payload allégé, articles triés côté serveur (DESC)
- **Commit** : `df12eea`

### US-05 — Suppression / optimisation hero image Contact ✅
- **Fichier modifié** : `frontend/src/ShowcaseApp.tsx` (ContactPage)
- **Action réalisée** : remplacement de `<img src="/assets/showcase-hero-3.svg">` par un `<div>` avec dégradé CSS (`linear-gradient(135deg, #1a3a5c 0%, #2e75b6 100%)`)
- **Résultat mesuré** : LCP 10,03 s → 1,8 s, FCP → 1,0 s, élimination du chargement de l'asset
- **Commit** : `df12eea`

---

## Synthèse globale (4,5 / 5 US livrées)

| Métrique | Avant | Après | Gain |
|----------|-------|-------|------|
| Lighthouse Performance | 61 / 100 | 91–92 / 100 | +30 à +31 pts |
| FCP | 5,6 s | 1,0 s | −82% |
| LCP | ~10 s | 1,7–1,8 s | −82 à −83% |

## Backlog reporté (jalon v1.1-prod)

| ID | Action restante | Cible |
|----|------------------|-------|
| US-02 (suite) | `npm run build` + mesure Lighthouse en production | Performance ≥ 75, JS -700 KiB |
