---
title: "Alphafold on ISU HPC infrastructure"
layout: single
header:
  overlay_color: "444444"
  overlay_image: /assets/images/margaret-weir-GZyjbLNOaFg-unsplash_dark.jpg
---



# AlphaFold2 *standalone* preinstalled on HPC@ISU

The *Pronto* and *Nova* clusters currently have three versions of AlphaFold pre-installed, which you can find using the `module` command:  

`module avail alphafold`    

```
---------------------------------------- /opt/rit/singularity/modules ----------------------------------------
   alphafold/2.0.0    alphafold/2.1.1    alphafold/2.1.2 (D)

  Where:
   L:  Module is loaded
   D:  Default Module
```
The latest version will be loaded by default (D), but you can select any of the available versions.    
```
module load alphafold                   # loads alphafold/2.1.2
module load alphafold/2.1.1             # loads alphafold/2.1.1
```
To facilitate the preparation of AlphaFold jobs and submission into the SLURM queue, the HPC team has prepared a set of instructions and tips available via the execution of `note_4_demo` alias. The notes along with our benchmark results are included in the *Performance of the AlphaFold* section.
```
note_4_demo                                                            # prints contents on the screen
less note_4_demo                                                       # opens the preview of the
cp -r  /opt/rit/singularity/images/alphafold/demo ~/your_workdir/      # copies the demo/ with sample SLURM scripts
```
After loading the selected AlphaFold module, you can use the predefined **alphafold** wraps, which contain aliases to the corresponding option sets. More detailed options for each of the wraps can be viewed with the `--help` or `--helpfull` options.
* `alphafold` , only single-chain modeling allowed
* `alphafold_casp14` , uses the settings from CASP14
* `alphafold_multimer` , multi-chain structure modeling allowed

## AlphaFold options

To display the full list of alphafold options, execute:

`alphafold --help`

The basic options you need to set up in each job submitted to the queue are:

| option | value | description |
|---------|---------|---------|
| --fasta_paths= | /absolute/path/to/your/FASTA/input_dir/filename.fasta | paths to input FASTA files |
| --output_dir= | /absolute/path/to/your/outputs | path to a directory that will store the results |

Other options that may be useful:

| flag | description |
|---------|---------|
| --use_precomputed_msas | If you job failed in the step after the sequence alignment, you can use this option to re-use previous sequence alignments and speed-up prediction. |
| --use_gpu_relax | The relaxation stage will run on GPU. The flag is in all `alphafold*` wraps already. Not need to add in user's script. |
| --norun_relax | The relaxation stage can now be disabled using the *run_relax* flag. Then, you can quickly get a few unrelaxed structure models.|

## AlphaFold Inputs

Likewise with ColabFold, the standalone implementation of AlphaFold on HPC clusters also requires the amino acid sequence of the protein in FASTA format as the only input file.    
* In particular, `alphafold` wrap is intended to model **monomeric** proteins, that is, proteins with a single chain. Therefore, there can only be one protein sequence in the input file and you will need a separate FASTA files for all your targets.

  Input file: `2gb1.fasta ` or `monomer.fa`

 ```
 >2GB1_1|Chain A|PROTEIN G|Streptococcus sp.
 MTYKLILNGKTLKGETTTEAVDAATAEKVFKQYANDNGVDGEWTYDDATKTFTVTE
 ```

* While, `alphafold_multimer` is designed to model **multimeric** proteins, that is, proteins with multiple chains. Therefore, there can only be one protein complex per sequence file, which has the multiple sequence entries `>` for each of the required chains.

  Input file: `complex.fasta` or `multimer.fa`

 ```
  >Chain_A
  MDEDGLPLMGSGIDLTKVPAIQQKRTVAFLNQFVVHTVQFLNRFSTVCEEKLADLSLRIQQ
  >CHAIN_B
  MNRTTPDQELVPASEPVWERPWSVEEIRRSSQSWSLAADAGLLQFLQEFSQQTISRTHEIKKQVDGLIRETKATDCRLHNVFNDFLMLSNTQFIENRVYDEEVEEPVL
 ```


