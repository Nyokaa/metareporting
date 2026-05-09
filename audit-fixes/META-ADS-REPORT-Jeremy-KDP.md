# Meta Ads Audit — Jeremy KDP

**Account ID:** 1761639380930417
**Business:** jeremyferrandbusiness
**Industry detected:** Info Products / Education (Amazon KDP — publication de livres)
**Currency:** EUR
**Period analyzed:** 9 avril 2026 → 8 mai 2026 (30 jours) + lifetime depuis 26-jan-2024
**Audit date:** 9 mai 2026

---

## Executive Summary

**Meta Ads Health Score : 48/100 — Grade D (Significant problems present)**

```
Pixel / CAPI Health  : 35/100  ███▌░░░░░░  (30%)  ⚠ Purchase tracking broken
Creative             : 70/100  ███████░░░  (30%)  ✓ CTR très solide
Account Structure    : 35/100  ███▌░░░░░░  (20%)  ⚠ overlap audiences
Audience             : 50/100  █████░░░░░  (20%)  ⚠ démographie diluée
```

**Verdict :** le compte génère du **lead à 5,62 € (bon)** mais n'imprime **1 seule vente trackée sur 9 908 €** dépensés (ROAS 0,11, lifetime 0,29). Le funnel post-lead et/ou le pixel Purchase event sont défaillants. Sans correction, chaque euro investi en acquisition est dilapidé.

### Top-line metrics — 30j
| Métrique | Valeur | Benchmark FR Info-Product | Verdict |
|---|---|---|---|
| Spend | 9 908,27 € | — | — |
| Impressions | 786 199 | — | — |
| Reach | 231 340 | — | — |
| Frequency | **3,40** | <3,0 (prospect) | ⚠ WARNING |
| CTR | **2,83 %** | ≥1,0 % | ✓ PASS |
| CPC | 0,45 € | 0,50–1,50 € FR | ✓ PASS |
| CPM | 12,60 € | 8–20 € FR | ✓ PASS |
| Leads | 1 763 | — | — |
| Cost / Lead | **5,62 €** | 5–15 € FR info-product | ✓ PASS |
| Omni Purchases | **1** | — | ❌ FAIL |
| **Purchase ROAS** | **0,11** | ≥1,5 break-even | ❌ FAIL |
| Cost / Purchase | 9 908 € | — | ❌ FAIL |

### Lifetime (depuis jan 2024)
22 935 € spend → 7 130 leads → 17 purchases → ROAS 0,29 → cost/purchase ≈ 1 349 €. La problématique est structurelle, pas conjoncturelle.

---

## 1. Pixel / CAPI Health (35/100 — 30 % du score)

### ❌ FAIL critiques

**M01 · Purchase event quasi-absent**
- 1 omni_purchase trackée sur 30j pour 9 908 € spend et 1 763 leads (0,06 % conv L→S)
- Lifetime : 17 purchases / 22 935 € → CPS 1 349 €
- Causes possibles (à investiguer **immédiatement** dans Events Manager) :
  1. Pixel Purchase ne fire pas (manque sur thank-you page / checkout, ou bloqué par le cookie banner)
  2. Pas de CAPI activée → 30–40 % de pertes iOS 14.5+
  3. Le Lead se transforme bien mais le tracking est cassé entre la formation et le checkout
  4. Le funnel post-lead (email/automation) ne convertit réellement pas
- **Quick win** : poser le pixel Purchase sur la thank-you de Stripe/Systeme.io/ClickFunnels et vérifier en Test Events. Si Stripe : utiliser le webhook → CAPI Purchase avec valeur.

**M02 · Inconsistent Lead optimization event**
- Anciennes campagnes (KDP DAYS, KDP IMAGE) optimisent sur custom event `944094221005232`
- Nouvelles (ABEHDT) optimisent sur `offsite_conversion.fb_pixel_lead` (standard Lead)
- → Le Pixel apprend sur 2 events distincts, fragmente l'apprentissage
- **Action** : standardiser sur le standard Lead, archiver le custom

