# Quiz — Réécriture des 8 questions sur le ratio de dépendance — Proposition v2
**Date :** 2026-06-19 · **But :** que le quiz calcule **directement** le Ratio de dépendance au propriétaire, pondéré 40 / 40 / 20, sans échelle inversée.
*(v2 : formulations ajustées avec Éric — plus québécoises, questions resserrées.)*

---

## Principe

- **3 axes, 8 questions : 3 Ventes · 3 Prestation · 2 Administration.**
- Chaque question : 4 réponses notées **0 à 3**, où **0 = aucune dépendance** (l'entreprise tient sans toi) et **3 = dépendance totale** (tout repose sur toi).
- On note l'**axe**, puis on applique la pondération **40 / 40 / 20**.
- Comme les réponses mesurent la dépendance directement, **le score EST le ratio** : plus de logique inversée, plus de `100 − x`.

---

## Axe 1 — Ventes & clients  *(poids 40 %)*

**V1. Est-ce que les clients achètent de toi ou de l'entreprise ?**
- 0 — Ils sont liés à l'entreprise; plusieurs personnes les servent.
- 1 — La plupart connaissent quelqu'un d'autre, mais je reste le contact principal.
- 2 — Quelques-uns parlent à l'équipe, mais la majorité veulent me parler à moi.
- 3 — Mes meilleurs clients achètent de moi; sans moi, la relation tombe.

**V2. Qui va chercher les nouvelles ventes ?**
- 0 — Une équipe ou un système d'acquisition tourne sans moi.
- 1 — On a un processus, mais je m'occupe des gros dossiers.
- 2 — Je pilote l'essentiel; l'équipe suit.
- 3 — S'il faut de nouveaux clients, c'est moi qui vais les chercher, point.

**V3. Qui fixe les prix et négocie les contrats ?**
- 0 — Des règles claires permettent à l'équipe de conclure sans moi.
- 1 — Mon équipe s'occupe du courant, je tranche les exceptions.
- 2 — Je valide presque toutes les ententes.
- 3 — Rien ne se price ni ne se signe sans moi.

## Axe 2 — Prestation & opérations  *(poids 40 %)*

**P1. Si tu t'absentais un mois sans préavis, la production et la livraison continueraient-elles ?**
- 0 — Oui, normalement; mon équipe s'en occupe.
- 1 — Oui, mais ça ralentirait sur les décisions.
- 2 — Partiellement; plusieurs choses attendraient mon retour.
- 3 — Non; ça s'arrête vite sans moi.

**P2. Les façons de faire clés (opérations, livraison) sont-elles documentées et faisables sans toi ?**
- 0 — Oui : écrites, à jour, accessibles.
- 1 — En partie; les plus critiques sont dans ma tête.
- 2 — Quelques notes éparpillées, difficiles à suivre.
- 3 — Tout est dans ma tête.

**P3. Quelqu'un, formé et reconnu par l'équipe, peut-il diriger les opérations à ta place ?**
- 0 — Oui : désigné, formé, et l'équipe le sait.
- 1 — Identifié, mais pas vraiment préparé.
- 2 — Quelqu'un pourrait « peut-être » gérer, rien de formel.
- 3 — Personne.

## Axe 3 — Administration (finances, accès, juridique)  *(poids 20 %)*

**A1. Si tu étais indisponible, quelqu'un d'autre pourrait-il payer, signer et accéder aux comptes ?**
- 0 — Oui : accès et pouvoir de signer en place, avec instructions.
- 1 — Il y a un co-signataire, mais sans instructions claires.
- 2 — Quelqu'un peut voir, mais pas agir ni payer.
- 3 — Personne ne peut payer ni signer sans moi.

**A2. Les documents critiques (contrats, accès, obligations) sont-ils centralisés et trouvables sans toi ?**
- 0 — Oui : centralisés, accessibles aux bonnes personnes.
- 1 — En partie; il faudrait me demander pour le reste.
- 2 — Éparpillés; difficiles à reconstituer.
- 3 — Tout passe par moi; personne ne saurait où chercher.

---

## Calcul

```
Ventes %        = (V1 + V2 + V3) / 9  × 100
Prestation %    = (P1 + P2 + P3) / 9  × 100
Administration% = (A1 + A2)      / 6  × 100

Ratio de dépendance = 0.40 × Ventes% + 0.40 × Prestation% + 0.20 × Administration%
```
Arrondir à l'entier.

### Zones (verrouillées)

| Ratio | Zone | Couleur |
|-------|------|---------|
| 0–20 % | **Solide** | cyan `#2DC3EA` |
| 21–60 % | **Vulnérable** | bleu roi `#123682` |
| 61–100 % | **Critique** | rouge `#ED1C24` |

---

## Affichage à l'écran (après saisie du courriel)

Remplacer les 4 dimensions génériques (Direction / Opérations / Clients / Protection) par **les 3 axes du ratio** :
- Le **Ratio de dépendance** en gros (avec la zone).
- Les **3 axes** : Ventes %, Prestation %, Administration % (mini-barres).
- Une ligne de message par zone (Solide / Vulnérable / Critique).
- « Ton rapport détaillé t'a été envoyé par courriel. »

Le détail riche (5-10 pages) reste dans le **PDF par courriel** — l'écran donne la gratification immédiate, le courriel garde sa valeur d'échange.

---

## Notes d'implémentation (frontend `site-pca-finexit`)

- Même structure qu'aujourd'hui (8 questions, réponses 0-3) → changement maîtrisé.
- Remplacer le texte des questions/réponses et **étiqueter chaque question par son axe** (`axe: 'ventes' | 'prestation' | 'admin'`).
- Remplacer le calcul `scorePct` par le calcul pondéré ci-dessus → c'est **le ratio** (plus d'inversion).
- Renommer les zones (Solide / Vulnérable / Critique), retirer vert/jaune/rouge, appliquer la charte.
- POSTer au backend `{ email, ratio, zone, axes:{ventes,prestation,admin} }` → le backend choisit le PDF de la bande (voir `PCA_Quiz-Email-PDF_Spec_v1.md`).

---

*v2 — formulations validées avec Éric. Prête à copier dans `site-pca-finexit` avec note d'implémentation pour la session Claude Code.*
