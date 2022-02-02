# Dask

dask

```python
# dask可以在大规模数据的情况下处理numpy、panda格式数据
import dask.array as darr
import dask.dataframe as ddfm
import numpy as np

normal_array = np.arange(10000)
# 根据给定的普通array对象，生成一个dask分区后的对象，每个分区数据量为chunks
darr_array = darr.from_array(normal_array, chunks=1000)  # darr_array可以进行array类似的操作，如mean、max、min等
# darr的优势在于，当数据量特别庞大时可以并发地使用多进程进行分区计算
```

