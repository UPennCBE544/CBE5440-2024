---
layout: page
mathjax: true
permalink: /Project/
---
## Course Project Logistics ##

1. [Introduction](#intro)
2. [Motivation](#MO)
3. [Terms to Know](#Terms)
4. [Plan](#Plan)

Turn in your final report by emailing a PDF file to:

```
alevoj@seas.upenn.edu, rthatch@seas.upenn.edu
```

<a name='intro'></a>

## Project Introduction ##

Goal: The main scientific goal is to probe the oxygen evolution reaction (OER) chemistry on higher Miller index surface facets of RuO<sub>2</sub> by simulating the adsorption of O, OH, H, OOH, OO, and H<sub>2</sub>O on various active sites. With the data generated, we aim to construct thermodynamic stability diagrams relative to bulk-cleaved surfaces and identify the most stable surface configurations as my group frequently does. Note, we will not consider defected surfaces due to the significantly increased workload they would impose. Students will compare their simulated nanoparticle models with experimentally derived nanoparticles, providing insights into the stability and morphology of nanoparticles during electrochemical processes.

<a name='MO'></a>

### Motivation ###

- **Catalyst Design for Functional Efficiency**: Selecting catalysts with the right functional properties is crucial for enabling manufacturable technologies. This includes considerations for cost efficiency, performance, durability, raw material abundance, and environmental impact. This project will specifically lend itself toward oulining a framework for studying activity and stability of nanoparticles. 

- **Sustainable Energy Applications**: The function we are designing for is the oxygen evolution reaction. A deeper understanding of nanocrystal stability and activity supports the advancement of stable and active electrocatalysts, which are essential for sustainable hydrogen fuel generation and other clean energy technologies.

- **Nanoparticle Shape Control and Optimization**: By modeling nanoparticle shapes, we gain insight into how environmental conditions (pH, applied potential, temperature, pressure, etc.) and chemical composition influence facet exposure and shape. This could lead to optimization strategies that improve catalyst activity and stability by tuning facet ratios and crystal morphology.

- **Experimental Comparison and Data Validation**: By aligning nanoparticle shapes, surface facets, and catalytic behaviors observed in simulations with those measured experimentally, we can validate our models and refine predictive accuracy. This comparison helps identify discrepancies, improve our understanding of real-world conditions, and build confidence in the applicability of the computational framework for guiding experimental design and optimizing catalyst performance

<a name='Terms'></a>

## Terminology ##
- **Surface Facet Miller Index**: The Miller index (hkl) describes the orientation of a crystal plane by indicating how it cuts through the unit cell of the crystal structure

- **Termination**: Termination refers to the specific arrangement and coordination of lattice metals and their corresponding oxygens at a surface. Different terminations, whether metal-terminated or oxygen-terminated, significantly affect surface properties, including reactivity and stability, and can result from various preparation methods.

- **Symmetric Surface**: A symmetric surface is characterized by an arrangement of atoms that is the same on both sides of the surface plane, exhibiting inversion symmetry. They may not always be stoichiometric, meaning the atomic ratios (e.g., metal to oxygen) can differ from the bulk composition.

- **Asymmetric Surface**: An asymmetric surface tends to lack inversion symmetry of atoms on both sides, but not always. We will define the clean (lacking adsorbates) asymmetric surfaces to be stoichiometric, maintaining a specific metal-to-oxygen ratio overall.

- **Surface Energy ($\gamma_{(hkl)}$)**: This can be thought of as the energy for the specific modeled surface to exist. It indicates the thermodynamic stability of a surface. Surface energy is influenced by surface geometry, termination, and adsorbates. $\gamma_{(hkl)}(pH,U) = -\frac{E_{slab} + N \cdot E_{bulk} - \sum_{i} \delta n_{i} \cdot \mu_{i}^{\text{REF}}(pH,U)}{2A}$. Note: $E_{bulk}$ is calculated by generating 4 of the same surface facet+termination each with different amounts of "bulk" and plotting total potential energy vs system size and getting the slope.

- **Wulff's Theorem**: This theorem states that the shape of a crystal/nanoparticle at equilibrium is determined by the minimization of its total surface energy. The equilibrium shape (also known as the **Wulff Construction**) is the convex hull of the surfaces with the lowest energies.

<a name='Plan'></a>

## Plan ##

For each symmetric Surface we need to go through the following path.

<img width="968" alt="Screenshot 2024-10-22 at 8 00 01 PM" src="https://github.com/user-attachments/assets/8ef50116-698b-476e-b0db-ed8eb3596ee4">

### Detailed plan: ###

We will break into groups of 2 students and each group will be assigned a series of surfaces they will be responsible for.
   
       a. {(2,2,1),(3,3,1),(4,4,1),(0,1,2)} - Group 1

       b. {(1,2,2),(1,3,3),(1,4,4),(0,2,1)} - Group 2

       c. {(2,1,1),(3,1,1),(4,1,1),(2,1,0)} - Group 3

       Groups: 
         (1) Conor & Erika
         (2) Daniel & George
         (3) Shiqiang & Jinyu
         (4) Yeri & Achala

0. Prep Work - we need a rutile RuO<sub>2</sub> bulk that is optimized

1. Generate Asymmetric Surface Facet - Provided by Rachel

2. Adsorb on the Asymmetric Surface -
      a. Copy this directory into your home:
         ```bash
         cp -r /home/x-rthatcher/scripts_Final_Project ~/
   
      b. Open the reference trajectory file:
         ```bash
         ag /anvil/projects/x-eve210010/REFERENCES/dopedSurface/ruo2/YOUR_FACET/clean/No_defect/0%_doped/PBE/relax/init.traj
   
      c. Determine which metal/oxygen atom/s you want to adsorb onto. If you have 4 or more metal atoms at the surface, you will need to adsorb on 1, approximately half, and all of the surface sites.
   
      d. Modify the Adsorption file to have YOUR_FACET and the indices of the atoms you want to adsorb on top of:
         ```bash
         nano /home/x-rthatcher/scripts_Final_Project/asymmetric_slabs/Adsorptions_Asymmetric.py
      <img width="652" alt="Screenshot 2024-11-20 at 1 29 57 PM" src="https://github.com/user-attachments/assets/a0329922-7904-48bc-9184-1c28667a6898">

4. Generate Pourbaix Diagram - 

5. Copy most stable adsorbate configuration - 
   - k-point convergence test: (1x1x1) (5x5x1) (15x15x1) (25x25x1)

6. Calculate Surface Energy - 


