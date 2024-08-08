# Jump Diffusion Model for Option Pricing

## Dynamics 
In this model, the option price follows a stochastic process which includes the typical Brownian diffusion process in addition to discrete jumps following a compound Poisson Process. From the reference paper, the price $S(t)$ can be modeled with the following dynamics 

$$\frac{dS(t)}{S(t^-)} = \mu dt + \sigma dW(t) + d(\sum_{i=1}^{N(t)} (V_i - 1))$$

* $\mu$ - Drift Rate
* $\sigma$ - Volatility
* $W(t)$ - Wiener Process 
* $N(t)$ - Poisson process of intensity λ
* $V_i$ - i.i.d. random variables representing jump size (Compound Poisson Process)

## Jumps
The jumps occur according to a poisson process $N(t)$ where $\lambda$ is the expected number of jumps per unit time. The model uses a log-normal distribution for the size of the jumps.
We adjust the voltatiliy and drift for each jump, $k$. 
* Adjusted Volatility: $\sigma_k = \sqrt{\sigma^2 + k \frac{\sigma_J^2}{T}}$
* Adjusted Drift: $r_k = r - \lambda k + \frac{k \log{(1+\mu_J)} } {T} $

Then we accordingly adjust d1 and d2 from the Black-Scholes Formulation: 
* $d1 = \frac{ln(S_0/K) + (r_k + \frac{\sigma_k^2}{2}) \dot T}{\sigma_k \sqrt{T}}$
* $d2 = d1 - \sigma_k \sqrt{T} $

## Final Pricing
$$Call \space Price = \sum_{n=1}^{\infty} P \times S_0N(d1) - Ke^{-r_k T}N(d2))$$

$P$ = Poisson probability of $k$ jumps in $T$ time = $\frac{e^{-\lambda T}(\lambda T)^T}{k!}$

## Advantages 
As described in the paper, there are a couple main advantages to using the Jump Diffusion Model as opposed to a standard Black-Scholes Model for Option Pricing: 
* Volatility Smile: The relationship between implied volatility and strike price of an option often forms a convex curve which is *not* accounted for by the Black-Scholes Model which makes an assumption of constant volatility
* Leptokurtic Features: Jumps can model assets whose return distributions have heavier tails or higher peaks, contrary to the Black-Scholes Model which assumes a normally distributed return
