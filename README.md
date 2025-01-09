# Digital VLSI SoC Design and Planning (8th January to 22nd January)

## Section 1: SKY130 Day 1 - Inception of Open-source EDA, OpenLANE, and SKY130 PDK

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
*(Include screenshots here)*

### 2. Calculate the Flop Ratio and Percentage of DFFs
#### Synthesis Statistics Report
*(Include screenshots of the synthesis statistics report with required values highlighted)*

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
