# Pandas Helper

Pandas Helper displays Data Frame and returns it's Markdown string. Usage example for Atom+Hydrogen/Knitty:

```py
# %% """ %%% """
"""
KNITTY = True
"""
# %%
try:
    # noinspection PyUnresolvedReferences,PyUnboundLocalVariable
    KNITTY
except NameError:
    KNITTY = False


import pandas as pd
import numpy as np
from pandoctools import pandas as th

df = pd.DataFrame(np.random.random(16).reshape(4, 4))

print(th.md_table(df, KNITTY))
print('')
print(': Table {#tbl:table1}')
```