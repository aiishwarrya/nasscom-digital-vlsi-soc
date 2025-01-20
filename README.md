<div align="center">

# Digital VLSI SoC Design and Planning (8th January to 22nd January)

</div>

---

<div align="center">
  
## Section 1: SKY130 Day 1 - Inception of Open-source EDA, OpenLANE, and SKY130 PDK

</div>

<details>
<summary><h2><strong>📚 Theory for Day 1</strong></h2></summary>



</details>

## Implementation
### Tasks
1. Run the `picorv32a` design synthesis using the OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio and the percentage of D Flip-Flops (DFFs).

### Formulas
```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```

```math
Percentage\ of\ DFFs = Flop\ Ratio \times 100
```

All logs, reports, and results for Section 1 can be found in the following run folder: 
[09-01_09-59](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/tree/main/09-01).


---

### 1. Run picorv32a Design Synthesis Using OpenLANE Flow
Commands to Invoke the OpenLANE Flow and Perform Synthesis:
```bash
# Change directory to the OpenLANE flow directory
cd path/to/openlane_working_dir/openlane

# Enter the OpenLANE Docker container
docker

# Launch the OpenLANE flow in interactive mode
./flow.tcl -interactive

# Load the required OpenLANE package
package require openlane 0.9

# Prep the design to generate necessary files and directories
prep -design picorv32a

# Run synthesis for the design
run_synthesis

# Exit the OpenLANE flow
exit

# Exit the Docker container
exit
```
---
### Screenshots of Running Commands
![Command 1](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss1.png)
![Command 2](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss2.png)
![Command 3](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss3.png)
![Command 4](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss4.png)
![Command 5](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss5.png)
![Command 6](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss6.png)

---
### 2. Calculate the Flop Ratio and Percentage of DFFs
#### Synthesis Statistics Report
![table showing D flipflops and number of cells](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss7.png)
![changes done in the syntheisis,results](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss8.png)
#### Calculation of Flop Ratio and DFF Percentage
```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```


```math
Percentage\ of\ DFFs = 0.108429685 \times 100 = 10.84296854\%
```

### Key Learnings
- Gained hands-on experience with OpenLANE for synthesis.
- Learned to calculate flop ratios and analyze synthesis reports.
- Understood the importance of open-source EDA tools in VLSI workflows.
---

<div align="center">
  
## Section 2: Sky130 Day 2 - Good floorplan vs bad floorplan and introduction to library cells

</div>

<details>
<summary><h2><strong>📚 Theory for Day 2</strong></h2></summary>

The floorplanning phase in VLSI design is crucial to ensure efficient chip design and functionality. 

- A **good floorplan** minimizes wire length, improves performance, and reduces power consumption.
- A **bad floorplan** can lead to congestion, delays, and inefficiencies.

Floorplanning involves defining regions for:
- Core logic
- Input/Output (I/O) pads
- Other design elements within the chip layout

**Library cells** are pre-designed, pre-verified logic components provided in standard cell libraries.  
These cells include:
- Basic logic gates
- Flip-flops
- Multiplexers  

These cells are optimized for specific process technologies such as SKY130 and serve as the building blocks for integrated circuits.

---

## SKY130_D2_SK1 - Chip Floor Planning Considerations

Chip floor planning considerations focus on organizing the placement of various blocks and cells to ensure optimal functionality, performance, and manufacturability.  

Key factors to consider:  
1. **Area Optimization:** Efficient use of silicon area to balance complexity and cost.  
2. **Routing Congestion:** Avoiding overcrowded regions to prevent delays and crosstalk.  
3. **Power Distribution:** Proper placement of power grids and decoupling capacitors to maintain power integrity.  
4. **Thermal Management:** Distributing components to minimize hotspots and ensure thermal balance.  
5. **I/O Placement:** Strategically placing input/output pads to reduce signal delays and ease external connectivity.

An ideal floorplan ensures proper balance among these considerations, resulting in a robust and efficient chip design.

---

## SKY_L1 - Utilization Factor and Aspect Ratio


#### **1. Utilization Factor (UF):**  
The utilization factor is defined as the ratio of the total area occupied by logic cells to the total core area of the chip.

**Formula:**  
**UF = (Total Logic Cell Area) / (Total Core Area)**

- A **high utilization factor** (e.g., 80%) indicates efficient use of silicon but may cause routing congestion.
- A **low utilization factor** provides more space for routing but may increase chip size.

#### **2. Aspect Ratio (AR):**  
The aspect ratio defines the proportions of the core area and is expressed as the ratio of the core height to its width.

**Formula:**  
**AR = (Core Height) / (Core Width)**

- **AR = 1:** Indicates a square layout, ideal for uniform routing.
- **AR ≠ 1:** May result in challenges in power distribution and signal integrity.

Designers aim for:
- A utilization factor between **50% to 80%**.
- An aspect ratio close to **1** to achieve an optimal floorplan and reduce design complexity.

---
## SKY_L2 - Concept of Pre-Placed Cells

Pre-placed cells are essential blocks positioned in fixed locations during the floorplanning stage to optimize chip functionality and layout.  

#### Key Characteristics:
- **Fixed Locations:** These cells, such as macros, memory blocks, or I/O pads, are placed early in the design process.  
- **Routing Optimization:** Helps to streamline routing paths and minimize congestion.  
- **Critical Components:** Often include high-power or performance-critical blocks that influence the overall chip design.  

Proper placement of pre-placed cells ensures better utilization, reduced delays, and improved chip performance.

---
## SKY_L3 - De-Coupling Capacitors

De-coupling capacitors (decaps) are used in integrated circuits to stabilize the power supply and reduce noise in the design.

#### Key Characteristics:
- **Power Stabilization:** They act as local energy reservoirs, supplying current to circuits during transient operations.  
- **Noise Reduction:** Decaps help filter out voltage spikes and reduce electromagnetic interference (EMI).  
- **Placement:** Typically placed close to critical components like macros, clock generators, or power-hungry logic.  

By providing a stable voltage supply, decoupling capacitors ensure consistent performance across the chip.

### Noise Margin Summary:
Noise margin is a measure of a circuit's ability to tolerate noise without compromising its logical operation.  
- **Key Parameters:**
  - **NMH (Noise Margin High):** The difference between the minimum output high voltage and the minimum input high voltage required by the next stage.  
  - **NML (Noise Margin Low):** The difference between the maximum output low voltage and the maximum input low voltage required by the next stage.  
- **Importance:** A higher noise margin ensures better immunity to noise, improving the robustness of the circuit.  

The incorporation of decoupling capacitors aids in maintaining proper noise margins by stabilizing the supply voltage.

---
## SKY_L4 - Power Planning

Power planning is a critical aspect of chip design that ensures a stable power supply to all components. Poor power planning can lead to issues such as ground bounce and voltage droop, which affect the circuit's functionality and reliability.

#### Key Issues in Power Planning:
1. **Ground Bounce:**
   - Occurs when multiple circuits switch simultaneously, causing transient currents in the ground network.
   - Results in a temporary increase in ground voltage, affecting signal integrity.

2. **Voltage Droop:**
   - Happens when the supply voltage dips below the required level due to high current demand or resistance in the power network.
   - Can lead to incorrect logic operation or circuit malfunction.

#### Solution: Providing Multiple VDD and VSS:
- **Multiple Power Rails:**
  - Distributing multiple VDD (power) and VSS (ground) rails across the chip reduces the resistance in the power network.
  - Helps in spreading the current evenly, minimizing ground bounce and voltage droop.

- **Dedicated Power Stripes:**
  - Wide and low-resistance power stripes are added to carry current efficiently and maintain a stable power supply.

- **Decoupling Capacitors:**
  - Placed close to the logic blocks to provide instantaneous power and filter out noise in the supply.

#### Benefits:
- Ensures consistent power delivery to all parts of the chip.
- Improves signal integrity and overall performance.
- Reduces the likelihood of failures due to power-related issues.

---
## SKY_L5 - Pin Placement and Logical Cell Placement Blockage

Pin placement and logical cell placement blockage are critical considerations in physical design to optimize the performance and manufacturability of the chip.

#### Key Concepts:

1. **Netlists of Logic Diagrams:**
   - The netlist is a detailed connection list derived from the logic diagram, representing how various cells (logic gates, flip-flops, etc.) are interconnected.
   - It serves as the foundation for physical placement and routing in the chip design flow.

2. **Input and Output Pin Placement:**
   - **Input Pins:** Positioned near the periphery of the die to allow efficient data entry into the core.
   - **Output Pins:** Placed near the edges of the die for seamless transmission of processed signals.
   - Strategic placement reduces wirelength, minimizes routing complexity, and ensures better signal integrity.

