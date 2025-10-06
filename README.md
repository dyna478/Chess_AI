# ChessAR - Moteurs d'Échecs avec IA Avancée

## 📋 Description

ChessAR est un projet de recherche comparant deux approches algorithmiques majeures pour les échecs : **Alpha-Beta Pruning (ABP)** et **Monte Carlo Tree Search (MCTS)**. Ce projet implémente ces deux algorithmes avec des optimisations avancées et fournit un framework de test complet pour évaluer leurs performances.

## 🎯 Objectifs du Projet

- Implémenter un moteur d'échecs utilisant l'algorithme Alpha-Beta avec élagage
- Implémenter un moteur d'échecs basé sur Monte Carlo Tree Search
- Comparer les performances des deux approches dans différentes conditions
- Reproduire et valider les résultats de recherche en intelligence artificielle appliquée aux jeux

## 🔧 Technologies Utilisées

- **Python 3.12+**
- **python-chess** : Bibliothèque pour la gestion des règles d'échecs
- **NumPy** : Calculs numériques
- **Matplotlib & Seaborn** : Visualisation des résultats
- **Pandas** : Analyse de données

## 🧠 Algorithmes Implémentés

### 1. Alpha-Beta Pruning (ABP)

Algorithme de recherche minimax optimisé avec :
- **Élagage Alpha-Beta** : Réduit l'espace de recherche
- **Tables de transposition** : Mémorise les positions déjà évaluées
- **Ordonnancement des coups** : MVV-LVA (Most Valuable Victim - Least Valuable Attacker)
- **Killer moves** : Mémorise les coups qui causent des coupures
- **Heuristique historique** : Améliore l'ordonnancement
- **Recherche de quiescence** : Évite l'effet d'horizon

**Fonctionnalités clés :**
- Profondeur de recherche configurable (par défaut : 5)
- Évaluation positionnelle avec piece-square tables
- Bonus de mobilité pour les pièces actives

### 2. Monte Carlo Tree Search (MCTS)

Algorithme de recherche par simulation avec :
- **Sélection UCB1** : Équilibre exploration/exploitation
- **Expansion intelligente** : Ajoute progressivement des nœuds
- **Politique de rollout** : Inspirée par Alpha-Beta pour positions non-volatiles
- **Rétropropagation** : Met à jour les statistiques de l'arbre

**Phases MCTS :**
1. **Sélection** : Parcourt l'arbre avec UCB1
2. **Expansion** : Ajoute un nouveau nœud
3. **Simulation** : Joue jusqu'à une position finale
4. **Rétropropagation** : Remonte les résultats

## 📊 Framework de Test

Le projet inclut un système complet de tests pour comparer les algorithmes :

### Tests Implémentés

1. **Test de biais d'exploration MCTS**
   - Compare différentes valeurs de constante d'exploration (C = 0.5, 1.0, 1.4, 2.0, 2.8)
   - 50 parties par configuration

2. **Test de temps de réflexion**
   - Évalue la performance à différents temps (0.1s, 0.25s, 0.5s, 1.0s, 2.0s)
   - 100 parties par configuration

3. **Test de temps asymétrique**
   - MCTS avec plus de temps vs ABP avec temps fixe
   - Identifie le temps nécessaire pour égaler/dépasser ABP

4. **Test de complexité d'évaluation**
   - Compare 3 niveaux : BASIC, MEDIUM, ADVANCED
   - 250 parties par niveau

5. **Tournoi tête-à-tête**
   - Configuration optimale pour chaque algorithme
   - 250 parties avec positions variées

### Fonctions d'Évaluation

#### BASIC
- Compte matériel uniquement
- Valeurs standard des pièces

#### MEDIUM
- Compte matériel + évaluation positionnelle
- Piece-Square Tables (PST)
- Score de mobilité : Sm = 10√n

#### ADVANCED
- Toutes les fonctionnalités MEDIUM +
- Pénalité pour roque non effectué
- Assistance finale de partie (roi vers coins)
- Évaluation pondérée selon phase de jeu

