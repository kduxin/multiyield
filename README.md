
# multiyield

This package implements a Python generator that get function results from multi-process workers.
The `faster_fifo` Queue (instead of the standard multiprocessing.Queue)
is used to achieve a throughput up to 130k per second.

Acknowledgement: this package borrowed code / design from https://github.com/ferventdesert/multi_yielder,
but is more than 10x faster.


# requirements
- Python 3
- faster_fifo


# Quickstart

## A simplest run case
```bash
python multiyield.py
```
which is equivalent to the following:
```python
from multiyield import yielder

def job(x, margin):
    return max(x**3, margin)

num_workers = 2
for x in yielder(range(1000000), func=job, num_workers=num_workers, 
                 additional_kwds={'margin': 3}, max_size_bytes=1024*1024):
    pass
```