3. **Logical Cell Placement Blockage:**
   - Certain regions in the die are marked as **placement blockages** to prevent logic cells from being placed there.
   - Reasons for blockages include:
     - Reserved areas for power/ground rails.
     - Regions for pre-placed cells like decoupling capacitors or macros.
     - Space allocation for clock trees or other critical structures.
   - Ensures a clean and efficient design without congestion or overlaps.

#### Benefits:
- Optimized routing paths, leading to reduced delays and power consumption.
- Enhanced signal integrity by minimizing parasitics.
- Ensures smooth integration of logical and physical design steps.

---
## SKY130_D2_SK2 - Library Binding and Placement

## SKY_L2 - Optimize Placement using Estimated Wire-Length and Capacitance

Placement optimization focuses on minimizing the wire-length and capacitance in the design to improve performance and reduce power consumption.

#### Key Characteristics:

- **Wire-Length Reduction**:  
  By estimating the wire-length between components, placement can be adjusted to shorten the interconnects, minimizing delays and reducing power consumption.

- **Capacitance Minimization**:  
  Placement optimization reduces parasitic capacitance, which can slow down signal transitions and lead to higher power usage. Shorter wires contribute to lower capacitance.

- **Repeaters Insertion**:  
  Repeaters can be added along long interconnects to boost signal strength, improving the overall delay performance of the design. Proper placement of repeaters helps in minimizing delay and power consumption.

#### Placement Strategy:

- **Cell Placement**:  
  Cells should be placed as close as possible to reduce the wire-length, which directly impacts the overall signal delay. A good placement strategy minimizes wire-length while ensuring the timing constraints are met.

- **Critical Path Optimization**:  
  Focus on placing critical components along the shortest possible paths to reduce the overall delay.

- **Repeaters Location**:  
  Inserting repeaters at optimal positions ensures that long wires do not lead to excessive signal delay, which would otherwise slow down the circuit performance.

By optimizing placement using estimated wire-length and capacitance, designers can ensure that the circuit meets performance goals, reduces power consumption, and improves overall efficiency.

## SKY_L3 - Final Placement Optimization

Final placement optimization ensures the design achieves optimal performance by refining the arrangement of components and addressing critical factors like routing, buffers, and area utilization.

#### Key Concepts:

#### 1. **Abutment:**
   - **Definition**: Aligning or placing components edge-to-edge without gaps to ensure efficient area usage and seamless routing.
   - **Importance**: Reduces unused chip area, simplifies interconnections, and minimizes parasitic effects caused by excessive spacing.
   - **Application**: Used extensively in macros, standard cell rows, and block-level layouts to achieve compact and efficient designs.

#### 2. **Buffer Insertion:**
   - **Purpose**: Buffers are inserted to strengthen weak signals, manage long wire delays, and ensure timing requirements are met.
   - **Key Strategies**:
     - Place buffers along critical paths where delays exceed thresholds.
     - Optimize buffer locations to balance signal integrity and power consumption.
   - **Benefits**:
     - Reduces skew and delay in clock distribution networks.
     - Improves overall signal quality in the design.

#### 3. **Routing of Different Components:**
   - **Critical Routing**: Prioritize the routing of high-speed and power-critical nets (e.g., clock and reset signals).
   - **Minimizing Crosstalk**: Maintain adequate spacing between parallel signal routes to reduce electromagnetic interference (EMI) and crosstalk.
   - **Layer Optimization**: Use metal layers effectively for signal routing, with higher layers for global signals and lower layers for local interconnections.
   - **Routing Congestion Analysis**: Identify and resolve bottlenecks in densely packed regions to prevent design rule violations.

#### Final Optimization Goals:
- Ensure proper alignment and abutment of all components to achieve efficient area utilization.
- Use buffers strategically to manage delays and improve signal integrity.
- Optimize routing paths to minimize wire-length, parasitics, and congestion.

By performing final placement optimization with careful attention to abutment, buffer insertion, and routing, designers can achieve a highly efficient and reliable VLSI design.

## SKY_L4 - Need for Libraries and Characterization

Libraries and their characterization are essential for achieving efficient and accurate VLSI designs. They provide the foundation for processes like logic synthesis, floorplanning, placement, clock tree synthesis (CTS), routing, and static timing analysis (STA).

#### Key Concepts:

#### 1. **Logic Synthesis**:
   - **Definition**: The process of converting high-level design descriptions (HDLs) into a gate-level netlist using standard cells from the library.
   - **Role of Libraries**: Libraries provide pre-characterized cells with timing, power, and area information, which guides the synthesis process to meet design constraints.
   - **Goal**: Optimize for speed, power, and area while ensuring logical correctness.

#### 2. **Floorplanning**:
   - **Definition**: Laying out the chip’s basic structure by defining the placement of macros, standard cell regions, and I/O pins.
   - **Library Dependency**: Accurate area and power characterization from libraries help define realistic floorplan dimensions.
   - **Importance**: Ensures that critical components are placed efficiently to minimize routing complexity and interconnect delays.

#### 3. **Placement**:
   - **Definition**: Arranging standard cells and macros within the floorplan to minimize wire-length and meet timing constraints.
   - **Library Role**: Cell timing and capacitance data guide placement tools to position cells for optimal performance.

#### 4. **Clock Tree Synthesis (CTS)**:
   - **Purpose**: Generate a clock distribution network that delivers the clock signal with minimal skew and optimal delay.
   - **Library Support**:
     - Buffers and inverters characterized in the library are used to build the clock tree.
     - Accurate delay models ensure a balanced clock tree.

#### 5. **Routing**:
   - **Definition**: Connecting all components in the design using metal layers based on the netlist.
   - **Library Dependency**:
     - Parasitic models from libraries are used for accurate resistance and capacitance calculations.
     - Guides wire width, spacing, and layer usage to meet design rules and minimize signal degradation.

#### 6. **Static Timing Analysis (STA)**:
   - **Definition**: A method to verify that the design meets timing constraints without requiring dynamic simulation.
   - **Library Role**:
     - Provides timing models for all cells, including delays, setup/hold times, and transition times.
     - Enables accurate path delay calculation and ensures the design operates reliably under all conditions.

#### Why Libraries and Characterization are Crucial:
- **Consistency**: Pre-characterized cells ensure predictable performance across tools and processes.
- **Efficiency**: Provides necessary data for optimization in all stages of the design flow.
- **Accuracy**: Enables precise timing, power, and area analysis for a robust design.

By leveraging libraries and their detailed characterization, designers can efficiently navigate through logic synthesis, floorplanning, placement, CTS, routing, and STA to achieve high-quality VLSI designs.

---

## SKY130_D2_SK3 - Cell Design and Characterization Flows

This task involves the creation and evaluation of a standard cell, focusing on its layout design and performance characterization. The primary goal is to ensure the cell adheres to design rules and meets desired electrical parameters.

#### Overview:

#### 1. **Cell Design**:
   - A standard logic cell, such as an inverter, was designed using the Magic tool.
   - The layout was created following the design rules defined by the SKY130 PDK to ensure manufacturability and performance reliability.

#### 2. **SPICE Netlist Extraction**:
   - Extracted the netlist from the layout for simulation and analysis.
   - This step ensures accurate representation of the design for further characterization.

#### 3. **Characterization**:
   - Performed simulations to analyze key parameters:
     - **Propagation delay**: Time taken for the signal to transition through the cell.
     - **Power consumption**: Evaluated under various operating conditions.
     - **Output waveforms**: Verified functional correctness and signal integrity.
   - Timing parameters were extracted to prepare the cell for integration into the standard-cell library.

#### Results:
- Successfully designed and characterized the standard cell.
- Verified compliance with DRC and functionality through simulations.

This implementation lays the groundwork for integrating custom cells into a larger design flow.

---

## SKY_L3 - Layout Design Step

The layout design step involves converting a circuit design into a physical layout that adheres to design rules, ensuring manufacturability and functionality.

#### Overview:

#### 1. **Network Graphs and Euler's Path**:
   - Created network graphs for NMOS and PMOS configurations.
   - Used Euler’s path to optimize the connectivity and layout topology for reduced complexity.

#### 2. **Stick Diagram**:
   - Translated the network graph into a stick diagram to visualize the arrangement of components and interconnections.
   - Ensured proper alignment of layers and minimized overlaps.

#### 3. **Layout Design in Magic**:
   - Converted the stick diagram into a detailed layout using the Magic tool.
   - Verified the layout with **Design Rule Check (DRC)** to ensure compliance with the SKY130 PDK design rules.

#### 4. **Generating Outputs**:
   - Exported the layout to:
     - **GDSII File**: For physical design integration into the larger chip design.
     - **SPICE Netlist (.cir)**: For electrical simulation and characterization.

#### Summary:
This process bridges the gap between the circuit design and the physical layout. By leveraging network graphs and layout optimization techniques, the generated layout ensures manufacturability while meeting performance requirements.

---
## SKY_L4 - Typical Characterization Flow

