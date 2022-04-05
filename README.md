# Immune-inspired node-fault detection in WSNs #

This page acts as a landing page for our immune-inspired fault detection approach for sensor networks that utilizes node-level diagnostics.
It summarizes the used resources and links to the respective repositories.
The approach combines the node-level self-diagnostics of the used sensor nodes with an immune-inspired fault detection algorithm based on a modified version of the deterministic dendritic cell algorithm (dDCA).


## Contents ##

* Implementation
  * Sensor node platform
  * Cluster head
  * Sink node
* Evaluation
  * Efficiency analysis
  * Simulation
  * Lab experiments
  * Indoor deployment


## Implementation ##

The entire approach has been implemented in a real wireless sensor network (WSN) consisting of several sensor nodes, a cluster head, and a sink node.
Information on the particular parts is presented in the following.


### Sensor node platform ###

The sensor nodes are based on the [AVR-based sensor node with XBee radio](https://github.com/DoWiD-wsn/avr-based_sensor_node), or short `ASN(x)`.
The nodes were programmed in C-language on the bare metal (i.e., without an operating system) using the software libraries available in the repository linked above.


### Cluster head ###

The cluster head is based on a Raspberry Pi 3 Model B+.
Information on the general setup is available in the [setup instructions](https://github.com/DoWiD-wsn/RPi_cluster_head/blob/master/source/setup.md).
The Python script implementing the modified dDCA is located in the [source directory](https://github.com/DoWiD-wsn/RPi_cluster_head/blob/dca/source/) of the `dca` branch.


### Sink node ###

Like the cluster head, also the sink node is based on a Raspberry Pi 3 Model B+.
Information on its components and setup is available in the respective [RPi-based Sink Node](https://github.com/DoWiD-wsn/RPi_sink_node) repository.


## Evaluation ##

Our approach was evaluated with a tripartite setup consisting of simulations, a lab experiment setup, and an indoor WSN deployment.
Details on each experiment are given below.


### Efficiency analysis ###

To evaluate the approach's efficiency, we analyzed its resource overhead.
In this context, we compared the memory requirements of the sensor node software with and without our detection approach enabled.
The version without the fault detection and without any node-level diagnostics is available in the `dca-central-analysis` branch of the `ASN(x)` repository in the [006-dca_centralized-without_diag](https://github.com/DoWiD-wsn/avr-based_sensor_node/tree/dca-central-analysis/source/006-dca_centralized-without_diag) directory.
An example implementation of the entire approach is provided as demo application in the default branch (master) in the `source` directory and is named [005-dca_centralized](https://github.com/DoWiD-wsn/avr-based_sensor_node/tree/master/source/005-dca_centralized).
The comparison is based on the memory calculation of the `avr-size` tool.
In both cases, the sources were compiled with optimization for size (`-Os`) and link-time optimization (`-lfto`).


### Simulation ###

We ran several simulations where we randomly injected faults in one of three base datasets.
The base datasets were recorded from our WSN deployments and show fault-free sensor values and node-level diagnostics.
The injected faults, on the other hand, are based on fault signatures captured in our previous works and our lab experiments described below.
The base datasets, the fault signatures, and the Python scripts used for the simulation are available in the [ASN(x) Analyses](https://github.com/DoWiD-wsn/asnx_analyses) repository.
The datasets generated during our simulations and the respective results of our fault detection approach as well as visualizations of the used data are stored in the [dca](https://github.com/DoWiD-wsn/asnx_analyses/tree/dca-central-analysis/dca) directory of the `dca-central-analysis` branch.


### Lab experiments ###

Additionally, we performed several experiments in a lab setup to evaluate the reaction of our approach to various environmental influences partly while forcing the sensor node in faulty conditions.
In this setup, the environmental conditions of the sensor node were controlled by our [Embedded Testbench](https://github.com/DoWiD-wsn/embedded_testbench) (short ETB).
In contrast to the indoor WSN deployment discussed below, the sensor node transmitted the data directly to the ETB via UART rather than sending it via Zigbee.
The respective source code is available in the `dca-etb-exp` branch in the `source` folder (i.e., [005-dca_centralized](https://github.com/DoWiD-wsn/avr-based_sensor_node/tree/dca-etb-exp/source/005-dca_centralized)).


### Indoor deployment ###

Our indoor deployment consists of seven sensor nodes (as described above) that were running software implementing extended node-level diagnostics.
As stated above, the source code is available in the `source` directory of the `master` branch named [005-dca_centralized](https://github.com/DoWiD-wsn/avr-based_sensor_node/tree/master/source/005-dca_centralized).
