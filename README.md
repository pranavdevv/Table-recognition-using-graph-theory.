
```

This is a maths club project done by
PRANAV V CSE
YUGENDHAR ECE
MADHUMITHA CSBS
PRIYADHARSHINI CSBS
AAKASH ECE

This is a table recognition project based on DGCNN. It is completely made with python.
It uses web framework to make it as a website. The problem with this project is that it is an untrained model. 

Most of the attempts to train the model with UNLV dataset by having 3 files as test, train and validation set went into vain.

This model uses OCR to find word locations and CNN to derive a feature map of the given image. Both the outputs are used to create a interaction map using GNN. Finally dense nets are used to get knowlege map as output.

The `python` dir is supposed to be the path where a script is to be run, or alternatively, it could be added to the
`$PYTHONPATH` environmental variable. It would contain further directories:
1. `bin` contain the scripts which are to be run from the terminal. Within bin, there would be multiple folders,
short for different classes of executable programs.
    1. `iterate` for running training or inference.
    2. `analyse` for analysing inference output.
    3. `checks` this was for testing various files while development. You can safely ignore it.
2. `iterators` provides functionality to iterate through the datasets while you are training or testing.
3. `layers` contains basic layers for graph networks
3. `models` contains the main model and network segments. Most of the functionality can be found in `basic_model.py`.
Start to trace from there.
4. `ops` contains basic modified operations. These contains the advanced graph operations code. 
5. `readers` is for readers, entities responsible for reading the data from `tfrecords`. Their format can be changed in
this file.
6. `libs` contains all other helper and library functions.

Within the context of this repository, `iterate` refers to any of train, test or anything which is done iteratively. You
can say anything that is done iteratively mostly on the GPU. So if there is an `iterator` somewhere, it probably refers
to an entity which handles training, testing etc.

## Preparation
1. Prepare the dataset. For this, you are required to divide the dataset into three different sections, test, train and validation.
 Test set will be used to run the analysis after training is done. Backpropagation will be run on the train set. Validation set is
  used to produce plots for tensorboard to monitor performance of the network.
2. The dataset files have to be in `tfrecords` format. Make a new file called `train_files.txt`. It should contain full paths of all the training tfrecords files. For example:
    ```
    /home/shahrukhqasim/dataset/train_1.tfrecord
    /home/shahrukhqasim/dataset/train_2.tfrecord
    /home/shahrukhqasim/dataset/train_3.tfrecord
    ```
3. Similarly, prepare `validation_files.txt`, `test_files.txt`. The contents of these three files should not be overlapping.
4. Make a config file according to the format given in `configs/config.ini.example`. This file determines all the settings, dataset locations and results generation paths. The example config file contains documentation for your ease. If you are unclear about a setting, send an email to me or generate an issue in this repository.
5. Each config file will contain multiple configurations. These configurations are recommended to be used for different models.
So, for instance, you make different configs for `DGCNN`, `GravNet` and `Convolutional` networks.

## Training
To run the training, you need to issue the following command:

```$ python bin/iterate/table_adjacency_parsing.py path/to/the/config/file config```

While you are running the training, you can monitor using tensorboard. The paths are to be set into the config file as described in the previous step. Use the following command to run the tensorboard:

```
$ tensorboard --logdir=/media/all/shahrukhqasim/Tables/TrainOut/betaout/summary
```

You can monitor the performance after that in your browser. The port number will be displayed when you run the above command.

## Inference
You first need to run inference which will generate `bin` files in numpy pickle format.

```$ python bin/iterate/table_adjacency_parsing.py path/to/the/config/file config --test True```

```
TODO: Analaysis code and further documentation is coming.
```
 
## Installation
Python 3.5+ is needed. We recommend  using virtualenv but anaconda should also work fine.

The required packages are listed in `requirements.txt`. They can be installed by:
```
$ pip install -r requirements.txt
```

In addition to this, you need to download another repository from here:

[github.com/jkiesele/caloGraphNN](https://github.com/jkiesele/caloGraphNN)

Let's say you clone it into `/home/shahrukhqasim/caloGraphNN`. You need to add this path to the `$PYTHONPATH` environmental variable.
```
$ export PYTHONPATH=$PYTHONPATH:/home/shahrukhqasim/caloGraphNN
```

In addition to this, you should run all the commands from inside of `python` directory. And `python` should also be present in `$PYTHONPATH` environmental variable.
```
$ export PYTHONPATH=$PYTHONPATH:/home/shahrukhqasim/TIES-2.0/python
```

You can also add `.` to the `$PYTHONPATH` if you know you will always run the commands from inside of `python` directory.

It is advised you make a `sh` file with these export commands and a command which activates the virtual environment.
 I use the following sourcing file (`ties.sh`):
```
source ~/Envs/h3/bin/activate
cd /Users/shahrukhqasim/Workspace/TIES-2.0/python
export PYTHONPATH=$PYTHONPATH:/Users/shahrukhqasim/Workspace/caloGraphNN:/Users/shahrukhqasim/Workspace/TIES-2.0
```

I source it every time I want to run training or inference using:
```
$ source ties.sh
```