The characterization flow ensures that a standard cell is accurately analyzed for its timing, power, and noise characteristics. This involves simulating its behavior under defined conditions.

#### Steps in the Characterization Flow:

#### 1. **Read Model Files**:  
   - Load all required model files, including process-specific data from the SKY130 PDK.

#### 2. **Read Extracted SPICE Netlist**:  
   - Import the SPICE netlist of the designed cell for simulation.

#### 3. **Define Buffer Behavior**:  
   - Specify the functional behavior of the cell (e.g., inverter or buffer) to guide the simulation.

#### 4. **Read Sub-Circuits**:  
   - Include necessary sub-circuits for a complete and accurate simulation setup.

#### 5. **Attach Power Sources**:  
   - Add appropriate power and ground connections to mimic real operating conditions.

#### 6. **Apply Stimulus**:  
   - Provide input waveforms or signals to drive the cell.

#### 7. **Provide Output Capacitance**:  
   - Attach load capacitance to simulate the effect of connecting the cell to subsequent stages.

#### 8. **Run Simulation Commands**:  
   - Execute commands such as transient, AC, or DC simulations to evaluate cell behavior.

#### Tools and Outputs:
- **Tool Used**: GUNA software was employed for detailed characterization.  
- **Outputs**: Timing, power, and noise characteristics were extracted and exported into `.lib` (library) files for integration into the standard-cell library.

#### Summary:
This characterization flow ensures the standard cell meets performance requirements and is ready for integration into digital design flows. GUNA aids in obtaining accurate results for timing, noise, and power analysis.

---

## SKY130_D2_SK4 - General Timing Characterization Parameters

Timing characterization evaluates critical parameters such as propagation delay, setup time, hold time, clock-to-Q delay, and transition time. These metrics ensure that cells perform reliably under varying conditions like input transitions and load capacitance. Tools like GUNA or SPICE are used to simulate and extract these parameters, with the results stored in `.lib` files for synthesis and static timing analysis (STA). Proper characterization forms the backbone of efficient and robust digital designs.

---

## SKY_L1 - Timing Threshold Definitions

This section focuses on timing characterization and the critical timing threshold definitions used to evaluate signal transitions.

#### Key Timing Threshold Definitions:
#### 1. **Slew Low Rise Threshold (slew_low_rise_thr)**:  
   Defines the lower voltage level for the rising edge of a signal transition.

#### 2. **Slew High Rise Threshold (slew_high_rise_thr)**:  
   Defines the upper voltage level for the rising edge of a signal transition.

#### 3. **Slew Low Fall Threshold (slew_low_fall_thr)**:  
   Indicates the lower voltage level for the falling edge of a signal transition.

#### 4. **Slew High Fall Threshold (slew_high_fall_thr)**:  
   Indicates the upper voltage level for the falling edge of a signal transition.

These thresholds ensure precise timing analysis by identifying critical voltage points during signal transitions.

#### Summary:  
Understanding and defining timing thresholds is essential for accurate characterization of signal transitions. These parameters play a pivotal role in evaluating the performance of cells in digital designs.

---

## SKY_L2 - Propagation Delay and Transition Time

This section covers propagation delay, the importance of threshold points, and key concepts related to transition times.

#### Key Concepts:
#### 1. **Propagation Delay**:  
   The time taken for a signal to propagate from the input to the output of a cell. It is typically measured between specified threshold points, such as 50% of the input and output voltages.

#### 2. **Importance of Threshold Points**:  
   Threshold points, like 10%, 50%, and 90%, are crucial for accurate measurement of signal transitions and propagation delays, ensuring consistent timing analysis.

#### 3. **Slew Formulas**:  
   Slew rate determines how quickly a signal changes from one voltage level to another. It is calculated using the voltage difference over the time interval between threshold points.

#### 4. **Transition Time**:  
   - **Rise Transition**: The time it takes for the signal to rise from a lower threshold (e.g., 10%) to a higher threshold (e.g., 90%).  
   - **Fall Transition**: The time it takes for the signal to fall from a higher threshold (e.g., 90%) to a lower threshold (e.g., 10%).

#### 5. **Output Current and Voltage Waveform**:  
   Introduction to the significance of output waveforms in characterizing a cell's timing behavior and analyzing its performance.

#### Summary:  
Understanding propagation delay and transition time is essential for precise timing analysis. These parameters play a critical role in evaluating signal integrity and ensuring robust circuit performance.

---

</details>

## Implementation of SKY130_D2_SK1 - SKY_L5 - Pin placement and logical cell placement blockage to SKY_L8 - Review floorplan layout in Magic

### Section 2 Tasks:
1. **Run `picorv32a` design floorplan using OpenLANE flow and generate necessary outputs.**
2. **Calculate the die area in microns from the values in the floorplan DEF file.**
3. **Load the generated floorplan DEF file into the Magic tool and explore the floorplan layout.**

---

### 1. Run `picorv32a` Design Floorplan Using OpenLANE Flow

#### Commands to invoke OpenLANE flow and perform floorplan:
```bash
# Change directory to OpenLANE flow directory
cd ~/tools/openlane

# Enter the OpenLANE Docker container
docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21

# Launch OpenLANE in interactive mode
./flow.tcl -interactive

# Load the required OpenLANE package
package require openlane 0.9

# Prepare the design for floorplan
prep -design picorv32a

# Run synthesis
run_synthesis

# Execute the floorplan
run_floorplan
```

#### **Screenshot Outputs:**
![Floorplan run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-1.png)

---

### 2. Calculate Die Area in Microns from the Floorplan DEF Values

#### Floorplan DEF Observations:
- **Unit Distance:** 1000 = 1 micron  
- **Die Width (in unit distance):**  
  660685 - 0 = **660685**  
- **Die Height (in unit distance):**  
  671405 - 0 = **671405**  
- **Conversion to microns:**  
  - **Die Width (in microns):**  
    Die Width = 660685 / 1000 = **660.685 μm**  
  - **Die Height (in microns):**  
    Die Height = 671405 / 1000 = **671.405 μm**  
- **Area of Die (in square microns):**  
  Area = 660.685 × 671.405 = **443587.212425 μm²**

#### **Screenshot Outputs:**
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-2.png)

---

### 3. Load Generated Floorplan DEF in Magic Tool

#### Commands to Load Floorplan DEF:
```bash
# Change directory to the generated floorplan DEF path
cd /home/vsduser/09-01_09-59/results/floorplan

# Load the DEF file in Magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

```

#### Observations in Magic:
- Equidistant placement of ports
- Decap cells and tap cells  
- Diagonally equidistant tap cells  
- Unplaced standard cells at the origin  

#### **Screenshot Outputs:** Magic visualization of the floorplan

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-3.png)

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-4.png)  

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-5.png)

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-6.png)

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-7.png)

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-8.png)

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-9.png)

---

## Implementation of SKY130_D2_SK2 - SKY_L5 - Congestion aware placement using RePlAce

This task involves running a congestion-aware placement of the `picorv32a` design using the OpenLANE flow and generating the necessary outputs. The placement step ensures standard cells are legally placed with minimal congestion, preparing the design for further stages of the flow.

---
### Steps to Run Congestion Aware Placement:

### 1. **Run Placement**:
   Use the default congestion-aware placement command in the OpenLANE flow:

   ```bash
   run_placement
   ```

#### Screenshots of Placement Run:

![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-12.png)

---

### 2. **Load Generated Placement DEF in Magic Tool**:
   To explore the placement output, load the generated DEF file in the Magic tool.

### Commands to Load Placement DEF:
   Open a new terminal and execute the following:

   ```bash
   # Change directory to the folder containing the generated placement DEF
   cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/09-01_09-59/results/placement/

   # Load the placement DEF in Magic tool
   magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
   lef read ../../tmp/merged.lef def read picorv32a.placement.def &
   ```

#### Screenshots of Placement DEF in Magic:
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-10.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-11.png)

---

3. **Exit OpenLANE Flow**:
   Once the placement step is complete, exit the OpenLANE environment.

### Commands to Exit:

```bash
   # Exit from OpenLANE flow
   exit

   # Exit from OpenLANE flow docker sub-system
   exit
```

---

By following the above steps, we successfully ran congestion-aware placement for the `picorv32a` design, loaded the placement DEF in the Magic tool for visualization, and verified the standard cells' placement.

---

<div align="center">

## Section 3: Sky130 Day 3 - Design library cell using Magic Layout and ngspice characterization

</div>

<details>

<summary><h2><strong>📚 Theory for Day 3</strong></h2></summary>

## SKY130_D3_SK1 - Labs for CMOS Inverter ngspice Simulations

This section begins with a revision of IO placer concepts and their practical implementation.

---

### SKY_L1 - SPICE Deck Creation for CMOS Inverter

