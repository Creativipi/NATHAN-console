# Estimation du Projet — NATHAN Console v2.0

**Date :** 2026-06-07
**Session :** PMC660 (S6, E2026)

> Ce document présente l'**estimation du projet selon trois gammes de performance**, chacune
> bâtie autour d'une classe de microcontrôleur (capacité de calcul, mémoire, I/O). Il alimente
> directement les tâches `MIP-08` (comparatif MCU), `MIP-09` (budget par scénario), `MIP-10`
> (effort) et `MIP-11` (ressources).
>
> **Principe directeur :** le projet est *PC-first* et *benchmark-driven* (`C-06`, `C-07`). Le
> choix réel du MCU n'est **pas** posé ici — il sera tranché en S7 après le benchmark PC
> (`S7-T04` → `S7-T06`). Ce document **estime** l'espace des solutions pour que l'équipe entre
> dans la décision avec des ordres de grandeur quantifiés, et non pour la pré-déterminer.
>
> Voir `REQUIS.md` (R-14 à R-30), `CONTRAINTES.md` (C-13/C-14 budget), `HYPOTHESES.md`
> (H-07/H-09/H-15) et `CAHIER-DES-CHARGES.md` §6 pour les besoins de référence.

---

## 1. Méthodologie d'estimation

### 1.1 Trois gammes plutôt qu'un seul chiffre

Parce que le composant central (le MCU) n'est pas encore choisi, **toute estimation ponctuelle
serait fausse**. On estime donc le projet selon **trois gammes de performance**, du strict
minimum viable au confortable :

| Gamme | Positionnement | MCU pivot | Intention |
|-------|----------------|-----------|-----------|
| **A — Économique** | Plancher MVP, coût et BOM minimaux | RP2350 | Atteindre tout juste les requis essentiels (R-14 : ≥4 sources) |
| **B — Équilibrée** *(recommandée)* | Marge confortable / risque maîtrisé | ESP32-S3 | Tenir les requis avec réserve, portage à faible risque |
| **C — Haute performance** | Marge maximale, latence minimale | STM32H7 (± DSP) | Dépasser les requis, absorber les imprévus de portage |

> Ces gammes ne sont pas des « versions du produit » mais des **scénarios d'estimation**. Le
> game engine étant agnostique du matériel (`C-05`, `R-31`), la bascule d'une gamme à l'autre est
> un *swap d'implémentation*, pas une réécriture — ce qui rend l'estimation par scénario légitime.

### 1.2 Tolérance

Conformément à `RPC1-12`, les chiffres budgétaires portent une **tolérance de ± 10 %** ; les
chiffres d'effort, une tolérance de **± 20 %** (incertitude de portage, `H-14`). Les prix sont en
**CAD**, hors taxes, sourcés DigiKey / Mouser / Amazon / JLCPCB (`H-26`).

### 1.3 Ce qui est commun aux trois gammes

Le développement logiciel (game engine, audio PC, jeu, IDE, communauté DV) est **identique dans
les trois gammes** — il se fait sur PC avant tout portage. Seuls varient : le MCU, sa mémoire,
le système haptique, le besoin éventuel d'un DSP externe, et l'effort de portage embarqué.

### 1.4 Lexique express (pour comprendre les calculs)

Les sections suivantes manipulent quelques termes techniques. Voici leur traduction en langage
courant — c'est tout ce qu'il faut pour suivre les calculs.

| Terme | En clair | Analogie |
|-------|----------|----------|
| **MCU** (microcontrôleur) | Le « mini-ordinateur » au cœur de la manette. C'est lui qui calcule le son et lit les boutons. | Le cerveau de la console. |
| **Cœur** (*core*) | Une unité de calcul du MCU. Un MCU à 2 cœurs peut faire deux choses en même temps (ex. : un cœur pour le son, un pour le jeu). | Deux employés au lieu d'un. |
| **MHz** (mégahertz) | La vitesse du cœur : *millions de battements par seconde*. 240 MHz = 240 millions de battements/s. | Le tempo d'un métronome : plus il est rapide, plus on fait d'opérations. |
| **Hz / kHz** (hertz) | « Fois par seconde ». 44,1 kHz = 44 100 fois par seconde. | Le nombre de photos par seconde d'une vidéo. |
| **Échantillon** (*sample*) | Une « photo » instantanée du son. Le son numérique est une suite de photos très rapprochées. | Une image d'un film ; mises bout à bout, elles font le mouvement (le son). |
| **MAC** (multiplication-accumulation) | L'opération de base du traitement du son : *multiplier deux nombres, puis additionner le résultat*. | Un seul appui sur une calculatrice : « × » puis « + ». |
| **MMAC/s** | *Millions de MAC par seconde.* Sert à mesurer la **charge de calcul** (ce qu'on demande) **et** la **capacité** (ce que le MCU peut fournir). | Comparer la taille d'une montagne de calculs à la vitesse de l'ouvrier. |
| **Filtre / `taps`** | Une « recette » de N nombres appliquée au son pour le transformer. Plus de `taps` = recette plus fine = meilleure qualité, mais plus de calculs. | Une recette de cuisine : plus d'ingrédients = plat plus raffiné mais plus long à préparer. |
| **HRTF** | La « signature acoustique » de la tête et des oreilles humaines. C'est elle qui nous fait *sentir* d'où vient un son (gauche, droite, derrière). | Des empreintes digitales, mais pour la façon dont vos oreilles déforment le son. |
| **Convolution** | L'opération qui applique la signature HRTF au son. C'est elle qui « place » le son dans l'espace. | Passer une photo dans un filtre Instagram : le filtre transforme l'image. |
| **RAM** (mémoire vive, en Mo/MB) | L'espace de travail temporaire du MCU. Si les données n'y tiennent pas, il faut une mémoire externe plus lente. | La taille du plan de travail dans une cuisine. |
| **Latence** | Le délai entre une action et son effet (ex. : appuyer → entendre le son). | Le temps de réaction. |
| **DSP** | Une puce spécialisée *uniquement* dans le calcul du son, très rapide pour ça. | Un calculateur de poche dédié au son, en renfort du cerveau principal. |

---

## 2. Modèle de charge — d'où vient le besoin de calcul

**Tout le dimensionnement du projet (et donc le choix entre les trois gammes) repose sur un seul
calcul.** Cette section l'explique en entier, étape par étape. Si on comprend cette section, on
comprend pourquoi un MCU plutôt qu'un autre, et pourquoi les prix s'étagent comme ils le font.

### 2.1 Pourquoi le son spatial coûte cher à calculer

Le principe du jeu : le joueur ne voit rien, il **entend** où sont les choses. Pour qu'un bruit
semble venir de la gauche, de la droite ou de derrière, on ne peut pas juste « monter le volume à
gauche ». Il faut reproduire la façon dont **la tête et les oreilles déforment réellement le son**
selon sa provenance. Cette déformation, c'est la **HRTF** (voir lexique §1.4).

Appliquer la HRTF à un son s'appelle une **convolution** : pour *chaque* instant du son, l'ordinateur
mélange le son avec la « signature d'oreille ». Et le son numérique contient **44 100 instants par
seconde** (qualité CD, imposée par `R-23` / `C-08`). Le calcul doit donc tourner 44 100 fois par
seconde, sans jamais prendre de retard, sinon le son se coupe ou grésille (`R-14`, `R-18`).

C'est cette obligation de « suivre le son en temps réel » qui rend le MCU central — et qui décide
de tout le reste.

> **Important — ce calcul est celui de *notre* moteur, pas d'une bibliothèque.** Le projet teste
> d'abord avec des bibliothèques existantes pour aller vite, mais l'objectif est un **moteur HRTF
> maison** (voir §6.2). Les chiffres ci-dessous correspondent à cette implémentation maison, dont
> on contrôle chaque paramètre (`taps`, nombre de sources) — c'est précisément ce contrôle qui
> permet de la faire tenir sur un MCU.

### 2.2 Le calcul, étape par étape (pour 1 seul son)

Comptons combien d'opérations de base (**MAC** — une multiplication suivie d'une addition) il faut
pour spatialiser **un seul** son pendant **une seconde**. On multiplie trois nombres :

