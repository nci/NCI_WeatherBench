# NCI WeatherBench Notebooks

This repository contains notebooks for NCI WeatherBench, which is a Deep learning benchmark developed at NCI, Australia. 
It is created using the Pangeo data specification (https://github.com/pangeo-data/WeatherBench); however, the data spans from 1959 to 2022, which is 50% more compared to that of the original one.
It is about 10TB in size and was created completely using the NCI high-performance compute and disk resources, to the best of our knowledge it is first the Australian Deep learning benchmark of this size.  
Details about the benchmark can be found here: https://geonetwork.nci.org.au/geonetwork/srv/eng/catalog.search#/metadata/f8295_5164_0873_0706  


## How to use 

0) Before you start.
    You must be a member of the following NCI projects
    ```bash
    wb00
    dk92
    vp91
    ```
Additionally, you need a project that has enough resources to run V100 GPUs for several hours. 
One can apply to join NCI projects here: https://my.nci.org.au/


1) Download the notebooks in any suitable location on Gadi 
```bash
cd /to/a/Gadi/location
git clone https://github.com/maruf-anu/NCI_WeatherBench.git
```

2) Launch an NCI ARE (https://are.nci.org.au) Jupyter instance with the following parameters. 
```bash
Walltime (hours): <As required>
Queue: gpuvolta
Compute Size: 1gpu (minimum or custom for more memory)
Project: <Choose one that has enough resources>
Storage: gdata/dk92+gdata/z00+gdata/wb00+scratch/vp91+<All other storage that you need>

Module directories: /g/data/dk92/apps/Modules/modulefiles
Modules: NCI-ai-ml/23.10 NCI_weatherbench/2024.03.21 
Jobfs size: 200GB
```
3) From the ARE instance, navigate to the notebook's location and run them individually.

## Notebooks

There are nine notebooks in the repository. The first three are baseline models, the next two are Keras/Tensorflow models, the next two are Pytorch implementations of the two previous notebooks, and the last two are for result visualization.  

- `1a.climatology-persistence.ipynb`: Contain two baseline prediction methods: persistance, and climatology.

- `1b.climatology-persistence.ipynb`: Same as the previous notebook but uses higher resolutions, 2.8125 and 1.40625. (Optional)

- `2.linear-regression-baseline.ipynb`: Another baseline model, linear regression is used.

- `3a.cnn-example.ipynb`: A CNN model training using Keras.

- `3b.cnn-example.ipynb`: Similar to the previous CNN model, however, trains three different models, a 3-day, 5-day, and 6-hour iterative prediction model.

- `3c.cnn-example.ipynb`: Pytorch implementation of the `3a.cnn-example.ipynb` notebook 

- `3d.cnn-example.ipynb`: Pytorch implementation of the `3b.cnn-example.ipynb` notebook 

- `4a.evaluation-checkpoint.ipynb`: Creates and saves prediction and calculates accuracy for all previous models (persistence, climatology, linear regression, and CNN)

- `4b.evaluation-checkpoint.ipynb`: Displays the results produced in the previous notebook.


**Note**
- Depending on the code, each notebook may take from 30 minutes to 2 hours to run. 
- When a notebook is finished, reset it to free the memory before running the next one. Otherwise, you may run out of memory.
- If a notebook runs out of memory, the system automatically restarts it. If you find this is happening to you, then simply start a bigger/custom ARE instance with more memory. 
- All created models and predictions are stored in the following directory: `/scratch/vp91/<USER>/NCI-Weatherbench/`. The `vp91` is a training project and is cleaned at regular intervals. If you want to save your data then copy it to a safe location. Alternatively, one can set a different location (`PREDDIR` variable) at the top of each notebook.