# Paperasse 974 — Fork Gigarun

Fork de [romainsimon/paperasse](https://github.com/romainsimon/paperasse) adapté pour les entreprises de **La Réunion (DOM 974)**.

---

## Apports par rapport à l'original

### 1. TVA 8,5% par défaut — `comptable/SKILL.md`

Le skill comptable applique le taux DOM **8,5%** (au lieu de 20%) par défaut sur tous les dossiers, sans configuration supplémentaire dans `company.json`.

Bascule vers le régime métropole uniquement si `company.json` indique explicitement `"departement": "metropole"`.

Taux DOM en vigueur à La Réunion :
| Taux | Application |
|------|------------|
| 8,5% | Taux normal |
| 2,1% | Taux réduit |

### 2. ZFANG — Zone Franche d'Activité Nouvelle Génération — `comptable/references/regional.md`

La fiche ZFA de l'original (dispositif éteint depuis 2019) est remplacée par une fiche ZFANG complète, source BOFiP **BOI-BIC-CHAMP-80-10-85** (consulté le 2026-05-08).

**Ce que couvre la fiche :**
- Base légale : art. 44 quaterdecies CGI + art. 1466 F CGI
- Régime standard : abattement IS/IR **50%**, plafond 150 000 €/an
- Régime majoré (secteurs prioritaires) : abattement **80%**, plafond 300 000 €/an
- Secteurs prioritaires éligibles au 80% : R&D, TIC, tourisme, agro-nutrition, environnement/ENR, BTP, réparation navale
- Secteurs exclus : BNC, finance, négoce pur, jeux d'argent
- Conditions : effectif < 250 salariés, CA < 50 M€, régime réel
- CFE/CVAE/Taxe foncière : exonérations sur délibération collectivité
- Cumuls autorisés et incompatibilités légales (art. 44 sexies, terdecies, 73 B CGI…)
- Formulaire déclaratif : **2082-SD (CERFA 14043)**
- Exemple de calcul IS avec abattement
- Durée du dispositif : jusqu'au 31 décembre 2030

### 3. Règles DOM intégrées au workflow comptable — `comptable/SKILL.md`

Tableau de référence rapide ajouté directement dans le SKILL.md :
- Octroi de mer (compte 6353)
- Abattement IS 50% (plafond 150 000 €/an, secteurs éligibles)
- Réduction LODEOM charges patronales
- Règles facturation DOM ↔ Métropole (exonération TVA sur exportation)

---

## Mise à jour depuis l'upstream

```bash
git remote add upstream https://github.com/romainsimon/paperasse.git
git fetch upstream
git merge upstream/master
# Résoudre les conflits éventuels sur comptable/SKILL.md et comptable/references/regional.md
```

Après chaque merge upstream, synchroniser les skills locaux (voir ci-dessous).

---

## Sync des skills locaux

Le script `_paperasse974-push/sync.ps1` copie les `SKILL.md` et `references/` du repo vers `~/.claude/skills/` (Exocortex), en UTF-8 sans BOM + LF.

```powershell
# Aperçu des changements
.\\_paperasse974-push\\sync.ps1 -DryRun

# Appliquer
.\\_paperasse974-push\\sync.ps1
```

**Ce qui est synchronisé :** `SKILL.md` + `references/` de chaque skill (comptable, fiscaliste, notaire, controleur-fiscal, commissaire-aux-comptes, syndic).

**Ce qui est ignoré :** `evals/`, `scripts/`, `templates/`, `data/` — fichiers repo uniquement, non lus au runtime par Claude Code.

---

## Maintenu par

[Gigarun](https://gigarun.re) — Infogérance IT à La Réunion
