# E2E ASR toolkit
This is an E2E ASR toolkit modified from Wenet (commit-id fca1d764492f8fe5bb4a1df55cd4c133ad804552).  
If this repositry can help you, we will be appreciate if you can star it and cite our papers.

This is the official implementation following paper:
[**Improving Mandarin Speech Recogntion with Block-augmented Transformer**](https://arxiv.org/abs/2207.11697) (Submitted to ICASSP 2022) 


We achieve state-of-the-art result on Aishell-1 Mandarin datasets.  
### Results
Currently we have released examples on Aishell-1 dataset.  
We achieve results on Aishell-1 below. All results are in CER%  

|  decoding mode/chunk size  | full |  
|  :----                     | :-:  |
|  attention decoder         |  -   | 
|  ctc greedy search         |  -   |
|  ctc prefix beam search    |  -   |
|  attention rescoring       | 4.29 |
|  LM + attention rescoring  | 4.05 |
 

### Update
- 2022/10/20: Release the first version, which contains se_layer into conformer for blockformer.

## Installation
The main dependencies of this code can be divided into two parts: `kaldi` and `wenet`  
- Install kaldi for feature extraction 
``` sh
  cd KALDI_ROOT
  git clone https://github.com/kaldi-asr/kaldi.git
  cd kaldi/tools/
  bash extras/check_dependencies.sh # make sure it's ok

  make -j 8
  cd ../src/
  ./configure --shared
  make depend -j 8
  make -j 8


- Clone the repo
``` sh
git clone https://github.com/LeonWlw/asr_blockformer.git
```

- Install Conda: please see https://docs.conda.io/en/latest/miniconda.html
- Create Conda env:

``` sh
conda create -n wenet python=3.8
conda activate wenet
pip install -r requirements.txt
conda install pytorch=1.10.0 torchvision torchaudio=0.10.0 cudatoolkit=11.1 -c pytorch -c conda-forge
```

- Optionally, if you want to use x86 runtime or language model(LM),
you have to build the runtime as follows. Otherwise, you can just ignore this step.

``` sh
# runtime build requires cmake 3.14 or above
cd runtime/libtorch
mkdir build && cd build && cmake .. && cmake --build .
```

## Discussion & Communication
you can directly discuss on [Github Issues](https://github.com/LeonWlw/asr_blockformer/issues).

## Acknowledge

1. We borrowed a lot of code from [Wenet](https://github.com/wenet-e2e/wenet) for conformer based modeling.
2. We borrowed a lot of code from [Kaldi](http://kaldi-asr.org/) for WFST based decoding for LM integration and feature extraction.

## Citations

``` bibtex
@ARTICLE{wei2022integrate,
  title={Improving Mandarin Speech Recogntion with Block-augmented Transformer},
  author={Xiaoming Ren, Huifeng Zhu, Liuwei Wei, Minghui Wu, Jie Hao},
  journal={arXiv preprint arXiv:2207.11697},
  year={2022}
}
```
