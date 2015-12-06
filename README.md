## Reproducing Random Numbers in Matlab and Python / NumPy

### Uniform Distribution (rand)

Current versions of Matlab and NumPy use the same random number generator. Thus, it is easy to create the same samples from a uniform distribution.

**Matlab**:
```matlab
rng(22); % seed
samples = rand(1, 5);
disp(samples);
% Output: 0.2085    0.4817    0.4205    0.8592    0.1712
```

**Python / NumPy**:
```python
import numpy as np
np.random.seed(22)
samples = np.random.rand(5)
print(samples)
# Output: [ 0.20846054  0.48168106  0.42053804  0.859182    0.17116155 ]
```

### Standard Normal Distribution (randn)

Unfortunately, Matlab and NumPy use different transformations to create samples from the standard normal distribution. Thus, we need our own implementation that uses the same transformation in both Matlab and Python / NumPy. For example, we can use [inverse transform sampling](https://en.wikipedia.org/wiki/Inverse_transform_sampling).

**Matlab**:
```matlab
rng(22); % seed
samples = rand(1, 5);
% transform from uniform to standard normal distribution using inverse cdf
samples = sqrt(2) * erfinv(2 * samples - 1);
disp(samples);
% Output: -0.8118   -0.0459   -0.2005    1.0767   -0.9496
```

**Python / NumPy**:
```python
import numpy as np
from scipy.special import erfinv
np.random.seed(22)
samples = np.random.rand(5)
# transform from uniform to standard normal distribution using inverse cdf
samples = np.sqrt(2) * erfinv(2 * samples - 1)
print(samples)
# Output: [-0.81177443 -0.04593492 -0.20051725  1.07665147 -0.94958511]
```

---

Compare this to the standard implementations of randn, which yield different results in Matlab and Python / NumPy.

**Matlab**:
```matlab
rng(22); % seed
samples = randn(1, 5);
disp(samples);
% Output: -1.1193   -0.0729   -0.2847    1.5111   -1.5112
```

**Python / NumPy**:
```python
import numpy as np
np.random.seed(22)
samples = np.random.randn(5)
print(samples)
# Output: [-0.09194992 -1.46335065  1.08179168 -0.23932517 -0.49112914]
```

