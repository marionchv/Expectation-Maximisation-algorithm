# Expectation - Maximisation algorithm

L'objectif de l'algorithme EM est de maximiser le log-likelihood  

$L_{(x_i)_i}(\pi,\theta) = \log\big(p((x_i)_i \mid \pi, \theta)\big)$

$X_i \mid Z_{ij} = 1 \sim \mathcal{N}(\mu_j,\Sigma_j)$

On écrit d'abord la décomposition variationnelle du log-likelihood :

$L_{(x_i)_i}(\alpha,\theta) = \mathcal{L}(R((z_i)_i);\alpha,\theta) + KL\big(R((z_i)_i)\,\|\,p((z_i)_i \mid (x_i)_i,\alpha,\theta)\big)$

Avec  

$\mathcal{L}(R((z_i)_i);\alpha,\theta) = \sum_{(z_i)_i} R((z_i)_i)\,\log\left(\frac{p((z_i)_i,(x_i)_i \mid \alpha,\theta)}{R((z_i)_i)}\right)$

, $KL$ la divergence de kullback-leibler et $R$ une loi quelconque sur tous les $z_i$.

## Etape E :

On se place à $(\alpha,\theta)$ fixés et on cherche à maximiser  
$\mathcal{L}(R((z_i)_i);\alpha,\theta)$  
par rapport à $R$.

$L_{(x_i)_i}(\alpha,\theta)$ ne dépend pas de $R$. Ainsi, $\mathcal{L}$ est maximum lorsque $KL$ est minimal, c.-à-d. lorsque  

$KL\big(R((z_i)_i)\,\|\,p((z_i)_i \mid (x_i)_i,\alpha,\theta)\big) = 0$

On obtient donc :  

$R((z_i)_i) = p((z_i)_i \mid (x_i)_i,\alpha,\theta) = \prod_{i=1}^n p(z_i \mid x_i,\alpha,\theta)$

En utilisant le théorème de Bayes on a :  

$p(z_i \mid x_i,\alpha,\theta) = \prod_{j=1}^M \tau_{ij}^{z_{ij}}$

avec  

$\tau_{ij} = \frac{\alpha_j\,\mathcal{N}(x_i;\mu_j,\Sigma_j)}{\sum_{l=1}^M \alpha_l\,\mathcal{N}(x_i;\mu_l,\Sigma_l)}$

→ **$p(z_i \mid x_i,\alpha,\theta)$ ne dépend que des $\tau_{ij}$ donc l'étape E consiste à calculer les $\tau_{ij}$.**

## Etape M :

On se place à $R((z_i)_i)$ fixé et on souhaite maximiser  
$\mathcal{L}(R((z_i)_i);\alpha,\theta)$  
par rapport à $(\alpha,\theta)$.

On a :  

$\mathcal{L}(R((z_i)_i);\alpha,\theta) = \mathbb{E}_{(z_i)_i}\big[\log\big(p((z_i)_i,(x_i)_i \mid \alpha,\theta)\big)\big] + \text{cte}$

On va donc chercher à maximiser :  

$\mathbb{E}_{(z_i)_i}\big[\log\big(p((z_i)_i,(x_i)_i \mid \alpha,\theta)\big)\big] = \sum_{i=1}^n \sum_{j=1}^M \tau_{ij}\,\log\big(\alpha_j\,\mathcal{N}(x_i;\mu_j,\Sigma_j)\big)$

par rapport à $(\alpha,\theta)$.

→ **L'étape M consiste à calculer les paramètres $\hat{\alpha}_j$, $\hat{\mu}_j$ et $\hat{\Sigma}_j$ qui maximisent cette espérance.**
