# Distributing circuits over heterogeneous, modular quantum computing network architectures: Experiment data

Here we give data relating to the experiments of [“Distributing circuits over heterogeneous, modular quantum computing network architectures”](https://arxiv.org/abs/2305.14148). Instillation instruction and documentation for `pytket-dqc` can be found at <https://github.com/CQCL/pytket-dqc> and <https://cqcl.github.io/pytket-dqc/> respectively, where some terminology used here relating to `pytket-dqc` is explained.

The first key file is `results.json`, containing information about the results of the experiments. This may be loaded into a python panda using the command
```
import pandas as pd
pd.read_pickle("results.json")
```
The columns of this dataframe are the following:

**original_circuit** - The circuit distributed. This can be loaded using a command like
```
from pytket import Circuit
import json

with open("{column entry}.json", 'r') as fp:
    Circuit.from_dict(json.load(fp))
```
where `{column entry}` should be replaced by the particular column entry corresponding to the circuit to be loaded.

**compilation_method** - The method used to distribute the circuit. Details about these compilation methods can be found in the paper [“Distributing circuits over heterogeneous, modular quantum computing network architectures”](https://arxiv.org/abs/2305.14148).

**compiled_circuit** - The result of the distribution. In the case that a Distributor from `pytket-dqc` is used this will be a `pytket-dqc` `Distribution` and can be loaded using a command like
```
from pytket_dqc import Distribution

with open("{column entry}.json", 'r') as fp:
    Distribution.from_dict(json.load(fp))
```
In the case that the method is not implemented in `pytket-dqc` this file will just contain the cost of the distribution, as measured by the number of ebits.

**architecture** - The network onto which the circuit is distributed. This can be loaded using a command like
```
from pytket_dqc import NISQNetwork

with open("{column entry}.json") as fp:
    NISQNetwork.from_dict(json.load(fp))
```

**time_taken** -  The time taken to arrive at the distribution, measured in seconds.

**compiled_circuit_cost** - The cost, in the number of ebits, of the resulting distribution.

The other important files are `circuits.json` and `architectures.json`. These may also be loaded as dataframes, and contain respectively additional information about the class of circuit and the network used during the experiments. Details about these circuit and network types can be found in the paper [“Distributing circuits over heterogeneous, modular quantum computing network architectures”](https://arxiv.org/abs/2305.14148). The remaining files have names which correspond to entries in the aforementioned dataframes, and contain information as described above. 