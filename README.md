# Jump Diffusion Model for Option Pricing

## Dynamics 
In this model, the option price follows a stochastic process which includes the typical Brownian diffusion process in addition to discrete jumps following a compound Poisson Process. From the reference paper, the price S(t) can be modeled with the following dynamics 

![image](https://github.com/user-attachments/assets/c202ff42-1513-4a0a-bc00-052290c1dccf)

* μ - Drift Rate
* σ - Volatility
* W(t) - Wiener Process 
* N(t) - Poisson process of intensity λ
* $V_i$ - i.i.d. random variables representing jump size (Compound Poisson Process)

## Jumps
The jumps occur according to a poisson process N(t) where $\lambda$ is the expected number of jumps per unit time. The model uses a log-normal distribution for the size of the jumps.
Then, we can adjust the voltatiliy and drift for each jump, k. 
* Adjusted Volatility: $\sigma_k = \sqrt{\sigma^2 + k \frac{\sigma_J^2}{T}}$
* Adjusted Drift: $r_k = r - \lambda k + k \log{1+\mu_J} / T $
