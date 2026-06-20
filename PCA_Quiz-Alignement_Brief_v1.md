# Quiz pca.finexit.ca — Brief d'alignement v1
**Date :** 2026-06-19 · **But :** aligner le quiz sur la charte figée ET sur le Ratio de dépendance au propriétaire. Le quiz devient « l'estimé gratuit » du Ratio (usage 1).
**Implémentation :** la landing vit dans `Projects/Portail-PCA/*.html` (lecture seule ici) → à appliquer en session Claude Code. Ce document fournit le mapping, les tokens et la copy.

---

## 1. Design — passer à la charte

| Élément | Actuel | Cible (charte figée) |
|---------|--------|----------------------|
| Police | Outfit | New Frank → **Inter** (`finexit-brand.css`) |
| Marine | `#0d2363` / `#061235` | `#07132A` |
| Accents zones | vert `#22C55E` / ambre `#EAB308` / rouge | **Cyan / bleu roi / rouge** (voir §3) |
| Composants | divers | boutons, badges, barres `finexit-brand.css` (coins vifs) |

Charger `finexit-brand.css`. Retirer tout vert/ambre (tons chauds interdits). Cyan `#2DC3EA` présent partout.

## 2. Le quiz = Ratio de dépendance estimé

8 questions, chacune notée 0–3 → score /24.
**Ratio estimé (%) = arrondi( score ÷ 24 × 100 ).**
On affiche le résultat comme **« Ton ratio de dépendance au propriétaire (estimé) : XX % »**.

## 3. Remap des zones (sur les bandes du Ratio v2)

| Score /24 | Ratio estimé | Zone | Couleur |
|-----------|--------------|------|---------|
| 0 – 4 | 0–20 % | **Solide** | cyan `#2DC3EA` |
| 5 – 14 | 21–59 % | **Vulnérable** | bleu roi `#123682` |
| 15 – 24 | 60–100 % | **Critique** | rouge `#ED1C24` |

*(Plus de feu vert/jaune/rouge — on adopte Solide / Vulnérable / Critique, cohérent avec le PCA et le portail.)*

Classes CSS prêtes : `fx-zone--solide` / `fx-zone--vulnerable` / `fx-zone--critique` et les badges `fx-zone-badge--*`.

## 4. Écran de résultat

1. **Le chiffre** — « Ratio de dépendance estimé : **XX %** », gros, cyan.
2. **Le badge de zone** — Solide / Vulnérable / Critique.
3. **2–3 lignes** selon la zone (reprendre/condenser les textes enrichis existants de `pca-finexit_questions-resultats.md`, re-bandés selon §3, ton tutoiement) :
   - **Solide** — ton entreprise tient sans toi. Base transférable. Reste à tester sous pression réelle.
   - **Vulnérable** — ça ralentit fortement; des angles morts à corriger. Vendable, mais avec des accrocs.
   - **Critique** — sans toi, ça s'arrête. C'est la priorité, et ça se règle.
4. **Le PDF générique (« fourre-tout »)** par zone — un document DIY qui amène à réfléchir et s'organiser (usage 1 du Ratio). À terme, pointe vers la plateforme.
5. **CTA** — vers le **PCA** (appel de cadrage / découverte). Bouton cyan, coins vifs.

## 5. Reste (hors design, à câbler côté dev)

- Capture lead déjà en place (`POST /api/pca-leads`) — conserver.
- Tracking GA4/Plausible (events `quiz_completed`, `email_submitted`) — toujours à faire.
- Séquence email post-quiz (3 courriels) — toujours à faire.

---

*v1 — base d'alignement. Le design et le remap des zones sont prêts à appliquer; la grille de critères détaillée du Ratio (v3) raffinera la correspondance questions ↔ axes.*
