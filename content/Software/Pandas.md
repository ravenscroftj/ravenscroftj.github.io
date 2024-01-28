---
tags:
  - python
---


## Iterating over chunks of Pandas Dataframes
Based on [this answer on stackoverflow](https://archive.jamesravey.me/archive/1656528957.888122/singlefile.html)
```python
  import numpy as np
  import pandas as pd
  
  df.groupby(np.arange(len(df))//10)
  ```

## Progress over Pandas Dataframes
```python
	  from tqdm.auto import tqdm
	  
	  tqdm.pandas()
	  
	  df.progress_apply(somefunc)
```