###SLURM script configuration

By the principal rule, all calculations performed in the HPC infrastructure should be delegated to the computing nodes. To do this, you need to prepare a configuration script and submit the job to a queue. The task manager on the HPC@ISU infrastructure is **SLURM**.

### Parameters required to set up AlphaFold tasks

Protein structure modeling with AlphaFold is a multi-operation process. For example, for sequence alignment and template search AlphaFold uses CPUs but other computational steps, such as amber-relaxation, can be accelerated by using available GPUs. Newer versions of AlphaFold can recognize more than one GPU card when starting but only one card is used in the tensorflow-GPU step. So, please **allocate only 1 GPU** card to avoid blocking resources for other users.

* See *[AlphaFold performance](04-AlphafoldPerformance.md)* section for details regarding content of the Table below

  | param | SMALL | MEDIUM | LARGE |  HUGE  | notes |
  |---------|---------|---------|---------|---------|---------|
  | SEQ length | <= 200aa | <= 800aa | <= 2500aa | > 2500aa |
  | #SBATCH |  |
  | --nodes= | 1 | 1 | 1 | 1 | AlphaFold runs on single node. No MPI. |
  | --ntasks= | 8 | 8<sup>*</sup> | 8<sup>*</sup> | 8<sup>*</sup> | AlphaFold uses hard-coded 8 or 4 CPUs<br>for sequence alignment and template search, <br>so ntasks has to be 8 or larger. |
  | --mem= | 180G | 180G | 180G | 256G or 312G | If you got run-out-of memory error, <br>simply increase the memory allocation. |
  | --time= | 1:0:0 | 5:0:0 | 10:0:0 | 1-0:0:0 | Request extension if needed. |
  | -p | gpu | gpu | gpu| amdgpu |
  | **NOVA** |
  | --gres= | gpu:1 | gpu:v100:1 | gpu:a100:1 | gpu:a100:1 | Allocate ONE GPU card. |
  | **PRONTO** |
  | --gres= | gpu:1 | gpu:rtx_6000:1 | gpu:a100-pcie:1 | gpu:a100-pcie:1 | Allocate ONE GPU card. |

  <sup>\*</sup> ntasks = 16 (MEDIUM) or 32 (LARGE, HUGE) for AlphaFold_**v2.1.1** <br>
  <sup>\*</sup> ntasks = 8 for AlphaFold_**v2.1.2** and the following

### Create SLURM script file

`touch alphafold_monomer.sh`

Then, copy-paste the example content (settings for SMALL monomeric protein) making sure to update the working directory path `m_work` and input file name `input.fasta` .

```
#!/bin/bash
#SBATCH --nodes=1                         # (required) number of requested nodes
#SBATCH --ntasks=8                        # (required) number of requested CPUs
#SBATCH --mem=180G                        # (required) memory allocation
#SBATCH --time=1:0:0                      # (required) runtime allocation
#SBATCH -p gpu                            # (required) type of GPU nodes
#SBATCH --gres=gpu:1                      # (required) number of requested GPUs (ONE only!)

#SBATCH --job-name="AF-TAG_pdb"           # (optional) job name visible in the queue
#SBATCH --output="out-TAG_pdb-%j"         # (optional) filename for standard output & errors

module load alphafold

### TIPS: use the full path for input and output, run sequences one by one.
m_work=/work/path_to/your/workdir
cd ${m_work}
time alphafold --fasta_paths=${m_work}/INPUTS/monomer.fasta --output_dir=${m_work}/OUTPUTS
```
**Sumbit job to queue**    
`sbatch alphafold_monomer.sh`


### Expected OUTPUTS
[]


[AlphaFold index](Alphafold-landingPage.md){: .btn  .btn--primary}
[Next](03B-Alphafold-SCINet.md){: .btn  .btn--primary}
[Table of contents](../index.md){: .btn  .btn--primary}
