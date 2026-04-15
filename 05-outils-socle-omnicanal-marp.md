---
marp: true
theme: marpcore
paginate: true
title: Outils du socle omnicanal - shortlist marché
---

# Outils du nouveau socle omnicanal

## Méthode de sélection

- Cibles: retail omnicanal international, architecture API-first, déploiement multi-pays.
- Format: 2 à 3 solutions « best fit » par capacité.
- Critères: couverture fonctionnelle, performance, extensibilité, intégration SI, gouvernance internationale, TCO.
- Positionnement: shortlist de cadrage, à confirmer en RFP.

---

# Socle transactionnel (commerce core)

| Capacité | Solutions shortlist (2-3) | Pourquoi pertinentes | Points de vigilance |
|---|---|---|---|
| Commerce composable (catalogue, panier, commande) | commercetools, SCAYLE, Elastic Path | API-first, modularité élevée, forte adéquation MACH | Coût d’intégration, complexité de gouvernance produit |
| OMS distribué (order orchestration) | Fluent Commerce, Manhattan Active Omni, OneStock | Gestion omnicanale mature (ship-from-store, click-and-collect, retours) | Frontière fonctionnelle avec ERP/legacy, effort de migration |
| POS moderne extensible | Adyen POS Platform, NewStore POS, Shopify POS (enterprise) | Unification paiement + parcours magasin, capacités cloud natives | Couverture processus magasin complexes selon pays |

---

# Paiement, fraude, fiscalité

| Capacité | Solutions shortlist (2-3) | Pourquoi pertinentes | Points de vigilance |
|---|---|---|---|
| Paiement / orchestration PSP | Adyen, Stripe, Worldpay | Couverture internationale, APIs robustes, omnicanal online + in-store | Stratégie multi-acquéreurs, dépendance contractuelle |
| Antifraude e-commerce | Forter, Riskified, Stripe Radar | Décision temps réel, réduction chargeback, intégration checkout | Taux de faux positifs, gouvernance des règles |
| Taxe/fiscalité internationale | Avalara AvaTax, Vertex, Sovos | Couverture réglementaire multi-pays et APIs dédiées | Paramétrage local, cycle de certification fiscale |

---

# Promotion, fidélité, recherche

| Capacité | Solutions shortlist (2-3) | Pourquoi pertinentes | Points de vigilance |
|---|---|---|---|
| Moteur promotionnel / incentives | Talon.One, Eagle Eye, Voucherify | Moteurs règles avancés, API temps réel, usage omnicanal | Complexité des règles, gouvernance métier |
| Fidélité temps réel | Antavo, Comarch Loyalty, Salesforce Loyalty Management | Programmes multi-pays, earn/burn temps réel, segmentation | Coût licence et intégration avec CRM/CDP |
| Searchandising / discovery | Algolia, Bloomreach Discovery, Constructor | Excellente pertinence recherche + merchandising pilotable | Qualité du flux produit, tuning continu |

---

# Intégration, data, observabilité

| Capacité | Solutions shortlist (2-3) | Pourquoi pertinentes | Points de vigilance |
|---|---|---|---|
| Event backbone / streaming | Confluent Cloud (Kafka), AWS Kinesis, Google Pub/Sub | Diffusion temps réel, découplage fort, scalabilité élevée | Modèle d’événements canoniques à stabiliser |
| API management | Kong, Apigee, MuleSoft API Manager | Gouvernance API, sécurité, analytics, portail développeurs | Coûts à volume, standardisation des politiques |
| Observabilité full-stack | Datadog, Dynatrace, New Relic | APM + logs + traces + SLO pour pilotage run | Coût d’ingestion, stratégie de tagging |

---

# Référentiel de décision (buy vs build)

| Domaine | Option recommandée | Raison |
|---|---|---|
| Paiement, antifraude, taxe, observabilité | Buy | Capacités non différenciantes, forte spécialisation éditeurs |
| Panier omnicanal, orchestration parcours client, règles de rupture | Build ou hybride | Différenciation métier et expérience client |
| OMS, promo/fidélité, searchandising | Hybride (buy + extensions) | Accélérer le time-to-market sans perdre la spécificité métier |

---

# Recommandation de cadrage RFP

## Périmètre pilote (6 mois)

- Commerce core: commercetools ou Elastic Path.
- OMS: Fluent Commerce ou OneStock.
- Paiement: Adyen ou Stripe.
- Promotions/fidélité: Talon.One + solution fidélité shortlistée.
- Searchandising: Algolia ou Bloomreach.

## Critères go/no-go

- p95 API sur parcours critique < 200 ms.
- Disponibilité checkout >= 99.9%.
- Capacité multi-pays prouvée sur 2 pilotes.
- Coût total (licence + intégration + run) dans l’enveloppe cible.