| Étape | Question | Valeur | D'où vient le chiffre |
|------:|----------|-------:|-----------------------|
| 1 | Combien d'instants de son par seconde ? | **44 100** | Qualité CD requise (`R-23`, `C-08`) |
| 2 | Combien de MAC pour appliquer le filtre à *un* instant ? | **128** | Longueur typique d'un filtre HRTF (`taps`), dataset MIT KEMAR (`§8.2`) |
| 3 | Combien d'oreilles (canaux) ? | **× 2** | Une convolution séparée pour l'oreille gauche et la droite (son binaural) |

Le calcul se lit comme une phrase :

```
Pour 1 son :  44 100 instants/s  ×  128 calculs par instant  ×  2 oreilles
            = 44 100 × 128 × 2
            = 11 289 600 MAC par seconde
            ≈ 11,3 millions de MAC/s   (on note « 11,3 MMAC/s »)
```

> **Autrement dit :** faire entendre *un seul* son comme venant d'une direction précise oblige le
> MCU à effectuer **plus de 11 millions de petits calculs chaque seconde**. C'est l'équivalent de
> 11 millions d'appuis sur une calculatrice par seconde — pour un son. Le requis `R-14` en demande
> au moins **quatre en même temps**.

### 2.3 De 1 son à plusieurs, et l'effet de la qualité

Deux leviers font varier ce coût :

- **Le nombre de sons simultanés** : on multiplie simplement. 4 sons = 4 × le coût d'un son.
- **La finesse du filtre (`taps`)** : plus de `taps` = son spatial plus crédible, mais plus de
  calculs. On reprend l'étape 2 du tableau avec 128, 256 ou 512.

| Finesse du filtre | Qualité spatiale | Coût pour **1 son** | Coût pour **4 sons** (`R-14`) | Coût pour **8 sons** |
|-------------------|------------------|---------------------:|-------------------------------:|---------------------:|
| 128 `taps` | Correcte (suffit au MVP) | 11,3 MMAC/s | **45 MMAC/s** | 90 MMAC/s |
| 256 `taps` | Bonne | 22,6 MMAC/s | 90 MMAC/s | 181 MMAC/s |
| 512 `taps` | Excellente | 45,2 MMAC/s | 181 MMAC/s | 362 MMAC/s |

> *Comment lire la case « 45 MMAC/s » :* c'est 11,3 (un son) × 4 sons. Doubler la finesse (128 → 256)
> double le coût ; doubler le nombre de sons le double aussi.
>
> **Surcharge à prévoir :** au-delà de la convolution, le MCU doit aussi choisir la bonne signature
> HRTF selon l'angle, baisser le volume des sons lointains, et mélanger tous les sons ensemble. On
> ajoute donc une marge de **+15 à 25 %** au-dessus des chiffres du tableau.

### 2.4 La mémoire : le deuxième besoin (et le vrai goulot de la gamme A)

Calculer ne suffit pas : le MCU doit **garder en mémoire de travail (RAM)** la table des signatures
HRTF (toutes les directions possibles). Cette table pèse **~1 Mo** (`H-09`, `§6.1`). En ajoutant
l'espace pour le jeu, les tampons audio et l'interpréteur de mini-jeux, le besoin total est estimé
à **~4 Mo de RAM** (`§6.1`).

> **Pourquoi c'est décisif :** un MCU a une petite RAM rapide « intégrée » et peut, parfois, utiliser
> une RAM « externe » plus grande mais **plus lente**. Si la table de 1 Mo ne tient pas dans la RAM
> intégrée, il faut la ranger dans la mémoire externe lente — ce qui ralentit *tous* les calculs du
> son. C'est exactement le problème de la gamme A (voir §2.5).

### 2.5 Ce que chaque MCU peut fournir — besoin vs capacité

Côté **besoin**, on connaît maintenant le chiffre clé : **~45 MMAC/s** pour tenir le minimum requis
(4 sons, filtre 128). Côté **capacité**, combien chaque MCU peut-il fournir ?