## 📈 Résultats et Visualisations

Le framework génère automatiquement :
- Fichiers JSON avec statistiques détaillées
- Fichiers CSV pour analyse
- Graphiques de performance :
  - Taux de victoire par type de test
  - Performance vs temps de réflexion
  - Comparaison par complexité d'évaluation
  - Distribution de la longueur des parties

## 🚀 Installation

```bash
# Cloner le repository
git clone https://github.com/votre-username/ChessAR.git
cd ChessAR

# Installer les dépendances
pip install python-chess numpy matplotlib seaborn pandas
```

## 💻 Utilisation

### Mode Interactif

```python
# Jouer contre l'IA (ABP)
from chess_engine import play_game
play_game()

# Commandes disponibles :
# - move e2e4 : Jouer un coup
# - depth X : Changer la profondeur de recherche
# - quit : Quitter
# - show : Afficher la position FEN
```

### Tests Automatisés

```python
# Test rapide (démo)
python testing_framework.py demo

# Analyse rapide
python testing_framework.py quick

# Réplication complète de la recherche
python testing_framework.py full

# Matchup personnalisé
python testing_framework.py custom
```

## 📁 Structure du Projet

```
ChessAR/
│
├── ChessAR.ipynb                 # Notebook Jupyter principal
├── testing_framework.py          # Framework de tests complet
├── tournament_results/           # Résultats des tournois
│   ├── exploration_bias_results.json
│   ├── think_time_results.json
│   ├── comprehensive_report.json
│   └── analysis_plots.png
└── starting_positions.txt        # 500 positions de départ
```

## 🔬 Méthodologie de Recherche

Le projet suit une méthodologie scientifique rigoureuse :

1. **Positions de départ variées** : 500 positions générées aléatoirement
2. **Matchs bicolores** : Chaque position jouée 2 fois (blanc/noir)
3. **Réplication** : Multiples parties pour significativité statistique
4. **Conditions contrôlées** : Paramètres identiques sauf variable testée

## 📊 Statistiques Collectées

Pour chaque partie :
- Résultat (victoire/défaite/nulle)
- Nombre de coups
- Temps total
- Nœuds explorés (ABP) ou itérations (MCTS)
- Raison de terminaison
- Statistiques par moteur

## 🎓 Concepts Théoriques

### Alpha-Beta Pruning
- Complexité : O(b^(d/2)) au meilleur cas vs O(b^d) pour minimax
- Efficacité dépend de l'ordonnancement des coups
- Déterministe et reproductible

### MCTS
- Asymptotiquement optimal
- Équilibre exploration/exploitation via UCB1
- Non-déterministe (dépend des simulations)
- Meilleur pour grands espaces de recherche

## 🔍 Observations Clés

1. **ABP** excelle avec :
   - Temps de calcul courts
   - Positions tactiques nettes
   - Profondeur de recherche importante

2. **MCTS** performe mieux avec :
   - Plus de temps de réflexion
   - Positions complexes et ouvertes
   - Évaluation simple mais simulations nombreuses

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à :
- Ouvrir des issues pour bugs ou suggestions
- Proposer des pull requests
- Améliorer la documentation
- Ajouter de nouveaux tests

## 📝 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 📚 Références

- Shannon, C. E. (1950). "Programming a Computer for Playing Chess"
- Knuth, D. E., & Moore, R. W. (1975). "An Analysis of Alpha-Beta Pruning"
- Kocsis, L., & Szepesvári, C. (2006). "Bandit Based Monte-Carlo Planning"
- Browne et al. (2012). "A Survey of Monte Carlo Tree Search Methods"

## 👨‍💻 Auteur

Développé dans le cadre d'un projet de recherche en intelligence artificielle appliquée aux jeux.

## 📧 Contact

Pour questions ou collaborations : [votre-email@example.com]

---

⭐ **Si ce projet vous intéresse, n'oubliez pas de lui donner une étoile !**
