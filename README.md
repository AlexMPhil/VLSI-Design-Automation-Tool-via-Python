# VLSI-Design-Automation-Tool-for-Physical-Design-using-Python


## Abstract

The rapid evolution of Very-Large-Scale Integration (VLSI) design has driven the
need for automation tools that can handle complex physical design tasks with precision and efficiency. EDA tools are indispensable in VLSI design because they
automate, optimize, and accurately handle the complexity of modern semiconductor circuits, ensuring efficient design cycles and reliable chip performance. This report presents the development of a VLSI design automation tool specifically for the
physical design phase, implemented using Python. The tool is designed to address
critical aspects such as partitioning, floorplanning, placement, and routing, providing a streamlined and modular approach to handling large circuits. Key results
highlight the tool’s potential for enhancing physical design workflows in academic
and industrial settings.


## Introduction
The field of Very Large Scale Integration (VLSI) design has seen significant advancements in recent times due to the growing demands for complex electronic systems
and tasks. However the design process still faces issues that require expert supervision in various aspects including but not limited to circuit design, physical layout
etc. Automation tools have been essential in making the process much more streamlined but there remains the fact that these tools are most often highly complex and
proprietary, rendering them difficult to understand and modify.
This report aims to address this gap by presenting the design and implementation
of a Python-based automation tool for the physical design phase of VLSI. The tool
is intended to simplify the design process, offering a flexible and accessible solution
to meet the needs of both academic and industrial users. By leveraging Python’s
capabilities, the proposed tool seeks to reduce the complexity of VLSI physical
design, enabling efficient design workflows.


## Problem Statement
The Project aims to design and develop a Python-based VLSI Design automation
tool focused on the physical design phase. The tool should be capable of handling
intermediate tasks such as partitioning, floorplanning, placement and routing and
should be modular, allowing for easy customization and integration with other tools
or processes. All of this is done with an input of netlist in a bench file format like
ISCAS85.


## Objectives

1. Develop a Python-based tool for automating the physical design phase of VLSI,
covering essential tasks such as Partitioning, Floorplanning, Placement, and (in future)
Routing.

2. Promote modularity by designing the tool in a way that enables users to customize and extend its functionality for specific use cases or design methodologies.

3. Implement efficient algorithms to optimize chip layout for performance, power,
area and validate the tool’s effectiveness through case studies or benchmarks.

4. Explore Python’s capabilities in handling complex data structures and optimization techniques to enhance the tool’s performance and user-friendliness
for VLSI physical design.





## Methodology

EDA tools play a significant role in real life by enabling the design of complex electronic systems found in everyday devices like smartphones, laptops, and medical
equipment. These tools automate the design of integrated circuits (ICs) that power
these devices, ensuring they are optimized for performance, energy efficiency, and
size. Without EDA tools, the development of modern technology—spanning from
consumer electronics to automotive systems and communication networks—would
be slow, costly, and prone to errors, making them essential for innovation and technological progress.

### 1) Creating graph based on bench file

After creating a Graph class, the first major section of code makes the user choose
which bench file to access. A bench file is a text only file that describes a circuit.
We now parse through the file using regular expressions. Commented lines and
empty lines are ignored while parsing. The readable lines have relevant information
extracted using the regular expressions p1, p2 and p3.


## Conclusion and Future Scope

Look into detailed tie-breaker logic for KL algorithm partition selection
• Look into perfecting the function to modify polish expression as there are times
where the modified expression doesn’t seem to be different. We should also
edit the function to modify polish expression to work for non standard nodes
• Edit region bound to possibly adjust according to x_lim and y_lim or just in
proportion to number of blocks to consider
• The next big step in Physical Design to implement is Routing. We need to
integrate Routing algorithms to complete the physical design flow, followed by
optimization to ensure minimal wire length, congestion, and power consumption.
• Implementing other minor changes like
– Optimizing the existing algorithms to see if we can achieve faster results
– When size of circuit is large and when KL algorithm iterations doesn’t
seem to be improving on score, then we should be able to implement a
task ender.
– Permanent storage of bench files as in built libraries instead of depending
on sharing in colab space before run time.



## References

1. ISCAS Netlist, [Link](https://sportlab.usc.edu/~msabrishami/benchmarks.html)

