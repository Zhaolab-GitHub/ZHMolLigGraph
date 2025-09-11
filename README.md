# [ZHMolLigGraphh](http://zhaoserver.com.cn/ZHmol-LigGraph/ZHmol-LigGraph.html)

## Overview of ZHMolLigGraph: 
ZHmol-LigGraph is a method that exploring ligand flexibility in nucleic acid scaffolds using graph neural networks 

**We also provide an online calculation server for convenient use:** 
[Click to access the online server](http://zhaoserver.com.cn/ZHmol-LigGraph/ZHmol-LigGraph.html)

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
conda activate ZHmol-LigGraph
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
* Data Files​​: Available at at [Zenodo](https://zenodo.org/records/15519001)
* Pretrained Models​​: Download prediction_model.pt and selection_model.pt from [Zenodo](https://zenodo.org/records/15519001) and place them in models/ directory.

## Usage
Examples have been put in data/ directory.  
For any nucleic acid-ligand complex structure (single or multiple inputs), you could run:

```
bash run_ZHmol-LigGraph.sh
```


### Output
Results are saved in data/after_dock/ as:
* .mol2 files (the obtained complex structures)
* .txt file (the probability to accept/reject decision (0-1))

## Contact
If you have any comments, questions or suggestions about the ZHMolLigGraph, please contact:  
Yunjie Zhao; E-mail: yjzhaowh@ccnu.edu.cn  
Chengwei Zeng; E-mail: cwzengwuhan@mails.ccnu.edu.cn
