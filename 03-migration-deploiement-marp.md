---
marp: true
theme: marpcore
paginate: true
title: Migration et déploiement
---

# Stratégie de migration

## Principes

- Prioriser les parcours à valeur client et risque maîtrisé.
- Isoler l’existant derrière des façades API stables.
- Remplacer par capacité, pas par application monolithique.
- Piloter la dette de coexistence avec jalons de décommissionnement.

---

# Dépendances critiques de migration

```mermaid
flowchart LR
  A[Identité et consentement] --> B[Client unifié]
  B --> C[Panier omnicanal]
  C --> D[Checkout/paiement]
  A --> E[Fidélité]
  F[Stock temps réel] --> C
  F --> G[Promesse de commande]
  G --> H[Commande/retours]
  D --> H
```
# Plan de migration

## Vagues proposées

1. Fondation: contrats API, événements canoniques, observabilité, sécurité.
2. Parcours vente: stock disponible, panier, checkout/paiement.
3. Post-achat: commande, retours cross-canal, service client.
4. Extension: fidélité avancée, promotions complexes, optimisation pays.

---

# Coexistence legacy

## Schéma de transition

```mermaid
flowchart LR
  C[Canaux] --> G[API gateway]
  G --> F[Façades anti-corruption]
  F --> L[Legacy POS/e-commerce/OMS]
  G --> N[Nouveaux services du socle]
  N --> E[Event backbone]
  L --> E
  E --> D[Data platform]
```

---

# Plan exécutable

## Horizon 0 à 6 mois

- Jalons: contrats API, événements canoniques, observabilité minimale, sécurité baseline.
- Périmètre: pilote 2 pays, 2 canaux, stock + panier + checkout.
- Critères de réussite: latence p95 cible tenue, stabilité en pic, zéro incident critique bloquant.
- Rollback: bascule contrôlée vers parcours legacy via feature flags et routage gateway.

---

# Plan exécutable

## Horizon 6 à 12 mois

- Jalons: commande/retours cross-canal, fidélité temps réel, industrialisation CI/CD multi-domaines.
- Périmètre: extension par cluster pays et rationalisation e-commerce redondant.
- Critères de réussite: baisse incidents majeurs, amélioration conversion, réduction flux batch critiques.
- Rollback: retour partiel par capacité (commande, retours, fidélité) sans rollback global.

---

# Plan exécutable

## Horizon 12 à 24 mois

- Jalons: décommissionnements legacy prioritaires, standard groupe stabilisé, optimisation coût-performance.
- Périmètre: généralisation internationale avec variantes locales encadrées.
- Critères de réussite: réduction TCO, baisse dette technique, adoption cible par pays.
- Rollback: plan de continuité limité aux fonctions critiques et fenêtre de retour définie.

---

# Go/no-go et rollback

## Seuils décisionnels explicites

| KPI | Seuil go-live | Seuil rollback |
|---|---|---|
| Disponibilité parcours checkout | >= 99.9% | < 99.5% sur 2 jours |
| Latence API p95 | <= 200 ms | > 300 ms sur 24h |
| Taux d’erreur API | < 1% | > 3% sur 2h |
| Taux incident critique | 0 bloquant | >= 1 incident bloquant non résolu > 30 min |
| Écart stock web/magasin | < 2% | > 5% sur 1 journée |

---

# Gouvernance opérationnelle

## RACI de référence

| Décision | A | R | C | I |
|---|---|---|---|---|
| Standard API/événement | CTO groupe | Lead architecte domaine | Pays IT lead, sécurité | PMO programme |
| Priorisation capacité | Sponsor métier groupe | Product manager domaine | Direction pays | Équipes run |
| Go/no-go vague pays | Directeur programme | Release manager | Ops pays, sécurité, finance | COMEX projet |
| Décommissionnement legacy | CTO groupe | Responsable plateforme | Pays IT lead | PMO |

---

# Gouvernance opérationnelle

## Comitologie, cadence et KPI décisionnels

- Comitologie: architecture board (mensuel), steering programme (hebdo), go/no-go release (par vague).
- Cadence: incréments trimestriels avec revues de valeur mensuelles.
- KPI décisionnels: disponibilité, latence p95, MTTR, taux d’incident critique, décommissionnement effectif.

---

# Dimension internationale

## Template pays

- Bloc global obligatoire: API contracts, sécurité, observabilité, modèle de données canonique.
- Bloc local paramétrable: fiscalité, moyens de paiement, langue, devise, mentions légales.
- Bloc local spécifique sous dérogation: cas réglementaires non couverts par paramétrage.

---

# Dimension internationale

## Variantes autorisées et non autorisées

| Domaine | Autorisé localement | Non autorisé localement |
|---|---|---|
| Fiscalité | Règles taxe et éco-participation | Changer le modèle de données canonique |
| Paiement | Moyens de paiement et PSP homologués | Contourner les contrôles antifraude groupe |
| Expérience | Langue, contenus, parcours éditoriaux | Modifier contrats API core |
| Fidélité/promo | Paramétrage des règles pays | Dupliquer le moteur central hors gouvernance |
# Déploiement

## Modèle industriel

- CI/CD standard par domaine avec quality gates.
- Tests automatiques: unitaires, contrats API, non-régression parcours.
- Tests de charge sur pics commerciaux avant chaque vague.
- Déploiement progressif: canary, blue/green selon criticité.

---

# Exploitation et fiabilité

## Run cible

- SRE transverse + équipes domaine responsables de bout en bout.
- Runbooks incidents standardisés et exercices de reprise planifiés.
- Mesure continue des SLO et error budgets par capacité.
- Gestion proactive de la qualité de données (fraîcheur, complétude, cohérence).

---

# Gestion internationale

## Cadre de déploiement multi-pays

- Core global commun, variantes locales par configuration.
- Templates de déploiement pays (taxes, paiements, langue, devise).
- Process de certification locale avant go-live.
- Ordonnancement des pays par complexité réglementaire et dépendances legacy.

---

# KPI de pilotage

| Axe | KPI |
|---|---|
| Business | conversion, panier moyen, taux de rupture visible |
| Opérations | délai de déploiement, incident majeur, MTTR |
| Technique | latence p95, disponibilité, taux d’erreur API |
| Transformation | taux de décommissionnement legacy, adoption pays |

---

# Décisions de lancement

- Valider le pilote initial: périmètre, pays, canaux, critères de succès.
- Sécuriser le budget de transformation et de sortie legacy.
- Installer la gouvernance produit/architecture et les rituels d’arbitrage.
- Engager l’exécution sur 3 horizons: 6 mois, 12 mois, 24+ mois.
