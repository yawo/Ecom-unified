---
marp: true
theme: marpcore
paginate: true
title: Cadrage et questions structurantes
---

# Cadrage

## Lecture du contexte

- Groupe international multi-marques, multi-pays, multi-canaux.
- Empilement historique: POS hétérogènes, e-commerce multiples, intégrations successives.
- Architecture en transition API-first, mais flux batch encore structurants.
- Objectif: socle omnicanal unifié sans rupture des opérations pays.

---

# Cadrage

## Ambiguïtés à clarifier

- Définition cible du « socle »: plateforme technique, produit métier, ou les deux.
- Frontière avec OMS et orchestrateur logistique existants.
- Granularité de la « vision unifiée du stock » (disponible, réservé, promis, ATP).
- Niveau d’unification fidélité/promo entre enseignes du groupe.
- Périmètre exact de la centralisation des ventes (temps réel vs consolidation différée).

---

# Questions structurantes

## Business et modèle opérationnel

- Quelles promesses client non négociables à 12 mois (J+1, click-and-collect, retour partout)?
- Quels pays et quelles enseignes définissent la référence de standard.
- Quel niveau d’autonomie local sur catalogue, pricing, promotions, fiscalité.
- Quelles contraintes contractuelles partenaires limitent la cible.

---

# Questions structurantes

## Architecture et données

- Quelle source de vérité pour produit, prix, stock, client, commande.
- Quels événements métier canoniques et quels contrats API imposer.
- Quels besoins d’offline POS et quelle stratégie de resynchronisation.
- Quelle politique d’identité client (matching, consentement, gouvernance RGPD).

---

# Questions structurantes

## Delivery et organisation

- Qui porte le ownership des domaines: équipe groupe, équipes pays, modèle hybride.
- Quelle capacité de transformation des équipes run/ops locales.
- Quels critères de passage en production par vague.
- Quel budget de sortie legacy par capacité.

---

# Registre de risques initial

| Risque | Impact | Probabilité | Parades |
|---|---|---:|---|
| Fragmentation décisionnelle | Élevé | Élevée | Gouvernance domaine + standards minimaux |
| Latence inter-systèmes | Élevé | Moyenne | Event backbone + cache + SLO contractuels |
| Coexistence legacy prolongée | Élevé | Élevée | Plan de décommissionnement daté |
| Dette qualité données | Élevé | Élevée | Data contracts + monitoring qualité |
| Charge pays excessive | Moyen | Élevée | Enablement central + usine de migration |

---

# Hypothèses de travail

- API gateway et data platform existantes sont conservées comme actifs structurants.
- Les capacités différenciantes sont traitées en priorité dans le socle.
- Les services transverses non différenciants privilégient des solutions du marché.
- La migration doit préserver la continuité des ventes et la conformité locale.

---

# Traçabilité des exigences du brief

## Couverture par deck

| Exigence du brief | Deck principal | Couverture |
|---|---|---|
| Vision cible | 00-synthese-marp.md | Vision, principes, macro-architecture |
| Questions structurantes | 01-cadrage-questions-marp.md | Questions business, data, organisation |
| Principes structurants | 00-synthese-marp.md / 02-architecture-cible-marp.md | API-first, event-driven, ownership |
| Positionnement des briques | 02-architecture-cible-marp.md | Mapping as-is vers to-be, responsabilités |
| Buy vs build / SaaS vs custom | 00-synthese-marp.md / 02-architecture-cible-marp.md | Arbitrages par capacité |
| Stratégie de migration | 03-migration-deploiement-marp.md | Vagues, coexistence, rollback |
| Approche de déploiement | 03-migration-deploiement-marp.md | Modèle industriel, run, KPI |
