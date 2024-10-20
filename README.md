### **Interest Rate Modeling and Simulation Project**

#### **1. Collect Historical Interest Rate Data**
- Start by fetching historical interest rate data, such as the 10-year US Treasury yield, to use as the basis for modeling.
- Clean and interpolate the data to handle any missing values, and prepare it as a time series of interest rates for further analysis.

#### **2. Calibrate the Hull-White Model Parameters**
- Use the Hull-White model to describe the evolution of interest rates over time. The Hull-White model follows the stochastic differential equation (SDE):

$$
dr(t) = \alpha \left( \theta(t) - r(t) \right) dt + \sigma dW(t)
$$

  Where:
  - $r(t)$ is the short rate at time $t$.
  - $\theta(t)$ is the long-term mean rate.
  - $\alpha$ is the mean-reversion rate (speed at which $r(t)$ reverts to $\theta(t)$).
  - $\sigma$ is the volatility of interest rate changes.
  - $dW(t)$ is the Wiener process (Brownian motion).

- Estimate the two key parameters from historical interest rate data:
  - **Mean Reversion Rate ($\alpha$)**: Measures how quickly interest rates revert to their long-term average.
  - **Volatility ($\sigma$)**: Captures the randomness or uncertainty in interest rate movements.
  
- Use Maximum Likelihood Estimation (MLE) to estimate these parameters from the data.
  - **$\alpha$**: The mean-reversion rate.
  - **$\sigma$**: The volatility.

#### **3. Simulate Interest Rate Paths Using the Hull-White Model**
- With the calibrated parameters ($\alpha$, $\sigma$), simulate the future evolution of interest rates over one year (252 trading days).
- Apply the **Euler-Maruyama method** to numerically solve the stochastic differential equation of the Hull-White model.

  The Euler-Maruyama discretization of the SDE is:

$$
r(t + \Delta t) = r(t) + \alpha \left( \theta - r(t) \right) \Delta t + \sigma \sqrt{\Delta t} \cdot Z
$$

  Where $Z$ is a standard normal random variable ($Z \sim N(0,1)$), and $\Delta t$ is the time step (1 day in years).
  
- Generate multiple possible future interest rate paths, each reflecting different random shocks to the rates based on the Hull-White model.

#### **4. Price Interest Rate Derivatives (Caps and Floors)**
- Price two common interest rate derivatives based on the simulated rate paths:
  - **Caps**: Protect against rising interest rates. The payoff occurs when the interest rate exceeds a pre-defined cap rate. The payoff for a caplet is:

$$
\text{Caplet Payoff} = \text{Notional} \times \max(r(t) - r_{\text{cap}}, 0)
$$

  - **Floors**: Protect against falling interest rates. The payoff occurs when the interest rate falls below a pre-defined floor rate. The payoff for a floorlet is:

$$
\text{Floorlet Payoff} = \text{Notional} \times \max(r_{\text{floor}} - r(t), 0)
$$

- For each simulated interest rate path, calculate the payoff for both caps and floors at each time step, discount them to the present value, and average the payoffs across all simulations to determine the total cap and floor values.
  
  - The **Cap Value** represents the average payoff when rates exceed the cap rate.
  - The **Floor Value** represents the average payoff when rates drop below the floor rate.

#### **5. Scenario Analysis**
- Analyze the impact of different economic scenarios by adjusting the model parameters:
  - **Higher Volatility ($\sigma$)**: Increases the variability in interest rate movements, leading to higher potential payoffs for both caps and floors.
  - **Lower Mean Reversion ($\alpha$)**: Allows rates to drift further from the long-term mean, increasing the range of potential outcomes.
  
- Recalculate the derivative prices under these different scenarios to observe how changing market conditions affect the value of interest rate caps and floors.

### **Conclusion**
Implement the Hull-White model using the calibrated parameters to simulate future interest rate movements. Use these simulated scenarios to price interest rate derivatives (caps and floors). Finally, perform scenario analysis by adjusting key parameters such as volatility and mean-reversion rate to understand the sensitivity of derivative prices to various economic conditions.
