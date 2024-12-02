# OpenCTest

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


## CSC 712 Project
This project aims to evaluate the effectiveness, applicability, and generalizability of openctest by applying it to popular open-source systems such as Alluxio, Apache Flink, Apache Kylin, and Apache Superset. The scope includes deploying openctest on these platforms to assess its capabilities and limitations. Specifically, the project involves testing the applicability of openctest on **Flink**, **Kylin**, and **Superset**, as well as investigating its generalizability across these systems. Through this analysis, the project seeks to highlight openctest’s potential as a robust testing tool for diverse software ecosystems.

### 1. Apache Flink (See our fork: [https://github.com/kofiarkoh/flink](https://github.com/kofiarkoh/flink))

#### System Requirement
- Java installation. (This project has been test on Java 17 but can it may also be run on Java 11)
- Maven must be installed. You may check by running `mvn -v` in your terminal. We have ran this against Maven 3.9

#### Runninng  Configuration Tests

> **NOTE:** The steps below have been run using **openjdk version 17.0.10** on **macOS Sequoia**.

We have alread applied CTEST to this project by adding the necessary CTEST specific code: [See Configuration Setup](https://github.com/kofiarkoh/flink/blob/master/flink-core/src/main/java/org/apache/flink/configuration/Configuration.java)

For demonstration purposes, the steps below simulates testing configuration tests induced failures 
using [TimeWindowTranslationTest](https://github.com/kofiarkoh/flink/blob/master/flink-runtime/src/test/java/org/apache/flink/streaming/runtime/operators/windowing/TimeWindowTranslationTest.java) test class inside the `flink-runtime` submodule _only_.
- Clone the project by running the command `git clone git@github.com:kofiarkoh/flink.git`
- Switch to the project directory by running `cd flink/flink-runtime`
- Run `mvn clean install -DskipTests  -Denforcer.skip=true -Drat.skip=true` to build the project
- Run the test below using default configuration values as specified in the test file. This test will PASS
```
 mvn surefire:test -Denforcer.skip=true -Dctest.config.save -Dmaven.test.failure.ignore=true -Dtest="org.apache.flink.streaming.runtime.operators.windowing.TimeWindowTranslationTest" -Drat.skip=true
```
![Failing Tests](https://raw.githubusercontent.com/kofiarkoh/flink/refs/heads/master/img/pass.png)
- Now lets change one conguration value used in the tests (this value is a valid configuration value). This test will PASS
```
mvn surefire:test -Denforcer.skip=true -Dctest.config.save -Dmaven.test.failure.ignore=true -Dtest="org.apache.flink.streaming.runtime.operators.windowing.TimeWindowTranslationTest" -Dconfig.inject.cli="parallelism.default=1" -Drat.skip=true
```
- To simulate a configuration induced test failure. Run the command below. _For this step, we set `parallelism.default` to an invalid value `1s` because valid value must be an integer. This test will FAIL because an invalid configuration value is injected into the test case
```
 mvn surefire:test -Denforcer.skip=true -Dctest.config.save -Dmaven.test.failure.ignore=true -Dtest="org.apache.flink.streaming.runtime.operators.windowing.TimeWindowTranslationTest" -Dconfig.inject.cli="parallelism.default=1s" -Drat.skip=true

```
![Failing Tests](https://raw.githubusercontent.com/kofiarkoh/flink/refs/heads/master/img/fail.png)

### 2. Apache Kylin

#### System Requirement
- Docker Installation (https://docs.docker.com/get-started/get-docker/)
- Linux machine

#### Docker Container Setup 
- Clone the branch `kylin`
```console
git clone -b kylin https://github.com/TomasAndersonFang/csc-712-final-project.git
```
- Build the Dockerfile
```console
cd csc-712-final-project/core
docker build --tag openctest .
```
- Run the container
```console
docker run -it --name ctest openctest
```
- Access the container
```console
docker exec -it ctest /bin/bash
```
#### Clone the project and Add Kylin in the project
- Clone the branch `kylin`
```console
git clone -b kylin https://github.com/TomasAndersonFang/csc-712-final-project.git
```
- Add Apache Kylin in `core` and `core/identify_param`
```console
cd csc-712-final-project/core
./add_project.sh kylin
cd ../identify_param
./add_project.sh kylin
```
#### Run Configuration Tests
- Go to the `generate_ctest` directory and run configuration tests. The test results will be store in the `test_result/kylin-common/` directory.
```console
cd core/generate_ctest
./generate_ctest.sh
```

### Implementations of applying openctest:
- Flink: https://github.com/kofiarkoh/flink
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

 ## Demonstration

 ### OpenCTest Demonstration on Flink

 [![Watch the video](https://github.com/user-attachments/assets/092fbdb6-0edf-4b9a-9636-607a2330343b)](https://drive.google.com/file/d/1sDHmN8qKRybBM9WC6RsE5NUP1g7GAFEi/view?resourcekey)

 ## Status Updates

 Our weekly status updates presented during class.
 
 [PowerPoint Presentation](https://docs.google.com/presentation/d/1KXfRPsoZes1UmxvamBb_bFWPSWMMfIyDqCr1yzzJiK8/edit#slide=id.p)
