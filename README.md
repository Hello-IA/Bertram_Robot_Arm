# BCN3D MOVEO — Journal de construction et documentation d'assemblage

> **Fork de [Toglefritz/Bertram_Robot_Arm](https://github.com/Toglefritz/Bertram_Robot_Arm)**, lui-même dérivé du projet open source **[BCN3D-Moveo](https://github.com/BCN3D/BCN3D-Moveo)** et du tutoriel **[Build a Giant 3D Printed Robot Arm](https://www.instructables.com/Build-a-Giant-3D-Printed-Robot-Arm/)** publié sur Instructables.

Ce dépôt conserve l'intégralité des fichiers du projet amont et y ajoute une **documentation d'assemblage complète, écrite pendant la construction réelle du bras** : nomenclature vérifiée avec les prix réellement payés, schémas de câblage inédits, choix de motorisation justifiés, réglages de drivers, et journal des pannes rencontrées avec leur résolution (ou leur non-résolution, quand c'est le cas).

---

## Sommaire

- [1. À propos du projet](#1-à-propos-du-projet)
  - [1.1 Contexte](#11-contexte)
  - [1.2 Objectifs](#12-objectifs)
  - [1.3 Ce que ce fork ajoute](#13-ce-que-ce-fork-ajoute)
  - [1.4 Chronologie](#14-chronologie)
- [2. Sources et documents de référence](#2-sources-et-documents-de-référence)
- [3. Architecture du système](#3-architecture-du-système)
  - [3.1 Principe général](#31-principe-général)
  - [3.2 Six moteurs pas-à-pas pour cinq axes](#32-six-moteurs-pas-à-pas-pour-cinq-axes)
  - [3.3 Attribution des axes RAMPS 1.4](#33-attribution-des-axes-ramps-14)
  - [3.4 Arborescence de l'alimentation](#34-arborescence-de-lalimentation)
- [4. Nomenclature et coûts](#4-nomenclature-et-coûts)
  - [4.1 Comment lire ces tableaux](#41-comment-lire-ces-tableaux)
  - [4.2 Mécanique](#42-mécanique)
  - [4.3 Moteurs et actionneurs](#43-moteurs-et-actionneurs)
  - [4.4 Électronique, drivers et alimentation](#44-électronique-drivers-et-alimentation)
  - [4.5 Récapitulatif des coûts](#45-récapitulatif-des-coûts)
  - [4.6 Anomalies relevées et corrections apportées](#46-anomalies-relevées-et-corrections-apportées)
  - [4.7 Coût du filament](#47-coût-du-filament)
- [5. Choix de la motorisation](#5-choix-de-la-motorisation)
- [6. Choix et configuration des drivers](#6-choix-et-configuration-des-drivers)
- [7. Impression 3D](#7-impression-3d)
- [8. Assemblage articulation par articulation](#8-assemblage-articulation-par-articulation)
- [9. Longueurs de courroies](#9-longueurs-de-courroies)
- [10. Firmware et contrôle](#10-firmware-et-contrôle)
- [11. Journal des pannes](#11-journal-des-pannes)
- [12. État d'avancement](#12-état-davancement)
- [13. Structure du dépôt](#13-structure-du-dépôt)
- [14. Crédits et licences](#14-crédits-et-licences)

---

## 1. À propos du projet

### 1.1 Contexte

Étudiant en **Master 2 AI2D** (Apprentissage, Information et Contenu / Intelligence Artificielle Distribuée et Robotique) à **Sorbonne Université – campus Jussieu**, j'ai décidé dans le cadre d'un projet personnel de construire un bras industriel open source de référence : le **BCN3D MOVEO**.

Le projet a démarré **fin septembre 2025** et s'est étalé sur plusieurs mois, en parallèle de la formation.

### 1.2 Objectifs

Trois objectifs :

1. **Acquérir des compétences hardware réelles.** Passer de la théorie robotique enseignée en cours à un système physique qu'il faut alimenter, câbler, régler et déboguer.
2. **Constituer une pièce de portfolio complète.** Pouvoir démontrer, la capacité à mener un projet robotique de bout en bout — mécanique, électronique, firmware, logiciel — dans la perspective d'un recrutement en entreprise du secteur robotique.
3. **Disposer d'une plateforme matérielle pour la suite.** Une fois le bras opérationnel, l'utiliser comme support pour implémenter les notions vues en cours de IA pour la robotique.

### 1.3 Ce que ce fork ajoute

Le dépôt amont fournit les fichiers du projet. Ce fork y ajoute :

| Apport | Détail |
|---|---|
| **Nomenclature réelle vérifiée** | Prix effectivement payés |
| **Schémas de câblage** | Aucun schéma driver ↔ RAMPS 1.4 n'existait pour ce projet ; ils ont été reconstitués à partir des datasheets |
| **Justification de la motorisation** | Pourquoi les moteurs du BOM d'origine et du tutoriel Instructables sont sous-dimensionnés, et par quoi les remplacer |
| **Réglages de drivers** | Positions de DIP switches, courants peak/RMS, microstepping, pour TB6560, TB6600 et DM542T |
| **Procédures d'assemblage pas à pas** | Ordre de montage, visserie exacte, tendeurs de courroie, longueurs de courroies calculées |
| **Journal des pannes** | Chaque blocage rencontré, la démarche de diagnostic, et l'issue — y compris les échecs |


### 1.4 Chronologie

| Période | Étape |
|---|---|
| Fin septembre 2025 | Découverte du projet, lecture du BOM et du manuel utilisateur BCN3D |
| Octobre 2025 | Reconstitution du schéma électrique, recherche des composants |
| Octobre 2025 | Blocage sur l'approvisionnement des moteurs du BOM d'origine → bascule sur le tutoriel Instructables |
| Automne 2025 | Commande et réception des composants, premiers essais électriques sur un moteur isolé |
| Automne–hiver 2025 | Impressions 3D au FabLab (PLA, PETG), échecs et reprises |
| Hiver 2025–2026 | Constat de sous-dimensionnement des moteurs → seconde commande |
| Mai 2026 | Poulies personnalisées OpenSCAD |
| Juin 2026 | Diagnostic des pertes de pas du coude |
| Juillet 2026 | Rédaction de cette documentation |

---

## 2. Sources et documents de référence

### Projet d'origine

- **Site officiel BCN3D MOVEO** — présentation du projet et téléchargement des fichiers
- **[GitHub BCN3D/BCN3D-Moveo](https://github.com/BCN3D/BCN3D-Moveo)** — dépôt officiel

### Variante suivie pour l'approvisionnement et le montage mécanique

- **[Instructables — Build a Giant 3D Printed Robot Arm](https://www.instructables.com/Build-a-Giant-3D-Printed-Robot-Arm/)** — un particulier propose une alternative au projet initial avec des moteurs plus accessibles, plus simples à obtenir et moins chers. C'est cette liste qui a débloqué l'approvisionnement.
- **[Toglefritz/Bertram_Robot_Arm](https://github.com/Toglefritz/Bertram_Robot_Arm)** — dépôt accompagnant ce tutoriel, dont ce dépôt est le fork.

### Firmware

- **Marlin** — le projet BCN3D MOVEO met à disposition un firmware qui est une **version de Marlin adaptée au bras robotique**. Marlin étant conçu pour imprimantes 3D, c'est exactement cohérent avec le choix d'une carte RAMPS 1.4.

### Support constructeur

- **StepperOnline** — le support technique a été sollicité par email à deux reprises pour clarifier la convention de courant de leurs fiches produit (voir [§5.3](#53-peak-vs-rms--le-piège-des-fiches-techniques)). Réponses très utiles, à conserver.

---

## 3. Architecture du système

### 3.1 Principe général

Après plusieurs recherches sur les composants matériels, le constat est le suivant : **le projet s'articule autour d'une RAMPS 1.4**, carte de contrôle conçue à l'origine pour les imprimantes 3D, montée sur un **Arduino Mega 2560**.

Une RAMPS 1.4 pilote nativement cinq axes : `X`, `Y`, `Z`, `E0` et `E1` (les deux extrudeurs). Dans ce projet, ces cinq sorties ne commandent pas des axes cartésiens et des extrudeurs, mais **les cinq articulations du bras**. Cette réaffectation est tout l'intérêt de l'approche : on récupère une chaîne d'outils mature (RAMPS + Marlin + Pronterface + G-code) sans rien écrire de spécifique au départ.

**Choix important pour ce build :** les drivers pas-à-pas ne sont **pas** les habituels A4988/DRV8825 enfichés sur la RAMPS. Les moteurs retenus demandent trop de courant. On utilise donc des **drivers externes** (TB6560, TB6600, DM542T) alimentés séparément, la RAMPS ne fournissant plus que les signaux logiques `STEP`, `DIR` et `ENABLE`.

### Schéma de câblage

Le schéma de lalimentations de driveur :

<img width="3529" height="2245" alt="Shema_branchement - Page 1" src="https://github.com/user-attachments/assets/041aba9b-2a42-440e-827b-9f0b2f2cb784" />

Le shéma de cablage de l'axe X avec le (17HS13-0404S1) :

<img width="1531" height="1880" alt="Diagramme vierge (3)" src="https://github.com/user-attachments/assets/1f1ad59b-ce78-4137-8293-e2dcba2a8de5" />

Le shéma de cablage de l'axe Y avec le (17HS24-2104S-PG5) :

<img width="1856" height="2414" alt="Diagramme vierge (9)" src="https://github.com/user-attachments/assets/f457bfa9-1010-4160-83f0-104f6f00617f" />

Le shéma de cablage de l'axe Z avec le (23HS45-4204S) :

<img width="1831" height="2414" alt="Diagramme vierge (11)" src="https://github.com/user-attachments/assets/5acf17f7-8143-4864-ac61-6b9853d0ae7f" />

Le shéma de cablage de l'axe E0 avec le (17HS24-0644S) :

<img width="1856" height="2414" alt="Diagramme vierge (8)" src="https://github.com/user-attachments/assets/99e8b656-0455-4a4c-9029-ee06907c3e92" />


Le shéma de cablage de l'axe E1 avec le (14HS13-0804S) :

<img width="1531" height="1880" alt="Diagramme vierge (5)" src="https://github.com/user-attachments/assets/ccd135a1-64cc-4aff-b5c1-ca4251551945" />



### 3.2 Six moteurs pas-à-pas pour cinq axes

Les plus observateurs remarqueront qu'il y a **six moteurs pas-à-pas pour seulement cinq articulations**. Ce n'est pas une erreur.

**L'articulation de l'épaule nécessite la puissance conjointe de deux moteurs NEMA 23** pour supporter le poids de tout le reste du bras sans perdre de pas. Un seul moteur, même bien dimensionné, décroche dès que le bras s'étend.

La règle de câblage reste **un driver par moteur** — on ne met jamais deux moteurs sur un driver. Mais les deux drivers de l'épaule **partagent la même sortie de la RAMPS** (l'axe `Z`) via un câble en Y, pour garantir un mouvement parfaitement synchrone.

Et c'est là que se cache le piège : les deux moteurs étant montés **face à face**, ils doivent tourner **en sens opposés**. On inverse donc les deux fils d'une bobine sur l'un des deux moteurs, à la sortie du driver. Détail complet en [§8.1](#81-épaule--axe-z).

### 3.3 Attribution des axes RAMPS 1.4

| Axe RAMPS | Articulation | Moteur | Driver 
|---|---|---|---|---|
| `X` |  **Poignet 1** (rotation avant-bras) | 17HS13-0404S1 (NEMA 17, 26 N·cm, 0,4 A) | TB6560 
| `Y` | **Coude** | 17HS24-2104S-PG5 (NEMA 17 + réducteur 5,18:1) | TB6600 
| `Z` | **Épaule** | 2 × 23HS45-4204S (NEMA 23, 3 N·m) | 2 × DM542T
| `E0` | Rotation de la base | 17HS24-0644S (NEMA 17, 60 N·cm, 0,6 A)   | TB6600 
| `E1` | Poignet 2 | 14HS13-0804S (NEMA 14, 18 N·cm, 0,8 A) | TB6560 
| — | Pince | Servo Hitec HS-645MG | Sortie servo RAMPS | Pince |

### 3.4 Arborescence de l'alimentation

L'alimentation est un point sensible de ce build, et une source d'erreurs classique : **la RAMPS et les drivers ne sont pas alimentés depuis le même rail**.

```
Secteur 230 V AC
      │
      └─► Alimentation 24 V DC / 25 A / 600 W
                │
                ├─► 24 V direct ──────────────► Drivers TB6600 / DM542T (puissance)
                │                                (bornes VCC / GND de puissance)
                │
                ├─► Convertisseur DC-DC 24 V → 12 V / 3 A
                │         └──────────────────► RAMPS 1.4, côté logique
                │
                ├─► Module step-down réglable LM2596
                │         └──────────────────► rail auxiliaire / servo
                │
                └─► Ventilateurs 24 V (80 mm et 50 mm) — refroidissement des drivers

USB (Arduino Mega 2560) ◄──── PC (Pronterface)
```

**Points de vigilance :**

- Les masses (`GND`) de l'alimentation 24 V et de la RAMPS **doivent être communes**, sinon les signaux `STEP`/`DIR` n'ont pas de référence et les drivers ne déclenchent pas.
- Les drivers externes chauffent réellement à ces courants. Les ventilateurs ne sont pas décoratifs.
- Le servo de la pince ne doit **jamais** être alimenté depuis le régulateur 5 V de l'Arduino : un HS-645MG en charge tire bien plus que ce que ce régulateur peut fournir.

<!-- IMAGE : photo de l'armoire électrique / plaque de montage des drivers -->
<!-- Emplacement suggéré : docs/images/alimentation-drivers.jpg -->

---

## 4. Nomenclature et coûts

### 4.1 Comment lire ces tableaux

Cette section est **la plus soignée du dépôt**, parce que c'est celle qui a le plus de valeur pour quelqu'un qui veut refaire le projet : une nomenclature théorique se trouve partout, une nomenclature avec les prix réellement payés et les pièges d'approvisionnement, beaucoup moins.

Trois colonnes distinctes, à ne pas confondre :

| Colonne | Signification |
|---|---|
| **Qté requise** | Nombre de pièces effectivement utilisées sur le bras |
| **Conditionnement** | Ce qui a réellement été acheté. La plupart des pièces se vendent par lot : commander 3 roulements coûte le prix d'un lot de 10 |
| **Prix unitaire** | Prix par pièce du lot acheté |
| **Montant payé** | **La dépense réelle.** C'est cette colonne, et seulement celle-là, qui est additionnée dans les totaux |

> ⚠️ **Conséquence :** `Qté requise × Prix unitaire ≠ Montant payé` sur la majorité des lignes. Ce n'est pas une erreur de calcul, c'est le surplus de conditionnement. Il est parfaitement normal de finir avec 7 roulements 3 × 10 × 4 mm en trop.

**Conversion de devises.** Certains articles ont été commandés sur `amazon.com` (États-Unis) et facturés en **dollars**. Ils sont marqués 🇺🇸 dans les tableaux. Les montants sont reportés tels qu'affichés sur la facture d'origine ; le total en euros est donc **légèrement approximatif** pour ces lignes. Une révision de la nomenclature devrait basculer ces références sur `amazon.fr` ou un équivalent européen.

**Vérification arithmétique.** Tous les sous-totaux et le total général de ce document ont été **recalculés ligne par ligne**. Le total annoncé dans mes notes initiales (579,37 €) était obsolète ; l'écart est expliqué en [§4.6](#46-anomalies-relevées-et-corrections-apportées).

---

### 4.2 Mécanique

#### 4.2.1 Roulements

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Roulement 8 × 22 × 7 mm | 10 | Lot de 20 | 0,39 € | **7,99 €** | Amazon | [B0D7YTRG6R](https://www.amazon.fr/dp/B0D7YTRG6R) |
| Roulement 5 × 16 × 5 mm | 8 | Lot de 10 | 0,88 € | **8,80 €** | Amazon | [B0D5XNGQKR](https://www.amazon.fr/dp/B0D5XNGQKR) |
| Roulement 4 × 13 × 5 mm | 9 | Lot de 10 | 0,92 € | **9,20 €** | Amazon | [B097TVMZ1L](https://www.amazon.fr/dp/B097TVMZ1L) |
| Roulement 3 × 10 × 4 mm | 3 | Lot de 10 | 0,91 € | **9,10 €** | Amazon | [B0DCNRFZRG](https://www.amazon.fr/dp/B0DCNRFZRG) |
| | | | **Sous-total** | **35,09 €** | | |

> Les roulements 8 × 22 × 7 mm sont ceux qu'on consomme le plus : ils servent aux articulations **et** aux tendeurs de courroie (3 par tendeur, empilés). Prévoir large.

#### 4.2.2 Tiges et arbres

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Tige filetée M8 × 40 mm | 1 | Lot de 4 | 1,57 € | **6,29 €** | Amazon | [B0D46N4XJJ](https://www.amazon.fr/dp/B0D46N4XJJ) |
| Tige d'acier ⌀8 mm × 200 mm | 2 | 2 pièces | 4,29 € | **8,59 €** 🇺🇸 | Amazon US | [B0BQBX718N](https://www.amazon.com/dp/B0BQBX718N) |
| | | | **Sous-total** | **14,88 €** | | |

> 🔁 **Doublon retiré.** Ma nomenclature d'origine listait une seconde fois les tiges d'acier ⌀8 × 200 mm dans une rubrique « Tiges en acier » distincte, à 7,39 €, avec la même référence produit `B0BQBX718N`. Il s'agissait du même achat compté deux fois. Voir [§4.6](#46-anomalies-relevées-et-corrections-apportées).

#### 4.2.3 Courroies

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Courroie crantée T5, 5 m au mètre | 1 rouleau | Rouleau 500 cm | 36,88 € | **36,88 €** 🇺🇸 | Amazon US | [B07NRY8C6X](https://www.amazon.com/dp/B07NRY8C6X) |
| | | | **Sous-total** | **36,88 €** | | |

> 🔁 **Doublon retiré.** Cette courroie apparaissait deux fois dans mes notes, sous deux rubriques différentes (« Ceintures » à 36,88 € et « Courroie de distribution » à 31,74 €), avec la **même référence produit** `B07NRY8C6X`. Un seul rouleau a été acheté. L'écart de prix entre les deux lignes s'explique probablement par une variation du prix Amazon entre deux consultations. La valeur retenue est **36,88 €**, celle de la facture.
>
> 💡 Un rouleau de 5 m est largement suffisant pour l'ensemble des articulations : voir [§9](#9-longueurs-de-courroies) pour le détail des longueurs.

#### 4.2.4 Accouplements

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Accouplement d'arbre 5 mm → 8 mm | 1 | Lot de 2 | 3,99 € | **7,98 €** | Amazon | [B096G1GZH5](https://www.amazon.fr/dp/B096G1GZH5) |
| | | | **Sous-total** | **7,98 €** | | |

#### 4.2.5 Visserie

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Kit vis + écrous + rondelles M3 (10 / 16 / 25 / 30 mm) | 1 kit | Kit assorti | 14,88 € | **14,88 €** | Amazon | [B0CJ28LJPW](https://www.amazon.fr/dp/B0CJ28LJPW) |
| Vis M3 × 40 mm | 7 | Lot de 10 | 0,86 € | **8,59 €** | Amazon | ⚠️ Référence indisponible |
| Kit vis + écrous M4 (10 / 20 / 40 mm) | 1 kit | Kit assorti | 11,99 € | **11,99 €** | Amazon | [B0CX1J8WNS](https://www.amazon.fr/dp/B0CX1J8WNS) |
| Vis M4 × 45 mm | 4 | Lot de 20 | 0,50 € | **9,95 €** | Amazon | [B09RWWT8W9](https://www.amazon.fr/dp/B09RWWT8W9) |
| Vis M4 × 55 mm | 4 | Lot de 20 | 0,55 € | **10,95 €** | Amazon | ⚠️ Référence indisponible |
| Vis M5 × 14 mm (tête cylindrique Allen, inox) | 16 | Lot de 20 | 0,48 € | **9,69 €** | Amazon | [B0DHPFHBRT](https://www.amazon.fr/dp/B0DHPFHBRT) |
| Vis M8 × 65 mm | 1 | Lot de 8 | 1,75 € | **13,99 €** | Amazon | [B0CTKDFBRL](https://www.amazon.fr/dp/B0CTKDFBRL) |
| | | | **Sous-total** | **80,04 €** | | |

> ⚠️ **Deux références ne sont plus disponibles** (M3 × 40 mm et M4 × 55 mm). Ce sont des vis totalement standard, trouvables chez n'importe quel fournisseur de visserie. Les montants sont conservés à titre de référence de coût.
>
> 💡 **Conseil d'achat :** privilégier les kits assortis M3 / M4 / M5 plutôt que les longueurs à l'unité. Le prix au kit est du même ordre, et on évite trois commandes séparées quand on découvre qu'il manque une longueur en cours de montage.

#### 4.2.6 Écrous

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Écrou de blocage (frein) M8 | 1 | Lot | 10,99 € | **10,99 €** | Amazon | ⚠️ Lien à corriger |
| | | | **Sous-total** | **10,99 €** | | |


#### 4.2.7 Inserts thermofixés

| Référence | Qté requise | Conditionnement | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| Kit inserts thermofixés M3 / M4 / M5 | 1 kit | Kit assorti | 19,99 € | **19,99 €** | Amazon | [B0DB1T7SM5](https://www.amazon.fr/dp/B0DB1T7SM5) |
| | | | **Sous-total** | **19,99 €** | | |

> Les inserts thermofixés (« heat-set inserts ») sont **non négociables** sur ce projet. Visser directement dans du plastique imprimé, sur des pièces qui subissent le couple d'un NEMA 23, arrache le filetage à la première contrainte. Prévoir un fer à souder avec panne dédiée.

#### Sous-total mécanique

| | Montant |
|---|---|
| Roulements | 35,09 € |
| Tiges et arbres | 14,88 € |
| Courroies | 36,88 € |
| Accouplements | 7,98 € |
| Visserie | 80,04 € |
| Écrous | 10,99 € |
| Inserts thermofixés | 19,99 € |
| **Total mécanique** | **205,85 €** |

---

### 4.3 Moteurs et actionneurs

Cette section est la plus instructive de la nomenclature, parce qu'elle contient **deux commandes successives** : celle du tutoriel Instructables, puis celle qui l'a corrigée.

#### ⛔ Moteurs achetés puis abandonnés — ne pas racheter

Ces moteurs ont été commandés en suivant le tutoriel Instructables. **Ils ne sont pas assez puissants pour obtenir un bras fiable.** Ils ont été remplacés sur la recommandation d'une personne ayant rencontré exactement le même problème en suivant ce tutoriel.

| Référence | Qté | Caractéristiques | Prix unitaire | Montant payé | Remplacé par |
|---|---|---|---|---|---|
| **17HS13-0404S-PG5** | 1 | NEMA 17 + réducteur planétaire 5:1, L = 33 mm, 0,4 A | 26,37 € | **26,37 €** | 17HS24-2104S-PG5 |
| **23HS30-2804S** | 2 | NEMA 23, 2,00 N·m, 2,8 A, 57 × 57 × 76,5 mm | 17,89 € | **35,78 €** | 23HS45-4204S |
| | | | **Sous-total perdu** | **62,15 €** | |

> **Ne les commandez pas.** Ces 62,15 € sont le coût de mon erreur de dimensionnement — la seule ligne de cette nomenclature qui soit purement une perte. Si vous refaites le projet, sautez directement aux références du tableau suivant.

#### ✅ Moteurs retenus

| Référence | Qté | Articulation | Caractéristiques | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|---|
| **23HS45-4204S** | 2 | Épaule (`Z`) | NEMA 23, **3,0 N·m** (425 oz·in), 4,2 A **peak**, 57 × 57 × 113 mm, 4 fils | 32,16 € | **64,32 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/nema-23-bipolaire-3nm-425oz-in-4-2a-57x57x114mm-4-fils-cnc-moteur-pas-a-pas-23hs45-4204s) |
| **17HS24-2104S-PG5** | 1 | Coude (`Y`) | NEMA 17 + réducteur planétaire **5,18:1**, L = 60 mm, 2,1 A **peak**, couple en sortie de boîte 3–5 N·m | 35,26 € | **35,26 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/nema-17-moteur-pas-a-pas-bipolaire-l-60mm-w-rapport-d-engrenage-5-1-boite-de-vitesses-planetaire-17hs24-2104s-pg5) |
| **17HS24-0644S** | 1 | Base (`X`) | NEMA 17, 65 N·cm (92 oz·in), 0,6 A, 42 × 42 × 60 mm, 4 fils | 12,98 € | **12,98 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/nema-17-bipolaire-1-8deg-65ncm-92-05oz-in-0-60a-42x42x60mm-4-fils-17hs24-0644s) |
| **17HS13-0404S1** | 1 | Poignet 1 (`E0`) | NEMA 17, 26 N·cm (36,8 oz·in), 0,4 A, 42 × 42 × 34 mm, 4 fils | 8,31 € | **8,31 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/nema-17-bipolaire-1-8deg-26ncm-36-8oz-in-0-4a-12v-42x42x34mm-4-fils-17hs13-0404s1) |
| **14HS13-0804S** | 1 | Poignet 2 (`E1`) | NEMA 14, 18 N·cm (25,5 oz·in), 0,8 A, 35 × 35 × 34,8 mm, 4 fils | 8,31 € | **8,31 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/nema-14-bipolaire-1-8deg-18ncm-25-5oz-in-0-8a-5-74v-35x35x34mm-4-fils-14hs13-0804s) |
| **Hitec HS-645MG** | 1 | Pince | Servo à engrenages métalliques, 2 roulements à billes, couple élevé | 30,25 € | **30,25 €** 🇺🇸 | Amazon US | [B003T6RSVQ](https://www.amazon.com/dp/B003T6RSVQ) |
| | | | | **Sous-total retenu** | **159,43 €** | | |

#### Sous-total moteurs

| | Montant |
|---|---|
| Moteurs retenus | 159,43 € |
| Moteurs abandonnés (dépense réelle, non réutilisable) | 62,15 € |
| **Total moteurs — dépense réelle** | **221,58 €** |
| **Total moteurs — pour refaire le projet** | **159,43 €** |

---

### 4.4 Électronique, drivers et alimentation

| Référence | Qté | Rôle | Prix unitaire | Montant payé | Fournisseur | Lien |
|---|---|---|---|---|---|---|
| **Arduino Mega 2560** | 1 | Microcontrôleur, exécute Marlin | 49,19 € | **49,19 €** | Amazon | [B0046AMGW0](https://www.amazon.fr/dp/B0046AMGW0) |
| **RAMPS 1.4** | 1 | Shield de contrôle 5 axes | 9,99 € | **9,99 €** | Amazon | [B07BSRS9WS](https://www.amazon.fr/dp/B07BSRS9WS) |
| Câble USB 2.0 type B | 1 | Liaison PC ↔ Arduino (Pronterface) | 7,75 € | **7,75 €** | Amazon | [B07L4KTXQR](https://www.amazon.fr/dp/B07L4KTXQR) |
| **Driver TB6560** | 4 achetés | Moteurs faible courant (base, coude, poignets) — max 3 A | 11,99 € | **47,96 €** | Amazon | [B07DK7CZK3](https://www.amazon.fr/dp/B07DK7CZK3) |
| **Driver TB6600** | 2 | Moteurs NEMA 23 de l'épaule — max 4 A | 14,99 € | **29,98 €** | Amazon | [B07YJD5QZ9](https://www.amazon.fr/dp/B07YJD5QZ9) |
| **Driver DM542T** | 2 | Tentative de montée en gamme sur l'axe `Z` — max 4,5 A peak / 3,2 A RMS | 21,58 € | **43,16 €** | StepperOnline | [Fiche](https://www.omc-stepperonline.com/fr/pilote-numerique-pas-a-pas-1-0-4-2a-20-50vdc-pour-nema-17-23-24-moteur-pas-a-pas-dm542t) |
| **Alimentation 24 V DC / 25 A / 600 W** | 1 | Alimentation principale des drivers | 29,99 € | **29,99 €** | Amazon | [B0BQJMSHVH](https://www.amazon.fr/dp/B0BQJMSHVH) |
| Câble secteur avec bornes, 230 V / 16 A | 1 | Raccordement de l'alimentation | 9,79 € | **9,79 €** | Amazon | [B0CZNTJWZR](https://www.amazon.fr/dp/B0CZNTJWZR) |
| Convertisseur DC-DC 24 V → 12 V / 3 A | 1 | Alimentation logique de la RAMPS | 12,72 € | **12,72 €** | Amazon | [B07PP5JJB6](https://www.amazon.fr/dp/B07PP5JJB6) |
| Module step-down réglable LM2596 | 1 | Rail auxiliaire réglable | 5,00 € | **5,00 €** | Letmeknow (Paris) | — |
| Ventilateur 24 V DC, 0,96 W, 80 × 80 × 25 mm | 1 | Refroidissement drivers | 8,22 € | **8,22 €** | Amazon | [B07B665FMH](https://www.amazon.fr/dp/B07B665FMH) |
| Ventilateurs 50 × 50 × 10 mm | 2 (lot) | Refroidissement ponctuel | 3,39 € | **6,79 €** | Amazon | [B0CTMPNKV8](https://www.amazon.fr/dp/B0CTMPNKV8) |
| | | | **Sous-total** | **260,54 €** | | |


---

### 4.5 Récapitulatif des coûts

Tous les montants ci-dessous ont été **recalculés ligne par ligne** à partir des tableaux précédents.

#### Dépense réelle sur le projet

| Poste | Montant |
|---|---|
| Mécanique (roulements, tiges, courroies, visserie, inserts) | 205,85 € |
| Moteurs et actionneurs | 221,58 € |
| Électronique, drivers, alimentation | 260,54 € |
| **TOTAL DÉPENSÉ (hors filament)** | **687,97 €** |

#### Coût pour refaire le projet aujourd'hui

En repartant de zéro avec le bénéfice de l'expérience — donc sans les deux références de moteurs sous-dimensionnées, et sans les DM542T qui n'ont pas fonctionné :

| Poste | Montant | Écart |
|---|---|---|
| Mécanique | 205,85 € | — |
| Moteurs (références retenues uniquement) | 159,43 € | − 62,15 € |
| Électronique (sans les DM542T) | 217,38 € | − 43,16 € |
| **TOTAL POUR REFAIRE** | **582,66 €** | **− 105,31 €** |

Et en remplaçant l'Arduino Mega officiel par un clone à ~18 € : **environ 551 €**.

#### Note sur le total de 579,37 € annoncé dans mes premières notes

Ce chiffre circulait dans mes notes de projet. **Il est obsolète et ne doit plus être utilisé.** La vérification permet de le reconstituer exactement :

```
Total actuel de la nomenclature complète        727,10 €
  − Drivers DM542T          (2 × 21,58 €)      − 43,16 €
  − Moteurs 23HS45-4204S    (2 × 32,16 €)      − 64,32 €
  − Moteur 17HS24-2104S-PG5                    − 35,26 €
  − Module step-down LM2596                     − 5,00 €
                                             ───────────
                                                579,36 €   ← à 1 centime d'arrondi près
```

**Conclusion :** 579,37 € était le total **avant** la seconde commande de moteurs, l'achat des DM542T et l'ajout du LM2596. C'est un instantané correct à une date donnée, pas une erreur de calcul — mais il sous-estime le coût réel de 108,60 €.

#### Réconciliation complète des totaux

Pour lever toute ambiguïté, voici les trois chiffres qui peuvent légitimement circuler et ce que chacun signifie :

| Chiffre | Signification | À utiliser pour |
|---|---|---|
| **727,10 €** | Somme brute de toutes les lignes de la nomenclature d'origine, **doublons inclus** | Rien — ce total contient deux articles comptés deux fois |
| **687,97 €** | Dépense réelle, doublons retirés | Répondre à « combien ça t'a coûté ? » |
| **582,66 €** | Coût de reconstruction optimisé | Répondre à « combien ça me coûterait ? » |

---

### 4.6 Anomalies relevées et corrections apportées

Cette section documente **toutes** les erreurs trouvées lors de la révision de ma nomenclature d'origine. Elle est là par honnêteté, et parce que ce sont des pièges très faciles à reproduire quand on tient une liste d'achats sur plusieurs mois.

| # | Anomalie | Impact | Correction |
|---|---|---|---|
| **1** | **Total obsolète** — 579,37 € annoncé | Sous-estimation de **108,60 €** | Total recalculé : 687,97 € en dépense réelle. Origine de l'écart identifiée et documentée en [§4.5](#45-récapitulatif-des-coûts) |
| **2** | **Doublon — tiges d'acier ⌀8 × 200 mm** listées dans deux rubriques (« Tiges » à 8,59 € et « Tiges en acier » à 7,39 €), même référence `B0BQBX718N` | Surestimation de **7,39 €** | Une seule ligne conservée, à 8,59 € (montant facturé) |
| **3** | **Doublon — courroie T5** listée dans deux rubriques (« Ceintures » à 36,88 € et « Courroie de distribution » à 31,74 €), même référence `B07NRY8C6X` | Surestimation de **31,74 €** | Une seule ligne conservée, à 36,88 €. Un seul rouleau de 5 m a été acheté |
| **4** | **Lien produit erroné** — l'écrou de blocage M8 et le kit de visserie M3 pointent vers la même référence `B0CJ28LJPW`, à deux prix différents | Aucun impact sur le total | Signalé dans le tableau. Lien à retrouver sur la facture |
| **5** | **Devises mélangées** — plusieurs articles commandés sur `amazon.com` en USD, reportés comme des euros | Léger biais sur le total, sens indéterminé | Articles marqués 🇺🇸. Ligne d'action : basculer sur des références EU |
| **6** | **Colonnes mal comprises** — la colonne « coût total » de mes notes contenait le **prix du lot**, pas `quantité × prix unitaire` | Aucun impact sur le total, mais illisible | Colonnes séparées et explicitées en [§4.1](#41-comment-lire-ces-tableaux) |
| **7** | **Deux références indisponibles** — vis M3 × 40 mm et M4 × 55 mm | Aucun | Signalé. Ce sont des vis standard, trouvables partout |
| **8** | **Quantité TB6560 ambiguë** — noté « 4 2 » dans mes notes | Aucun | Le montant payé (47,96 €) correspond sans ambiguïté à **4 unités** à 11,99 €. Toutes ne sont pas montées sur le bras |

**Les deux doublons (#2 et #3) se compensent partiellement avec le total obsolète (#1)**, ce qui explique pourquoi l'erreur n'avait pas sauté aux yeux : la somme brute des lignes (727,10 €) et le total annoncé (579,37 €) étaient tous les deux faux, dans des directions différentes.

---

### 4.7 Coût du filament

Le filament n'est **pas** inclus dans les totaux ci-dessus, parce qu'il dépend trop du matériau et des réglages :

| Paramètre | Fourchette |
|---|---|
| Coût total du plastique | **100 € à 200 €** |
| Facteurs de variation | Type de filament (PLA / PETG / ABS), taux de remplissage, nombre de réimpressions après échec |

**Budget total réaliste du projet, filament compris : 690 € à 890 €.**

Voir [§7](#7-impression-3d) pour le détail des matériaux et les échecs d'impression rencontrés.

---

## 5. Choix de la motorisation

### 5.1 Épaule — la remontée en couple, en trois étapes

L'épaule est l'articulation critique : elle porte **tout** le reste du bras, à bout de levier. C'est là que j'ai dû revoir mon dimensionnement deux fois.

| Étape | Moteur | Couple de maintien | Verdict |
|---|---|---|---|
| **1. Recommandation du site de référence** | 23HS22-2804S | 1,24 N·m | ❌ Plusieurs témoignages de builders indiquent que **ce n'est pas suffisant**. Jamais commandé |
| **2. Premier choix** | 23HS30-2804S | 2,00 N·m | ⚠️ Commandé, monté, insuffisant en pratique |
| **3. Choix final** | **23HS45-4204S** | **3,00 N·m** | ✅ Retenu |

**Le raisonnement de l'étape 2 (et pourquoi il était incomplet).** En passant de 1,24 à 2,00 N·m, je pensais avoir pris assez de marge. Le moteur demande 2,8 A, ce qui se rapproche fortement de la limite des TB6560 (3 A) — j'ai donc choisi **deux TB6600** capables de fournir jusqu'à 4 A, pour rester large et éviter la surchauffe.

Le point que je n'avais pas anticipé : le couple de maintien n'est pas le couple disponible en mouvement. En microstepping fin et sous charge dynamique, le couple utile s'effondre bien avant la valeur de la fiche technique. 2 N·m annoncés ne donnent pas 2 N·m au bout du bras.

**Le choix final : 23HS45-4204S, 3,0 N·m, 4,2 A peak.** Combiné aux deux moteurs travaillant en tandem sur l'axe `Z`, cela donne la réserve nécessaire.

### 5.2 Coude — l'apport du réducteur

Le coude est situé assez bas sur le bras et doit supporter le poids relativement important de tout ce qui est en aval. Cette articulation demande donc un **couple élevé**.

Plutôt que d'empiler des moteurs — ce qui augmenterait considérablement le poids et l'encombrement, et déplacerait le problème sur l'épaule — la solution retenue est un **moteur à réducteur planétaire intégré**. Le réducteur confère au moteur du coude un avantage mécanique suffisant pour actionner le reste du bras avec un seul moteur.

| Étape | Moteur | Réduction | Courant | Verdict |
|---|---|---|---|---|
| **1. Premier choix** | 17HS13-0404S-PG5 | 5:1 | 0,4 A | ⚠️ Commandé, couple insuffisant |
| **2. Choix final** | **17HS24-2104S-PG5** | **5,18:1** | 2,1 A peak | ✅ Retenu — couple en sortie de boîte 3–5 N·m |

> Le moteur retenu lève le coude sans difficulté. Il subsiste un problème de **perte de pas à la remontée** en microstepping 1/8 et 1/16, diagnostiqué en [§11](#11-journal-des-pannes) — la cause n'est pas le moteur.

### 5.3 Peak vs RMS — le piège des fiches techniques

**C'est le point technique le plus important de tout ce document, et celui qui m'a coûté le plus de temps.**

Les fiches produit StepperOnline annoncent un courant par phase — 4,2 A pour le 23HS45-4204S, 2,1 A pour le 17HS24-2104S-PG5. J'ai contacté **le support StepperOnline par email**, à deux reprises, pour lever l'ambiguïté.

**Réponse officielle : ces valeurs sont des courants de crête (peak), pas des courants RMS.**

La conversion est un simple facteur √2 ≈ 1,414 :

| Moteur | Courant annoncé (peak) | Courant RMS réel |
|---|---|---|
| 23HS45-4204S | 4,2 A | **≈ 2,97 A** |
| 17HS24-2104S-PG5 | 2,1 A | **≈ 1,49 A** |

**Pourquoi c'est un piège.** Les drivers, eux, ne parlent pas tous la même langue : certains annoncent leur limite en peak, d'autres en RMS, et beaucoup de tables de DIP switches donnent les deux dans des colonnes voisines qu'on confond facilement. **Régler un driver sur 2,1 A en croyant que c'est du RMS revient à faire tourner le moteur en permanence à son courant de crête maximal.** Conséquences : le moteur chauffe, il sature en couple plus vite qu'attendu, et il perd des pas précisément dans les phases où on a besoin de lui.

**Recommandation explicite de StepperOnline :** ne pas faire fonctionner un moteur à son niveau de crête en continu. On peut se rapprocher de la limite RMS pour privilégier la performance, mais à condition de **surveiller la température du moteur** et de restreindre cet usage à des durées courtes.

**À retenir avant de toucher à un seul DIP switch :** vérifier si la valeur imprimée sur votre driver est peak ou RMS, et si celle de la fiche de votre moteur l'est aussi. Si vous ne savez pas, écrivez au fabricant — c'est gratuit et ils répondent.

---

## 6. Choix et configuration des drivers

### 6.1 Tableau comparatif

| Driver | Courant max | Alimentation | Utilisé pour | Bilan |
|---|---|---|---|---|
| **TB6560** | 3 A | 24 V | Base, coude, poignets 1 et 2 | ✅ Fonctionne. Attention à la polarité `ENABLE` — voir [§6.2](#62-tb6560--la-subtilité-enable) |
| **TB6600** | 4 A | 24 V | Épaule (2 unités) | ✅ Fonctionne de manière fiable, y compris avec les NEMA 23 à 3 N·m |
| **DM542T** | 4,5 A peak / 3,2 A RMS | 20–50 V DC | Tentative sur l'épaule | ❌ **N'a jamais fait tourner un moteur.** Voir [§6.5](#65-dm542t--panne-non-résolue) |

### 6.2 TB6560 — la subtilité ENABLE

Le premier câblage a été réalisé **sur un seul moteur, avec un seul driver**, afin de limiter les dégâts en cas de court-circuit. Bonne décision : le moteur n'a pas démarré.

Après plusieurs recherches, la cause a été identifiée. Sur **le modèle de TB6560 que j'ai commandé**, la logique de la broche `ENABLE` est **inversée par rapport à la convention habituelle** : il faut recevoir `ENABLE` à **LOW pour allumer** le moteur, et à **HIGH pour l'éteindre**.

**Câblage correct pour cette carte :**

| Borne du driver | Se connecte à |
|---|---|
| `EN−` | Sortie `ENABLE` de la RAMPS 1.4 |
| `EN+` | `GND` |

<!-- IMAGE : schéma de câblage TB6560 avec EN- sur ENABLE RAMPS et EN+ sur GND -->
<!-- Emplacement suggéré : docs/images/cablage-tb6560-enable.png -->

> ⚠️ **Cette polarité n'est pas universelle.** Les cartes TB6560 sont largement clonées et la logique `ENABLE` varie d'une révision à l'autre. Si votre moteur reste inerte alors que `STEP` et `DIR` sont corrects et que l'alimentation est bonne, **testez les deux polarités de `ENABLE`** avant de chercher plus loin. C'est cinq minutes de test contre potentiellement plusieurs heures de diagnostic.

### 6.3 TB6600 — le driver qui a tenu

Les TB6600 sont les drivers qui font effectivement tourner l'épaule. Rien de particulier à signaler dans leur configuration : câblage en **anode commune** (`+5 V` sur `PUL+` et `DIR+`, signal sur `PUL−` et `DIR−`), réglage du courant par DIP switches, et ils fonctionnent.

C'est leur fiabilité qui a servi de **référence de contrôle** pendant tout le diagnostic des DM542T : même code, même moteur, même câblage logique — le TB6600 tourne, le DM542T non. Sans ce point de comparaison, le diagnostic aurait été bien plus difficile.

### 6.4 DM542T — configuration retenue

Configuration établie après échange avec le support StepperOnline, pour les moteurs 23HS45-4204S (4,2 A peak / ≈ 2,97 A RMS) :

**Courant — SW1, SW2, SW3**

Le DM542T ne propose pas exactement 4,2 A peak. Les deux crans les plus proches sont 3,76 A et 4,5 A peak. Le réglage retenu est **4,5 A peak (≈ 3,18 A RMS)** : soit environ **6 % au-dessus** du RMS nominal du moteur, ce qui reste dans une marge thermique acceptable tout en préservant le couple maximal. Le cran inférieur aurait sacrifié du couple sur l'articulation qui en a le plus besoin.

**Courant de repos — SW4**

| Position | Effet | Retenu |
|---|---|---|
| `SW4 = ON` | Courant plein au repos | — |
| **`SW4 = OFF`** | **Demi-courant au repos** | ✅ |

`SW4 = OFF` est le bon réglage pour un bras robotique : les moteurs passent l'essentiel de leur temps à **maintenir une position sans bouger**, et le demi-courant réduit significativement l'échauffement dans cette phase.

**Microstepping — SW5 à SW8**

Point de vocabulaire qui prête à confusion : la table sérigraphiée sur le DM542T n'indique pas « 1/8 » ou « 1/16 », mais des **pulses/rev**. La relation est directe :

```
Pulses/rev = STEPS_PER_REV × MICROSTEPPING
```

Pour un moteur 1,8° (200 pas/tour) en 1/16 de pas :

```
Pulses/rev = 200 × 16 = 3200
```

Réglage retenu : **3200 pulses/rev**, correspondant à `MICROSTEPPING = 16` dans le code.

> ⚠️ **La correspondance exacte des positions ON/OFF varie selon la révision du driver.** Lisez la table sérigraphiée sur **votre** boîtier plutôt que de recopier un tableau trouvé en ligne — y compris celui-ci.

### 6.5 DM542T — panne non résolue

Les DM542T avaient été achetés pour monter en gamme sur l'axe `Z`. **Aucun des deux n'a jamais fait tourner un moteur.** Le détail complet du diagnostic — long, méthodique, et infructueux — est en [§11](#11-journal-des-pannes). C'est le seul point du projet qui reste ouvert, et il est documenté en tant que tel plutôt que passé sous silence.

**Décision prise :** rester sur les TB6600, qui fonctionnent. Le bras est opérationnel sans les DM542T.

---

## 7. Impression 3D

### 7.1 Choix des matériaux

**Toutes les pièces ne peuvent pas être imprimées en PLA.**

Certaines pièces sont destinées à **contenir les moteurs**. Sous l'effet combiné des contraintes mécaniques et de la chaleur dégagée par les moteurs, le PLA se déforme — il y a un risque réel de torsion de la pièce, qui désaligne l'articulation. Pour ces pièces, il faut un filament plus résistant en température : **ABS ou PETG**.

| Type de pièce | Filament | Raison |
|---|---|---|
| Supports moteur, corps d'articulation | **ABS ou PETG** | Contrainte mécanique + chaleur du moteur → risque de torsion en PLA |
| Pièces structurelles non chauffées | PLA acceptable | Plus facile à imprimer, moins cher |

Les impressions ont été réalisées **au FabLab** (pour l'ABS, qui demande un caisson) et sur une **imprimante Bambu Lab** pour le reste.

### 7.2 Échecs et réglages

Le journal des impressions, honnêtement :

| Tentative | Matériau | Réglage | Résultat |
|---|---|---|---|
| 1 | ABS | Remplissage 40 % | ❌ **Échec — warping important.** Décollement des bords, pièce inutilisable |
| 1 (bis) | ABS | Remplissage 40 % | ❌ **Coupure de courant** en cours d'impression, arrêt définitif |
| 2 | ABS | Remplissage **25 %** | ⚠️ **Défauts importants.** Une partie s'est cassée — recollée au pistolet à colle |

**Ce que j'en retire :**

- L'ABS **exige** un caisson fermé et un plateau bien chaud. Le warping n'est pas un défaut de réglage marginal, c'est le comportement par défaut de l'ABS sans environnement contrôlé.
- Baisser le remplissage de 40 % à 25 % réduit le temps d'impression et la matière, mais **fragilise** les pièces structurelles. Sur des pièces qui reçoivent le couple d'un NEMA 23, ce n'est pas un bon compromis. Le PETG est probablement le meilleur choix : quasiment la tenue en température de l'ABS, sans le warping.
- **Prévoyez des réimpressions.** Elles font partie du budget filament de 100–200 €.

<!-- IMAGE : comparaison des deux tentatives d'impression ABS (warping / casse) -->
<!-- Emplacement suggéré : docs/images/impression-warping.jpg -->

### 7.3 Poulies personnalisées — méplat en D (OpenSCAD)

Les poulies du commerce ne correspondaient pas au besoin. J'ai donc **modifié un générateur de poulies paramétriques OpenSCAD** pour l'adapter à l'arbre du NEMA 23.

**Objectif :** un alésage avec **méplat en D**, correspondant exactement à l'arbre du 23HS45-4204S, sans vis de blocage ni écrou prisonnier. Le méplat seul assure la transmission du couple et l'immobilisation en rotation.

**Cotes de l'arbre, relevées sur la datasheet du 23HS45-4204S :**

| Cote | Valeur |
|---|---|
| Diamètre d'arbre | 10 mm (± 0,012 mm) |
| Largeur du côté plat | 9,5 mm (± 0,15 mm) |
| Profondeur du méplat depuis le bord | 0,25 – 0,30 mm |

**Paramètres OpenSCAD retenus :**

```scad
motor_shaft   = 10.1;   // alésage légèrement majoré pour le jeu d'impression
pulley_b_dia  = 30;     // diamètre de la base
pulley_t_ht   = 15;     // hauteur de la partie dentée
pulley_b_ht   = 4;      // hauteur de la base
no_of_nuts    = 0;      // pas d'écrou prisonnier
retainer      = 1;      // rebord haut
idler         = 1;      // rebord bas
// hauteur des deux rebords : 2.0 mm
```

**Méthode géométrique — le point qui compte.** L'approche intuitive consiste à soustraire un cube de l'alésage cylindrique pour créer le plat. **Ça ne marche pas correctement** : cela laisse des vides et retire de la matière au mauvais endroit.

La bonne méthode est une **`intersection()` entre le cylindre d'alésage et un cube décalé**, ce qui découpe directement le cylindre à la dimension du plat, proprement :

```scad
intersection() {
    cylinder(r = motor_shaft/2, h = ..., $fn = 100);
    translate([0, -(motor_shaft/2 - d_cut_depth), 0])
        cube([motor_shaft * 2, motor_shaft, ...], center = true);
}
// limite la dimension Y à motor_shaft/2 - d_cut_depth = 4.75 mm
```

**Rebords (flanges).** Un rebord de 2,0 mm en haut et en bas de la poulie empêche la courroie de sauter latéralement. Sur un bras qui bouge dans plusieurs plans, contrairement à une imprimante 3D, ce n'est pas un luxe.

> 💡 Une poulie de coude doit être montée **sans base** (`pulley_b_ht = 0`) — voir [§8.2](#82-coude--axe-y).

---

## 8. Assemblage articulation par articulation

> **Convention de lecture :** toutes les dimensions de visserie sont en **millimètres**. Une vis « M4 × 10 » est une vis métrique de 4 mm de diamètre et 10 mm de longueur.

### 8.1 Épaule — axe `Z`

L'articulation la plus complexe du bras, et celle où une erreur de câblage peut casser des pièces.

#### Matériel

| Élément | Quantité |
|---|---|
| Moteur 23HS45-4204S (NEMA 23, 3 N·m) | 2 |
| Driver TB6600 | 2 |
| Câble en Y (dérivation des signaux) | 1 |

#### Étape 1 — Fabriquer le câble en Y

Les deux moteurs doivent tourner **parfaitement à l'unisson**. Pour cela, on récupère les signaux `STEP`, `DIR` et `ENABLE` envoyés par la RAMPS 1.4 **sur l'axe `Z`**, puis on réalise une dérivation — plus précisément un **câble en Y** — afin de relier `STEP`, `DIR`, `ENABLE` et `GND` **aux deux TB6600 sur la même entrée**.

**Code couleur utilisé :**

| Signal | Couleur |
|---|---|
| `DIR` | Bleu |
| `STEP` | Vert |
| `ENABLE` | Orange |
| `GND` | Noir |

> J'ai utilisé des **gaines thermorétractables transparentes** sur les soudures en Y, pour pouvoir inspecter visuellement la jonction. C'est plus rigolo, et surtout ça permet de vérifier une soudure suspecte sans tout décâbler.

<!-- IMAGE : câble en Y avec gaines transparentes -->
<!-- Emplacement suggéré : docs/images/cable-en-y.jpg -->

#### Étape 2 — Vérifier avant de monter

Une fois le câble en Y branché et les drivers alimentés, connectez les moteurs et faites-les tourner **avant tout montage mécanique**.

#### ⛔ Étape 3 — ARRÊTEZ-VOUS AVANT DE MONTER

> ### ⚠️ AVERTISSEMENT
>
> **Vous vouliez assembler ça comme ça ? Arrêtez-vous, pauvres fous !**
>
> Même si les deux moteurs tournent parfaitement à l'unisson, **on ne peut pas les monter tels quels**. Ils tournent dans le **même sens**. Or ils sont montés **face à face** : dans cette configuration, ils exercent des rotations opposées sur la même transmission. Les courroies n'apprécient pas du tout, et **cela risque de tout casser**.

**La correction.** Pour que les deux moteurs tournent dans des sens opposés — et donc produisent un mouvement cohérent une fois montés face à face — il faut **inverser deux fils d'une même bobine sur l'un des deux moteurs**, à la sortie du driver.

Sur les moteurs StepperOnline 4 fils, les bobines se répartissent ainsi :

| Bobine | Fils |
|---|---|
| A | **Noir** + **Vert** |
| B | Rouge + Bleu |

**Il suffit d'inverser le fil noir et le fil vert sur un seul des deux moteurs.** Cela inverse la polarité de la bobine A, donc le sens de rotation.

> 💡 **Vérifiez vos bobines au multimètre** avant de câbler. Mesurez la résistance entre paires de fils : les deux fils d'une même bobine présentent une résistance faible (quelques ohms), deux fils de bobines différentes un circuit ouvert. Le code couleur des moteurs varie selon les fabricants — ne faites pas confiance à un tableau, mesurez.

<!-- IMAGE : schéma de branchement des deux moteurs Z avec inversion noir/vert -->
<!-- Emplacement suggéré : docs/images/cablage-epaule-inversion.png -->

**Résultat attendu :** deux moteurs jumelés qui effectuent exactement les mêmes mouvements, **mais en miroir**. C'est ce qu'on veut.

#### Étape 4 — Courroie

Voir [§9](#9-longueurs-de-courroies) : **courroie de 90 dents** pour cette articulation.

---

### 8.2 Coude — axe `Y`

#### Matériel

| Élément | Quantité |
|---|---|
| Moteur 17HS24-2104S-PG5 (NEMA 17 + réducteur 5,18:1) | 1 |
| Driver TB6560 | 1 |
| Roulement 8 × 22 × 7 mm | 3 (tendeur) + 2 (arbre) |
| Vis M4 × 20 mm + écrou M4 | 1 (tendeur) |
| Vis M4 × 10 mm | 4 (fixation à l'épaule) |
| Vis M3 × 40 mm | 1 (montage du tendeur) |
| Vis M3 × 10 mm | 4 (fixation du moteur) |
| Poulie T5, 14 dents, **sans base** | 1 |

> **Note historique.** Ce coude était initialement équipé du 17HS13-0404S-PG5 (0,4 A, réduction 5:1), piloté par un TB6560 réglé sur 0,4 A. Le couple s'est révélé insuffisant et le moteur a été remplacé par le **17HS24-2104S-PG5** (2,1 A peak / ≈ 1,49 A RMS, réduction 5,18:1). Le TB6560 (3 A max) reste compatible, mais **le réglage de courant du driver doit être refait** : viser **≈ 1,5 A RMS**, pas 2,1 A. Voir [§5.3](#53-peak-vs-rms--le-piège-des-fiches-techniques).

#### Étape 1 — Câblage

Brancher le moteur au TB6560 selon le schéma générique ([§3.1](#31-principe-général)), avec la polarité `ENABLE` de [§6.2](#62-tb6560--la-subtilité-enable).

<!-- IMAGE : schéma de câblage du coude -->
<!-- Emplacement suggéré : docs/images/cablage-coude.png -->

#### Étape 2 — Construire le tendeur de courroie

**Empilez trois roulements 8 × 22 × 7 mm** et maintenez-les en place avec une **vis M4 × 20 mm et un écrou M4**.

<!-- IMAGE : tendeur de courroie, 3 roulements empilés -->
<!-- Emplacement suggéré : docs/images/tendeur-courroie.jpg -->

#### Étape 3 — Insérer l'écrou de logement du tendeur

Ajoutez l'écrou qui va permettre de positionner le tendeur dans la pièce imprimée.

#### Étape 4 — Fixer le coude à l'épaule

Fixez l'articulation du coude sur l'épaule avec **4 vis M4 × 10 mm**.

<!-- IMAGE : fixation du coude sur l'épaule, 4 vis M4 -->
<!-- Emplacement suggéré : docs/images/coude-fixation-epaule.jpg -->

#### Étape 5 — Monter le tendeur

Ajoutez le tendeur de courroie avec une **vis M3 × 40 mm**.

#### Étape 6 — Roulements de l'arbre

Ajoutez **deux roulements** qui vont permettre à la tige métallique de tourner librement.

#### Étape 7 — Fixer le moteur

Fixez le moteur sur l'articulation avec **4 vis M3 × 10 mm**.

<!-- IMAGE : moteur du coude fixé sur l'articulation -->
<!-- Emplacement suggéré : docs/images/coude-moteur.jpg -->

#### Étape 8 — Monter la poulie

Montez la **poulie T5 à 14 dents**. ⚠️ **Cette poulie ne doit pas avoir de base** — voir [§7.3](#73-poulies-personnalisées--méplat-en-d-openscad) pour la génération d'une poulie sans base.

#### Étape 9 — Courroie

Voir [§9](#9-longueurs-de-courroies) : **courroie de 89 dents** pour cette articulation.

✅ **L'articulation du coude est fixée.** Il reste à ajouter l'avant-bras.

---

### 8.3 Avant-bras et poignet 1

#### Matériel

| Élément | Quantité |
|---|---|
| Moteur 17HS13-0404S1 (NEMA 17 bipolaire, 26 N·cm, 0,4 A) | 1 |
| Driver TB6560 | 1 |
| Inserts thermofixés M3 | 6 |

#### Étape 1 — Câblage

Dans l'avant-bras se trouve le moteur qui fait tourner le **poignet 1** : un NEMA 17 bipolaire **17HS13-0404S1**. Le brancher sur la RAMPS 1.4 via un TB6560, selon le schéma générique.

<!-- IMAGE : schéma de câblage du poignet 1 -->
<!-- Emplacement suggéré : docs/images/cablage-poignet1.png -->

#### Étape 2 — Poser les inserts thermofixés

Commencez par installer **6 inserts thermofixés M3** dans la pièce imprimée de l'avant-bras.

**Méthode :** fer à souder à ~200 °C avec une panne dédiée aux inserts (ou une panne conique sacrifiée), insert posé à l'entrée du trou, pression **verticale et lente**. L'insert doit descendre en fondant le plastique, sans le repousser sur les côtés. S'arrêter dès que l'insert est **affleurant**, pas en dessous.

<!-- IMAGE : pose des inserts thermofixés M3 dans l'avant-bras -->
<!-- Emplacement suggéré : docs/images/inserts-avant-bras.jpg -->

#### Étapes suivantes

🔲 **Section à compléter** — montage mécanique de l'avant-bras sur le coude, transmission vers le poignet 1.

---

### 8.4 Base, poignet 2 et pince

🔲 **Sections à documenter.**

| Sous-ensemble | Moteur | État |
|---|---|---|
| Rotation de la base (axe `X`) | 17HS24-0644S | Monté, non documenté |
| Poignet 2 (axe `E1`) | 14HS13-0804S | Monté, non documenté |
| Pince | Servo Hitec HS-645MG | À documenter — le servo se pilote via la sortie servo de la RAMPS, pas via un driver pas-à-pas |

---

## 9. Longueurs de courroies

Le calcul de la longueur de courroie suit une règle simple, valable pour toutes les articulations :

```
Longueur de courroie (en dents) = dents en contact extérieur
                                + dents enfoncées côté gauche
                                + dents enfoncées côté droit
```

Sur ce bras, on peut enfoncer **5 dents de chaque côté** dans le logement prévu.

| Articulation | Dents en contact extérieur | Enfoncées (2 × 5) | **Courroie retenue** |
|---|---|---|---|
| **Épaule** (axe `Z`) | 80 | 10 | **90 dents** ✅ |
| **Coude** (axe `Y`) | 81 | 10 | **89 dents** ⚠️ |

> ⚠️ **Incohérence à vérifier sur le coude.** Mes notes de montage indiquent 81 dents en contact extérieur et une courroie de 89 dents. Or 81 + 5 + 5 = **91**, pas 89. Une des deux valeurs est fausse : soit le contact extérieur est de 79 dents, soit la courroie retenue est bien de 91 dents. **La courroie de 89 dents est celle qui a été montée et qui fonctionne** — la valeur à corriger est donc probablement le décompte du contact extérieur. À remesurer sur la pièce et à corriger ici.

**Découpe pratique.** Un rouleau de 5 m de courroie T5 (pas de 5 mm) contient **1000 dents**. Les deux articulations documentées en consomment 179. Il reste largement de quoi équiper les autres articulations et refaire une courroie en cas d'erreur de découpe.

---

## 10. Firmware et contrôle

### 10.1 Marlin

Le projet BCN3D MOVEO met à disposition un **firmware dérivé de Marlin**, le logiciel open source des imprimantes 3D, adapté au bras robotique.

**Pourquoi c'est le bon choix ici.** Marlin fournit gratuitement l'accélération, la gestion du microstepping, l'interpréteur G-code, les limites de course et la communication série. Réécrire tout cela pour piloter cinq axes serait un projet à part entière. On récupère une base éprouvée, et on peut se concentrer sur la mécanique.

**Conséquence pratique :** on contrôle le bras robotique **avec les mêmes outils qu'une imprimante 3D**, ce qui est parfaitement cohérent avec le matériel utilisé.

### 10.2 Pronterface et G-code

Le pilotage se fait avec **Pronterface**, en envoyant des requêtes G-code sur la liaison série.

**Séquence de test — un petit mouvement sur chaque axe :**

```gcode
G91           ; mode déplacement RELATIF (impératif : évite un mouvement vers un zéro non défini)

G1 X0.1 F300  ; base
G1 Y0.1 F300  ; coude
G1 Z0.1 F300  ; épaule

T0            ; sélection de l'outil 0
G1 E0.1 F300  ; poignet 1

T1            ; sélection de l'outil 1
G1 E0.1 F300  ; poignet 2
```

**Points à comprendre :**

| Commande | Rôle |
|---|---|
| `G91` | **Mode relatif.** Sur un bras sans homing configuré, `G90` (absolu) déclencherait un déplacement vers une origine inconnue. À mettre systématiquement en tête de séquence |
| `G1 <axe><valeur> F<vitesse>` | Déplacement linéaire. `F300` = 300 mm/min, volontairement lent pour les premiers essais |
| `T0` / `T1` | **Sélection de l'extrudeur.** Marlin ne pilote qu'un extrudeur `E` à la fois : il faut basculer avec `T0`/`T1` pour adresser `E0` puis `E1`. Sans cette bascule, les deux commandes `E` iraient au même moteur |
| Valeurs de `0.1` | Amplitude minimale. **Commencez toujours petit** : une erreur de sens de rotation ou de facteur d'échelle se rattrape sur 0,1 mm, pas sur 50 mm |

### 10.3 Script Arduino de test unitaire

Pendant le diagnostic des drivers, il est utile de **court-circuiter Marlin** pour piloter un seul moteur en direct. Cela élimine toute la couche firmware du champ des hypothèses.

```cpp
// ============================================
// Test de rotation — axe Z sur RAMPS 1.4
// Tourne en boucle : 1 tour dans un sens,
// pause, 1 tour dans l'autre sens, pause.
// ============================================

// --- Broches de l'axe Z sur RAMPS 1.4 ---
#define Z_STEP_PIN   46
#define Z_DIR_PIN    48
#define Z_ENABLE_PIN 62   // A8

// --- Réglages ---
#define STEPS_PER_REV  200    // moteur 1.8° → 200 pas/tour
#define MICROSTEPPING  16     // doit correspondre au réglage du driver (= 3200 pulses/rev)
#define VITESSE_US     5000   // délai entre pas, en MICROsecondes (5000 = lent, 500 = rapide)

long totalSteps = (long)STEPS_PER_REV * MICROSTEPPING;   // 3200 = 1 tour complet

void setup() {
  pinMode(Z_STEP_PIN,   OUTPUT);
  pinMode(Z_DIR_PIN,    OUTPUT);
  pinMode(Z_ENABLE_PIN, OUTPUT);

  digitalWrite(Z_ENABLE_PIN, LOW);   // LOW = driver activé sur RAMPS 1.4

  Serial.begin(115200);
  Serial.println("Moteur Z pret !");
}

void loop() {
  Serial.println("-> Sens horaire");
  digitalWrite(Z_DIR_PIN, HIGH);
  faireNbPas(totalSteps);

  delay(1000);

  Serial.println("<- Sens anti-horaire");
  digitalWrite(Z_DIR_PIN, LOW);
  faireNbPas(totalSteps);

  delay(1000);
}

void faireNbPas(long nbPas) {
  for (long i = 0; i < nbPas; i++) {
    digitalWrite(Z_STEP_PIN, HIGH);
    delayMicroseconds(VITESSE_US);   // ⚠️ delayMicroseconds, PAS delay
    digitalWrite(Z_STEP_PIN, LOW);
    delayMicroseconds(VITESSE_US);
  }
}
```

> ### 🐛 Le bug qui coûte une heure
>
> Dans une première version de ce script, `faireNbPas()` utilisait **`delay(5000)`** au lieu de **`delayMicroseconds(5000)`**. Résultat : le moteur attend **5 secondes entre chaque pas** au lieu de 5 millisecondes. Sur 3200 pas, un tour prendrait **4 heures et 27 minutes**.
>
> Le symptôme est trompeur : le moteur semble parfaitement immobile, l'arbre est dur (bobines alimentées), aucun message d'erreur. On cherche du côté du câblage pendant une heure alors que le code fait exactement ce qu'on lui a demandé.
>
> **Si un moteur paraît immobile, vérifiez d'abord vos unités de temporisation.**

**Correspondance entre le code et le driver.** La valeur `MICROSTEPPING` du code doit correspondre exactement au réglage physique des DIP switches :

```
MICROSTEPPING (code)  ×  STEPS_PER_REV  =  pulses/rev (driver)
        16            ×       200        =       3200
```

Si les deux ne correspondent pas, le moteur tourne — mais pas du bon nombre de tours. C'est le genre d'erreur qui ne se voit qu'une fois le bras assemblé.

---

## 11. Journal des pannes

Cette section est volontairement détaillée, y compris sur les échecs. Une documentation d'assemblage qui ne montre que ce qui a marché est de peu d'utilité à celui qui bloque.

---

### Panne #1 — Le moteur ne démarre pas (TB6560) — ✅ RÉSOLU

| | |
|---|---|
| **Symptôme** | Premier essai sur un moteur isolé avec un seul driver : rien ne se passe |
| **Contexte** | Câblage volontairement limité à un seul moteur pour réduire les risques en cas de court-circuit |
| **Cause** | Le modèle de TB6560 commandé a une logique `ENABLE` **inversée** : `LOW` pour allumer, `HIGH` pour éteindre |
| **Solution** | `EN−` → sortie `ENABLE` de la RAMPS, `EN+` → `GND` |
| **Leçon** | Sur les cartes clonées, ne présumez jamais de la polarité `ENABLE`. Testez les deux configurations avant de chercher ailleurs |

---

### Panne #2 — Couple insuffisant à l'épaule — ✅ RÉSOLU

| | |
|---|---|
| **Symptôme** | L'épaule perd des pas sous le poids du bras |
| **Cause** | Sous-dimensionnement en couple. Le moteur recommandé par le site de référence (23HS22-2804S, 1,24 N·m) est notoirement insuffisant — plusieurs témoignages de builders le confirment. Mon premier remplacement (23HS30-2804S, 2,00 N·m) ne suffisait pas non plus |
| **Solution** | Passage au **23HS45-4204S** (3,00 N·m), en tandem de deux moteurs sur l'axe `Z` |
| **Leçon** | Le couple de maintien de la fiche technique n'est **pas** le couple disponible en mouvement sous charge. Prévoyez un facteur de sécurité généreux, particulièrement sur l'articulation qui porte tout le bras |

---

### Panne #3 — Couple insuffisant au coude — ✅ RÉSOLU

| | |
|---|---|
| **Symptôme** | Le coude ne lève pas l'avant-bras |
| **Cause** | Le 17HS13-0404S-PG5 (0,4 A, réduction 5:1) ne fournit pas assez de couple |
| **Solution** | Passage au **17HS24-2104S-PG5** (2,1 A peak, réduction 5,18:1, couple en sortie 3–5 N·m) |
| **Leçon** | Un réducteur planétaire est plus efficace que l'ajout d'un second moteur : il ne rajoute ni poids ni encombrement en aval, et ne déplace donc pas la contrainte sur l'épaule |

---

### Panne #4 — Perte de pas du coude à la remontée — ✅ CAUSE IDENTIFIÉE

| | |
|---|---|
| **Symptôme** | Le moteur du coude lève bien la charge, mais **perd des pas à la remontée** (contre la gravité) en microstepping **1/8 et 1/16**. Courroie très tendue |
| **Cause identifiée** | **Deux facteurs qui se cumulent :**<br>• **Tension de courroie excessive.** Une courroie trop tendue exerce une charge radiale importante sur l'arbre de sortie du réducteur. Cela crée une friction qui est **amplifiée à travers le rapport de réduction 5,18:1** — et donc soustraite au couple utile côté moteur<br>• **Microstepping fin.** Plus le microstepping est fin, plus le couple par micro-pas est faible. C'est intrinsèque, pas un défaut de réglage |
| **Facteur aggravant** | Driver réglé sur 2,1 A en croyant qu'il s'agissait de RMS, alors que c'est du **peak** → le moteur tournait déjà en permanence proche de sa limite de crête, saturant en couple plus vite qu'attendu ([§5.3](#53-peak-vs-rms--le-piège-des-fiches-techniques)) |
| **Correctifs** | 1. **Détendre la courroie** — c'est le levier principal, et le plus simple<br>2. **Recalculer le courant du driver** pour viser ≈ 1,5 A RMS (et non 2,1 A)<br>3. Envisager un microstepping plus grossier (1/4) sur cette articulation si le problème persiste |
| **Leçon** | Une courroie tendue à fond n'est pas une courroie bien réglée. Derrière un réducteur, la friction parasite est multipliée par le rapport de réduction |

---

### Panne #5 — Les DM542T ne font tourner aucun moteur — ❌ NON RÉSOLU

La panne la plus longue et la plus frustrante du projet. Documentée intégralement, y compris son échec, parce que la **méthode de diagnostic** reste utile même sans résolution.

| | |
|---|---|
| **Symptôme** | Le moteur de l'axe `Z` tourne avec un **TB6600**, mais **jamais** avec un **DM542T** — même code, même moteur, même câblage logique. Arbre **dur** (donc bobines bien alimentées), **LED verte fixe** sur le driver (donc pas de défaut signalé) |
| **Configuration** | RAMPS 1.4 + Arduino Mega 2560, 23HS45-4204S, alimentation 24 V dédiée aux drivers, RAMPS alimentée en 12 V via convertisseur DC-DC |

#### Tout ce qui a été vérifié — et qui est correct

| Vérification | Mesure / constat |
|---|---|
| Alimentation du driver | 24 V ✅ |
| Signal `PUL` | Impulsions détectées, 2,4 V en moyenne (cohérent avec un rapport cyclique 50 %) ✅ |
| Signal `DIR` | 4,8 V ✅ |
| LED d'état | Verte fixe, aucun défaut signalé ✅ |
| Arbre moteur | Dur → bobines alimentées, le driver délivre du courant ✅ |
| `ENA` débranché | Configuration = driver activé ✅ |
| Identification des bobines | Mesurée au multimètre : Noir + Vert / Rouge + Bleu, câblées `A+` / `A−` / `B+` / `B−` ✅ |
| DIP courant | 4,2 A peak / 3,0 A RMS ✅ |
| DIP microstepping | 3200 pulses/rev ✅ |
| Code | Identique, et **fonctionne sur le TB6600** ✅ |
| **Second driver DM542T** | **Même comportement** → écarte l'hypothèse d'un exemplaire défectueux |
| Câblage en anode commune | Testé (`+5 V` sur `PUL+`/`DIR+`, signal sur `PUL−`/`DIR−`, comme sur le TB6600) → sans effet |

#### L'erreur de raisonnement, identifiée en cours de route

Une leçon de méthode qui vaut plus que la panne elle-même :

> **Toutes ces mesures sont des mesures de TENSION. Aucune ne prouve que le courant circule réellement dans l'optocoupleur d'entrée du DM542T.**
>
> Le DM542T exige **7 à 16 mA** dans son entrée optique pour déclencher (spécifié dans sa datasheet : *Logic Signal Current 7~16 mA*).
>
> Un multimètre en mode tension a une impédance d'entrée de ~10 MΩ. **Il affichera 4,8 V sur `DIR` même si absolument aucun courant ne traverse l'optocoupleur.** Tous les « 4,8 V » et « 2,4 V » relevés confirment seulement qu'**une tension est présente aux bornes** — pas que l'opto est piloté.
>
> C'est exactement le type de défaut qui passe inaperçu : tensions parfaites, opto non alimenté, driver qui ne reçoit rien → arbre dur mais aucun pas.

#### Le piège de la mesure de courant

Une mesure de courant a bien été tentée et a donné **0 mA**. **Cette lecture était fausse** : le fil de signal était resté connecté **en parallèle** du multimètre pendant le test. Le courant passait donc par le fil et contournait entièrement l'appareil.

> 💡 **Pour mesurer un courant, il faut ouvrir le circuit et insérer le multimètre en série.** En parallèle, on ne mesure rien — on lit zéro, et on tire la mauvaise conclusion. C'est une erreur classique qui a fait perdre du temps ici.

#### État actuel

**Cause racine non identifiée.** L'hypothèse la plus probable est une **incompatibilité entre la sortie de signal de la RAMPS 1.4 et les exigences d'entrée de l'optocoupleur du DM542T** — courant de commande insuffisant, la RAMPS n'étant pas conçue pour piloter des entrées optiques gourmandes.

**Pistes non explorées :**

- Mesurer réellement le courant dans l'entrée opto, **en série**, cette fois
- Intercaler un buffer / driver de ligne entre la RAMPS et le DM542T pour fournir les 7–16 mA
- Ajuster la résistance de limitation en série sur `PUL−` / `DIR−`
- Vérifier la largeur d'impulsion minimale exigée par le DM542T (il est possible que les impulsions générées soient trop courtes)

**Décision :** les TB6600 fonctionnent et font le travail. Le bras est opérationnel. Cette panne reste **ouverte et documentée** plutôt que masquée.

---

### Panne #6 — Erreurs `avrdude` à l'upload — ⚠️ CONTOURNÉ

| | |
|---|---|
| **Symptôme** | Erreurs `avrdude` lors du téléversement du firmware sur l'Arduino Mega |
| **Contournement** | Vérifier le port série sélectionné, débrancher/rebrancher l'USB, fermer Pronterface (qui garde le port ouvert) avant de compiler |
| **Note** | ⚠️ Cause racine non consignée. Section à compléter si le problème réapparaît |

---

### Panne #7 — Warping et casse en impression ABS — ⚠️ CONTOURNÉ

Voir [§7.2](#72-échecs-et-réglages) pour le détail. Résumé : ABS sans caisson correct → warping systématique ; baisser le remplissage de 40 % à 25 % réduit le warping mais fragilise la pièce, qui casse. Recollage au pistolet à colle comme mesure temporaire. **Le PETG est le choix recommandé** pour refaire ces pièces.

---

## 12. État d'avancement

### ✅ Terminé

- Reconstitution complète du schéma électrique du projet
- Nomenclature établie, achats effectués, coûts vérifiés
- Câblage et validation de tous les drivers TB6560 et TB6600
- Motorisation définitive dimensionnée et installée
- Épaule (axe `Z`) : câble en Y, inversion de bobine, montage
- Coude (axe `Y`) : câblage, tendeur, fixation, poulie
- Avant-bras : câblage du poignet 1, pose des inserts
- Poulies personnalisées à méplat en D (OpenSCAD)
- Chaîne de contrôle Marlin + Pronterface fonctionnelle
- **Bras robotique assemblé et fonctionnel**

### 🔄 En cours

- Rédaction de cette documentation
- Réglage fin de la tension de courroie du coude (panne #4)
- Séance photo du montage pour illustrer ce README

### 🔲 À faire

| Tâche | Priorité |
|---|---|
| Documenter l'assemblage de la base, du poignet 2 et de la pince | Haute |
| Confirmer l'affectation des axes `X` et `E1` ([§3.3](#33-attribution-des-axes-ramps-14)) | Haute |
| Remesurer le décompte de dents du coude ([§9](#9-longueurs-de-courroies)) | Moyenne |
| Retrouver le lien produit de l'écrou de blocage M8 | Basse |
| Basculer les références `amazon.com` vers des équivalents européens | Basse |
| Reprendre les pièces ABS défectueuses en PETG | Moyenne |
| Résoudre ou clore définitivement la panne DM542T | Basse |
| Implémenter la cinématique inverse et la planification de trajectoire | Projet suivant |

---

## 13. Structure du dépôt

```
.
├── README.md                    ← ce document
├── docs/
│   ├── images/                  ← photos de montage et schémas
│   ├── schemas/                 ← schémas de câblage (sources éditables)
│   └── datasheets/              ← fiches techniques moteurs et drivers
├── firmware/
│   ├── marlin/                  ← firmware Marlin adapté au MOVEO
│   └── tests/
│       └── moteur_Z_boucle.ino  ← script de test unitaire (§10.3)
├── cad/
│   └── poulie_meplat_D.scad     ← générateur de poulies OpenSCAD modifié (§7.3)
├── stl/                         ← pièces imprimables (héritées du dépôt amont)
└── bom/
    └── nomenclature.csv         ← nomenclature exportable (§4)
```

> 🔲 Cette arborescence est **cible** : certains répertoires restent à créer au fur et à mesure de la mise en ligne des fichiers.

---

## 14. Crédits et licences

### Chaîne de paternité

```
BCN3D Technologies — projet BCN3D-Moveo (original)
        │
        └─► Toglefritz — Bertram_Robot_Arm + tutoriel Instructables
                    │
                    └─► ce dépôt — documentation d'assemblage et adaptations
```

| Contribution | Auteur |
|---|---|
| **Conception du bras, fichiers STL, firmware Marlin adapté** | [BCN3D Technologies](https://github.com/BCN3D/BCN3D-Moveo) |
| **Variante à moteurs accessibles, tutoriel de construction** | [Toglefritz](https://github.com/Toglefritz/Bertram_Robot_Arm) — [Instructables](https://www.instructables.com/Build-a-Giant-3D-Printed-Robot-Arm/) |
| **Schémas de câblage drivers externes, nomenclature européenne vérifiée, poulies à méplat en D, documentation d'assemblage, journal de dépannage** | ce dépôt |

**Remerciements :**

- Au **FabLab** pour l'accès aux imprimantes ABS et l'accompagnement.
- Au **support technique StepperOnline**, pour avoir clarifié par email la convention peak/RMS de leurs fiches produit — une réponse qui a directement débloqué le diagnostic de deux pannes.
- Aux builders de la communauté MOVEO dont les retours d'expérience sur le sous-dimensionnement des moteurs m'ont évité une troisième commande.

### Licence

Ce dépôt hérite de la licence du projet amont. Consultez le fichier `LICENSE` du dépôt et celui de [BCN3D/BCN3D-Moveo](https://github.com/BCN3D/BCN3D-Moveo) avant toute réutilisation.

Les ajouts propres à ce fork — documentation, schémas, nomenclature, code OpenSCAD — sont publiés dans le même esprit d'ouverture. Si cette documentation vous sert, la meilleure façon de remercier est d'ouvrir une *issue* pour signaler ce qui manque ou ce qui est faux : elle a été écrite pour être corrigée.

---

> ### ⚠️ Avertissement de sécurité
>
> Ce projet fait intervenir du **230 V secteur**, une alimentation **24 V à 25 A** capable de délivrer 600 W, et des moteurs pas-à-pas au couple suffisant pour **blesser gravement une main** prise dans une articulation.
>
> - Ne travaillez jamais sur le câblage sous tension.
> - Vérifiez systématiquement la continuité des masses avant la première mise sous tension.
> - Gardez les mains **hors de l'enveloppe de travail** du bras pendant les essais de mouvement.
> - Prévoyez un **coupe-circuit accessible** avant le premier mouvement, pas après.
>
> Ce document est un journal de construction personnel, pas une notice validée. Vous êtes responsable de votre montage.