Un cœur à `X` MHz fait `X` millions de battements/s, et peut faire **environ 1 MAC par battement**
(parfois plus grâce à des instructions spécialisées). En pratique, le cœur ne calcule jamais à
100 % (il gère aussi les boutons, la carte SD, l'USB…). On retient donc une efficacité réaliste
d'**environ 60 %**, sur **un seul cœur dédié au son** :

| MCU | Cœur dédié au son | Calcul de la capacité | Capacité utile | RAM intégrée | Combien de sons (filtre 128) ? |
|-----|-------------------|-----------------------|---------------:|--------------|--------------------------------|
| **RP2350** | 1× @150 MHz | 150 × 60 % | ~90 MMAC/s | **520 Ko** (table 1 Mo n'y tient pas) | ~8 en théorie, mais **2–4 en réalité** (frein mémoire) |
| **ESP32-S3** | 1× @240 MHz | 240 × ~70 %* | ~150–200 MMAC/s | **8 Mo** (large) | **4–6 confortablement** |
| **STM32H7** | 1× @480 MHz | 480 × ~70 %* | ~300–400 MMAC/s | 1 Mo + externe rapide | **6–8 avec marge** |

> \* ESP32-S3 et STM32H7 disposent d'instructions « SIMD/DSP » qui font plus d'un MAC par battement
> sur le traitement du son ; on retient une efficacité un peu plus haute (~70 %). Ces chiffres sont
> des **estimations d'ordre de grandeur** (à confirmer par le benchmark réel en S7, `S7-T04`), pas
> des mesures.

**Le rapprochement besoin ↔ capacité donne directement le verdict :**

- **RP2350** : sur le papier 90 MMAC/s ÷ 11,3 ≈ 8 sons. Mais sa RAM de 520 Ko **ne peut pas
  contenir** la table HRTF de 1 Mo → on doit utiliser la mémoire externe lente, ce qui fait
  retomber le réel à **2–4 sons**. Il atteint donc le minimum `R-14` (4 sons) **tout juste**.
- **ESP32-S3** : 150–200 MMAC/s pour un besoin de 45, **et** 8 Mo de RAM → le besoin tient sans
  contorsion. C'est la gamme **confortable**.
- **STM32H7** : 300–400 MMAC/s → il pourrait monter à des filtres plus fins (256–512) ou plus de
  sons. C'est la gamme **à large marge**.

> **À retenir :** les trois MCU peuvent atteindre le minimum requis (4 sons), mais avec des marges
> très différentes. Et le facteur qui disqualifie le plus petit n'est **pas sa vitesse de calcul,
> c'est sa mémoire trop petite** pour la table HRTF.

### 2.6 Deux façons de calculer le son : séquentiel (logiciel) vs parallèle (matériel dédié)

Tout le §2 suppose que **le MCU calcule le son lui-même, en logiciel** : son processeur fait les
millions de MAC **les uns après les autres** (calcul *séquentiel*). C'est simple, mais c'est aussi
ce qui plafonne : la vitesse dépend de la fréquence du cœur (§2.5).

Il existe une **deuxième façon de faire**, qui devient possible **parce qu'on possède notre propre
moteur** : déporter le calcul du son dans un **petit circuit électronique dédié, externe au MCU**.
Ce circuit (un **FPGA** ou un **CPLD** — de la logique programmable) exécute le filtre **en
parallèle dans son câblage**, beaucoup de multiplications **en même temps** à chaque coup d'horloge,
au lieu d'une à la fois. Le MCU n'a alors plus qu'à **envoyer les données** ; il ne « calcule » plus
le son.

| | Calcul **séquentiel** (logiciel, sur le MCU) | Calcul **parallèle / matériel** (circuit dédié externe) |
|--|----------------------------------------------|----------------------------------------------------------|
| **Qui calcule** | Le processeur du MCU, opération par opération | Un FPGA/CPLD, plusieurs opérations en même temps |
| **Rôle du MCU** | Tout : il est le goulot | Juste *envoyer les échantillons* — charge quasi nulle |
| **Limite** | La fréquence du cœur (§2.5) | Le nombre de « multiplieurs » câblés dans le circuit |
| **Analogie** | Une personne qui fait 11 M de calculs à la calculatrice | 100 personnes qui calculent chacune un bout, simultanément |
| **Ce qu'on appelle ça** | Logiciel temps réel | Logique combinatoire / pipeline matériel |

> **Pourquoi c'est un atout stratégique :** si le benchmark (S7) révèle qu'**aucun MCU abordable ne
> suffit** pour la qualité visée (ex. 8 sources à filtres longs), on n'est pas bloqué. Comme on
> maîtrise l'algorithme, on peut le **graver dans un circuit dédié**. La performance ne dépend alors
> **plus** de la puissance du MCU : on peut même garder le MCU le moins cher (gamme A) et lui adjoindre
> ce module audio. **C'est le palier de repli ultime de `H-07`** — il n'existerait pas si on dépendait
> d'une bibliothèque fermée. Chiffrage et options : voir §4.2 (ligne « décharge audio matérielle »).

---

## 3. Les trois gammes en détail

### Gamme A — Économique (RP2350)

| Aspect | Estimation |
|--------|-----------|
| **Sources spatiales** | 2–4 @128 taps (R-14 tout juste atteint) |
| **Latence audio** | ~30–45 ms (R-15 < 50 ms : OK, marge faible) |
| **RAM** | **Goulot** — HRTF en PSRAM externe QSPI = pénalité de latence/débit |
| **Haptique** | 5 moteurs ERM via MOSFET (pas de driver dédié) |
| **Effort de portage** | **Élevé** : optimisation mémoire fine, possible recours à l'assembleur |
| **Risque** | Le plus haut — peu de marge si le benchmark PC révèle un besoin > estimé |
| **Atout** | MCU le moins cher (~1$), BOM minimal, meilleur coût unitaire pour la V1 vendable (`C-14`) |

> Fallbacks associés (`H-07`) : filtres 128 taps, 2–3 sources max, stéréo simple sans HRTF — ou, pour
> viser haut malgré le petit MCU, **décharge audio matérielle** (FPGA/CPLD, §2.6 / §4.2).

### Gamme B — Équilibrée *(recommandée)*

| Aspect | Estimation |
|--------|-----------|
| **Sources spatiales** | 4–6 @128–256 taps (R-14 dépassé) |
| **Latence audio** | ~20–35 ms (R-15 : OK avec marge) |
| **RAM** | 8 MB PSRAM intégrée — HRTF + buffers + MicroPython sans contorsion |
| **Haptique** | 5 moteurs ERM (MOSFET) ou LRA + DRV2605L au choix |
| **Effort de portage** | **Modéré** — USB OTG natif, ESP-IDF mûr, I2S simple |
| **Risque** | Maîtrisé — la PSRAM absorbe les surprises mémoire du benchmark |
| **Atout** | Meilleur rapport marge/coût/risque ; écosystème logiciel riche |

### Gamme C — Haute performance (STM32H7 ± DSP)

| Aspect | Estimation |
|--------|-----------|
| **Sources spatiales** | 6–8 @256–512 taps (qualité spatiale supérieure) |
| **Latence audio** | ~10–25 ms (R-15 : très large marge) |
| **RAM** | 1 MB interne rapide + SDRAM externe ; décharge audio matérielle optionnelle (§2.6 / §4.2) |
| **Haptique** | 5 moteurs LRA + DRV2605L (réponse < 100 ms garantie, `H-17`) |
| **Effort de portage** | **Modéré-élevé** — HAL STM32 plus verbeux, intégration SDRAM/DSP |
| **Risque** | Faible côté performance ; risque déplacé vers la complexité d'intégration |
| **Atout** | Marge maximale pour absorber tout imprévu HRTF temps réel |

---

## 4. Estimation budgétaire — développement et prototype (THT)

Budget plafond **500$ CAD** (`C-13`, `R-59`), réserve imprévus ~30 % incluse. Coûts en CAD.

> **Prix relevés le 2026-06-07** auprès de fournisseurs canadiens (CAD, hors taxes/port sauf
> mention). Voir §4.4 pour les sources, et l'**Annexe A** pour la description en clair de chaque
> composant.

### 4.0 Stratégie de fabrication : du build de développement (THT) à la V1 finie (CMS, prête à vendre)

Le projet vise une **V1 finie en CMS, prête à vendre** — c'est **elle qu'on remet au groupe de
testeurs DV** (S8) et qu'on démontre à l'Expo MégaGÉNIALE. Le thru-hole **n'est pas le produit** :
c'est l'**étape de développement et de validation** qui mène à cette V1. Les deux sont **dans le
périmètre du projet** (et non « plus tard / post-projet »). C'est cette distinction qui explique
l'écart de prix entre le §4 (développement/THT) et le §5 (V1 finie/CMS).

| | **Build de développement / prototype (THT)** | **V1 finie — produit livré aux testeurs (CMS)** |
|--|----------------------------------------------|--------------------------------------------------|
| **Rôle** | Valider l'électronique, déboguer, itérer | **Le produit final** remis au groupe de testeurs (`S8-T10`) + démo Expo (`S8-T07`) |
| **Technologie** | **Thru-hole (THT)** — composants « traversants » soudés à la main | **CMS / SMT** — composants « montés en surface », assemblés par machine (four à refusion) |
| **Forme du MCU** | **Carte de développement (devkit)** + breadboard, puis PCB THT soudé main | **Puce nue** soudée directement sur le PCB de la manette |
| **Pourquoi** | Rapide à monter/déboguer/itérer au labo UdeS (`C-28`) ; dé-risque avant de figer le layout CMS | Compact, robuste, esthétique produit, **coût unitaire visé < 100$** (`C-14`) → **vendable** |
| **Quand** | S6–S7 (dev) → prototype THT validé | **S8** (V1 livrée aux testeurs et démontrée à l'Expo) |
| **Chiffré au** | **§4** (cette section) | **§5** |
| **Exemple concret** | ESP32-S3 **DevKit** à 16,95$ | Puce **ESP32-S3** nue à ~5$ |

> **À retenir :** ce qui est **remis aux testeurs et montré à l'Expo est la V1 finie en CMS**, pas un
> montage thru-hole soudé à la main. Le THT sert à y arriver sans risque. **Modèle économique :** le
> budget de **~500 $ est le coût de *développement*** — il paie le matériel de dev, le prototypage
> THT **et le 1ᵉʳ exemplaire fini de la V1 en CMS** (coût non récurrent, payé une seule fois). Une
> fois ce design figé, **chaque réplique** de la V1 coûte **100–200 $/unité** (§5), et tend vers
> **< 100 $** en production de masse (`C-14`).

### 4.1 Postes communs aux trois gammes (prototype THT)

| Poste | Détail | Coût (CAD) | Source |
|-------|--------|-----------|--------|
| Entrées | 2 joysticks analogiques (2,95$ × 2) + 3 boutons arcade + 2 micro-switchs + 2 tactiles | ~24$ | PiShop.ca (joysticks) ; Amazon.ca (boutons) |
| Audio | Module DAC I2S PCM5102 + jack 3.5 mm stéréo | ~15$ | Amazon.ca / DigiKey.ca |
| Stockage | Module micro SD + carte 16 Go | ~16$ | Amazon.ca |
| Alimentation | LiPo ≥2000 mAh (~14$) + module de charge USB-C TP4056 (~3$) + LDO 3.3V + interrupteur | ~22$ | Amazon.ca / CanadaRobotix |
| Passifs / connectique | Résistances, condos, MOSFET, LED, fils, embases | ~20$ | Amazon.ca / DigiKey.ca |
| Fabrication PCB | JLCPCB 5 unités (~2$) + livraison Canada (~25$) (`C-27`) | ~30$ | JLCPCB |
| Boîtier | Filament PLA/PETG impression FDM (`C-26`) | ~12$ | — |
| Matériel de dev | 2–3 manettes USB (`TECH-03`, ~60$) + casque stéréo (~25$) | ~85$ | Amazon.ca |
| **Sous-total commun** | | **~224$** | |

### 4.2 Postes variables selon la gamme

| Poste variable | Gamme A | Gamme B | Gamme C |
|----------------|---------|---------|---------|
| MCU (devkit prototype) | RP2350 / Pico 2 **6,95$** | ESP32-S3 DevKit **16,95$** | STM32H7 : WeAct ~18$ **ou** NUCLEO-H743ZI **40,71$** |
| Mémoire externe | PSRAM QSPI ~7$ | incluse (8 MB PSRAM) | incluse (WeAct) / SDRAM ~8$ |
| Décharge audio matérielle *(option de repli, voir §2.6)* | possible | possible | possible |
| Système haptique (5 moteurs) | ERM + MOSFET ~15$ | ERM ~15$ **ou** LRA + DRV2605L | LRA + DRV2605L |
| **Sous-total variable** | **~29$** | **~32$ (ERM)** | **~26$ à 110$** selon options |

> **⚠️ Alerte coût haptique :** le driver **DRV2605L en breakout coûte 12,95$/unité** (PiShop.ca).
> En piloter 5 individuellement = **~65$**, ce qui domine le poste variable. Pour le prototype,
> deux options moins chères : **(a)** PWM via MOSFET (2N7002, < 1$/canal) — option par défaut ;
> **(b)** puces **DRV2605 nues** (~3–4$/u au lieu du breakout). Réserver les breakouts au
> bring-up/validation, pas au montage final des 5 voies.

> **Option « décharge audio matérielle » (palier de repli `H-07`, voir §2.6).** N'est ajoutée que si
> le benchmark (S7) montre que le MCU seul ne suffit pas. Deux variantes, chiffrées en CAD :
>
> | Variante | Ce que c'est | Coût dév. (carte) | Coût V1 CMS (puce) | Remarque |
> |----------|--------------|----------------|------------------------|----------|
> | **FPGA / CPLD — « moteur combinatoire maison »** | Notre algorithme HRTF gravé en logique parallèle (ex. Lattice iCE40 UP5K) | carte ~40$ (UPduino) | puce ~7–10$ | **Correspond à la vision « le nôtre »** ; toolchain open-source (yosys/nextpnr), compatible `C-25` ; effort HDL à prévoir |
> | **DSP audio tout-fait (ex. ADAU1701)** | Puce DSP du commerce, programmée par outil propriétaire | carte ~20–25$ | puce ~8–10$ | Plus rapide à intégrer mais **fonction figée** (filtres/EQ), capacité limitée, moins « maison » |
>
> *Effet sur les gammes :* cette option **découple la performance audio de la puissance du MCU** — on
> peut viser une qualité élevée **même avec la gamme A**. Coût matériel modeste (~+40$ en dév., ~+10$
> sur la V1 CMS) ; le vrai coût est l'**effort de conception logique (HDL)**, à arbitrer au choix du
> MCU (`S7-T07`) seulement si le benchmark l'impose.

### 4.3 Total développement / prototype THT par gamme

| | Gamme A | Gamme B (ERM) | Gamme C |
|--|---------|---------------|---------|
| Commun | 224$ | 224$ | 224$ |
| Variable | 29$ | 32$ | 26$ (ERM, WeAct) → 110$ (NUCLEO + 5× DRV2605L breakout) |
| **Sous-total** | **~253$** | **~256$** | **~250–334$** |
| Réserve imprévus (~30 %) | ~76$ | ~77$ | ~75–100$ |
| **Total dév./THT estimé (± 10 %)** | **~330$** | **~333$** | **~325–435$** |
| **Reste pour la V1 CMS (sur 500$)** | ~170$ | ~167$ | ~65–175$ |

> **Comment lire ce tableau (les 4 lignes de calcul) :**
> 1. *Commun* = le sous-total du §4.1 (~224 $, identique aux 3 gammes).
> 2. *Variable* = le sous-total du §4.2 (ce qui change selon le MCU et l'haptique).
> 3. *Sous-total* = commun + variable.
> 4. *Réserve imprévus* = +30 % du sous-total, exigée par `C-13` (pannes, erreurs de commande,
>    re-fabrication d'un PCB…). *Total* = sous-total + réserve. Exemple gamme A :
>    `224 + 29 = 253 $`, puis `253 × 1,30 ≈ 330 $`.
>
> **Conclusion budgétaire :** ce total ne couvre que le **développement/THT**. Il laisse ~165–170 $
> (gammes A/B) sur le plafond de 500 $ pour la **V1 finie en CMS** (§5) — ce qui suffit pour **1
> unité** mais devient serré au-delà (voir le bilan consolidé §5.2). Côté technique, le facteur
> discriminant entre gammes reste la **marge de performance vs. le risque de portage** ; le poste
> matériel le plus sensible est le **driver haptique** (breakout vs MOSFET/puce nue), pas le MCU.

---

## 4.4 Sources des prix (relevé 2026-06-07, CAD)

| Composant | Prix relevé | Fournisseur |
|-----------|-------------|-------------|
| Raspberry Pi Pico 2 (RP2350) | 6,95$ | [PiShop.ca](https://www.pishop.ca/product/raspberry-pi-pico-2/) |
| ESP32-S3 DevKit (avec headers) | 16,95$ | [PiShop.ca](https://www.pishop.ca/product/esp32-s3-microcontroller-2-4-ghz-wi-fi-development-board-w-headers/) |
| NUCLEO-H743ZI (STM32H7) | 40,71$ | [DigiKey.ca](https://www.digikey.ca/en/products/detail/stmicroelectronics/NUCLEO-H743ZI/7809236) |
| WeAct STM32H743 — *petite carte tierce bas coût intégrant la puce STM32H7, USB-C et lecteur SD (alternative économique au NUCLEO officiel de ST)* | ~18$ (incl. port) | [AliExpress](https://www.aliexpress.com/item/1005006632336183.html) |
| Joystick analogique 2 axes + bouton | 2,95$ /u | [PiShop.ca](https://www.pishop.ca/product/analog-2-axis-thumb-joystick-with-select-button/) |
| Driver haptique DRV2605L (breakout) | 12,95$ /u | [PiShop.ca](https://www.pishop.ca/product/adafruit-drv2605l-haptic-motor-controller/) |
| Module DAC I2S PCM5102 | ~10–14$ | [Amazon.ca](https://www.amazon.ca/joystick-module/s?k=PCM5102) |
| LiPo 2000 mAh 3.7V | ~12–15$ | [Amazon.ca](https://www.amazon.ca/EEMB-2000mAh-Battery-Rechargeable-Connector/dp/B08214DJLJ) |
| Module charge USB-C TP4056 | ~2–3$ /u (multipack) | [Amazon.ca](https://www.amazon.ca/Lithium-Battery-Charging-Protection-Functions/dp/B07MDPLQ18) |
| PCB 2 couches, 5 unités | ~2$ + ~25$ port Canada | [JLCPCB](https://jlcpcb.com/quote) |

> Prix sujets à variation (stock, promotions, taux de change, port). À re-valider avant l'achat
> réel (S7, après le choix du MCU) et à consigner dans le rapport de dépenses (`C-15`).

---

## 5. Coût de réplication de la V1 (copies après développement)

**Modèle économique en deux temps** (clarifié avec l'équipe) :

- **Développement (§4) → ~500 $ :** ce budget produit le **premier exemplaire fini de la V1** en CMS.
  C'est un coût *non récurrent* (NRE) : il paie le matériel de dev, le prototypage THT, la conception
  du PCB et le **1ᵉʳ montage CMS**. On ne le paie qu'une fois.
- **Réplication (cette section) → 100–200 $/unité :** une fois le design figé, **chaque copie** de la
  V1 coûte bien moins, car il n'y a plus de développement à refaire — seulement de la matière et de
  l'assemblage. Cible de l'équipe : **100–200 $/unité en petite série**, convergeant vers **< 100 $
  en production de masse** (`C-14` / `R-60`).

### 5.1 BOM matière par réplique (puces nues)

Base : prix puce du cahier (`§6.1` : RP2350 ~1$, ESP32-S3 ~5$, STM32H7 ~10$) + composants CMS.

| Gamme | BOM matière /unité | Commentaire |
|-------|--------------------|-------------|
| A | ~45–60$ | Le moins cher |
| B | ~55–75$ | Recommandée |
| C | ~80–105$ | Plus cher (décharge audio + 5 drivers LRA à arbitrer) |

### 5.2 Coût complet par réplique selon le volume

Au BOM matière s'ajoutent le **PCB** et l'**assemblage CMS**. L'assemblage a une part **fixe**
(stencil, mise en route — ~25–40$ par lot) amortie sur le nombre d'unités, et une part **par unité**.
Le **mode d'assemblage n'est pas encore tranché** ; les deux options sont chiffrées :

| Mode d'assemblage | Petite série (quelques unités) | Production de masse |
|-------------------|--------------------------------|---------------------|
| **JLCPCB PCBA (machine)** | ~120–200 $/u (frais fixes amortis sur peu d'unités) | **< 100 $/u** (frais fixes dilués, achats groupés) |
| **Soudure CMS à la main (UdeS)** | ~100–160 $/u (pas de frais fixes, mais main-d'œuvre + risque, BGA exclus) | non pertinent (ne passe pas à l'échelle) |

> **Lecture :** la cible **100–200 $/réplique** de l'équipe est **réaliste en petite série** (gammes
> A/B), quel que soit le mode d'assemblage. La cible **< 100 $** (`C-14`) est un objectif de **volume**
> : elle s'atteint en CMS automatisé avec achats groupés, surtout en gamme A/B. La gamme C n'y arrive
> que **sans décharge audio externe et en haptique MOSFET/puce nue**.
>
> **À confirmer pour préciser ces chiffres :** le **mode d'assemblage** (PCBA vs main vs hybride) et
> le **nombre de répliques** visé pour les testeurs. Le coût de la 1ʳᵉ V1 reste, lui, couvert par le
> budget de développement (§4, ~500 $).

---

## 6. Estimation de l'effort (`MIP-10`)

**Comment lire cette estimation.** L'effort se calcule en deux temps :

1. **Le plafond est imposé, pas estimé.** Le cours fixe ~135 h par tranche de 3 crédits et par
   personne (`C-17`). Sur les 3 sessions (3 + 6 + 3 crédits) cela fait **540 h par personne**, et
   avec 8 membres : **540 × 8 = 4320 h**. C'est un *budget d'heures fermé* — on ne peut pas en
   ajouter, seulement décider comment les répartir.
2. **La répartition, elle, est notre estimation.** On distribue ces 4320 h entre les 6 flux de
   travail (les colonnes du diagramme de `TACHES.md`) plus la gestion académique, au prorata de
   l'ampleur de chaque flux. Les pourcentages ci-dessous sont des jugements d'équipe à affiner au
   suivi hebdomadaire (tolérance ± 20 %, `H-14`).

> *Lecture d'une ligne :* « Flux A — 640 h, 15 % » signifie qu'on estime que le moteur de jeu
> mobilisera environ 15 % de l'effort total, soit 640 h cumulées sur les 8 personnes et 3 sessions
> (≈ 80 h par personne si une seule s'en occupait, ou ≈ 20 h chacune si réparti sur 4 personnes).

| Flux / poste | Heures estimées | Part |
|--------------|-----------------|------|
| Gestion & livrables académiques (MIP, RPC1/2, RLP, RAE, réunions, audits, tableaux de bord) | ~1030h | 24 % |
| Flux A — Game engine (ENG) | ~640h | 15 % |
| Flux B — Audio HRTF (AUD) | ~640h | 15 % |
| Flux C — Hardware (ELEC) | ~590h | 13 % |
| Flux D — Contenu de jeu (JEU) | ~550h | 13 % |
| Flux E — IDE accessible (ENG) | ~640h | 15 % |
| Flux F — Communauté DV + éthique | ~230h | 5 % |
| **Total** | **~4320h** | **100 %** |

### 6.1 Surcoût d'effort de portage selon la gamme

L'effort logiciel PC est constant ; seul le **portage embarqué** (flux B + C, surtout en S8)
varie :

| Gamme | Effort de portage relatif | Justification |
|-------|---------------------------|---------------|
| A | **+30 à +50 %** vs base | Optimisation mémoire RAM serrée, PSRAM externe, possible assembleur |
| B | **base (référence)** | USB OTG natif, ESP-IDF mûr, PSRAM généreuse |
| C | **+15 à +25 %** vs base | HAL plus verbeux, intégration SDRAM/DSP, mais large marge CPU |

> Implication planning : la gamme A est la moins chère en pièces mais la **plus chère en heures**
> de portage — un arbitrage classique capacité-matérielle vs effort-humain.

### 6.2 Trajectoire du moteur audio : bibliothèque d'amorçage → moteur maison → embarqué

**Point clé du projet :** on **démarre avec des bibliothèques existantes pour valider vite, mais
l'objectif est un moteur audio maison.** Cela se reflète dans la répartition de l'effort du Flux B
(~560 h) en trois phases. Les chiffres du §2 (charge de calcul) correspondent à la **phase 2** —
le moteur qu'on construit, pas une boîte noire.

| Phase | Quand | Ce qu'on utilise | Ce qu'on construit | Part du Flux B |
|-------|-------|------------------|--------------------|----------------|
| **1. Amorçage / preuve de concept** | S6 | Bibliothèques existantes : **miniaudio** (sortie son sur PC), datasets HRTF de référence (MIT KEMAR, CIPIC, SOFA) pour valider la perception (`H-08`) | Prototypes jetables : 1 source qui tourne au casque, tests perceptuels | ~30 % (~170 h) |
| **2. Moteur HRTF maison** | S7 | miniaudio **seulement** comme « robinet » de sortie son sur PC | **Notre convolution HRTF, notre pipeline de spatialisation** (contrôle total des `taps`, du nombre de sources, de la mémoire — c'est ce que chiffre le §2). C'est l'IP du projet. | ~40 % (~225 h) |
| **3. Portage embarqué** | S8 | **Aucune bibliothèque PC** (elles ne tournent pas sur MCU) | Sortie **I2S + DMA écrite à la main** + notre moteur HRTF porté sur le MCU | ~30 % (~165 h) |

**Pourquoi construire le nôtre (et pas se reposer sur une bibliothèque) :**

- **Performance maîtrisable** — seule une implémentation maison permet d'ajuster `taps` et nombre de
  sources pour tenir dans le budget de calcul du MCU (§2). Une bibliothèque généraliste ne se règle
  pas aussi finement.
- **Portabilité** — une bibliothèque audio PC (miniaudio) **ne fonctionne pas sur le MCU**. Le code
  embarqué doit de toute façon être écrit par l'équipe ; partir d'un moteur maison **réduit donc le
  risque de portage** plutôt que de l'augmenter. Le contrat `SpatialAudioEngine` isole déjà le moteur
  de l'implémentation (`H-10`, `C-05`).
- **Open-source sans dépendance lourde** — `C-25` / `C-30` exigent des composants libres et
  redistribuables ; un moteur maison + un dataset libre (MIT KEMAR) évite toute dépendance bloquante.
- **Échappatoire matérielle (le levier le plus important)** — maîtriser l'algorithme permet, si
  aucun MCU abordable ne suffit, de le **graver dans un circuit dédié (FPGA/CPLD)** qui calcule le
  son en parallèle pendant que le MCU se contente d'envoyer les données (voir §2.6). Cette porte de
  sortie **n'existe pas avec une bibliothèque fermée**. C'est le palier de repli ultime de `H-07`.
- **Objectif pédagogique** — le projet vise l'apprentissage et la reprise par la communauté (README) ;
  le moteur audio est au cœur de cet héritage.

> **Impact sur l'estimation :** **coût matériel = 0 $** (miniaudio est MIT, les datasets sont libres —
> déjà noté `CAHIER-DES-CHARGES.md` §10). Le « coût » du moteur maison est **en heures**, déjà inclus
> dans les ~560 h du Flux B. Le risque associé (réussir un HRTF temps réel maison) est porté par
> `H-07`, avec ses paliers de repli (filtres plus courts, moins de sources, DSP externe, stéréo
> simple).

---

## 7. Bilan de puissance et autonomie (`R-24`, `H-18`)

Cette section ne se contente pas d'estimer l'autonomie : elle la **construit à partir de la
consommation réelle de chaque composant**, tirée des fiches techniques (*datasheets*). C'est la
méthode d'un bureau d'études — chaque chiffre est traçable à sa source.

### 7.1 Méthode

L'autonomie est une division :

```
autonomie (heures) = capacité utile de la batterie (mAh) ÷ consommation moyenne du circuit (mA)
```

Deux conventions, justifiées :
- **Capacité utile = 85 %** de la capacité nominale. On n'exploite jamais 100 % d'une batterie LiPo
  (coupure de sécurité avant décharge profonde + pertes du régulateur). Sur 2000 mAh :
  `2000 × 0,85 = 1700 mAh` réellement disponibles.
- **Consommation = somme des composants**, chacun à sa valeur datasheet. Les moteurs ne vibrent que
  par à-coups : on les compte donc à leur **taux d'activité réel** (*duty cycle*) en jeu, estimé à
  ~15 % en moyenne (impulsions de bâton, chocs), et à 100 % pour le **pic** (combat, tous moteurs).

### 7.2 Consommation réelle par composant (sources datasheet)

| Composant | Courant (valeur datasheet) | Condition | Source |
|-----------|----------------------------|-----------|--------|
| **MCU — RP2350** | ~25 mA (cœur) → **~35 mA** système 3,3 V | 150 MHz actif | [Raspberry Pi RP2350 datasheet](https://datasheets.raspberrypi.com/rp2350/rp2350-datasheet.pdf) |
| **MCU — ESP32-S3** | **13–107 mA**, repère **~70 mA** | 240 MHz 2 cœurs, radio coupée (modem-sleep) | [Espressif ESP32-S3 datasheet, Table 4-9](https://documentation.espressif.com/esp32-s3_datasheet_en.pdf) |
| **MCU — STM32H743** | 275 µA/MHz × 480 = **~132 mA** (cœur) → **~175 mA** avec périphériques | 480 MHz Run mode | [ST STM32H743 datasheet (DS12110)](https://www.st.com/resource/en/datasheet/stm32h743vi.pdf) |
| **DAC — PCM5102A** | 8 mA (num.) + 22 mA (analog) = **30 mA** | 3,3 V, lecture 48 kHz | [TI PCM5102A datasheet (SLAS859A) p.6](https://www.ti.com/product/PCM5102A) |
| **Carte micro SD** | pic ~50–100 mA, **~5 mA moy.** | échantillons pré-chargés en RAM (`§6.6`) | Usage typique SPI |
| **Moteur ERM ×5** | **85 mA** nominal /u (120 mA au démarrage) | 3 V, par moteur | [Precision Microdrives / fiches ERM](https://www.precisionmicrodrives.com/eccentric-rotating-mass-vibration-motors-erms) |
| **Divers** (LDO quiescent, pull-ups) | **~5 mA** | — | Estimation |

> Les LED (`R`) ne sont pas comptées : le gameplay n'en dépend pas (`C-01`, aucun retour visuel).

### 7.3 Autonomie résultante par gamme

On additionne les composants en **usage typique** (moteurs à 15 %) : `5 × 85 mA × 15 % ≈ 64 mA` pour
l'haptique, + DAC 30 + SD 5 + divers 5, + le MCU de la gamme.

| Gamme | Détail du calcul (usage typique) | Conso. moyenne | Autonomie (1700 mAh ÷ conso.) | Cible ≥ 4 h ? |
|-------|----------------------------------|---------------:|------------------------------:|---------------|
| **A (RP2350)** | 35 (MCU) + 30 + 5 + 64 + 5 | **~139 mA** | **~12 h** | ✅ Large |
| **B (ESP32-S3)** | 70 (MCU) + 30 + 5 + 64 + 5 | **~174 mA** | **~9–10 h** | ✅ Confortable |
| **C (STM32H743)** | 175 (MCU) + 30 + 5 + 64 + 5 | **~279 mA** | **~6 h** | ✅ Suffisant |

### 7.4 Pic de courant (dimensionnement de la batterie et du régulateur)

Un bureau d'études vérifie aussi le **pire cas instantané** : les 5 moteurs à fond (5 × 85 = 425 mA,
voire 600 mA au démarrage) **plus** l'audio actif. Pic ≈ **MCU + 30 + 5 + 425 + 5** :

| Gamme | Pic de courant estimé | Implication |
|-------|----------------------:|-------------|
| A | ~500 mA | OK pour une LiPo 2000 mAh (décharge 0,25 C) |
| B | ~535 mA | OK |
| C | ~640 mA | OK ; prévoir un régulateur 3,3 V supportant ≥ 1 A |

> **Lecture :** même au pic, on reste bien sous la capacité de décharge d'une LiPo standard. Le pic
> sert surtout à **dimensionner le régulateur 3,3 V** (viser ≥ 1 A) et les pistes du PCB, pas à
> limiter l'autonomie (les pics sont brefs).
>
> **Réserve (`H-18`) :** ces chiffres reposent sur des *taux d'activité estimés* ; ils seront
> confirmés par une mesure réelle sur le prototype assemblé (S8). Si l'autonomie mesurée descend
> sous 4 h, le plan de contingence est une batterie **2500–3000 mAh** (quelques dollars de plus,
> absorbés par la réserve d'imprévus du §4) ou la mise en veille (*sleep*) entre les actions.

---

## 8. Synthèse comparative et impact sur l'estimation

| Critère | Gamme A | Gamme B *(reco.)* | Gamme C |
|---------|---------|-------------------|---------|
| Sources HRTF (R-14 ≥4) | 2–4 ⚠️ | 4–6 ✅ | 6–8 ✅✅ |
| Latence audio (R-15 <50ms) | OK serré | OK marge | OK large |
| RAM | Goulot | Confortable | Large |
| Coût développement, dév.+THT *(prix réels 2026-06-07)* | ~330$ | ~333$ | ~325–435$ |
| Coût réplique petite série (cible 100–200$) | ~100–150$ ✅ | ~110–170$ ✅ | ~150–200$ ⚠️ |
| Effort de portage | Le plus élevé | Le plus faible | Modéré |
| Autonomie (≥4h, bilan §7) | ~12 h | ~9–10 h | ~6 h |
| Risque global | Élevé | **Maîtrisé** | Faible (perf) / modéré (intégration) |

---

## 9. Risques pesant sur l'estimation

| Risque | Gamme la plus exposée | Mitigation (`HYPOTHESES.md`) |
|--------|----------------------|------------------------------|
| HRTF temps réel plus coûteux qu'estimé | A | Fallbacks H-07 : filtres courts, moins de sources, stéréo — ou **décharge audio matérielle** (FPGA/CPLD, §2.6) qui rend la performance indépendante du MCU |
| Tables HRTF > RAM disponible | A | H-09 : compression, moins de positions, PSRAM |
| Aucun MCU < 15$ ne satisfait tous les I/O | A | H-15 : puce externe (USB/PWM), accepter coût unitaire plus élevé |
| Moteurs ERM trop lents (R-16 <100ms) | A, B (ERM) | H-17 : LRA + DRV2605L (breakout 12,95$/u, ou puce nue ~3–4$/u), chiffré gamme C |
| Délai PCB > 3 semaines | toutes | H-16 : commander tôt, breadboard de repli |
| Portage > effort estimé | A | H-14 : marge temps, architecture en interfaces isole les changements |
| Moteur HRTF maison plus dur que prévu | toutes | H-07 : paliers de repli (filtres courts, moins de sources, DSP, stéréo) ; le contrat isole le moteur (§6.2) |
| Dépendance à une bibliothèque audio non portable | toutes | H-10 : la lib (miniaudio) ne sert qu'à la sortie PC ; le moteur maison + le contrat `SpatialAudioEngine` évitent tout verrou pour le portage MCU |

---

## 10. Recommandation

1. **Conserver les trois gammes ouvertes jusqu'au benchmark PC** (`S7-T04`). C'est la raison
   d'être de la stratégie PC-first (`C-06`) : ne pas choisir avant de mesurer.
2. **Hypothèse de planification : la gamme B (ESP32-S3)**, car elle offre la meilleure marge pour
   le coût et le risque les plus faibles, sans bloquer un repli vers A (économie) ou C (performance).
3. **Budgéter le développement (~500 $) comme le coût de la 1ʳᵉ V1 finie** (NRE : dev + THT + 1ᵉʳ
   montage CMS). Planifier sur l'enveloppe la plus chère (gamme C, dév.+THT ~435 $) laisse une marge
   étroite pour le 1ᵉʳ montage CMS ; retenir A ou B élargit cette marge. **Les répliques (100–200 $/u,
   §5) sont un coût distinct** du budget projet — prévoir leur financement (partenaire, `H-27`).
4. **Trancher le système haptique en priorité** — c'est désormais, prix réels à l'appui, le poste
   variable le plus sensible (DRV2605L breakout 12,95$/u × 5 ≈ 65$). Privilégier le PWM/MOSFET ou
   les puces DRV2605 nues pour le montage final (`H-17`), réserver les breakouts au bring-up.
5. **Garder le moteur audio maison comme assurance, et la décharge matérielle (FPGA/CPLD) comme
   palier de repli** (§2.6 / §4.2). Posséder l'algorithme transforme un éventuel échec « le MCU est
   trop faible » en simple décision d'architecture (déporter le calcul en logique parallèle), sans
   refonte. À n'activer que si le benchmark (S7, `S7-T07`) le justifie — coût matériel modeste, mais
   effort de conception logique (HDL) à provisionner si on s'y engage.

> L'estimation finale, chiffrée et arbitrée, sera produite dans le **rapport de justification du
> choix du MCU** (`S7-T06`) et reportée au budget prévisionnel du RPC1 (`RPC1-12`).

---

## Annexe A — Nomenclature et description des composants

Cette annexe décrit **chaque pièce en langage clair** : à quoi elle sert, sa forme au stade de
**développement** (thru-hole, soudable à la main) et sa forme dans la **V1 finie** (CMS, montée par
machine, prête à vendre). C'est la référence pour lire le BOM (`BOM/Bill-of-materials.md`) et les
tableaux de coût (§4 développement, §5 V1) et de consommation (§7).

### A.1 Cerveau et mémoire

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **Microcontrôleur (MCU)** | Le « mini-ordinateur » qui fait tout tourner : calcule le son spatial, lit les boutons, gère l'USB. C'est lui qu'on choisit parmi 3 gammes. | Carte de développement (*devkit*) à broches | Puce nue soudée sur le PCB |
| → **RP2350** | MCU le moins cher (celui du Raspberry Pi Pico 2). Rapide, mais peu de mémoire interne → gamme économique. | Carte Pico 2 (6,95$) | Puce RP2350 (~1$) |
| → **ESP32-S3** | MCU avec **8 Mo de mémoire intégrée** et instructions audio rapides → gamme équilibrée recommandée. | DevKit ESP32-S3 (16,95$) | Puce ESP32-S3 (~5$) |
| → **STM32H743** | MCU le plus rapide (480 MHz) → gamme haute performance. Plus complexe à mettre en œuvre. | Carte WeAct (~18$) ou NUCLEO (40,71$) | Puce STM32H743 (~10$) |
| **PSRAM externe** | Mémoire de travail supplémentaire, ajoutée quand le MCU n'en a pas assez (cas du RP2350) pour loger les tables HRTF. | Puce sur petit module | Puce CMS sur le PCB |

### A.2 Audio

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **DAC PCM5102A** | *Convertisseur numérique→analogique* : transforme le son calculé par le MCU en signal électrique qu'un casque peut jouer. Qualité hi-fi (SNR 112 dB). | Module tout-fait à broches | Puce CMS + composants autour |
| **Jack 3.5 mm** | La prise où l'on branche le casque. | Connecteur traversant soudé | Connecteur CMS |
| **Casque stéréo** | Indispensable : le son binaural (3D) ne fonctionne qu'au casque, jamais sur haut-parleur (`C-02`). | Casque du commerce (accessoire) | Idem (non intégré) |
| **FPGA / CPLD** *(option de repli, §2.6)* | Circuit de logique programmable où l'on **grave notre algorithme HRTF** : il calcule le son en parallèle, le MCU n'envoie que les données. Rend la performance indépendante du MCU. | Carte type UPduino (~40$) | Puce CMS (~7–10$) |
| **DSP audio tout-fait** *(alternative)* | Puce du commerce (ex. ADAU1701) dédiée au son, mais à fonction figée (filtres/EQ) et programmée par outil propriétaire — moins « maison » que le FPGA. | Module (~20–25$) | Puce CMS (~8–10$) |

### A.3 Commandes (entrées du joueur)

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **Joystick analogique** | Les deux « manches » pour se déplacer et viser. Donnent une position précise (pas juste 8 directions). | Module à broches (2,95$/u) | Joystick CMS soudé |
| **Boutons arcade 30 mm** | Gros boutons d'action (A, B, C), facilement repérables au toucher (`C-03`). | Boutons traversants câblés | Idem (mécaniques, restent gros) |
| **Micro-switchs / boutons tactiles** | Petites gâchettes (L1, R1) et boutons système (Start, Select). | Traversants | CMS |

### A.4 Retour haptique (vibrations)

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **Moteur ERM ×5** | 5 petits moteurs à *masse excentrée* (comme la vibration d'un téléphone) disposés en arc pour indiquer une direction. Solution simple et économique. | Moteurs câblés | Idem (pièce mécanique) |
| **Moteur LRA** *(option)* | Moteur à *résonance linéaire* : vibration plus nette et **plus rapide à réagir** que l'ERM (meilleur respect du `R-16`). | Câblé | Idem |
| **Driver DRV2605L** *(option, avec LRA)* | Puce de pilotage qui génère des effets de vibration propres et réactifs pour un moteur. **Coûteuse en breakout (12,95$)** → privilégier la puce nue ou le MOSFET. | Module breakout | Puce CMS |
| **MOSFET** | Petit interrupteur électronique commandé par le MCU pour faire vibrer un moteur en dosant l'intensité (PWM). Solution la moins chère. | Boîtier traversant | Boîtier CMS minuscule |

### A.5 Stockage et alimentation

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **Carte micro SD + lecteur** | Mémoire amovible qui contient les **sons et les mini-jeux** (`C-12`). Permet de mettre à jour le contenu sans reprogrammer la console. | Module lecteur à broches | Connecteur SD CMS |
| **Batterie LiPo** | La pile rechargeable qui alimente la manette (`R-24`). Capacité en mAh = autonomie (§7). | Pack avec fils | Idem (cellule) |
| **Module de charge USB-C (TP4056)** | Le circuit qui recharge la batterie en toute sécurité quand on branche un câble USB-C. | Petit module à broches | Puce CMS + composants |
| **Régulateur LDO 3,3 V** | Abaisse et stabilise la tension de la batterie (3,7 V) vers les 3,3 V dont l'électronique a besoin. | Boîtier traversant | Boîtier CMS |

### A.6 Circuit et développement

| Composant | À quoi ça sert (en clair) | Forme dév. (THT) | Forme V1 finie (CMS) |
|-----------|---------------------------|------------------------|------------------------|
| **PCB (circuit imprimé)** | La carte verte sur laquelle tout est soudé et relié. Fabriquée en externe (JLCPCB, `C-27`). | Trous pour composants traversants | Pastilles pour composants CMS |
| **Manette USB (Xbox/PS4)** | Sert **uniquement pendant le développement sur PC** : remplace la vraie manette tant que le matériel n'existe pas (`TECH-03`, `H-13`). | Accessoire du commerce | Non concernée (outil de dev) |

> **En résumé :** pendant le **développement**, presque tout est un **module ou un devkit à broches,
> soudable à la main** (§4) ; dans la **V1 finie remise aux testeurs**, ces modules sont remplacés
> par les **puces nues équivalentes en CMS** (§5), ce qui rend le produit compact, robuste et
> vendable (< 100$/unité, `C-14`) sans changer la fonction.

---

*Document vivant — à mettre à jour après le benchmark PC (S7) et à chaque révision du BOM ou des prix.*
