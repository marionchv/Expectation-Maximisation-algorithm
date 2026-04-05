# Expectation - Maximisation algorithm

L'objectif de l'algorithme EM est de maximiser le log-likelihood  
$$
L_{(x_i)_i}\left(\pi,\theta\right) = \log\big(p((x_i)_i \mid \pi, \theta)\big)
$$

$$
X_i \mid Z_{ij} = 1 \sim \mathcal{N}(\mu_j,\Sigma_j)
$$

On écrit d'abord la décomposition variationnelle du log-likelihood :  
$$
L_{(x_i)_i}\left(\alpha,\theta\right) = \mathcal{L}\left(R((z_i)_i) ; \alpha, \theta\right) + KL\left(R((z_i)_i) \,\|\, p((z_i)_i \mid (x_i)_i,\alpha, \theta) \right)
$$

Avec  
$$
\mathcal{L}\left(R((z_i)_i) ; \alpha, \theta\right) = \sum_{(z_i)_i} R((z_i)_i) \log \frac{p((z_i)_i, (x_i)_i \mid \alpha, \theta)}{R((z_i)_i)}
$$

, $KL$ la divergence de kullback-leibler et $R$ une loi quelconque sur tous les $z_i$.

## Etape E :

On se place à $(\alpha,\theta)$ fixés et on cherche à maximiser  
$$
\mathcal{L}\left(R((z_i)_i) ; \alpha, \theta\right)
$$  
par rapport à $R$.

$$
L_{(x_i)_i}\left(\alpha,\theta\right)
$$
ne dépend pas de $R$. Ainsi, $\mathcal{L}$ est maximum lorsque $KL$ est minimal, cad lorsque  
$$
KL\left(R((z_i)_i) \,\|\, p((z_i)_i \mid (x_i)_i,\alpha, \theta) \right) = 0
$$

On obtient donc :  
$$
R((z_i)_i) = p((z_i)_i \mid (x_i)_i,\alpha, \theta) = \prod_{i=1}^n p(z_i \mid x_i,\alpha, \theta)
$$

En utilisant le théorème de Bayes on a :  
$$
p(z_i \mid x_i,\alpha, \theta) = \prod_{j=1}^M \tau_{ij}^{z_{ij}}
$$

with  
$$
\tau_{ij} = \frac{\alpha_j \mathcal{N}(x_i;\mu_j,\Sigma_j)}{\sum_{l=1}^M \alpha_l \mathcal{N}(x_i;\mu_l,\Sigma_l)}
$$

$\rightarrow$ **$p(z_i \mid x_i,\alpha, \theta)$ ne dépend que des $\tau_{ij}$ donc l'étape E consistera à calculer les $\tau_{ij}$.**

## Etape M :

On se place à  
$$
R((z_i)_i)
$$  
fixé et on souhaite maximiser  
$$
\mathcal{L}\left(R((z_i)_i) ; \alpha, \theta\right)
$$  
par rapport à $(\alpha,\theta)$.

On a :  
$$
\mathcal{L}\left(R((z_i)_i) ; \alpha, \theta\right) = \mathbb{E}_{(z_i)_i}\left[\log\big(p((z_i)_i, (x_i)_i \mid \alpha, \theta)\big)\right] + \text{cte}
$$

On va donc chercher à maximiser :  
$$
\mathbb{E}_{(z_i)_i}\left[\log\big(p((z_i)_i, (x_i)_i \mid \alpha, \theta)\big)\right] = \sum_{i=1}^n \sum_{j=1}^M \tau_{ij} \log\big(\alpha_j \mathcal{N}(x_i;\mu_j,\Sigma_j)\big)
$$

par rapport à $(\alpha,\theta)$.

$\rightarrow$ **L'étape M consiste à calculer les paramètres $\hat{\alpha}_j$, $\hat{\mu}_j$ et $\hat{\Sigma}_j$ qui maximisent cette espérance.**
