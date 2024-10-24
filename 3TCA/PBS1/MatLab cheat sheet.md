# MatLab Cheat Sheet

## Formules de probabilité
- Probabilité: $P(A) = \frac{Nombre\ d'issues\ favorables}{Nombre\ d'issues\ possibles}$
- Probabilité conditionnelle: $P(A|B) = \frac{P(A \cap B)}{P(B)}$
- Indépendance: $P(A \cap B) = P(A) \cdot P(B)$


## Fonctions de base

- Moyenne d'une série de données: `mean(data)` $M = \frac{1}{n} \sum_{i=1}^{n} x_i$
- Variance d'une série de données: `var(data)` $V = \sigma^2 = \frac{1}{n} \sum_{i=1}^{n} (x_i - M)^2$
- Ecart-type d'une série de données: `std(data)` $\sigma = \sqrt{V}$

## Lois de probabilité
### Loi normale
- Fonction de densité de probabilité $p_X(x) = P(X = x)$ : `normpdf(x, mu, sigma)` 
- Fonction de répartition $F_X(x) = P(X \leq x)$ : `normcdf(x, mu, sigma)`
- Fonction de quantile $Q_X(x) = P(X \geq x)$ : `1 - normcdf(p, mu, sigma)`

### Loi exponentielle
- Fonction de densité de probabilité $p_X(x) = P(X = x)$ : `exppdf(x, lambda)`
- Fonction de répartition $F_X(x) = P(X \leq x)$ : `expcdf(x, lambda)`
- Fonction de quantile $Q_X(x) = P(X \geq x)$ : `1 - expcdf(p, lambda)`

### Loi de Poisson
- Fonction de masse de probabilité $p_X(x) = P(X = x)$ : `poisspdf(x, lambda)`
- Fonction de répartition $F_X(x) = P(X \leq x)$ : `poisscdf(x, lambda)`
- Fonction de quantile $Q_X(x) = P(X \geq x)$ : `1 - poisscdf(p, lambda)`

### Loi binomiale
- Fonction de masse de probabilité $p_X(x) = P(X = x)$ : `binopdf(x, n, p)`
- Fonction de répartition $F_X(x) = P(X \leq x)$ : `binocdf(x, n, p)`
- Fonction de quantile $Q_X(x) = P(X \geq x)$ : `1 - binocdf(p, n, p)`

## Aproximation par la loi normale
### Loi de Poisson
- Approximation de la loi de Poisson par une loi normale : $X \sim \mathcal{P}(\lambda) \approx \mathcal{N}(\lambda, \sqrt{\lambda})$
- Approximation de la loi binomiale par une loi normale : $X \sim \mathcal{B}(n, p) \approx \mathcal{N}(np, \sqrt{np(1-p)})$


## Cas particuliers

$p_{X|X\geq A}(Y) = \frac{p_X(Y)}{1-F_X(A)} \Longleftrightarrow$ `pxy = normcdf(Y, mu, sigma) / (1 - normpdf(A, mu, sigma)`





