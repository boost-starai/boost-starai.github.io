---
layout: splash
permalink: /software/boostsrl-python-wrappers/
title: 'BoostSRL: Python Wrappers'
author: Alexander Hayes
excerpt: 'A Python wrapper for BoostSRL to help automate learning/inference tasks.<br /><br />{::nomarkdown}<iframe style="display: inline-block;" src="https://ghbtns.com/github-btn.html?user=starling-lab&repo=boostsrl-python-package&type=star&count=true&size=large" frameborder="0" width="120px" height="30px"></iframe> <iframe style="display: inline-block;" src="https://ghbtns.com/github-btn.html?user=starling-lab&repo=boostsrl-python-package&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="158px" height="30px"></iframe>{:/nomarkdown}'
header:
  overlay_color: "#5e616c"
  cta_label: '<i class="fas fa-download"></i> Download'
  cta_url: "https://github.com/starling-lab/boostsrl-python-package/releases"
  caption: 'Copyright © 2017-2018 StARLinG Lab. This program comes with absolutely no warranty. This is free software, available under the terms of the GPL-3.0.'
---

<p align="center">
	<img src="https://github.com/starling-lab/boostsrl-python-package/raw/master/media/box2.png" />
</p>

| License | Build Status | Codecov |
| :---: | :---: | :---: |
| [![][license img]][license] | [![Build Status](https://travis-ci.org/starling-lab/boostsrl-python-package.svg?branch=master)](https://travis-ci.org/starling-lab/boostsrl-python-package) | [![][codecov img]][codecov link] |

---

# boostsrl

*boostsrl* is a Python wrapper for BoostSRL to help automate learning and inference tasks.

## Getting Started

### Prerequisites

* Java 1.8
* Python (2.7, 3.3, 3.4, 3.5, 3.6)
* subprocess32 (if using Python 2.7: `pip install subprocess32`)
* graphviz-0.8

### Installation

* The latest stable build can be installed with pip:

  ```bash
  $ pip install git+git://github.com/batflyer/boostsrl-python-package.git
  ```

### Basic Usage

```python
>>> from boostsrl import boostsrl

'''Step 1: Background Knowledge'''

# Sample data is built in from the 'Toy Cancer' Dataset, retrieve it with example_data
>>> bk = boostsrl.example_data('background')

# Create the background knowledge or 'Modes,' where 'cancer' is the target we want to predict.
>>> background = boostsrl.modes(bk, ['cancer'], useStdLogicVariables=True, treeDepth=4, nodeSize=2, numOfClauses=8)

'''Step 2: Training a Model'''

# Retrieve the positives, negatives, and facts.
>>> train_pos = boostsrl.example_data('train_pos')
>>> train_neg = boostsrl.example_data('train_neg')
>>> train_facts = boostsrl.example_data('train_facts')

# Train a model using this data:
>>> model = boostsrl.train(background, train_pos, train_neg, train_facts)

# How many seconds did training take?
>>> model.traintime()
0.705

'''Step 3: Test Model on New Data'''

# Retrieve the positives, negatives, and facts.
>>> test_pos = boostsrl.example_data('test_pos')
>>> test_neg = boostsrl.example_data('test_neg')
>>> test_facts = boostsrl.example_data('test_facts')

# Test the data
>>> results = boostsrl.test(model, test_pos, test_neg, test_facts)

'''Step 4: Observe Performance'''

# To see the overall performance of the model on test data:
>>> results.summarize_results()
{'CLL': '-0.223184', 'F1': '1.000000', 'Recall': '1.000000', 'Precision': '1.000000,0.500', 'AUC ROC': '1.000000', 'AUC PR': '1.000000'}

# To see probabilities for individual test examples:
>>> results.inference_results('cancer')
{'!cancer(Watson)': 0.6924179024024251, 'cancer(Xena)': 0.8807961917687174, '!cancer(Voldemort)': 0.6924179024024251, 'cancer(Yoda)': 0.8807961917687174, 'cancer(Zod)': 0.8807961917687174}

```

## Contributing

Please refer to [CONTRIBUTING.md](https://github.com/starling-lab/boostsrl-python-package/blob/master/.github/CONTRIBUTING.md) for documentation on submitting issues and pull requests.

## Versioning

We use [SemVer](http://semver.org/) for versioning. See [Releases](https://github.com/batflyer/boostsrl-python-package/releases) for all stable versions that are available.

## Acknowledgements

* Professor Sriraam Natarajan
* Members of StARLinG Lab

[license]:license.txt
[license img]:https://img.shields.io/github/license/starling-lab/boostsrl-python-package.svg

[codecov img]:https://codecov.io/gh/starling-lab/boostsrl-python-package/branch/master/graphs/badge.svg?branch=master
[codecov link]:https://codecov.io/github/starling-lab/boostsrl-python-package?branch=master
