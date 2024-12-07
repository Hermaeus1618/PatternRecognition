# STOCK PATTERN RECOGNITION DATASET

Here is the complete dataset in ZIP Format.
The code cannot be provided as the model was a cooporate project,
but the training data is gathered form public source and can be distributed.

This file contains several files which are numpy 1-D array in binary format.
These files are generated from `numpy.ndarray.tobytes()` to directly write inside ZIP stream.

File includes 37 different patterns although number of dataset per pattern are variable.
Recommended dataset size for better training is >300.

Values are seprated by "\_GAP\_" string which can be easily converted back into list by `pd.Series().str.split()` like:
``` python
with zipfile.ZipFile(DATASET.zfs, "r") as ZFILE:
    PATTERNDF=pd.Series([F.filename for F in ZFILE.infolist()])
PATTERNDF=PATTERNDF.str.split("_GAP_", expand=True)
```
Naming convention for Numpy files:
`IOC_GAP_CupAndHandle_GAP_HOUR1_GAP_1722503700_GAP_1725272100`
STOCK_GAP_PATTERN_GAP_TIMEFRAME_GAP_START_GAP_END

- IOC: Name of stock.
- CupAndHandle: Name of pattern.
- HOUR1: Timeframe in which the pattern is formed.
- 1722503700: Timestamp of pattern start.
- 1725272100: Timestamp of pattern end.

__Some points about dataset:__
Arrays are 1-Dimensional consist of price of stock which is forming the pattern.
Datasets are variable in length.
Price data has to be normalized before training.
Normalization can be as simple as `ARRAY/ARRAY.mean()`, avoid using complex normalization algorithms.

__Some about training:__
Due to variable length model need to include `LSTM` layer with `Embedding` layer as input.

Values other than <PATTERN> are useless for training purpose, these are included to avoid naming conflit in the data generation algorithm.
After which you can filter the pattern (or patterns for categorical classification) from dataframe.

For training a binary classification model use 1:1 ratio for both dataset.

Can expect to get ocassional updates for **DATASET.zfs** in near future.
