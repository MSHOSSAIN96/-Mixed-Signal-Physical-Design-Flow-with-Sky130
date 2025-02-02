# -Mixed-Signal-Physical-Design-Flow-with-Sky130
 This directory describes how the PNR of an analog IP, 2:1 analog multiplexer is carried out by opensource EDA tools, OpenLANE. It also discusses the steps to modify the current IP layouts in order to ensure its acceptance by the EDA tools.


**Chapter 1: Generating hard-macro LEF for basic analog block**

**1.a Introduction to mixed-signal flow & EDA tools**

**What is mixed signal?**

Mixed signal is a design which consists of both analog as the digital components in the same packageas as can be seen in the traditional mixed signals, consist of a separate digital and a separate analog component.

Both of them combine, including a chip, whereas in the modern mixed signal you can see that the digitalanalog components are present as it was in the traditional ones.But along with that of mixed signal, block is also present.

Mixed Signals Block is a block which consists of both digital analog component inside a single component,unlike the one the traditional which would separate.So first, why is there a need for mixed signals nowadays, the analog component is rapidly increasing,which requires us for mixed signals the same.

![Screenshot 2024-12-27 112111](https://github.com/user-attachments/assets/e286be9e-7f49-489b-b1b2-cbdd5abbb95f)

**Example of Mixed-Signal Design**

Consider an integrated system that includes the following components:

1.DAC (Digital-to-Analog Converter)

2.ADC (Analog-to-Digital Converter)

3.PLL (Phase-Locked Loop)

This system is a purely mixed-signal design as it seamlessly combines both analog and digital functionalities.

The integration of these components demonstrates a perfect example of a mixed-signal package.It showcases how analog and digital elements work together within a single system, exemplifying the essence of mixed-signal design.


![Screenshot 2024-12-27 112620](https://github.com/user-attachments/assets/57640798-95a5-4383-8b85-22c9e189b3e2)

**Q-Flow:**

A design flow that uses various open-source tools to perform different functionalities.

**Examples of Tools:**

Yosys & ABC: Perform synthesis.

Graywolf: Handles placement.

QRouter: Performs routing.

Magic: Finalizes the layout.

Vesta: Used for STA (Static Timing Analysis).

These tools are combined and used in synchronization to achieve the design objectives.

**Limitations:** Primarily academic in nature, meaning it is not as robust or feature-complete as industrial tools.


![Screenshot 2024-12-27 113756](https://github.com/user-attachments/assets/cc5113ce-7bb5-4034-a8bc-c96dc10bb0b4)

**Inputs for RTL-to-GDS Flow:**

To perform the RTL-to-GDS flow, various input files are required. These inputs help define and analyze the physical and functional characteristics of the design.

**1. LEF (Library Exchange Format) File**

Purpose: Provides an abstract view of the cells.

Contents: 

a. PR Boundary (Placement and Routing Boundary).

b. Pin Position.

c. Metal Layer Information.

Generated Using: Tools like Magic can extract this file, representing the physical layout and boundaries for timing analysis.

**2. LIB (Liberty Timing File)**

Purpose: Contains timing-related information about the cells.

Contents:

a.Cell Delays, Transition Times, Setup and Hold Time Requirements.

b.Look-Up Tables (LUTs) defining areas of the cells and leakage power.

c.Rise and Fall Capacitances.

**Example Snippet:**

Maximum transition: 2.5 ns.

Capacitance: 0.001 pF.

Input and Output directions are defined for the pins.

**3. Verilog File**

Purpose: Hardware Description Language (HDL) file used to describe the functionality of the design.


Contents:Describes the logic or behavior of the hardware, such as multiplexers or logic gates.


Example:For a multiplexer, if the Select signal is 0, the output corresponds to I0; if 1, the output corresponds to I1.


**Each file serves a specific purpose:**

1.LEF provides an abstract physical layout.

2.LIB offers detailed timing information.

3.Verilog defines the logical behavior of the design.

These inputs are crucial for the RTL-to-GDS flow, ensuring both functional accuracy and physical feasibility of the design.


**1.b Macro LIB file modification:**

![Screenshot 2024-12-27 140524](https://github.com/user-attachments/assets/59734d3e-d791-4404-81a9-e5d9de310f3c)

**Understanding the LEF File Creation:**

The LEF (Library Exchange Format) file is essential for representing the physical abstraction of the cells. To create the LEF file, the layout must be modified or adjusted to meet proper alignment and dimensional requirements. 

1. Ground and Fence Alignment
   
**Requirement**:

The ground and fence dimensions must be aligned correctly.

In the Sky130 process (SkyWater 130nm PDK), the dimensions are as follows:

The purple part (Ground or Power Rail): 48 microns.

The blue part (Local Interconnect Line): 18 microns.

Purpose:These specific dimensions are set to ensure compatibility with other standard cells in the design.

**2. Why Exact Dimensions Are Necessary:**

Design Compatibility:The dimensions need to match precisely so that adjacent standard cells fit seamlessly.

Example: Besides this design, there will be other standard cells. All these components must fit into the same defined grid without overlaps or misalignments.

Avoiding Overlaps or Gaps:If dimensions are incorrect, issues like overlaps or gaps may occur, disrupting the design flow.

**3. Importance of Proper Dimensions**

Load Distribution: Accurate dimensions ensure even load distribution across the layout.

Legalization Problem: Proper alignment prevents legalization issues during the design flow, ensuring that all cells are placed correctly on the grid.

Error Prevention: Incorrect alignment or dimensions can lead to significant problems during layout and validation, causing delays in the design process.

The ground and fence dimensions, such as 48 microns for the ground and 18 microns for the local interconnect line, are critical for ensuring design compatibility.
Adhering to exact parameters is essential to prevent issues like misalignment, overlaps, or legalization problems.
Maintaining these standards ensures a smooth and error-free layout design process.

![Screenshot 2024-12-27 141513](https://github.com/user-attachments/assets/61c30d96-d867-4691-9f04-ef6da920a439)

**Understanding Cell Height and Fences in Layout Design**

1. Cell Height
   
**Definition of Cell Height:**

The height of a macro or IP can vary based on the design.It must conform to specific standards, typically either:

Single Height: 272 units
Double Height: 544 units

Consistency in Heights:

Cells cannot have arbitrary heights like 1.5, 1.7, or 1.3 units.

They must strictly adhere to either single height or double height to maintain compatibility and avoid misalignment.

**Clarification on Height Measurement:**

The 544-unit height does not represent the full height of the cell.

Instead, it refers to the distance between specific reference points, such as half of the power rail at the top to half of the power rail at the bottom.

This ensures uniformity across cells without designing the entire cell as "double height."

**2. Fence Structures**

Importance of Fences:

Fences are critical in defining the placement regions of cells.

They help in organizing and constraining the layout during placement and routing.

**Integration with Design Tools:**

These fences are dumped into the layout tools and play a key role in defining physical boundaries for cells.

Cell Heights: Stick to defined standards (single height = 272 units, double height = 544 units).

Fences: Ensure proper definition and alignment for placement accuracy.

Avoid Overcomplications: Be clear about the measured dimensions and avoid unnecessary changes that might disrupt standardization.




