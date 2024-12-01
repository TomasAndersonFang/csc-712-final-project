# openctest

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


## CSC 712 Project
This project aims to evaluate the effectiveness, applicability, and generalizability of openctest by applying it to popular open-source systems such as Alluxio, Apache Flink, Apache Kylin, and Apache Superset. The scope includes deploying openctest on these platforms to assess its capabilities and limitations. Specifically, the project involves testing the applicability of openctest on **Flink**, **Kylin**, and **Superset**, as well as investigating its generalizability across these systems. Through this analysis, the project seeks to highlight openctest’s potential as a robust testing tool for diverse software ecosystems.

### Demo


### Implementations of applying openctest:
- Flink: 
- Superset: https://github.com/TomasAndersonFang/csc-712-final-project/commit/6eb1c819d303d47625aa529aefb8bb31c9e642dd
- Kylin: https://github.com/TomasAndersonFang/csc-712-final-project/commit/f087fae14f65b2273e1028ad5356e876ab4d88fb

### Test Results:
- Alluxio: https://github.com/kofiarkoh/csc_712_software_testing_project_work/tree/main/results/alluxio-core
- Flink: https://github.com/kofiarkoh/csc_712_software_testing_project_work/tree/main/flink
- Superset: https://github.com/TomasAndersonFang/csc-712-final-project/blob/Superset/core/generate_ctest/result/report.csv
- Kylin: https://github.com/TomasAndersonFang/csc-712-final-project/tree/kylin/core/generate_ctest/test_result/kylin-common


## Overview


This repository releases the prototype and datatsets of the `ctest` paper:

**[Testing Configuration Changes in Context to Prevent Production Failures](https://www.usenix.org/conference/osdi20/presentation/sun "paper")** <br/>
In Proceedings of the 14th USENIX Symposium on Operating Systems Design and Implementation (OSDI'20), Nov. 2020.

Please cite the paper if you use the code or the datasets.

## Repository Structure

### [core](https://github.com/xlab-uiuc/openctest/tree/main/core "core")

 The prototype for generating and running ctests.
 
### [data](https://github.com/xlab-uiuc/openctest/tree/main/data "data")

 The datasets evaluated in the paper.