**M03 · CAPI/EMQ — non-vérifiable via API mais hautement probablement absent**
- Audience Network délivre à 17,39 % CTR / 25,66 % sur rewarded_video → comportement typique de tracking client-only sans dédup CAPI
- Sans le pixel ID, je ne peux pas pull EMQ/dedup rate. À vérifier manuellement dans Events Manager

### À vérifier manuellement (Events Manager)
- [ ] EMQ Score Lead ≥ 8.0 (objectif Andromeda)
- [ ] EMQ Score Purchase ≥ 8.0
- [ ] Dedup rate ≥ 90 %
- [ ] Conversions API active
- [ ] `em`, `ph`, `external_id` envoyés
- [ ] AEM (Aggregated Event Measurement) prioritisé (Purchase > Lead > etc.)
- [ ] Domain verification

---

## 2. Creative (70/100 — 30 % du score)

### ✓ PASS
- **CTR 2,83 %** account-level — excellent, créatives engageantes
- **Engagement** : 168 651 page engagements, 12 342 link clicks → contenu clivant qui résonne
- **Reels performants** : Facebook Reels 5,10 €/lead, Instagram Reels 5,42 €/lead — meilleurs placements

### ⚠ WARNING
- **M10 · Diversité créative non-mesurée via API** mais le naming "ABEHDT - Challenge KDP Mai" répété sur 4 campagnes laisse penser à des créatives similaires (alerte Andromeda — Meta supprime les ads >60 % similaires)
- **Action** : auditer manuellement dans Ads Manager. Objectif Andromeda = ≥10 créatives **vraiment distinctes** par account (angles, hooks, formats différents)

### Recommandations
- Tester du UGC / témoignages d'élèves ayant publié sur KDP
- Diversifier les hooks : "transformation" vs. "process" vs. "preuve sociale"
- Tester carousel + image statique en plus des vidéos

---

## 3. Account Structure (35/100 — 20 % du score)

### ❌ FAIL

**M20 · Audience overlap massif sur Challenge KDP Mai**
- 1 campagne globale **ABEHDT - Challenge KDP Mai** (3 593 €, 854 leads, 4,21 €) — **best performer**
- 3 campagnes en parallèle ICP1/ICP2/ICP3 (1 759/1 753/1 762 €, CPL 6,69-7,63 €) — toutes BROAD
- Les 4 ad sets BROAD compétissent sur la même audience FR → enchères contre soi-même, **frequency 3,40** au lieu de <3,0
- L'ICP global non-segmenté (4,21 €) **convertit 1,8× mieux** que les 3 ICP segmentés → la segmentation ICP n'apporte rien
- **Quick win** : kill ICP1/2/3, garder uniquement ABEHDT global avec budget consolidé (400 €/jour → 700 €/jour)

**M21 · Pléthore de campagnes legacy en "off"**
- 23 campagnes au total, dont ~17 inactives (KDP DAYS 1-15, LIVRE OFFERT, APPEL TEST, KDP IMAGE...)
- Pollue le compte, fragmente le pixel learning historique
- **Action** : archiver/supprimer toutes les campagnes inactives

**M22 · Bid strategy uniforme = "Highest Volume"**
- Acceptable pour scaler le Lead, mais avec un CPL stabilisé à 5,62 €, **passer à Cost Cap** à 5,50–6,00 € permettrait de protéger l'efficacité au scale

### ⚠ WARNING
- **M23 · Budget < 5× CPA sur ICP1/2/3** → 140 €/jour ÷ CPL 7 € = 20× CPA ✓ OK pour Lead mais en réalité ces ad sets sortent du Learning trop vite à cause du fragmentation
- **Pas d'Advantage+ Sales Campaign** → pas applicable (compte Lead-gen, pas e-commerce direct)
- **Aucune campagne de retargeting** (voir section 4)

