<div align="center">

# Digital VLSI SoC Design and Planning (8th January to 22nd January)

</div>

---
## Section 1: SKY130 Day 1 - Inception of Open-source EDA, OpenLANE, and SKY130 PDK

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
[Download Logs and Reports](https://drive.google.com/drive/folders/1pE5U-MDwS9-30--uNBwj4ezLeI0nOAl6)

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
## Section 2: Sky130 Day 2 - Good floorplan vs bad floorplan and introduction to library cells

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

## Section 3: Sky130 Day 3 - Design library cell using Magic Layout and ngspice characterization

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

</details>


## Implementation of SKY_L0 - IO Placer Revision

To optimize the equidistant placement of cells during IO placement, we used the following command:

```bash
set ::env(FP_IO_MODE) 2

```
![input change command](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-1.png)

## Implementation of SKY_L5 - Lab steps to git clone vsdstdcelldesign

Here’s the content formatted for GitHub with the commands included:

#### SKY_L5 - Lab Steps to Git Clone VSD Standard Cell Design

This task involves cloning a GitHub repository containing a custom inverter standard cell design, exploring its layout in Magic, performing spice extraction, editing the spice model file, and running post-layout simulations.

---

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

#### **3. Perform Spice Extraction**:
- Extract the SPICE netlist from the custom inverter layout in Magic for further analysis.

#### **4. Post-Layout Simulation**:
- Edit the extracted SPICE file to include appropriate models and parameters for simulation.
- Run post-layout simulations using ngspice to analyze the inverter's behavior.

#### **5. Debug DRC Issues**:
- Identified and fixed problems in the Design Rule Check (DRC) section of the older Magic tech file for the SKY130 process.

---

### **Key Outputs**:
- Successfully cloned the `vsdstdcelldesign` repository.
- Opened and explored the custom inverter layout in Magic.
- Extracted the SPICE netlist of the layout.
- Performed accurate post-layout simulations using ngspice.

  #### Screenshots of the following commands
  
![command run ](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-2.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-3.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-4.png)
![command run](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day3-5.png)

---





