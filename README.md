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

</details>

## Implementation of SKY_L5 - Pin placement and logical cell placement blockage to SKY_L8 - Review floorplan layout in Magic

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
cd ~/tools/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Load the DEF file in Magic tool
magic -T ~/tools/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

#### Observations in Magic:
- Equidistant placement of ports
- Decap cells and tap cells  
- Diagonally equidistant tap cells  
- Unplaced standard cells at the origin  

#### **Screenshot Outputs:**
- Magic visualization of the floorplan
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-3.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-4.png)  
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-5.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-6.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-7.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-8.png)
![DEF Observations](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/day2-9.png)

---
