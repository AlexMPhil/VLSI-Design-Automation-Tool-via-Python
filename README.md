# VLSI-Design-Automation-Tool-via-Python
**Designing a VLSI Design Automation Tool for Physical Design in
Python**


**TABLE OF CONTENT**

  ---------------------------------------------------------------------------
  **S     **Topic**                                                  **Pg**
  No**                                                               
  ------- ---------------------------------------------------------- --------
  **1**   **Abstract**                                               **2**

  **2**   **Introduction**                                           **2**

  **3**   **Problem Statement**                                      **3**

  **4**   **Objectives**                                             **3**

  **5**   **Literature Review**                                      **4**

  **6**   **Methodology**                                            **5**

  **7**   **Progress and Results**                                   **8**

  **8**   **Conclusion and Future Work**                             **12**

  **9**   **References**                                             **13**
  ---------------------------------------------------------------------------

**ABSTRACT**

The rapid evolution of Very-Large-Scale Integration (VLSI) design has
driven the need for automation tools that can handle complex physical
design tasks with precision and efficiency. This report presents the
development of a VLSI design automation tool specifically for the
physical design phase, implemented using Python. The tool is designed to
address critical aspects such as partitioning, floorplanning, placement,
and routing, providing a streamlined and modular approach to handling
large circuits. Key results highlight the tool\'s potential for
enhancing physical design workflows in academic and industrial settings.

**INTRODUCTION**

The field of Very Large Scale Integration (VLSI) design has seen
significant advancements in recent times due to the growing demands for
complex electronic systems and tasks. However the design process still
faces issues that require expert supervision in various aspects
including but not limited to circuit design, physical layout etc.
Automation tools have been essential in making the process much more
streamlined but there remains the fact that these tools are most often
highly complex and proprietary, rendering them difficult to understand
and modify.

This report aims to address this gap by presenting the design and
implementation of a Python-based automation tool for the physical design
phase of VLSI. The tool is intended to simplify the design process,
offering a flexible and accessible solution to meet the needs of both
academic and industrial users. By leveraging Python's capabilities, the
proposed tool seeks to reduce the complexity of VLSI physical design,
enabling efficient design workflows.

**PROBLEM STATEMENT**

The Project aims to design and develop a Python-based VLSI Design
automation tool focused on the physical design phase. The tool should be
capable of handling intermediate tasks such as partitioning,
floorplanning, placement and routing and should be modular, allowing for
easy customization and integration with other tools or processes. All of
this is done with an input of netlist in a bench file format like
ISCAS85.

**OBJECTIVES**

-   Develop a Python-based tool for automating the physical design phase
    of VLSI, covering essential tasks such as Partitioning,
    Floorplanning, Placement, and Routing.

-   Promote modularity by designing the tool in a way that enables users
    to customize and extend its functionality for specific use cases or
    design methodologies.

-   Implement efficient algorithms to optimize chip layout for
    performance, power, area and validate the tool\'s effectiveness
    through case studies or benchmarks.

-   Explore Python's capabilities in handling complex data structures
    and optimization techniques to enhance the tool\'s performance and
    user-friendliness for VLSI physical design.

**LITERATURE REVIEW**

**Xiaoping Tang; Ruiqi Tian; M.D.F. Wong \[1\] :** During the research
pointed out that minimizing wire length during partitioning and
floorplanning is a key challenge. Several methods have been proposed to
optimize wire length, one of which focuses on the optimal distribution
of white space among blocks to ensure minimal total wire length for a
given floorplan topology. This method optimizes a composite cost
function that balances area and wire length. The approach guarantees
optimality while handling various design constraints such as fixed
frame, I/O pins, pre-placed blocks, boundary blocks, alignment and
abutment, rectilinear and soft blocks, and bounded net delay.
Importantly, it integrates these constraints without compromising the
quality of the result. This method provides an efficient and effective
solution for floorplan refinement, as demonstrated by experimental
results. For future improvements, researchers aim to extend this method
to address routing congestion and buffer insertion during floorplanning.

**T. Takahashi; P.N. Gua; C.K.Cheng; T.Yoshimura \[2\] :** Focused on
the Rectangle Packing (RP) problem, where the goal is to minimize the
enclosing area of rectangular blocks. Given that RP is NP-hard,
heuristic approaches like simulated annealing are commonly used,
iterating through potential placements to find near-optimal solutions. A
key challenge highlighted in their work is the representation of
placements, such as using the coordinates of the lower-left corners of
rectangles. While this method is intuitive, it leads to a vast solution
space and necessitates checking for overlapping blocks. The importance
of efficient representation in these heuristic algorithms is emphasized,
as it directly affects the generation and evaluation of feasible
solutions.

**METHODOLOGY**

a\) Creating graph based on bench file

After creating a Graph class, the first major section of code makes the
user choose which bench file to access. A bench file is a text only file
that describes a circuit. We now parse through the file using regular
expressions. Commented lines and empty lines are ignored while parsing.
The readable lines have relevant information extracted using the regular
expressions p1, p2 and
p3.![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image1.png){width="3.911568241469816in"
height="4.227543744531934in"}

-   p1 matches node keywords like INPUT and OUTPUT

-   p2 captures operands within parenthesis

-   p3 captures operation within parenthesis which is representative of
    > gate type

At the end of it, we also remove the input nodes from the graph because
they aren\'t specific fates and must be taken out of consideration for
arrangement of future tasks like partitioning.

If we have an odd number of nodes, then we add a dummy node as well for
the aforementioned reason.

b\) Graph analysis

![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image7.png){width="3.2343755468066493in"
height="3.6290452755905513in"}