#### Key Concepts:
#### 1. **SPICE Deck Composition**:  
   The SPICE deck is a netlist defining the circuit's components, their connectivity, and simulation parameters. For a CMOS inverter, it includes:  
   - **PMOS and NMOS Transistors**: Defines their parameters like width (W) and length (L).  
   - **Output Load Capacitor**: Represents the load driven by the inverter.  

#### 2. **Steps for SPICE Deck Creation**:  
   - **Component Connectivity**: Establish connections between PMOS, NMOS, input node, output node, and supply voltages.  
   - **Component Values**: Assign proper values for transistor dimensions, load capacitance, and supply voltages.  
   - **Identifying Nodes**: Define nodes for input, output, VDD, GND, and internal connections.  
   - **Naming Nodes**: Use clear and consistent names for nodes to maintain readability and ease of debugging.  
   - **Writing the SPICE Deck**: Compile the component definitions, connectivity, and simulation commands into a single file.

#### Summary:  
Creating a SPICE deck is a critical step in circuit simulation, ensuring accurate representation of the CMOS inverter. Proper node identification, connectivity, and parameter assignment are essential for effective simulation and analysis.

---

### SKY_L2 - SPICE Simulation Lab for CMOS Inverter

#### Key Concepts:
In this step, we extend the SPICE deck from the previous section by including simulation commands and model files.

#### 1. **Simulation Setup**:  
   - **Cload, VDD, Vin**: The output load capacitor (Cload), supply voltage (VDD), and input voltage (Vin) are defined for the simulation.  
   - **Simulation Commands**:  
     - **.op**: Performs an operating point analysis to find the DC values of all nodes.  
     - **.dc**: Runs a DC sweep to analyze the response of the circuit over a range of input voltages.  
   - **Model Files**: Describes the characteristics of the PMOS and NMOS transistors for accurate simulation results.

#### Summary:  
This simulation step models the CMOS inverter’s behavior under different input conditions, helping to analyze its performance and optimize the design.

---

### SKY_L3 - Switching Threshold Vm

#### Key Concepts:
The video focuses on the evaluation of the static behavior of the CMOS inverter, particularly the **switching threshold (Vm)**.

#### 1. **Static Behavior Evaluation**:  
   - The switching threshold (Vm) is the input voltage at which the output voltage of the CMOS inverter transitions from low to high or vice versa.  
   - Vm is crucial for determining the inverter's switching point, where the output voltage is approximately halfway between VDD and GND.

#### 2. **Importance of Vm**:  
   - Ensures proper operation of the inverter, defining the point where the inverter correctly switches states, avoiding issues like slow transitions or incorrect logic levels.

#### Summary:  
Evaluating the switching threshold helps to characterize the inverter's static performance and optimize its behavior for reliable operation in digital circuits.

---

## SKY130_D3_SK2 - Inception of Layout – CMOS Fabrication Process  

### SKY_L1 - Create Active Regions  

This section introduces the 16-mask CMOS fabrication process, focusing on the creation of active regions.

#### **Steps in the Process**:  
#### 1. **Select a Substrate**:  
   Begin with a silicon wafer as the base material for the CMOS fabrication.  

#### 2. **Create Active Regions**:  
   Define areas for transistor activity using photolithography techniques.  

#### 3. **Deposit Substances (e.g., Photoresist)**:  
   Apply a thin layer of photoresist material to the wafer's surface for pattern definition.  

#### 4. **Mask Removal**:  
   Use photomasks to expose the photoresist selectively, enabling the patterning of active regions.  

#### 5. **Resist Removal**:  
   Chemically remove the exposed or unexposed photoresist, depending on the process (positive or negative resist).  

#### 6. **LOCOS (Local Oxidation of Silicon)**:  
   Perform LOCOS to isolate active regions and create field oxides.  

#### **Summary**:  
The creation of active regions is a fundamental step in the CMOS fabrication process. It involves substrate preparation, photolithography, and isolation techniques like LOCOS to define transistor areas precisely.

---
### SKY_L2 - Formation of N-Well and P-Well  

This section discusses the formation of the N-well and P-well, crucial steps in the CMOS fabrication process.

#### **Steps in the Process**:  
#### 1. **Formation of P-Well**:  
   - Boron ions are implanted into the substrate to create the P-well.  
   - The process uses **ion implantation** to ensure precision.

#### 2. **Formation of N-Well**:  
   - Phosphorus ions are implanted into the substrate to create the N-well.  
   - Similar to the P-well formation, ion implantation ensures accurate doping.  

#### 3. **High-Temperature Furnace Process**:  
   - The substrate undergoes a **twin-tub process** in a high-temperature furnace.  
   - This step diffuses the dopants, forming the wells with proper depth and concentration.  

#### **Summary**:  
The formation of N-well and P-well involves selective doping using boron and phosphorus, respectively, followed by high-temperature treatment. These wells provide the foundation for CMOS transistors in the twin-tub process.

---

### SKY_L3 - Formation of Gate Terminal

#### Key Steps:
#### 1. Threshold Voltage Equation:  
   - The threshold voltage equation is considered to ensure proper transistor operation.  
   - Adjustments to doping concentration are made accordingly.  

#### 2. Masking:  
   - A mask is applied to define the regions where doping is to be introduced.  

#### 3. Doping for NMOS and PMOS:  
   - For NMOS: Boron is introduced through ion implantation, ensuring it remains on the surface.  
   - For PMOS: A similar process is followed with appropriate dopants.  

#### 4. Deposition of Poly-Silicon Layer:  
   - A poly-silicon layer is deposited to serve as the gate terminal material.  
   - A low-resistance layer is formed to ensure efficient current control and switching.

### Summary:  
The gate terminal formation process combines precise doping and material deposition to create a reliable control structure for transistors. It ensures optimal threshold voltage and enhances the electrical performance of the CMOS device.

---

### SKY_L4 - Lightly Doped Drain (LDD) Formation

#### Key Steps:
#### 1. Hot Electron Effect:  
   - LDD formation helps mitigate the hot electron effect by reducing the electric field at the drain junction.  

#### 2. Short Channel Effect:  
   - LDD structures are designed to minimize the short channel effect in modern CMOS devices.  

#### 3. Plasma Anisotropic Etching:  
   - Plasma anisotropic etching is used to create precise patterns for the lightly doped regions.  

#### 4. Side Wall Spacers:  
   - Side wall spacers are introduced to separate the lightly doped regions from the heavily doped source and drain areas.  

#### Summary:  
LDD formation addresses critical challenges in CMOS technology, such as the hot electron effect and short channel effects, ensuring the reliability and performance of scaled-down transistors.

---

### SKY_L5 - Formation of Source and Drain

#### Key Steps:
#### 1. Addition of Screen Oxide:  
   - A thin layer of screen oxide is deposited to prevent channeling during ion implantation.  

#### 2. High-Temperature Furnace:  
   - The wafer is subjected to a high-temperature furnace to activate the dopants and anneal the implanted regions.  

#### Summary:  
The formation of source and drain involves precise control of doping and thermal processing to ensure accurate transistor behavior and optimal performance.

---

### SKY_L6 - Local Interconnect Formation

The process of local interconnect formation begins with the removal of thin oxide layers previously deposited over the Source and Drain (S, D) regions, opening these areas for contact. Titanium is then sputtered onto the wafer surface to facilitate the formation of interconnects. Following this, the wafer is subjected to high-temperature annealing, typically between 650 and 700 degrees Celsius, which results in the creation of titanium silicide (TiSi) at the contact regions. To ensure surface cleanliness and remove impurities, the wafer undergoes RCA cleaning as a final step. This sequence ensures reliable electrical connections for the Source and Drain, essential for device functionality.

---

### SKY_L7 - Higher Level Metal Formation

#### 1. **Deposition of SiO₂**:  
   A layer of silicon dioxide (SiO₂) is deposited, doped with phosphorus and boron for added protective properties.

#### 2. **Planarization with CMP**:  
   Chemical Mechanical Planarization (CMP) is performed to create a smooth and even surface.

#### 3. **Drilling Contact Holes**:  
   Contact holes are drilled into the SiO₂ layer to facilitate electrical connections.

#### 4. **Aluminum Deposition**:  
   An aluminum layer is deposited over the surface to complete the interconnection process, ensuring efficient electrical pathways.
   
---

## SKY130_D3_SK3 - Sky130 Tech File Labs

#### Overview
The SKY130_D3_SK3 lab series focuses on using the SkyWater 130nm technology file to perform simulations, layout design, and analysis. These labs include key steps like editing SPICE model files, running ngspice simulations, and analyzing the output for critical parameters.

### SKY_L3 - Lab Introduction to Magic Tool Options and DRC Rules

#### Summary

This video lab introduced the **Magic tool** and its website contents. It provided an overview of:
- **Magic Tool Options**: Basic commands, navigation, and setup for layout creation.
- **DRC Rules**: Design Rule Checks, including the guidelines and parameters to ensure layouts adhere to fabrication constraints.
  