---

## 4. Audience & Targeting (50/100 — 20 % du score)

### Démographie (30j)

| Tranche | Spend % | Lead | CPL | Verdict |
|---|---|---|---|---|
| 35-44 male | 4,8 % | 136 | **3,52 €** 🏆 | Champion |
| 45-54 female | 15,8 % | 300 | 5,23 € | Top performer volume |
| 55-64 female | 14,8 % | 265 | 5,55 € | Solid |
| 65+ female | 10,4 % | 182 | 5,64 € | ⚠ probablement non-buyer |
| 65+ male | 12,8 % | 201 | 6,31 € | ⚠ probablement non-buyer |
| 18-24 (M+F) | 1,9 % | 28 | 6,2-6,9 € | Hors-cible |
| 25-34 (M+F) | 8,7 % | 135 | 6,3-6,6 € | OK |

**M30 · Démographie diluée vers 65+** — 23,2 % du spend sur les 65+ (2 327 €). Pour un info-product Amazon KDP, la cible buyer est probablement 30-55 ans. Les 65+ remplissent les forms (curiosité) mais n'achètent pas → contribue au ROAS 0,11.

### ❌ FAIL

**M31 · Audience Network = trafic faux**
- AN Classic : CTR **12,19 %** (vs benchmark 1-2 %), CPL 4,11 € à 11 leads
- Rewarded Video : CTR **25,66 %**, CPL 7,06 € — clic forcé pour gagner une vie de jeu mobile
- Sur AN au global : CTR 17,39 %, frequency 3,57 — trafic robotisé
- **Quick win** : exclure Audience Network entièrement (Advantage+ Placements → désactiver AN, ou Manual placements)

**M32 · Aucune campagne retargeting**
- 7 130 leads lifetime + 144 020 visiteurs IG Reels 30j = 7-15k leads chauds disponibles
- Aucune custom audience exploitée, aucune Lookalike testée (au moins via les leads ID `944094221005232`)
- **Quick win** : créer 1 campagne ABO avec 2 ad sets :
  - RTG visiteurs site 30j (ex-buyers)
  - LAL 1-3 % seed = lead form fillers 90j

### ⚠ WARNING

**M33 · Aucun Lookalike testé** — avec 7 130 leads, c'est une seed de Lookalike or. Tester LAL 1 %, 3 %, 5 %.

**M34 · Page name "(unknown)"** — la Page liée au compte (ID 279026725305217) renvoie "(unknown)". Vérifier qu'elle est bien active, vérifiée, et que le nom est public.

---

## 5. Placements — actionable insights

| Placement | Spend | CPL | Verdict |
|---|---|---|---|
| Facebook Feed | 5 270 € | 5,87 € | ✓ Workhorse |
| Facebook Reels | 1 756 € | **5,10 €** | ✓ Champion |
| Instagram Reels | 1 637 € | 5,42 € | ✓ Champion |
| Instagram Stories | 685 € | 5,85 € | ✓ Solid |
| Instream Video | 119 € | 4,12 € | ✓ Excellent |
| Facebook Stories | 242 € | 8,34 € | ⚠ underperforms |
| Audience Network | 102 € | 5,36 € | ❌ Faux trafic — exclude |
| Threads | 4 € | — | OK à laisser, volume nul |
| Messenger | <1 € | — | OK à laisser |

**Recommandation** : Advantage+ Placements activé mais avec **AN exclu**. Les Reels FR/IG portent 35 % du résultat à coût optimal — pousser plus de créa native verticale 9:16.

---

## Findings résumés