Following that, we add a few elements for visual purposes where we
decide the color and size of nodes based on what gate they represent, as
well as create a list of tuples called edges_with_weights where the edge
weight depends on what node starts at the edge. This is to represent the
possible gate delay.

We then move to creating a directional graph specifically from the Graph
object using the NetworkX library. After this, we move on to generating
the adjacent matrix for the abovementioned graph, where matrix size
corresponds to the number of nodes and values in the matrix represent
edge
weights.![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image9.png){width="4.2198950131233595in"
height="2.8064020122484687in"}

We then use this to execute a shortest path algorithm, which in this
case is Djikstra's algorithm, to show shortest path from various modes
to a specific output (if the user has choice of multiple outputs) and
will show the path taken as well.

c\) Partitioning

The algorithm base we opted for is the Kernighan Lin (KL) algorithm.
This done using a user defined function Kernighan_Lin that takes two
arguments:

-   G: The graph object to be analyzed

-   Init_part: An optional argument of an initial partition

![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image4.png){width="3.2604888451443568in"
height="3.9319335083114613in"}

First we calculate the bisection size. Then if init_part is provided,
then we use those partitions for the processing. If init_part is not
provided then we shuffle a copy of all the nodes and randomize the
initial bipartition.

We then define a cost function based on weight of the edge between two
nodes and then use it while we iterate through a predefined number of
iterations.

We use dictionaries I_List, E_List and D_List to store respective values
about each node (D=E-I) and then loop through all nodes in each
partition. We use these values to calculate G / gain for swapping nodes
and store it in G_List.

We then identify the best ode pair to swap with max gain, and in case of
tie we use a tie-breaker criterion via edge cost. We then swap the pair
and take those nodes of consideration for future swaps. Loop continues
and G_Sum is updated if it crosses the current best (G_Ceil). The
current partition with the best max gain and iteration number is stored
in an entity named Distribution.

**PROGRESS AND RESULTS**

-   We are able to convert any bench file content into the corresponding
    graph of nodes successfully, given that the bench files in
    discussion are stored in the Colab space beforehand. We are also
    able to visualize the graph with each node representing gates and
    the edge weights based on the node that starts the edge.

> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image11.png){width="6.542357830271216in"
> height="3.754744094488189in"}

-   We are able to view the adjacency matrix for the graph as well as
    Djikstra's algorithm to find the shortest path as well as mention
    the same path in output. We are able to do this for different
    outputs, if there are multiple.

> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image2.png){width="2.8429254155730534in"
> height="2.7656255468066493in"}
>
> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image3.png){width="5.901042213473316in"
> height="2.524965004374453in"}

-   Initially for the KL algorithm for Partitioning, we had coded
    through logic of GValue comparison but we kept running into errors
    that we have yet to debug, hence opting for a simpler version of the
    same algorithm where the control parameter is the no of
    inter-partition edges.

> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image6.png){width="4.197916666666667in"
> height="3.350181539807524in"}
>
> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image8.png){width="6.203125546806649in"
> height="3.6076334208223972in"}
>
> ![](vertopal_2a1c76cf5cce4dbf86cc7e194ff4a749/media/image10.png){width="4.284869860017498in"
> height="3.4218755468066493in"}

-   One of the challenges we faced for floorplanning is the creation of
    polish expressions for non-standard graphs that have cycles in it.

-   **Github link**:
    [[https://github.com/AlexMPhil/VLSI-Design-Automation-Tool-via-Python.git]{.underline}](https://github.com/AlexMPhil/VLSI-Design-Automation-Tool-via-Python.git)

-   **Google Colab link**:[[VLSI Major Project
    Space.ipynb]{.underline}](https://colab.research.google.com/drive/1FBbH4zXiq_-YVozcwhHWwlkVbWABD6LA?usp=sharing)

**CONCLUSION AND FUTURE WORK**

-   Develop efficient partitioning algorithms that minimize interconnect
    delays, reduce area, and improve performance, while refining the KL
    algorithm to enhance accuracy and smoothness in partition selection,
    particularly in Gval comparison, ensuring scalability for large
    circuit designs. As of now, the computation time is incredibly high
    for larger circuits.

-   We are currently working on the floor planning grid display and
    algorithm, which we have temporarily fixed on Simulated Annealing
    for the same.

-   After which we need to integrate Routing algorithms to complete the
    physical design flow, followed by optimization to ensure minimal
    wire length, congestion, and power consumption.

-   Implementing other minor changes like

    -   Optimizing the existing algorithms to see if we can achieve
        > faster results

    -   When size of circuit is large and when KL algorithm iterations
        > doesn\'t seem to be improving on score, then we should be able
        > to implement a task ender

    -   Permanent storage of bench files as in built libraries instead
        > of depending on sharing in colab space before run time.

    -   If the circuit has singular output, then code should avoid
        > asking which output to consider.

    -   If the size of the circuit is large, then for each algorithm we
        > should have the option of reducing the image computation and
        > output statements displayed.

**REFERENCES**

1)  ISCAS Netlist

> [[https://sportlab.usc.edu/\~msabrishami/benchmarks.html]{.underline}](https://sportlab.usc.edu/~msabrishami/benchmarks.html)

2)  [[Minimizing wire length in floorplanning \| IEEE Journals &
    > Magazine \| IEEE
    > Xplore]{.underline}](https://ieeexplore.ieee.org/document/1673748)

3)  [[Floorplanning using a tree representation: a summary \| IEEE
    > Journals & Magazine \| IEEE
    > Xplore]{.underline}](https://ieeexplore.ieee.org/document/1242834)