---

## SKY130_D4_SK2 - Timing analysis with ideal clocks using openSTA

### SKY_L1 - Setup timing analysis and introduction to flip-flop setup time


</details>

## Implementation of SKY_L0 - IO Placer Revision

To optimize the equidistant placement of cells during IO placement, we used the following command:

```bash
set ::env(FP_IO_MODE) 2

```
![input change command](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-1.png)

## Implementation of SKY_L5 - Lab steps to git clone vsdstdcelldesign

This task involves cloning a GitHub repository containing a custom inverter standard cell design, exploring its layout in Magic, performing spice extraction, editing the spice model file, and running post-layout simulations.

#### **Steps Implemented**:

#### **1. Clone the Custom Inverter Design**:
- Clone the repository into the OpenLANE directory.
  
  ```bash
  # Change directory to OpenLANE
  cd Desktop/work/tools/openlane_working_dir/openlane

  # Clone the repository with custom inverter design
  git clone https://github.com/nickson-jose/vsdstdcelldesign

  # Change into repository directory
  cd vsdstdcelldesign
  ```

#### **2. Load Custom Inverter Layout**:
- Copy the Magic `.tech` file to the repository directory for easy access.
- Open the custom inverter layout in Magic.

  ```bash
  # Copy magic tech file to the repo directory
  cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

  # Check contents to ensure everything is present
  ls

  # Command to open custom inverter layout in Magic
  magic -T sky130A.tech sky130_inv.mag &
  ```

  #### Screenshots of the following commands
  
![command run ](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-2.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-3.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-4.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-5.png)

---

## Implementation of SKY_L8 - Lab introduction to Sky130 basic layers layout and LEF using inverter

In this lab, we explore the layout of the inverter to identify PMOS and NMOS using the `%what` command in the `tkcon.tcl` window. The focus is on analyzing the connections between the components, verifying their placement, and understanding how basic layers are represented in the layout.

 #### Screenshots

![identifying pmos and nmos](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-6.png)
![identifying pmos and nmos](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-7.png)

---
## Implementation of SKY_L9 - Lab Steps to Create Standard Cell Layout and Extract SPICE Netlist

This lab demonstrates the process of extracting the entire standard cell layout into a SPICE netlist using commands. The focus is on converting the physical layout into a SPICE-compatible format for further simulation and analysis.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

 #### Screenshots

![Extraction](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-8.png)
![Extraction](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-9.png)

---

## Implementation of SKY130_D3_SK3 

In this lab, we edited the SPICE model file to prepare it for analysis through simulation. The unit distance in the layout grid was also measured to ensure precision. Once the final SPICE file was edited, it was ready for ngspice simulation.

### 1. Editing the SPICE Model File
After ensuring the layout grid was measured correctly, we edited the SPICE file for the inverter. This step prepares the file for further simulation and analysis. The final edited SPICE file was saved and set up for the ngspice simulation process.

**Screenshots of the final edited SPICE file:**
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-10.png)

### 2. Post-layout ngspice Simulations
The next step involved running the post-layout simulation using ngspice. We used the following commands to load the SPICE file and run the simulation:

```bash
ngspice sky130_inv.spice
```

After the simulation was loaded, we generated the plot of the output versus time using the following command:

```bash
plot y vs time a
```

**Screenshots from ngspice run:**
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-11.png)
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-12.png)

### 3. Generated Plot
Once the ngspice simulation was complete, the plot was generated to visualize the results.

**Screenshot of the generated plot:**
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-13.png)

### 4. Rise Transition Time Calculation
The rise transition time was calculated by measuring the time it took for the output to rise from 20% to 80%. The results were as follows:

**Rise Transition Time:**
- Rise Time = T_80% - T_20% = 2.64 V - 660 mV = 0.06396 ns = 63.96 ps

**Screenshots of the rise time:**
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-14.png)
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-20.png)
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-18.png)
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-19.png)

### 5. Rise Cell Delay Calculation
The rise cell delay was calculated by measuring the time for the output to rise from 50% to 50%, and the result was:

**Rise Cell Delay:**
- Rise Cell Delay = T_50% - T_50% = 2.21144 ns - 2.15008 ns = 0.06136 ns = 61.36 ps

**Screenshots of the rise cell delay:**
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-16.png)
![ngspice](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-17.png)

---

### Fixing DRC Issues in Skywater Process Magic Tech File

This document provides step-by-step instructions to identify and correct issues in the DRC section of the Skywater process's old Magic tech file.

#### Reference Link
- Sky130 Periphery Rules: [Skywater PDK Periphery Rules](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

#### Steps to Reproduce and Fix DRC Issues

#### 1. Download and View Corrupted Skywater Process Magic Tech File

```bash
# Change to home directory
cd

# Download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Extract the compressed lab files
tar xfz drc_tests.tgz

# Change to the lab directory
cd drc_tests

# List all files in the current directory
ls -al

# View the .magicrc file
gvim .magicrc

# Open the Magic tool with better graphics
magic -d XR &
```

#### Screenshots
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-21.png)
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-22.png)

### 2. Issue: Incorrect Implementation of `poly.9` Rule

#### Problem
- The `poly.9` rule was not detecting violations for spacing < 0.48μ.

#### Correction
- Modified the rule in the `sky130A.tech` file to include proper spacing checks.

```bash
# Load the updated tech file in Magic
tech load sky130A.tech

# Re-run the DRC check to identify updated errors
drc check

# Select the region displaying errors and view messages
drc why
```

#### Screenshots
- loading poly
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-25.png)
- updating the `sky130A.tech`file
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-29.png)
- magic window with rule implemented
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-30.png)

### 3. Issue: Incorrect Implementation of `nwell.4` Rule

#### Problem
- The `nwell.4` rule did not detect missing taps in the `nwell` region.

#### Correction
- Updated the rule in the `sky130A.tech` file for accurate detection of missing taps.

```bash
# Load the updated tech file in Magic
tech load sky130A.tech

# Change the DRC style to full
drc style drc(full)

# Re-run the DRC check to identify updated errors
drc check

# Select the region displaying errors and view messages
drc why
```

#### Screenshots
- Updating `sky130A.tech` file to correct the error
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-31.png)
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-32.png)

- Updated drc check
![commands](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-33.png)

---

<div align="center">
  
## Section 4: Sky130 Day 4 - Pre-layout timing analysis and importance of good clock tree

</div>

<details>
<summary><h2><strong>📚 Theory for Day 4</strong></h2></summary>

---

### **SKY_L4 - Introduction to Delay Tables**  

#### **Power-Aware Clock Tree Synthesis (CTS):**  
Power-aware CTS is a specialized approach to designing clock trees in digital circuits. It focuses on minimizing power consumption while maintaining the performance of the clock tree. The goal is to reduce dynamic and leakage power without compromising clock integrity or timing accuracy. This involves balancing factors such as skew, latency, and power dissipation during the synthesis process.

#### **Delay Tables - Introduction:**  
A delay table is a structured data representation that provides delay values for various cell types under different operating conditions. It includes information about:  
1. **Input Slew:** The rate at which the input signal changes.  
2. **Output Load:** The load the cell drives, typically measured in capacitance.  
3. **Timing Characteristics:** Delay values for rising and falling edges, capturing the cell’s behavior under specified conditions.  

These tables help design tools accurately calculate path delays and optimize timing, ensuring the design meets performance constraints.

---

### **SKY_L5 - Delay Table Usage Part 1 & SKY_L6 - Delay Table Usage Part 2**  

#### **Levels of Buffering**  
Buffering is a crucial aspect of circuit design, used to:  
1. Strengthen weak signals.  
2. Drive larger loads efficiently.  
3. Reduce delays by appropriately placing buffers between high-capacitance nodes.  

The placement and sizing of buffers significantly influence timing and power performance.  

#### **Delay Tables for Buffer Sizes**  
Delay tables provide timing information for various buffer sizes under different conditions:  
- **Size 1 Buffer:** A smaller buffer optimized for driving low loads with minimal power.  
- **Size 2 Buffer:** A larger buffer capable of driving higher loads at the cost of slightly increased power and area.  

Each buffer size has its own delay characteristics, captured in its respective delay table.  

#### **Input Slew and Output Load Impact**  
1. **Input Slew:** Refers to how quickly a signal transitions from low to high or vice versa. A slower slew can increase delay, while a faster slew reduces it.  
2. **Output Load:** Represents the load the buffer drives, typically measured in capacitance. Higher loads lead to increased delay, emphasizing the importance of matching buffer strength to load requirements.  

Understanding these parameters ensures efficient circuit design with optimal performance and power trade-offs.  

---

## **SKY130_D4_SK2 - Timing Analysis with Ideal Clocks Using OpenSTA**

