# edpr

Package R qui résout numériquement des équations aux dérivées partielles
paraboliques (diffusion) en deux dimensions d'espace et en temps, par
différences finies. Il valide le résultat face à une solution exacte et le
représente graphiquement.

Application fournie : la diffusion d'un polluant, avec le cas du lac Nyos.

## Installation

# install.packages("devtools")
devtools::install_github("TON_PSEUDO/edpr")
## Équation résolue

∂C/∂t = D (∂²C/∂x² + ∂²C/∂y²)

## Utilisation

library(edpr)

# 1. Décrire le problème
p <- edp_probleme(
  D = 0.1,
  domaine = list(x = c(-10, 10), y = c(-10, 10), t = c(0, 20)),
  u0 = function(x, y) exp(-(x^2 + y^2) / 0.5),
  bords = "neumann"
)

# 2. Résoudre
sol <- edp_resoudre(p, n = 101)

# 3. Dessiner
edp_tracer(sol, t = c(0, 5, 20))
| Fonction | Rôle |
|---|---|
| edp_probleme() | décrire le problème (D, domaine, condition initiale, bords) |
| edp_resoudre() | résoudre par différences finies |
| edp_valider() | comparer à une solution exacte |
| edp_tracer() | cartes à plusieurs instants |

## Limites actuelles

- Diffusion pure : pas encore de vent ni de relief.
- Condition aux bords : « rien ne sort » (Neumann) uniquement.

## Licence

MIT
