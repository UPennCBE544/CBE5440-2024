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

- **Surface Energy ($\gamma_{(hkl)}$)**: This can be thought of as the energy for the specific modeled surface to exist. It indicates the thermodynamic stability of a surface. Surface energy is influenced by surface geometry, termination, and adsorbates. $\gamma_{(hkl)}(pH,U) = -\frac{E_{slab} + N \cdot E_{bulk} - \sum_{i} \delta n_{i} \cdot \mu_{i}^{\text{REF}}(pH,U)}{2A}$

- **Wulff's Theorem**: This theorem states that the shape of a crystal/nanoparticle at equilibrium is determined by the minimization of its total surface energy. The equilibrium shape (also known as the **Wulff Construction**) is the convex hull of the surfaces with the lowest energies.

<a name='Plan'></a>

## Plan ##

For each symmetric Surface we need to go through the following path.

<img width="958" alt="Screenshot 2024-10-22 at 7 23 03 PM" src="https://github.com/user-attachments/assets/dc8f80d2-f07c-4d43-8055-ea16aec4a15b">---

### Detailed plan: ###
1. We will break into groups of 3 students
   
3. Each group will be assigned a series of surfaces they will be responsible for
   
       a. {(0,1,2),(0,2,1),(2,1,0)}

       b. {(2,2,1),(3,3,1),(4,4,1)}

       c. {(1,2,2),(1,3,3),(1,4,4)}

       d. {(1,1,2),(1,1,3),(1,1,4)}

       e. {(2,1,1),(3,1,1),(4,1,1)}

4. Build a surface
5. Relax a surface
6. k-point check (5x5x1) (15x15x1) (25x25x1)
7. 

