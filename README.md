# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
import numpy as np 
import math 
from scipy.stats import chi2 
data = list(map(int, input("Enter observations: ").split())) 
 
data = np.array(data) 
max_x = max(data) 
obs = [np.sum(data == x) for x in range(max_x + 1)] 
 
N = sum(obs) 
 
# Mean (lambda) 
mean = sum(x * obs[x] for x in range(len(obs))) / N 
 
print("\n x   P(x=x)   Obs.Fr   Exp.Fr    xi") 
print("------------------------------ 
Experiment:
chi_sq = 0 
for x in range(len(obs)): 
    # Poisson probability 
    p = math.exp(-mean) * (mean ** x) / math.factorial(x) 
    # Expected frequency 
    exp = N * p 
    # Chi-square component 
    if exp > 0: 
        xi = (obs[x] - exp) ** 2 / exp 
        chi_sq += xi 
    else: 
        xi = 0 
 
    print(f"{x:2d}   {p:0.3f}     {obs[x]:2d}      {exp:0.2f}     {xi:0.2f}") 
    df = max_x - 1 
    critical = chi2.ppf(0.99, df) 
 
    print("\nCalculated value of Chi square is", round(chi_sq, 2)) 
    print("Table value of chi square at 1% level is", round(critical, 2)) 
    if chi_sq < critical: 
    print("The given data can be fitted in poisson Distribution at 1% LOS") 
    else: 
    print("The given data cannot be fitted in poisson Distribution at 1% LOS")
```
 

# Output : 
<img width="626" height="322" alt="image" src="https://github.com/user-attachments/assets/a1352410-e1f7-4465-b3e0-a6b6d65326d2" />




# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