### **SKY_L1 - Setup Timing Analysis and Introduction to Flip-Flop Setup Time**

#### 1. **Introduction**
   - This session focuses on **timing analysis using ideal clocks**, analyzing the relationship between the launch clock, capture clock, and combinational delays.  
   - The primary goal is to ensure data stability for flip-flops by adhering to setup timing constraints.

#### 2. **Timing Analysis with a Single Clock**
   - A single clock is utilized as both the **launch clock** and **capture clock**.
   - The main condition for timing is:  
     - **Combinational Delay < Clock Period**  
   - This ensures the signal reaches the capture point within the designated clock cycle.

#### 3. **Introduction of a Capture Flip-Flop**
   - A **capture flip-flop** is added to analyze more intricate timing constraints.  
   - The updated condition becomes:  
     - **Combinational Delay < T - S**  
     Where:  
     - **T**: Clock period.  
     - **S**: Setup time of the flip-flop.

#### 4. **Important Notes**
   - **Setup Time (S):**  
     - The minimum duration before the clock edge during which the input signal must remain stable at the flip-flop.  
   - This timing analysis forms the foundation for future exploration of complex clock domains and timing paths.

---

### **SKY_L2 - Introduction to Clock Jitter and Uncertainty**

Clock jitter and clock uncertainty are crucial concepts in timing analysis, building upon the principles discussed in the previous session. Clock jitter refers to the variation in the timing of clock edges caused by factors such as power supply noise, temperature fluctuations, and process variations. On the other hand, clock uncertainty encompasses all timing variations, including jitter and skew between different clock paths. A key takeaway from this session is the concept of the **timing window**, which represents the interval during which data must meet setup and hold time requirements. This timing window ensures that the data is captured reliably, even in the presence of clock-related variations.

---

## SKY130_D4_SK3 - Clock Tree Synthesis (TritonCTS) and Signal Integrity   

#### Overview   
Clock Tree Synthesis (CTS) is a critical phase in digital design, where the goal is to ensure that the clock signal reaches every sequential element (e.g., flip-flops) in the design with minimal skew and within the required timing constraints. In this session, we explore the concepts of clock distribution, skew, and the role of buffering and repeaters to maintain signal integrity across the design.  

#### Key Concepts   
#### 1. **Clock Tree Synthesis (CTS):**   
   - CTS involves the generation of a clock distribution network to minimize skew (the timing difference between clock signals arriving at different elements).  
   - Tools like TritonCTS are used to implement and optimize the clock tree to meet timing and power requirements.  

#### 2. **Signal Integrity:**   
   - The integrity of the clock signal is critical to prevent timing violations.  
   - Buffering and repeaters are employed to strengthen weak signals and reduce RC delays (resistance-capacitance delays) that degrade the clock signal over long distances.  

---

### SKY_L1 - Clock Tree Routing and Buffering Using H-Tree Algorithm   

#### Overview   
The H-Tree algorithm is an effective approach for routing clock signals, ensuring balanced distribution and minimized skew across the design. This session focuses on the role of H-Tree concepts in clock tree routing, buffering, and repeater insertion.  

#### Key Concepts   
#### 1. **H-Tree Algorithm for Clock Routing:**  
   - The H-Tree structure provides a symmetrical clock routing network, ensuring equal path lengths from the clock source to all sequential elements.  
   - It minimizes skew by maintaining consistent delays across all branches of the tree.  

#### 2. **Buffering and Repeaters:**  
   - Buffers and repeaters are strategically placed along the clock tree to drive the signal across large distances without distortion or delay.  
   - These elements help address signal integrity challenges like cross-talk and excessive capacitance. 

---

### SKY_L2 - Crosstalk and Clock Net Shielding  

#### Overview  
Crosstalk, glitches, and clock net shielding are critical aspects of maintaining signal integrity and ensuring reliable circuit operation. This session focuses on setup timing analysis, the effects of crosstalk-induced delta delay, and techniques like clock net shielding to mitigate these issues effectively.  

#### Key Concepts  

#### 1. **Setup Timing Analysis:**  
   - Ensures that data arrives at the input of a flip-flop before the triggering edge of the clock signal.  
   - Violations in setup timing can lead to incorrect circuit behavior and data corruption.  

#### 2. **Crosstalk and Delta Delay:**  
   - Crosstalk occurs when signals in nearby wires interfere, causing unexpected voltage variations.  
   - This interference results in delta delay, which impacts signal propagation time and can affect timing margins.  
   - Skew caused by crosstalk disrupts synchronization between clock signals, impacting overall performance.  

#### 3. **Glitch and Its Impact:**  
   - A glitch is a temporary, unintended voltage spike caused by crosstalk or timing inconsistencies.  
   - Glitches on clock nets can propagate, leading to power wastage, functional errors, and timing violations.  

#### 4. **Clock Net Shielding:**  
   - Shielding techniques involve placing grounded or fixed-voltage nets near clock nets to reduce noise.  
   - These methods minimize crosstalk and ensure stable, consistent clock propagation.  
   - Shielding also prevents glitches and helps maintain proper timing across the design.

Here is the content in your GitHub format:  

---

## SKY130_D4_SK4 - Timing Analysis with Real Clocks Using OpenSTA  

### Overview  
Timing analysis is a crucial step in digital design verification, ensuring that the design meets all timing requirements. In this session, we explore the concepts of setup and hold time analysis using real clocks, focusing on their impact on circuit performance. OpenSTA is utilized to perform precise timing analysis, considering parameters such as slack, data arrival time, and data required time.  

### Key Concepts  

#### 1. **Setup Time Analysis Using Real Clocks:**  
   - Setup time analysis ensures that data arrives at the capture flip-flop before the active edge of the clock.  
   - Involves two flip-flops:  
     - **Launch Flop:** The flip-flop that sends the data.  
     - **Capture Flop:** The flip-flop that receives the data.  
   - Key parameters include:  
     - **Slack:** The difference between data required time and data arrival time.  
     - **Data Required Time:** The time by which data must arrive to avoid a violation.  
     - **Data Arrival Time:** The actual time at which data reaches the capture flop.  

#### 2. **Hold Time Analysis Using Real Clocks:**  
   - Hold time analysis ensures that data is stable for a minimum duration after the clock edge to be correctly latched.  
   - Key requirement: The combinational delay must exceed the hold time of the capture flop.  

---  

### SKY_L1 - Setup Timing Analysis Using Real Clocks  

### Overview  
Setup timing analysis is vital for ensuring reliable data transfer in sequential circuits. This session delves into timing verification for a single clock, emphasizing slack, data required time, and data arrival time.  

### Key Concepts  

#### 1. **Setup Timing Analysis:**  
   - Ensures that data arrives at the capture flip-flop before the active edge of the clock.  
   - Parameters analyzed include:  
     - **Slack:** Indicates timing margin between data required and arrival times.  
     - **Data Required Time:** The clock-dependent deadline for data arrival.  
     - **Data Arrival Time:** The time taken for data to propagate through combinational logic.  

#### 2. **Hold Timing Analysis Introduction:**  
   - Ensures data stability after the clock edge.  
   - Combinational delay must surpass the hold time requirement to avoid errors.

---

### SKY_L2 - Hold Timing Analysis Using Real Clocks  

### Overview  
Hold timing analysis ensures that data remains stable for a specified duration after the clock edge to prevent timing violations. This session concludes the discussion on hold analysis, emphasizing the importance of slack, uncertainty, and maintaining timing reliability. The next logical step involves extending setup analysis to scenarios with multiple clocks.  

### Key Concepts  

#### 1. **Hold Timing Analysis Conclusion:**  
   - The focus is on ensuring that data stability is maintained during the hold time.  
   - **Uncertainty Value:** Reflects variations in clock and data propagation, impacting hold time margins.  

#### 2. **Slack in Hold Timing:**  
   - Slack should be **positive** or **zero** to ensure no hold violations.  
   - Negative slack indicates that the timing requirements are not met, necessitating further optimization.  

#### 3. **Next Step – Setup Analysis with Multiple Clocks:**  
   - Extending the analysis to account for interactions between multiple clocks.  
   - Adds complexity but is critical for ensuring timing integrity in advanced designs.  

---  


</details>

## Implementation of SKY130_D4_SK1 - SKY_L1, SKY_L2, SKY_L3

### Standard Cell Layout Rules and Requirements

This document outlines the essential rules for designing standard cells in the SKY130 process. Adhering to these rules ensures compatibility with automated tools, seamless routing, and compliance with design-for-manufacturing (DFM) guidelines.


#### **Rules for Standard Cell Layout**

#### 1. Input and Output Port Alignment
- **Requirement:** Input and output ports must be located at the intersection of horizontal and vertical routing tracks.
- **Purpose:** 
  - Enables seamless signal routing.
  - Ensures compatibility with the grid defined for automated place-and-route (PnR) processes.

