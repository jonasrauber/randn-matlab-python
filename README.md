# Reproducing Random Numbers in Matlab and Python / NumPy

## Uniform Distribution (rand)

Current versions of Matlab and NumPy use the same random number generator. Thus, it is easy to create the same samples from a uniform distribution.

**Matlab**:
```matlab
rng(22); % seed
samples = rand(1,10);
disp(samples);
% Output: 0.2085    0.4817    0.4205    0.8592    0.1712    0.3389    0.2705    0.6910    0.2204    0.8120
```

**Python / NumPy**:
```python
import numpy as np
np.random.seed(22)
samples = np.random.rand(10)
print(samples)
# Output: [ 0.20846054  0.48168106  0.42053804  0.859182    0.17116155  0.33886396  0.27053283  0.69104135  0.22040452  0.81195092 ]
```

# Standard Normal Distribution (randn)

*tbd*

