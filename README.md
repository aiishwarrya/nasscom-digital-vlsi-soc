<div align="center">

# Digital VLSI SoC Design and Planning (8th January to 22nd January)

</div>


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

### Screenshots of Running Commands
![Command 1](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss1.png)
![Command 2](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss2.png)
![Command 3](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss3.png)
![Command 4](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss4.png)
![Command 5](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss5.png)
![Command 6](https://github.com/aiishwarrya/nasscom-digital-vlsi-soc/blob/main/screenshots/ss6.png)


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

</details>