#### 2. Standard Cell Width
- **Requirement:** The width of the standard cell must be an **odd multiple of the x-pitch** (0.46 µm for SKY130).
- **Examples:** Valid widths include:
  - \( 0.46 \, \mu\text{m}, 1.38 \, \mu\text{m}, 2.3 \, \mu\text{m}, \dots \)
- **Purpose:**
  - Maintains alignment with horizontal track spacing.
  - Simplifies horizontal routing and ensures manufacturability.

#### 3. Standard Cell Height
- **Requirement:** The height of the standard cell must be an **even multiple of the y-pitch**.
- **Examples:** Valid heights include:
  - \( 0.92 \, \mu\text{m}, 1.84 \, \mu\text{m}, 2.76 \, \mu\text{m}, \dots \)
- **Purpose:**
  - Ensures compatibility with vertical track spacing.
  - Facilitates power, ground, and signal routing across multiple rows of standard cells.


#### **Purpose of These Rules:**
1. **Manufacturability:** Ensures compliance with DFM guidelines, minimizing risks during fabrication.
2. **Design Automation:** Simplifies integration with automated tools like synthesis, PnR, and timing analysis.
3. **Uniformity:** Maintains consistent cell placement and connectivity across the design.

#### **Why These Rules Matter?**
These guidelines form the backbone of standard cell library development, ensuring robust, scalable, and manufacturable designs for the SKY130 PDK.


## Tasks done 

### 1. Opening the Custom Inverter Layout
#### Commands
```bash
# Change directory to the custom inverter design
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Open the custom inverter layout in Magic
magic -T sky130A.tech sky130_inv.mag &
```
#### Screenshots
**Tracks Info of `sky130_fd_sc_hd`:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-1.png)


### 2. Setting Grid as Tracks of Locali Layer
#### Commands for Tkcon Window
```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
#### Screenshots
**Commands Run:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-2.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-3.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-4.png)


### 3. Saving and Reopening the Layout
#### Commands
```tcl
# Save the layout with a custom name
save sky130_vsdinv.mag

# Open the newly saved layout
magic -T sky130A.tech sky130_vsdinv.mag &
```
#### Screenshot
**Newly Saved Layout:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-5.png)


### 4. Generating LEF from the Layout
#### Commands
```tcl
# Write LEF file
lef write
```
#### Screenshots
**Commands Run:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-6.png)
**Generated LEF File:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-7.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-8.png)


### 6. Copying LEF and Library Files
#### Commands
```bash
# Copy LEF file to the design's src directory
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and verify the copied LEF file
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy library files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and verify the copied library files
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
#### Screenshot
**Commands Run:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-10.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-11.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-12.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-13.png)


### 7. Editing `config.tcl`
#### Commands to Include Custom Cell
```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```
#### Screenshot
**Edited `config.tcl`:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-14.png)


### 8. Running OpenLANE Flow with Custom Inverter
#### Commands
```bash
# Change to OpenLANE flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# Launch OpenLANE flow in Docker
docker

# Open OpenLANE flow in interactive mode
./flow.tcl -interactive

# Load OpenLANE package
package require openlane 0.9

# Prep the design
prep -design picorv32a

# Include newly added LEF to OpenLANE flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Run synthesis
run_synthesis
```
#### Screenshots
**Commands Run:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-15.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-16.png)
**Synthesis Completed:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-17.png)


### 9. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-26.png)


### 10. Removing Violations Introduced by the Custom Inverter

#### Commands to View and Modify Design Parameters

```tcl
# Prep the design to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Include newly added LEF file in OpenLANE flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Display and set values for design variables to improve timing
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"

echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1

echo $::env(SYNTH_DRIVING_CELL)

# Run synthesis again with updated parameters
run_synthesis
```

#### Screenshots
**Merged LEF File in `/tmp` Directory:**  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-18.png)
  
**Commands Run:**  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-19.png)  

#### Observations
Area increased slightly, and **Worst Negative Slack (WNS)** improved to 0.

#### Screenshot

**Comparison of Values Before and After Update:**  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-20.png)  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-21.png)



### 11. Running Floorplan and Placement for Custom Inverter Integration
#### Commands to Run Floorplan
```tcl
# Run the floorplan
run_floorplan
```
#### Alternate Commands for Floorplan
```tcl
# Commands sourced in `run_floorplan`
init_floorplan
place_io
tap_decap_or
``` 

#### Commands to Run Placement
```tcl
# Run placement
run_placement
```
#### Screenshots
**Commands Run:**  
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-22.png) 

### 12. Viewing Placement DEF in Magic
#### Commands to Load Placement DEF in Magic
```bash
# Change directory to placement DEF file location
cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-01_08-54/results/placement/

# Load the placement DEF file in Magic
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
#### Screenshots
**Placement DEF in Magic:**  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-23.png)


#### Command for Viewing Internal Layers of Cells
```tcl
# Expand layers to view internal connectivity
expand
```
#### Screenshots
**Abutment of Custom Cell with Library Cells:**  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-24.png)  
  ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-25.png)

---

## Implementation of SKY130_D4_SK2 - SKY_L3, SKY_L4, SKY_L5

---

### 1. Post-Synthesis Timing Analysis with OpenSTA

Since we have a 0 WNS (Worst Negative Slack) after the improved timing run, we will perform timing analysis on the initial synthesis run, which contains several violations without any added parameters for timing improvement.

#### Steps to Invoke the OpenLANE Flow, Include New LEF, and Perform Synthesis

1. **Navigate to the OpenLANE Directory**:
   ```bash
   cd Desktop/work/tools/openlane_working_dir/openlane
   ```

2. **Invoke OpenLANE Docker Sub-System**:
   Since we have aliased the long Docker command to `docker`, we can invoke the OpenLANE flow Docker sub-system by running:
   ```bash
   docker
   ```

3. **Enter Interactive Mode in OpenLANE**:
   ```tcl
   ./flow.tcl -interactive
   ```

4. **Load OpenLANE Package and Prepare the Design**:
   ```tcl
   package require openlane 0.9
   prep -design picorv32a
   ```

5. **Include Newly Added LEF Files**:
   ```tcl
   set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
   add_lefs -src $lefs
   ```

6. **Set SYNTH_SIZING Environment Variable**:
   ```tcl
   set ::env(SYNTH_SIZING) 1
   ```

7. **Run Synthesis**:
   ```tcl
   run_synthesis
   ```

   **Final Screenshot of Commands Run**:
   ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-27.png)

#### Running STA in Another Terminal

1. **Navigate to the OpenLANE Directory**:
   ```bash
   cd Desktop/work/tools/openlane_working_dir/openlane
   ```

2. **Invoke OpenSTA with the Pre-STA Configuration**:
   ```bash
   sta pre_sta.conf
   ```

   **Screenshots of Commands Run**:
    ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-31.png)
    ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-30.png)

    The `pre_sta.conf` file for STA analysis is located in the `openlane` directory.
      ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-29.png)
   
    The `my_base.sdc` file for STA analysis is created in the `openlane/designs/picorv32a/src` directory based on `openlane/scripts/base.sdc`.
      ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-28.png)

#### Optimizing Timing by Reducing Fanout

Since higher fanout causes more delay, we can reduce the fanout and re-run synthesis.

1. **Prepare the Design Again with a New Tag**:
   ```tcl
   prep -design picorv32a -tag 17-01_17-45 -overwrite
   ```

2. **Include Newly Added LEF Files**:
   ```tcl
   set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
   add_lefs -src $lefs
   ```

3. **Set SYNTH_SIZING and SYNTH_MAX_FANOUT Environment Variables**:
   ```tcl
   set ::env(SYNTH_SIZING) 1
   set ::env(SYNTH_MAX_FANOUT) 4
   ```

4. **Check the Current Value of SYNTH_DRIVING_CELL**:
   ```tcl
   echo $::env(SYNTH_DRIVING_CELL)
   ```

5. **Run Synthesis Again**:
   ```tcl
   run_synthesis
   ```

   **Final Screenshot of Commands Run**:
   ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-32.png)

#### Running STA Again in Another Terminal

1. **Navigate to the OpenLANE Directory**:
   ```bash
   cd Desktop/work/tools/openlane_working_dir/openlane
   ```

2. **Invoke OpenSTA with the Pre-STA Configuration**:
   ```bash
   sta pre_sta.conf
   ```

   **Screenshots of Commands Run**:
   ![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-33.png)


---

### 10. Timing ECO Fixes to Remove Violations

To remove timing violations, we start by analyzing and optimizing timing by replacing OR gates of drive strength 2 with OR gates of drive strength 4. This process helps manage fanouts and improve slack.

Start by reporting all the connections to a net using the command:
```tcl
report_net -connections _10566_
```

Check the command syntax for replacing cells:
```tcl
help replace_cell
```

Replace the cell driving 4 fanouts with a stronger drive strength:
```tcl
replace_cell _13165_ sky130_fd_sc_hd__or3_4
```

Generate a custom timing report to evaluate the changes:
```tcl
report_checks -fields {net cap slew input_pins} -digits 4
```

![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-34.png)

Result - slack reduced.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-35.png)

Repeat the above steps for other nets experiencing similar issues. For example, for the net `_11675_`, replace the corresponding cell and generate a report:
```tcl
report_net -connections _10563_

