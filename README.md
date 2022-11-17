# Paper Implementataion: Deep Statistical Solvers

![image](https://user-images.githubusercontent.com/73030180/202532571-6ff3f7e1-1b71-46aa-ba42-2e537118e05f.png)

For the course project of DS303, We worked on the implementation of the paper [Deep Statistical Solvers](https://hal.inria.fr/hal-02974541) (accepted at NeurIPS 2020) in TensorFlow. This project helped us understand the working of **Graph Neural Networks**.




## Datasets

For each dataset, download all the files that are available at the links below, and place them in the corresponding folder:

- [Dataset Linear systems](http://doi.org/10.5281/zenodo.4024811) --> place them in `datasets/linear_systems`
- [Dataset AC power flow 14 nodes](http://doi.org/10.5281/zenodo.4024866) --> place them in `datasets/acpf_14`
- [Dataset AC power flow 118 nodes](http://doi.org/10.5281/zenodo.4024875) --> place them in `datasets/acpf_118`


## Training

To train the models used in the paper, here are the exact commands that were used:

- Linear systems experiments

```
python main.py --data_dir=datasets/linear_systems --max_iter=1000000 --minibatch_size=100 --track_validation=1000 --learning_rate=1e-3 --discount=0.9 --latent_dimension=10 --hidden_layers=2 --correction_updates=30 --alpha=0.001
```

- AC power flow 14 nodes experiments

```
python main.py --data_dir=datasets/acpf_14 --learning_rate=3e-3 --minibatch_size=1000 --alpha=1e-2 --hidden_layers=2 --latent_dimension=10 --correction_updates=10 --track_validation=1000
```

- AC power flow 118 nodes experiments

```
python main.py --data_dir=datasets/acpf_118 --learning_rate=3e-3 --minibatch_size=500 --alpha=3e-4 --hidden_layers=2 --latent_dimension=10 --correction_updates=30 --track_validation=1000 --discount=0.9
```

## Results

Here are the metrics for the three different experiments, and for each of the three corresponding models.
The main metric is indeed the correlation with the best existing optimization method.
Check the notebooks to obtain these results.

### Linear systems experiments

The best existing method is the LU decomposition.

| Model name         | Model 0 | Model 1 | Model 2 |
| ------------------ |---------|---------|---------|
| Correlation w/ LU  | 99.99%  | 99.99%  | 99.99%  |
| Loss 10th perc.    | 3.0 E-4 | 3.8 E-4 | 2.7 E-4 |
| Loss median        | 6.0 E-4 | 1.3 E-3 | 6.9 E-4 |
| Loss 90th perc.    | 1.5 E-3 | 4.0 E-3 | 2.3 E-3 |

### AC power flow - 14 nodes

The best existing method is the Newton-Raphson method (NR). The correlation is in term of active power flows through 
power lines.

| Model name         | Model 0 | Model 1 | Model 2 |
| ------------------ |---------|---------|---------|
| Correlation w/ NR  | 99.99%  | 99.99%  | 99.99%  |
| Loss 10th perc.    | 2.5 E-5 | 3.4 E-5 | 4.1 E-5 |
| Loss median        | 4.0 E-5 | 6.3 E-5 | 1.0 E-4 |
| Loss 90th perc.    | 1.0 E-4 | 1.5 E-4 | 4.4 E-4 |

### AC power flow - 118 nodes

The best existing method is the Newton-Raphson method (NR). The correlation is in term of active power flows through 
power lines.

| Model name         | Model 0 | Model 1 | Model 2 |
| ------------------ |---------|---------|---------|
| Correlation w/ NR  | 99.99%  | 99.99%  | 99.99%  |
| Loss 10th perc.    | 5.3 E-7 | 1.3 E-6 | 1.7 E-7 |
| Loss median        | 1.3 E-6 | 1.7 E-6 | 2.8 E-7 |
| Loss 90th perc.    | 3.4 E-6 | 2.5 E-6 | 4.8 E-7 |
