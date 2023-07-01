## [StarGAN-VC-Mode-Transformation]

This is a pytorch implementation of the paper: [Multiple Speech Mode Transformation using Adversarial Network](https://ieeexplore.ieee.org/document/9986477).

**The converted voice examples are in *samples***



## [Dependencies]
- Python 3.6+ (3.7.13 used)
- numpy (1.16.2 used)
- tensorflow (2.8.0 used)
- pytorch 1.0
- librosa 
- pyworld 
- tensorboardX
- scikit-learn


## [Usage]

### Download dataset


The dataset is present [here](https://drive.google.com/drive/folders/1DI22XoZNRS4p4ek2r-Jv1Lep8byko2uy?usp=share_link). 
The dataset is in Bengali language and it contains 160 utterences for each mode in the training set, while 30 in the test set. Each wav file is about 5 seconds and it contains non parallel utterances.

1. **training set:** In the paper, **three modes** were selected from `the dataset`. So we created the corresponding folder(eg. conv(Conversation), lec (Lecture), read (Read/Extempore) ) to `./data/speakers`, each containing 160 audio samples.
2. **testing set:** In the paper,  **three modes** were selected from `the dataset`. So we created the corresponding folder(eg. conv(Conversation), lec (Lecture), read (Read/Extempore) ) to `./data/speakers_test`.

The data directory now looks like this:

```
data
├── speakers  (training set)
│   ├── conv 
│   ├── lec 
│   ├── read 
├── speakers_test (testing set)
│   ├── con 
│   ├── lec 
│   ├── read 
├──
```

### Preprocess

Extract features (mcep, f0, ap) from each speech clip.  The features are stored as npy files. We also calculate the statistical characteristics for each speaker.

```
python preprocess.py
```

This process may take minutes !

```
data
├── speakers  (training set)
│   ├── conv 
│   ├── lec 
│   ├── read 
├── speakers_test (testing set)
│   ├── con 
│   ├── lec 
│   ├── read 
├── processed
     ├──...
```


### Train

```
python main.py

or

To continue from a saved checkpoint use:
python main.py --resume_iters 150000
```


### Convert



```
python main.py --mode test --test_iters 150000 --src_speaker conv --trg_speaker "['conv','read']"
```

Note: 
 * Consider looking at the [notebook](StarGan_VC_Pytorch.ipynb) to setup and proceed with the training and testing purpose.


## [Network structure]

![Snip20181102_2](https://github.com/hujinsen/StarGAN-Voice-Conversion/raw/master/imgs/Snip20181102_2.png)


 Note: 
 * This implementation follows the [original StarGAN-VC paper’s](https://arxiv.org/abs/1806.02169) network structure, which we were able to use successfully for mode conversion.
 
 ## [Reference]

* [StarGAN-VC paper](https://arxiv.org/abs/1806.02169)

* [StarGAN paper](https://arxiv.org/abs/1711.09020)

* [CycleGAN-VC paper](https://arxiv.org/abs/1711.11293)

## [Acknowledgement]

[StarGAN-VC code](https://github.com/hujinsen/pytorch-StarGAN-VC) (Original Network Architecture)

[StarGAN-VC code](https://github.com/liusongxiang/StarGAN-Voice-Conversion)

[StarGAN code](https://github.com/yunjey/stargan)