| ID | Sévérité | Catégorie | Findings |
|---|---|---|---|
| M01 | 🔴 Critical | Tracking | Purchase event ne fire pas / CAPI absent — 1 sale en 30j |
| M20 | 🔴 Critical | Structure | 4 ad sets BROAD compétissent → consolider en 1 |
| M31 | 🔴 Critical | Audience | Audience Network = trafic robotisé (CTR 25 %) |
| M32 | 🟠 High | Audience | Aucun retargeting malgré 7 130 leads lifetime |
| M02 | 🟠 High | Tracking | 2 events Lead différents (custom + standard) |
| M30 | 🟠 High | Audience | 23 % du spend sur 65+ probablement non-buyer |
| M22 | 🟡 Medium | Bidding | Passer Highest Volume → Cost Cap 5,50€ pour scaler |
| M33 | 🟡 Medium | Audience | Aucun Lookalike testé sur seed leads |
| M21 | 🟡 Medium | Structure | 17 campagnes legacy à archiver |
| M34 | 🟡 Medium | Setup | Page Facebook "(unknown)" — vérifier |
| M10 | 🟡 Medium | Creative | Diversité créative à auditer manuellement (Andromeda) |
| M03 | 🟡 Medium | Tracking | EMQ / dédup CAPI à vérifier manuellement |

---

## Quick Wins — 7 jours

1. **🔴 Réparer le pixel Purchase** (impact ×10 sur ROAS visible)
   - Events Manager → Test Events → reproduire un achat → vérifier que `Purchase` fire avec value + currency
   - Activer CAPI via Stripe webhook ou Zapier (gratuit jusqu'à 1k events/mois)
   - Domain verification
2. **🔴 Killer les 3 campagnes ICP1/2/3** et consolider sur "ABEHDT - Challenge KDP Mai" (CPL 4,21 € → meilleure performance prouvée). Budget : 700 €/jour (vs 820 € actuels = -15 %)
3. **🔴 Exclure Audience Network** dans tous les ad sets actifs (Manual placements OU Advantage+ - décocher AN)
4. **🟠 Resserrer la démographie à 25-55** sur le BROAD principal (sortir 65+ et 18-24) → -25 % spend gaspillé
5. **🟠 Créer 1 campagne retargeting ABO** :
   - Ad set 1 : visitors 30j (exclude leads + buyers)
   - Ad set 2 : LAL 1-3 % from leads 90j
   - Budget : 50 €/jour pour démarrer

## Roadmap 30 jours

6. Standardiser le Lead event sur `offsite_conversion.fb_pixel_lead` partout (kill custom 944094221005232)
7. Archiver les 17 campagnes legacy (KDP DAYS 1-15, etc.)
8. Audit créatives manuelles : valider que ≥10 créatives **distinctes** tournent (Andromeda)
9. Tester Cost Cap @ 5,50 € sur ABEHDT après stabilisation
10. Lancer 3 LAL : 1 %, 3 %, 5 % seed = leads 90j

## Roadmap 90 jours

11. Mesurer EMQ et viser ≥8.0 sur Lead **et** Purchase
12. Tester un funnel webinar/VSL → Purchase si l'objectif final est la formation KDP
13. Reels-first : produire 4-6 nouvelles créatives Reels par mois
14. Évaluer Threads placement (early-mover, GA jan 2026)

---

## Limites de l'audit

- **EMQ / dedup CAPI / domain verif** : non-accessibles via le MCP. À vérifier dans Events Manager
- **Pixel ID** : non-extractible via les tools disponibles
- **Diversité créative** : score basé sur les méta-données (objectifs, naming) — un audit visuel manuel des créatives (UGC vs production, hooks, formats) est nécessaire pour le score Andromeda complet
- **Funnel post-lead** : non-mesurable côté Meta. La cause probable du ROAS 0,11 (broken pixel ou broken funnel) demande à voir Stripe / l'email automation / la landing thank-you

---

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Built by agricidaniel — Join the AI Marketing Hub community
🆓 Free  → https://www.skool.com/ai-marketing-hub
⚡ Pro   → https://www.skool.com/ai-marketing-hub-pro
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
