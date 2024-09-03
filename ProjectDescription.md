---
layout: page
mathjax: true
permalink: /Project/
---
## Course Project ##


1. [Introduction](#intro)
2. [Alkaline Oxide](#MO)
3. [Silicate](#silicate)


For the Final Project, you will perform a comprehensive study on CO<sub>2</sub> adsorption on mineral surfaces and its transformation due to interaction with these surfaces. The students will be assigned into two groups. One group will study magnesium-based oxides and silicates, while the other group will study calcium-based oxides and silicates. Each group will present their results in class that will be critiqued by the other groups. Finally, each group will jointly write a final report on the combined data.


Turn in your final report by emailing a PDF file to:

```
alevoj@seas.upenn.edu, yingjies@seas.upenn.edu
```
<a name='intro'></a>

## Introduction ##

Goal: Determine the lowest CO<sub>2</sub> adsorption energies and the molecular configurations.

Plan: Use DFT to calculate CO<sub>2</sub> adsorption energies for each adsorption site and initial configuration (details are given below). Determine the molecular bond lengths and bond angle for each converged calculation. Plot the Density of States (DOS) of the configuration with the lowest adsorption energy. 

### Motivation ###

- In designing an efficient carbon mineralization material, knowing if it can uptake CO<sub>2</sub> is critial. In other word, we are urged to know if CO<sub>2</sub> can adsorb (adsorption thermodynamics) on it and react.
- Reactive magnesium oxide cement (RMC) is widely studied for carbon capture processes. Hydrated MgO has stronger abilities to adsorb CO<sub>2</sub> and produce carbonated products. We will determine the structure of hydrated MgO through analyzing the stability phase diagram that relates Gibbs free energy of dissociative particle adsorption to water derivative chemical potential (details will be given below).
- There are many possible bulk cleavage planes for MgO and CaO. The most studied ones are (100), (110), and (111). The stability of these facets varies greatly, leading to significantly different adsorption phenomena of CO<sub>2</sub> on different facets.
- Mg and Ca containing (alumino)silicates naturally exist in mine waste tailings. The use of these tailings is considered an alternative avenue for mineralization because they are an inherently cost-effective feedstock that could generate revenue in addition to captuing CO<sub>2</sub>. The presence of Si adds complexity to the study due to the different Si coordination numbers.
- When CO<sub>2</sub> is hydrated, it can undergo protonation/deprotonation through interaction with water to form charged intermediates depending on the solution pH. These species typically are HCO<sub>3</sub><sup>-</sup> and CO<sub>3</sub><sup>2-</sup>. This motivates us to study how these species interaction with mineral surfaces is differed from molecular CO<sub>2</sub>.
- Therefore, we will be studying the chemistry of carbon mineralization and down the line understanding how that chemistry changes with respect to the many factors, such as cation, facet, presence of water, Si coordination, pH conditon, etc.
  
<a name='MO'></a>

## Alkaline Oxide ##

This is part one of the final project. In this part, you will be studying your assigned MgO (or CaO) surface with appropriate facet and termination, including whether it is moisturized.

### Surface Facet (Cleavage Plane) ###

Both MgO and CaO are simple compounds with a cubic crystal. A surface facet is created by performing cleavage on a bulk material. The resulting faceted surface is denoted by the Miller indices, such as (100), (010), (211), etc. In general, we compare the cleavage energy density to determine whether a certain facet is stable relative to another. The calculation of the cleavage energy density is given as follows:

$$
\epsilon_{cleave}(i,j) = -\frac{1}{2A}(E_{slab}^{i}+E_{slab}^{j}-2E_{bulk})
$$

where $$\epsilon_{cleave}(i,j)$$ is the cleavage energy density and i, j are the indices for two complementary facet terminations (you will know this better later). $$A$$ is the surface area of a unit cell. Please DO NOT run jobs to calculate the cleavage energy density yourself, as we have only limited computational resources.


**Task 1: Create a surface off of bulk**

First, run the commands below to obtain the optimized bulk MgO and CaO structure and the script to create surfaces. Now that you are already familiar with Linux, you need to organize your workspace. Please feel free to create directories to make your life easier! Note you only need to run one line out of the first two lines below, depending on your assignment.

```python
cp /home/x-syj1022/minerals/MgO/opt.traj ./
cp /home/x-syj1022/minerals/CaO/opt.traj ./
cp /home/x-syj1022/scripts/surface.py ./ 
```
Make sure you understand what the script does. You need to modify the line below based on the specific facet you are assigned to. Please check what your assignment is carefully. Here ``(1, 0, 0)`` is the target facet and ``2`` means you are making a four-layer slab (double the unit cell in z-direction). 

```python
s1 = surface(bulk, (1, 0, 0), 2) #specify surface off of bulk
```

Note our goal is to create a 2x2x2 slab model. If you are working with (111) facet, please change this to:

```python
s1 = surface(bulk, (1, 1, 1), 5) #specify surface off of bulk
```

You might be wondering why we specify the number of layers as `5` here, but you will know why soon. Then please make sure you add vacuum space in z-direction. This is done by the code:

```
s1.center(vacuum=11, axis=2) #specify vacuum dimension and axis
```

After you have run `python surface.py` and check it through `ase gui init.traj`, you should be able to see structures exactly as shown below. Note this is a side view - press `X` to view from the side. If you work with (100) facet, please compare with the bottom left image, and if you work with (111) facet, please compare with the bottom right image.

<center><img src="../Images/raw_surface.png" alt="window" style="width: 800px;"/><br>
</center>

If you work with (100) facet, you may ignore this step, because (100) facet is perfectly symmetric from top to bottom. If you work with (111) facet, you will see you are actually assigned with either (111)-M or (111)-O. This denotes the termination - your surface can either end with metals or oxygens. You need to do one step further to make sure you have the correct facet termination. Recall I previously asked you to add one additional layer. Now this makes it easier for you to trim the structure. You might need some intuition on how to do this, but if you feel lost, follow these instructions: If you work with (111)-M, please remove the entire top layer of oxygens and the entire bottom layer of metals. If you work with (111)-O, please remove the entire bottom layer of metals and the entire bottom layer of oxygens. Once you finish, check the total number of atoms. There must be eight metals and eight oxygens for (100) facets, and there must be sixteen metals and sixteen oxygens for (111) facets.

Now remember we need a 2x2x2 slab model, but our current (100) model is 1x1x2. **If you work with (111), you DO NOT need to do this.** To repeat the cell in both x and y directions, go to `View` then `Repeat` and set to the correct values. Next, hit the `Set unit cell` button. Double check if your cell is actually doubled in both directions. 

Finally, select the bottom layers (two layers for (100) and four layers for (111)). This should be half of your entire cell. And then go to `Tools` -> `Constraints` -> `Fix`. You should see a "cross" symbol on every atom you selected. This means we are contraining the bottom two layers to their bulk lattice coordinates and only allowing the top two layers to relax.

Always remember to save your `.traj` file!

Once you finish setting up the surface, please check with me. You need Yingjie's permission to move on from here.


**Task 2: Add moisture components to your surface**

You do not need to work on this part if you are not assigned with an moisturized surface. HOWEVER, everyone needs to read and understand the instructions below, as everyone will work with moisturized surface in part 2 of the final project.

As we can imagine, when water interacts with the surfaces, it might directly adsorb with its molecular form or dissociatively adsorb in which case it breaks down into hydrogen, oxygen, and hydroxide. These particles play very important roles in altering carbonation performance. But to start with, we need to investigate if each individual (pairing) of them favors adsorption on the mineral surfaces. To find out, Colin and Yingjie have constructed these stability phase diagrams as shown below. Note for our current analysis, we only investigate the surfaces decorated with the dissociated particles (you might have molecular water directly adsorbed but this is quite computationally expensive to run). Here, you are only responsible for being able to intrepret from the diagrams. If you are interested in how to derive the equations leading to the diagrams, we can discuss later. In these diagrams, the black dashed line falls on the chemical potential of saturated water. This means water reaches an equilibrium between liquid and gaseous phases at this chemical potential. Right to the line means water can condense as a liquid and left to the line means water is in its vapor phase. Base on your knowledge of thermodynamics, identify the most stable (likely) hydrated surfaces when saturated water is present and add these particles to your structure.

<center><img src="../Images/MgO.png" alt="window" style="width: 800px;"/><br>
<img src="../Images/CaO.png" alt="window" style="width: 800px;"/><br>
</center>

Recall from HW5 on how to add atoms on top of another. Note by our convention, we only adsorb `OH` on the metals and `H` on the oxygens. If you need to add `H and OH`, please makes sure these particles are right next to each other.

**Task 3: HCO<sub>3</sub><sup>-</sup> and CO<sub>3</sub><sup>2-</sup> adsorption and thier chemical transformation**

As we have briefly touched on in HW5, the CO<sub>2</sub> adsorption can take place on many sites in addition to the lattice oxygen, and the CO<sub>2</sub> molecule can line up differently. DFT calculations can give reliable results for finding local minima in the total energy as the positions of the nuclei vary, but they do not provide any guarantee that the global energy minimum has been found. To use our best efforts to find the global minimum, we need to comprehensively walk through the many different possibilites. Yingjie has summarized the adsorption sites and initial configurations you need to investigate. The original paper to propose this method can be found here: (https://www.sciencedirect.com/science/article/pii/S1383586621010327).

<center><img src="../Images/position.png" alt="window" style="width: 800px;"/><br>
</center>

Recall in HW5 that you have manually added a CO<sub>2</sub> molecule on the MgO (100) surface and ran the calculations. Although you are not asked to do so, you may have access to my automation scripts for adding CO<sub>2</sub> on different sites with different initial configurations, in accordance to the diagram shown above. `CO2_M_ads.py` can automatically add CO<sub>2</sub> on `M_site` and `O_site`, `CO2_MO_ads.py` can automatically add CO<sub>2</sub> on the `M-O` bond, and `CO2_center_ads.py` as automatically add CO<sub>2</sub> on the center (four-fold center on (100) and three-fold center on (111)). I recommend you to download and understand these scripts. You are also welcome to play around with using the scripts to add CO<sub>2</sub> on your assigned surfaces, for familiarization purposes. But remember DO NOT submit jobs for CO<sub>2</sub>.

```python
cp /home/x-syj1022/scripts/CO2_M_ads.py ./
cp /home/x-syj1022/scripts/CO2_MO_ads.py ./
cp /home/x-syj1022/scripts/CO2_center_ads.py ./
```
As a background, the CO<sub>2</sub> speciation in water is greatly affected by solution pH, as shown in the plot below:

<center><img src="../Images/speciation.png" alt="window" style="width: 500px;"/><br>
</center>

Now in the final project, you will extend to study HCO<sub>3</sub><sup>-</sup> and CO<sub>3</sub><sup>2-</sup> adsorption. Please be aware that DFT cannot directly deal with charged species. Instead, we add the HCO<sub>3</sub><sup>-</sup> and CO<sub>3</sub><sup>2-</sup> as neutrally charged species, i.e. HCO<sub>3</sub>* and CO<sub>3</sub>*. DFT calculations can automatically correct the total charges. This can be verified by Bader Charge Analysis, but we will not dig into doing this for the final project. You are recommended to start with CO<sub>3</sub>*, since there are scripts to automatically CO<sub>3</sub>* on various sites. Please copy these scripts to your directory and make changes correspondingly. Note this is the hardest part of the final project and needs a lot of geometry work. Please feel free to ask for help from Yingjie on this part. 

```python
cp /home/x-syj1022/scripts/CO3_M_ads.py ./
cp /home/x-syj1022/scripts/CO3_MO_ads.py ./
cp /home/x-syj1022/scripts/CO3_center.ads.py ./
```

Once each calculation is done, you can visualize the final relaxed structure by running `python pwlog2traj_const.py ./pw.out rlx.traj`. This script can also be found in Yingjie's `scripts` folder. You may also directly use the alias `pwl`. What this script does is it converts the position information stored in `pw.out` into a graphically visualizable form. From there you can obtain useful information such as CO<sub>2</sub> bond lengths, bond angles, and if there are any abnormal events. These events include bond breakage within CO<sub>2</sub>, bond reformation, and severe surface reconstruction. In some cases, your structure may be refolded due to the periodic boundary conditions. If this happens to you, you can repeat your cell in `y` dimension once.

Below shows an example of a summary of CO<sub>2</sub> adsorption calculations:

<center><img src="../Images/example1.png" alt="window" style="width: 800px;"/><br>
</center>

Similarly, you may want to create a table for each of HCO<sub>3</sub>* and CO<sub>3</sub>* like the examples shown below. As you might have noticed, CO<sub>2</sub> (linear) is structurally very different from CO<sub>3</sub>* (trigonal planar). We would use `flat` to describe the horizontal configurations. Note you get `flat2` by rotating `flat1` by 30 degrees (check the automation scripts). 

Please organize your summary tables as shown below. In the convergence column, you may fill it with the path to your folder if that job fails.

<center><img src="../Images/CO3_table.png" alt="window" style="width: 800px;"/><br>
</center>
<center><img src="../Images/HCO3_table.png" alt="window" style="width: 800px;"/><br>
</center>

To make the automation scripts work, you are suggested to organize your directories in such a structure:

<center><img src="../Images/structure.png" alt="window" style="width: 300px;"/><br>
</center>

Upon completing CO<sub>3</sub>*, please write your own scripts to add HCO<sub>3</sub>*. This should only require a tiny adjustment on the CO<sub>3</sub>* scripts. If you feel lost, here is a showcase for HCO<sub>3</sub>* adsorption on MgO (111)-Mg at all 12 sites:

<center><img src="../Images/showcase.png" alt="window" style="width: 800px;"/><br>
</center>

If you run into job failing situations due to "invalid memory allocation", you may resume your jobs at the point they fail. To do this, please copy the `auto_cont.py` script and run it. This automatically submits a resumed job.

```bash
cp /home/x-syj1022/scripts/auto_cont.py ./
```

```python
python auto_cont.py
```

**Task 4: Self-consistent Field (SCF) calculations**

Referring back to the formula for adsorption energy calculation:

$$
\Delta E_\mathrm{ads} = E_\mathrm{slab+CO_{2}}  - E_\mathrm{slab} - E_\mathrm{CO_{2}}
$$

The calculated adsorption energy is a result of both CO<sub>2</sub> interaction with a surface AND surface relaxation. But we are only interested in the contribution from CO<sub>2</sub> interaction with the surface. To eliminate the interference of surface relaxation, we need to use the energy for the relaxed surface (but without the adsorbed CO<sub>2</sub>) for $$E_\mathrm{slab}$$ (in HW5 you were not asked to do so because the surface was barely relaxed, thus the relaxation effect was negligible). To proceed, you first translate `pw.out` into `rlx.traj` as previously discussed. Then you want to remove the CO<sub>3</sub>* or HCO<sub>3</sub>* from the relaxed structure and perform an SCF calculation. An SCF calculation computes the total energy of the given structure without performing geometric optimization. Make a directory and store the `rlx.traj` under the new directory. Go to the directory and type `scf` that calls the alias to automatically perform the atom deletion and job submission. Note this script only works for CO<sub>3</sub>*, and you need to make modification for removing HCO<sub>3</sub>*.  **You need to do this step for each completed relax calculations!** 

Note: Please use -1570.466 eV for the energy of HCO<sub>3</sub>* and -1554.607 eV for the energy of CO<sub>3</sub>*.

**Task 5: Density of States (DOS) calculations**

Once you have gone through all the calculations discussed above. Determine the starting conditions that resulted in the lowest adsorption energy. We want to plot the DOS of the lowest energy case. To run the DOS calculation, you first need to run an SCF calculation. Please write a script as follows to read `rlx.traj` and specify an SCF calculation. 

```python
from ase import io
from ase import Atoms
from espresso import espresso
from ase.optimize import QuasiNewton
from ase.constraints import FixAtoms
import sys
import pickle

slab =  io.read('rlx.traj')
slab.set_pbc([True,True,True])


calc = espresso(mode='scf',         #perform an scf calculation
                pw=500,             #plane-wave cutoff
                dw=5000,            #density cutoff
                xc='BEEF-vdw',      #exchange-correlation functional
                kpts=(4,4,1),       #k-point sampling;
                nbands=-30,         #20 extra bands besides the bands needed to hold
                sigma=0.1,
                opt_algorithm = 'bfgs',
                fmax = 0.03,
                nstep=500,
                nosym=True,
                #pot_extrapolation='second_order',
                #tempw=300,  #FOR MD
                convergence= {'energy':1e-5,
                    'mixing':0.1,
                    'nmix':10,
                    'mix':4,
                    'maxsteps':2000,
                    'diag':'david'
                    },  #convergence parameters
                 dipole={'status':True}, #dipole correction to account for periodicity in z
                 output = {'avoidio':False,
                    'removewf':True,
                    'wf_collect':False},
                 #U={'Ti':2.0},
                 #U_projection_type='atomic',
                 spinpol=False,
                 parflags='-npool 1',
                 onlycreatepwinp='pw.in',
                 outdir='.')   #output directory for Quantum Espresso files


slab.set_calculator(calc)
calc.initialize(slab)
```

Next, add the following lines in your submission script and submit the job. Note we have done this before in HW5, but now you need to make modifications to your `anvil.sub` yourself!

```bash
cd $SLURM_SUBMIT_DIR #Move to supply directory

mkdir -p $SCRATCH/$SLURM_JOBID
cp pw.in $SCRATCH/$SLURM_JOBID
cp dos.in $SCRATCH/$SLURM_JOBID

cd $SCRATCH/$SLURM_JOBID

mpirun /home/x-syj1022/apps/qe-7.2/bin/pw.x -nd 4   <pw.in> pw.out

/home/x-syj1022/apps/qe-7.2/bin/dos.x -in dos.in > dos.out  #DOS calculations

cp pw.out $SLURM_SUBMIT_DIR
cp dos.out $SLURM_SUBMIT_DIR
cp dos.dos $SLURM_SUBMIT_DIR
```
Please make sure you have `dos.in` in your directory. You can find it from my scripts:

```bash
cp /home/x-syj1022/scripts/dos.in ./
```

It should look like this:

```bash
&dos
   prefix='calc',
   outdir='.'
   Emin=-80.0
   Emax=20.0
   fildos='dos.dos'
/
```

Plot DOS using the script that Yingjie provides for you. This can be found by running:

```bash
cp /home/x-syj1022/scripts/dosplot.py ./
```

**Task 6: Bader charge analysis**

In order to determine the charge redistribution throughout the adsorption processes, we will perform a Bader charge analysis. For each adsorption case, you need to run three calculations: one for the system (slab + carbon intermediate), slab only, and carbon intermediate only. You will need the following scripts and they can be found in Yingjie's `scripts`: `bader.sub`, `relax-create-bader.py`, `pp.in`, and `fast_bader.py`. Check the script `fast_bader.py` and you will find that the script can automatically help you submit jobs.

<a name='silicate'></a>

Once the jobs are done, you should be able to see a `density.cube` for each calculation (in total three). Send these three files to Yingjie, and Yingjie will use VESTA to plot the charge density distribution for you. You are not required to do this yourself.

## Silicate ##

Please DO NOT proceed until Yingjie permits you so. We need to budget our computational resources before we make a decison on the complexity of this part.

This is part two of the final project. In this part, you will be studying your assigned silicate (forsterite, enstatite, larnite, wollastonite) surface with appropriate facet and termination. You will be carrying out similar calculations as before. You need less calculations but each calculations will take longer.

Starting from here, you are suggested to work together with your assigned teammates for combined results and analysis.

Although MgO and CaO are chemically the simpliest minerals for carbonation, you have already seen the thorough investigation of surface CO<sub>2</sub> adsorption is rather demanding. As we delve into more complex and asymmetric surfaces, the calculations that need to be done are skyrocketing. For example, for each larnite unit cell, there are four unique calciums and six oxygens exposed, whereas there are only one unqiue calcium and one oxygen in CaO. To fully cover every single site as what we have done for MgO and CaO, it requires 20 times as much as our previous work! Of course, the computational resources don't allow us to do this. Instead, we are going to start with focusing on one of the oxygen sites only, but note the oxygen sites are no longer equivalent, as the strucutre is highly assymmetric.

**Task 1: Adsorption energy of CO<sub>2</sub>, CO<sub>3</sub>, and HCO<sub>3</sub>**

Now that you have mastered the adsorption energy calculations in part one, you should find it relatively easy to work on this task. You only need one site, which is one of the oxygen sites. Please check your assigned material and find the oxygen site to be studied (marked in a black circle), as shown in the image below:

<center><img src="../Images/O_site.png" alt="window" style="width: 800px;"/><br>
</center>

The silicate surface structures can be obtained from Yingjie's directory:

```bash
cp /home/x-syj1022/CBE544/Bulks/(your silicate)/(your facet)/init.traj

##For example, if you are assigned with forsterite (010)
cp /home/x-syj1022/CBE544/Bulks/forsterite/010/init.traj
```

Same as before, you will study three configurations for both CO<sub>3</sub> and HCO<sub>3</sub>, namely `on`, `flat1`, and `flat2`. For CO<sub>2</sub>, you will study `on`, `along_x`, and `along_y`. Hope these names are self-explanatory, but please let Yingjie know if you have confusion on this. Hence, in total you will have 9 calculations, along with one SCF calculation for each as you have done this before. Please make a similar table as you have done before. There should be three rows for each carbon species and hence nine rows in total.

The reference energy for CO<sub>2</sub> is -1090.607 eV.

**Task 2: Reaction pathways**

Now you have all the adsorption energies of the three carbon species on both your assigned alkaline oxide and silicate (Yingjie provides you with the data of CO<sub>2</sub> on alkaline oxide along with the energies for bare surfaces, as shown below). Note if you need more geometric details, you may request from Yingjie. 

<center><img src="../Images/MO_CO2.png" alt="window" style="width: 900px;"/><br>
</center>

<center><img src="../Images/bare.png" alt="window" style="width: 400px;"/><br>
</center>

You will construct a plot showing the reaction pathway of mineral carbonation. A demonstration is given below:

<center><img src="../Images/pathway.png" alt="window" style="width: 800px;"/><br>
</center>

You will need the following references while constructing your reaction pathways: energy for H<sub>2</sub>O is -496.271 eV, energy for H<sub>2</sub> is -32.942 eV, energy for H is -16.471 eV.

**Task 3: Group study on the reaction pathways**

Upon obtaining the reaction pathways for your two material surfaces, you are asked to compare your results with your group members. Summarize any trends that your team observes. Key questions to be answered can be found in the final presentation and report requirements slides. Support your hypotheses with geometric arguments and/or Bader charge analysis. Please notify Yingjie beforehand if you plan to run additional Bader charge analysis. 
