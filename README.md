# Beyond Typosquatting, An in-depth Look at Package Confusability

This is the artifact for the package confusability paper. This project implements the detection rules for the categories defined by our paper. The detection rules are implemented in `core`


## What is included
The dataset collected and the evaluation tools for the dataset.
The core detection implementations
Tools used to implement various parts

## Setup
Create a Python virtual environment
```
Python3 -m venv myvenv
```
Then, activate the virtual environment

Follow [this link](https://docs.python.org/3/tutorial/venv.html) from Python docs.

One of the detection rule requires the "fasttext-vectors" word vector. Download it from `https://dl.fbaipublicfiles.com/fasttext/vectors-english/crawl-300d-2M-subword.zip` unzip it, paste the unzipped crawl-300d-2M-subword folder in [data](data) and update the relative path in `tools/fasttext.py`. Finally convert it into the saved model using the following command:
```
python3 tools/fasttext.py
```

The saved model needs to be placed into `core/models`. 

Alternatively you can download the required `fasttext-vectors.kv.vectors.npy` file from [OSF](https://osf.io/m387c?view_only=b56d63194ef84ce4ba85ec00ee57cd05) and save it in  `/core/models`

To install the required dependencies

```
$ pip3 install -r requirements.txt
```

## Running the detection tools

To test the accuracy of the detection rules in the attack dataset, run the evaluation code:

```
$ python3 evaluation/test_accuracy.py data/clean_package_data.csv
```

Displays typo-squatting categories exhibited by adversarial package WRT base package:

```
$ python3 __main__.py <base_package_name> <potentially_malicious_package_name>
```

For example:
```
python3 __main__.py gray-matter grey-matter
```

To run the detector rules in a sample of our popular and unpopular package files run the following.

```
$ python3 __main__.py --base_file data/test/popular-100-sample.csv --adv_file data/test/unpopular-100-sample.csv
```

The folder `data/test` holds the complete dataset of npm popular and npm unpopular packages.

Learn more about flags and usage:
```
$ python typomind -h
```

The full analysis of npm ecosystem takes a long time and we execute the analysis on a SLURM cluster at our institution, consisting of 1000+ x86 CPUs and 8+ TB of aggregated RAM.

To implement SLURM, you can wrap the python3 __main__.py file into a multithreaded code and use SLURM to run it

```
$ srun <executable file> <options>
```
