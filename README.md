# Supplementary Docs

1. A detailed overview of the training process

    
        https://github.com/AnonUserGit/AIMC2022/blob/main/Detailed%20Training%20Overview.pdf
    
    
2. A Tutorial on how to use the system


        https://vimeo.com/706414509
    
    
3. A video recording of a typical jam session with the system 


        https://vimeo.com/706414714
    
    
4. Audio Recordings of some Jams & Generations using the system


        https://soundcloud.com/anonomy-submer/sets/generations-using-the-system

      





# Velocity Groove to Drum Performance with Transformer Neural Networks
This project and many of the ideas that we have tried out are based on the work done
by the Magenta team in their [Groove project](https://magenta.tensorflow.org/datasets/groove) and paper [Learning to
Groove with Inverse Sequence Transformations](https://arxiv.org/abs/1905.06118), including the very own definition of
the Tap2Drum task and the Groove MIDI Dataset.

In this work, we use a transformer encoder with a direct representation to convert a velocity groove to a drum performance.

To track the learning and metrics of the model we have used the [wandb](https://wandb.ai/) library and API. You can find
all our experiment runs in this [wandb project](https://wandb.ai/[anon]).

To try some of our trained models out, you can check out our [colab notebook](./Transformer_Groove_Tap2Drum_Demo.ipynb).

If you want to get the train script running locally, make sure to
1. Install our conda environment (using [environment.yml](./environment.yml)) to get all dependencies, or download all dependencies and install them through `pip`.
2. Download the zipped dependencies folder ([dependencies.zip](./dependencies.zip)) and place the repositories at the same level as this one, like so:
```
project_name
├───BaseGrooveTransformers
│   └───...
├───GrooveEvaluator
│   └───...
├───hvo_sequence
│   └───...
├───preprocessed_dataset
│   └───...
└───TransformerGrooveTap2Drum
    └───...
```

The repo has been developed along (and depends on) these projects (some of the links might not work for the moment, as
they are still private repositories, but will eventually be public):  
- [hvo_sequence](https://github.com/[anon]/hvo_sequence) - HVO data structure definition (which is the data type we
will use to train the model) & functions to transform between hvo, [note_seq](https://github.com/magenta/note-seq)
and MIDI formats
- [GMD2HVO_PreProcessing](https://github.com/[anon]/GMD2HVO_PreProcessing) - Used to extract 2-bar sequences from
the [Groove MIDI Dataset](https://magenta.tensorflow.org/datasets/groove), convert them to HVO format and save the
preprocessed dataset
- [preprocessed_dataset](https://github.com/[anon]/preprocessed_dataset) - Zipped preprocessed datasets in HVO format
- [BaseGrooveTransformers](https://github.com/[anon]/BaseGrooveTransformers) - Transformer model used
- [GrooveEvaluator](https://github.com/[anon]/GrooveEvaluator) - Evaluator that calculates a number of metrics
given some ground truths and predictions and is able to export html and audio files.


Now you should be ready to run the training script located in this repository,
[`model/train_tap2drum.py`](./model/train_tap2drum.py).

One more thing! If you would like to track your model in wandb, make sure you have logged in and change
your project name/config to your own in [`model/train_tap2drum.py`](./model/train_tap2drum.py) line 54:
```python
wandb.init(config="configs/myconfig.yaml", project="myproject")
```

If you don't want to upload any data to wandb, you can uncomment lines 25-26:
```python
import os
os.environ["WANDB_MODE"]="offline"
```

And that should hopefully work!

