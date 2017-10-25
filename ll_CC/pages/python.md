# Python

## matplotlib docker 실행 시 png로 이미지 저장

```
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

... do something ...

plt.savefig('./name.png')

```