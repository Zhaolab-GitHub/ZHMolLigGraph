# [ZHMolLigGraph](http://zhaoserver.com.cn/ZHMolLigGraph/ZHMolLigGraph.html)

## Overview of ZHMolLigGraph: 
**Exploring ligand flexibility in nucleic acid scaffolds using graph neural networks** 

**We also provide an online calculation server for convenient use:** 
[Click to access the online server](http://zhaoserver.com.cn/ZHMolLigGraph/ZHMolLigGraph.html)

## Environment Setup

### Prerequisites:
* OS: Ubuntu 20.04 LTS
* NVIDIA GeForce 2080
* Python 3.8.18
* CUDA 10.2

### Installation Steps:
Follow these steps to set up your environment. We have successfully tested this in a clean environment:  

(1) Quick Install
```
conda env create -f environment.yml
conda activate ZHMolLigGraph
```

(2) Or you could also create a new conda environment as follows:
```
conda create -n ZHMolLigGraph python=3.8.18
conda activate ZHMolLigGraph
```

```
pip install h5py==3.10.0
pip install scipy==1.10.1
pip install tqdm==4.66.1
pip install pandas==2.0.3
pip install torch==1.7.1
```

```
pip install torch_cluster-1.5.8-cp38-cp38-linux_x86_64.whl
pip install torch_scatter-2.0.5-cp38-cp38-linux_x86_64.whl 
pip install torch_sparse-0.6.8-cp38-cp38-linux_x86_64.whl
pip install torch_geometric==1.6.3
pip install torchvision==0.8.2
```

## Data & Pretrained Models
* Data Files​​: Available at [Zenodo](https://zenodo.org/records/17097553)
* Pretrained Models​​: Download prediction_model.pt and selection_model.pt from [Zenodo](https://zenodo.org/records/17097553) and place them in models/ directory.

### Workflow
1. Prepare the receptor structure, ligand structure, and an initial docked pose.
2. Run `ZHMolLigGraph.py` with the required input files and pretrained models.
3. The program performs flexibility exploration and feasibility selection.
4. Refined poses and prediction scores are written to the output directory.

## Usage
```
usage: ZHMolLigGraph.py [-h] [--gpu_id GPU_ID] [--ligand_file LIGAND_FILE] [--nucleic_file NUCLEIC_FILE] [--pose_file POSE_FILE]
                        [--output_file OUTPUT_FILE] [--prediction_model PREDICTION_MODEL] [--selection_model SELECTION_MODEL]
                        [--tmp_dir TMP_DIR]
```
                  
Example files are provided in the data/ directory.

### Required input files
For each nucleic acid–ligand complex, the following three input files are required:

- `--nucleic_file`: receptor structure in PDB format (e.g., `data/native/298D.rec.pdb`)
- `--ligand_file`: ligand structure in MOL2 format (e.g., `data/native/298D.lig.mol2`)
- `--pose_file`: initial docked complex / input pose in PDB format to be refined (e.g., `data/before_dock/298D.pdb`)

Run the following command using 298D as an example:

```
python ZHMolLigGraph.py \
  --ligand_file=data/native/298D.lig.mol2 \
  --nucleic_file=data/native/298D.rec.pdb \
  --pose_file=data/before_dock/298D.pdb \
  --output_file=data/after_dock/298D \
  --prediction_model=models/prediction_model.pt \
  --selection_model=models/selection_model.pt \
  --tmp_dir=ZHMolLigGraph_tmp/
```
You can run
```
python ZHMolLigGraph.py  -h
```
to view the full command-line help and argument descriptions.

optional arguments:
  -h, --help            show this help message and exit
  --gpu_id GPU_ID       GPU device ID
  --ligand_file LIGAND_FILE
                        input ligand file
  --nucleic_file NUCLEIC_FILE
                        input nucleic file
  --pose_file POSE_FILE
                        input docked pose / complex file
  --output_file OUTPUT_FILE
                        output file of the ligand, should be given as an output prefix rather than a full filename.
  --prediction_model PREDICTION_MODEL
                        path to the pose prediction model
  --selection_model SELECTION_MODEL
                        path to the pose selection model
  --tmp_dir TMP_DIR     temporary directory for ZHMolLigGraph processing


### Output files
For an input complex such as `298D`, the program writes:

- `data/after_dock/298D.mol2`: refined ligand pose(s)
- `data/after_dock/298D.txt`: acceptance/rejection probability for the generated pose(s)

Temporary files are written to the directory specified by `--tmp_dir`.

### Runtime note
The neural-network inference step is relatively fast. In the current pipeline, the most time-consuming step is the Open Babel–based conformational optimization / minimization during pose generation and refinement. Therefore, total runtime depends strongly on the number of poses processed and on the available CPU/GPU hardware.

## Contact
If you have any comments, questions or suggestions about the ZHMolLigGraph, please contact:  
Yunjie Zhao; E-mail: yjzhaowh@ccnu.edu.cn  
Chengwei Zeng; E-mail: cwzengwuhan@mails.ccnu.edu.cn
