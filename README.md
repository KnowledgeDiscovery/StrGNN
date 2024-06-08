# StrGNN

The `StrGNN` repository contains code for an end-to-end structural temporal Graph Neural Network model for detecting anomalous edges in dynamic graphs. The method implemented here is described in [this paper](https://dl.acm.org/doi/pdf/10.1145/3459637.3481955).


## Installation

Go to detection folder and install required packages

```
bash install.sh
```

## Dataset Preprocessing

Please follow the example format in data folder to preprocess data:

* acc_email.npy is the graph input with shape (T, N, N), where T is the number of snapshot and N is the number of nodes in the graph

* email0.01 contains train_pos_id, train_neg_id, test_pos_id, test_neg_id, train_pos, train_neg, test_pos, test_neg:

* train_pos_id is with shape (N,). It indicates the which snapshot the edge (in train_pos) come from

* train_pos is with shape (N, 2). Each row i corresponds to a edge in the snapshot train_pos_id[i]

* train_neg_id is with shape (N,). It indicates the which snapshot the edge (in train_neg) comes from

* train_neg is with shape (N, 2). Each row i corresponds to a non-exist edge (sample for training classifier) in the snapshot train_neg_id[i]

* similar for test_pos_id, test_neg_id, test_pos, test_neg



## Model Training

Please use example command to train the model. More training setup available in Main.py

```
python Main.py --graph=acc_email.npy --split=email0.01
```

Anomaly detection with time-evolving graph. Parameters are the same as accumulate setting, the only difference is that the graph is time-evolving graph

```
python Main_statistic.py --graph=sta_email.npy --split=email0.01_sta
```


## Citation

If you find the code in this respository useful for your research, please cite our paper:
```
@inproceedings{cai2021structural,
  title={Structural temporal graph neural networks for anomaly detection in dynamic graphs},
  author={Cai, Lei and Chen, Zhengzhang and Luo, Chen and Gui, Jiaping and Ni, Jingchao and Li, Ding and Chen, Haifeng},
  booktitle={Proceedings of the 30th ACM international conference on Information \& Knowledge Management},
  address = {New York, NY, USA},
  pages={3747--3756},
  year={2021},
  numpages = {10}
}
```

## Acknowledgements 

The code is implemented based on 

https://github.com/muhanzhang/SEAL

https://github.com/muhanzhang/pytorch_DGCNN

## Other information

- Accumulated Graph and Time-evolving Graph:

   Typically, there are two ways to model dynamic systems as dynamic graphs, namely, accumulated graph and time-evolving graph. The accumulated graph automatically and incrementally constructs an entire graph using all vertices and edges until the current timestamp. In contrast, the time-evolving graph is constructed using vertices and edges only appearing in the current timestamp. Therefore, each snapshot represents the graph state at a single instant of time.

## License

Creative Commons Attribution-NonCommercial (CC BY-NC) 4.0 International License

The OC4Seq is released under a CC BY-NC 4.0 International License:
https://creativecommons.org/licenses/by-nc/4.0.

NonCommercial — You can not use the code for commercial purposes.
