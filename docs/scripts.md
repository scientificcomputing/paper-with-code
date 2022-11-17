# Setting up your scripts

There are in general two types of scripts in a scientific paper: scripts for creating the figures and tables in the paper, and other scripts. You should strive to make a clear distinction here, especially if your analysis scripts take a long time to run. 

## Scripts for reproducing figures and tables
These scripts should preferably work with input data from file.
Common formats for raw data are [h5](https://docs.fileformat.com/misc/h5/) (preferable for applications executed in parallel with [MPI](https://www.mcs.anl.gov/research/projects/mpi/)), [csv](https://docs.fileformat.com/spreadsheet/csv/) if you want to use [pandas](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html).


## Scripts for running the analysis
These scripts should have a clearly stated interface for input parameters, using for instance [argparse](https://docs.python.org/3/library/argparse.html) or [click](https://click.palletsprojects.com/en/latest/).
It is preferable to have default parameters for these scripts.

If you want to run such a script for a wide range of parameters, you could use argparse in the following way
```python
from typing import Sequence, Optional
import pprint
import argparse


def analysis(argv: Optional[Sequence[str]]) -> int:
    parser = argparse.ArgumentParser(
        formatter_class=argparse.ArgumentDefaultsHelpFormatter)
    parser.add_argument(
        "-N", type=int, help="Optional input integer", default=0)
    parser.add_argument("-T", type=float, help="Input float")

    parser.add_argument("--run_code", dest="code", action="store_true",
                        help="Optional flag", default=False)
    args = vars(parser.parse_args(arguments))

    print(f"Arguments gotten: {pprint.pformat(args)}")
    return 0


if __name__ == "__main__":
    N = [1, 2, 5, 8]
    for run in [True, False]:
        for n in N:
            arguments = ["-N", f"{n}", "-T", "3.5"]
            if run:
                arguments.append("--run_code")
            print("-"*25)
            print(f"Input arguments {arguments}")
            analysis(arguments)

```
