---
tags:
  - 🖍️Learning
  - 🧮Math
  - 🖥️Computing
---
```python
a = np.arange(10)
b = np.arange(10)

#simple case
a[a<6] #array([0, 1, 2, 3, 4, 5])

# advanced case
mask = (a<6) & (b>4)
a[mask] #array([5])
mask * a #array([0, 0, 0, 0, 0, 5, 0, 0, 0, 0])
```