replace_cell _13161_ sky130_fd_sc_hd__or3_4

report_checks -fields {net cap slew input_pins} -digits 4
```
Command runs
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-36.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-37.png)

Result - slack reduced.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-38.png)

Continue to address nets like `_13132_` and `_13157_` in a similar manner to further optimize timing. Each time, replace the cell with a stronger drive strength and verify the slack reduction.

this is for cell `_13132_`
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-39.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-40.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-41.png)

this is for cell `_13157_` as the delay time is 1.5317
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-42.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-43.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-44.png)


Finally, verify that the instance `_27762_` has been replaced with the stronger drive strength OR gate:
```tcl
report_checks -from _27860_ -to _27762_ -through _26365_
```
Screenshot of replaced instance.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-45.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-46.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-47.png)

After making these changes, the worst negative slack (WNS) is reduced from -23.9000 ns to -22.6173 ns, an improvement of approximately 1.2827 ns.

### 11. Replacing the Old Netlist and Running PnR Stages

With the timing ECO fixes applied, we replace the old netlist with the newly generated netlist. This updated netlist will be used for the physical design flow, including floorplanning, placement, and clock tree synthesis (CTS).

First, make a copy of the old netlist:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-01-17-45/results/synthesis/
ls
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
ls
```
Screenshot of commands run.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-48.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-49.png)

Overwrite the current synthesis netlist with the updated one:
```tcl
help write_verilog
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v
exit
```

Verify that the netlist has been overwritten by checking the replacement of the instance `_13157_` with the updated OR gate.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-50.png)

Once confirmed, proceed with the design flow for physical design. Prep the design again to update the necessary variables:
```tcl
prep -design picorv32a -tag 24-03_10-03 -overwrite
```

Include the newly added LEF files:
```tcl
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

Set new values for synthesis strategy and sizing:
```tcl
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
```

Proceed with the floorplan, placement, and CTS steps:
```tcl
init_floorplan
place_io
tap_decap_or
run_placement
unset ::env(LIB_CTS)
run_cts
```
Screenshots of commands run.
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-51.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-52.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-53.png)
![Screenshot](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day4-54.png)

---

<div align="center">
  
## Section 5: Sky130 Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

</div>

<details>
<summary><h2><strong>📚 Theory for Day 5</strong></h2></summary>

---

## SKY130_D5_SK1 - Routing and Design Rule Check (DRC)  

### Overview  
The final step in the RTL-to-GDSII flow involves routing the connections between design components and ensuring compliance with design rules. This session focuses on the routing process, specifically Maze Routing using Lee's algorithm, and highlights the significance of performing a Design Rule Check (DRC) to verify adherence to fabrication constraints.  

### Key Concepts  
### 1. **Routing Basics:**  
   - Routing connects different components in the layout through metal layers, following predefined paths.  
   - TritonRoute is a tool used in the SKY130 PDK for efficient routing and DRC compliance.  

### 2. **Maze Routing and Lee's Algorithm:**  
   - Lee's algorithm, introduced in 1961, is a foundational approach to Maze Routing.  
   - It operates on a routing grid, systematically exploring adjacent boxes to find the shortest path between two components.  
   - This ensures efficient routing while avoiding blockages and overlapping paths.  

---  

### SKY_L1 - Introduction to Maze Routing Using Lee's Algorithm  

### Overview  
This session dives into the fundamentals of Maze Routing, with a focus on Lee's algorithm. It explains the routing grid concept and the step-by-step process of finding a path between two components while adhering to design rules.  

### Key Concepts  
### 1. **Routing Grid:**  
   - The layout is divided into a grid, where each box represents a potential routing space.  
   - Adjacent boxes are evaluated to create a path between the start and end points.  

### 2. **Lee's Algorithm:**  
   - Lee's algorithm systematically explores adjacent boxes to find the shortest path, ensuring all constraints are met.  
   - It is particularly effective for solving routing problems in complex layouts.  

---  

### SKY_L2 - Lee’s Algorithm Conclusion  

### Overview  
This session concludes the discussion on Lee's algorithm by demonstrating the practical application of routing. It showcases the process of selecting paths and solving additional routing problems using the most preferred methods.  

### Key Concepts  
### 1. **Path Selection:**  
   - The algorithm determines the optimal path by systematically evaluating available options within the routing grid.  
   - Each step considers blockages and preferred routes to ensure an efficient design.  

### 2. **Iterative Problem-Solving:**  
   - Additional routing scenarios are presented, showcasing how Lee's algorithm adapts to different challenges.  
   - This emphasizes its robustness and widespread preference in routing solutions.  

---  

### SKY_L3 - Design Rule Check  

### Overview  
Design Rule Check (DRC) is a critical step in ensuring that the layout adheres to manufacturing constraints. This session explains the typical design rules for wires and vias that must be validated before proceeding to fabrication.  

### Key Concepts  
### 1. **Wire Design Rules:**  
   - **Minimum Wire Width:** Ensures the wire's physical dimensions meet the manufacturing requirements.  
   - **Wire Pitch:** Specifies the distance between the centers of adjacent wires to avoid overlapping.  
   - **Wire Spacing:** Defines the minimum distance between adjacent wires to prevent signal interference.  

   Common violations, such as signal shorts, are identified during the DRC process.  

### 2. **Via Design Rules:**  
   - **Via Width:** Ensures that the vias connecting different metal layers meet the required dimensions.  
   - **Via Spacing:** Verifies that the distance between adjacent vias complies with the design rules to avoid electrical shorts or crosstalk.  

---

## SKY130_D5_SK3 - TritonRoute Features  

### Overview  
TritonRoute is a detailed routing engine that plays a critical role in completing the physical design process in modern ASIC design. It handles various challenges of routing, such as connectivity, layer management, and adherence to design rules. This session likely explores key features of TritonRoute and its methods for achieving efficient routing.

---

### SKY_L1 - TritonRoute Feature 1: Honors Pre-Processed Route Guides  

### Overview  
This section likely introduces how TritonRoute uses pre-processed route guides generated during global routing. These guides serve as a blueprint, ensuring the detailed routing stays within specified boundaries and adheres to design constraints.  

### Key Concepts  
1. **Pre-Processed Route Guides:**  
   - Generated during the global routing phase.  
   - Help TritonRoute maintain routing integrity and avoid design rule violations.  

2. **Routing Optimization:**  
   - Ensures routing is efficient and minimizes path overlap or unnecessary detours.

---

### SKY_L2 - TritonRoute Features 2 & 3: Inter-Guide Connectivity and Intra- & Inter-Layer Routing  

### Overview  
This section likely discusses two key capabilities of TritonRoute:  
1. Connecting routing guides efficiently across the layout (inter-guide connectivity).  
2. Managing signal routing within a layer (intra-layer) and between layers (inter-layer), ensuring seamless signal paths.  

### Key Concepts  
1. **Inter-Guide Connectivity:**  
   - Ensures continuous routing between different pre-processed route guides.  

2. **Intra- & Inter-Layer Routing:**  
   - Handles routing within a single metal layer and across multiple layers.  
   - Focuses on layer transitions using vias and adhering to DRC rules.  

---

### SKY_L3 - TritonRoute Method to Handle Connectivity  

### Overview  
This section likely explains how TritonRoute ensures all required connections are made while resolving conflicts and avoiding design rule violations. Advanced algorithms are used to manage signal paths effectively across the design.  

### Key Concepts  
1. **Connectivity Algorithms:**  
   - Strategies to route signals while avoiding shorts and maintaining timing.  

2. **Conflict Resolution:**  
   - Methods to resolve congestion or overlap in the routing process.  

---

### SKY_L4 - Routing Topology Algorithm and Final Files List Post-Route  

### Overview  
This section likely covers the algorithms used by TritonRoute to determine routing topologies, which define the structure of the routes for optimal performance. Additionally, it might describe the final files generated after routing is completed, which are crucial for subsequent steps in the ASIC flow.  

### Key Concepts  
1. **Routing Topology Algorithm:**  
   - Determines the shape and structure of signal paths, ensuring minimal delay and power consumption.  

2. **Post-Route Files:**  
   - Final routed layout files (e.g., DEF, GDS) and reports indicating design rule compliance and routing quality.  

---

</details>

## Implementation of SKY130_D5_SK2 - Power Distribution Network and routing 



  














