# Markov Chain Credit Risk Model (Excel)
About this Project This is a 35-year simulation engine designed to forecast how a loan portfolio moves between credit ratings over time. I built this to visualize how Capital at Risk grows the longer a debt is held.

How it Works

Transition Matrix: I used the S&P Global historical transition matrix (1981-2023) to define the probability of a borrower moving from one rating (AAA through Default) to another in a single year.

Simulation: The model uses iterative matrix multiplication to project the portfolio's rating vector up to 35 years into the future.

Key Findings: The model demonstrates the non-linear nature of credit risk. For example, it showed that Capital at Risk is roughly 18x higher for B-rated lending compared to BBB-rated lending.


