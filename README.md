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
samples = rand(1,10);
samples = sqrt(2) * erfinv(2 * samples - 1);
disp(samples);
% Output: tbd
```

**Python / NumPy**:
```python
import numpy as np
from scipy.special import erfinv
np.random.seed(22)
samples = np.random.rand(10)
samples = np.sqrt(2) * erfinv(2 * samples - 1)
print(samples)
# Output: [ 0.20846054  0.48168106  0.42053804  0.859182    0.17116155  0.33886396  0.27053283  0.69104135  0.22040452  0.81195092 ]
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
samples = np.random.randn(10)
print(samples)
# Output: [-0.09194992 -1.46335065  1.08179168 -0.23932517 -0.49112914]
```

