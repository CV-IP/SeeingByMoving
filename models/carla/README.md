# Documentation

This folder contains code for SbM experiments on replica dataset. Install the dependencies following the main `README.md`. The general structured of the `model` and `experiment` files described in main `README.md` file is followed here as well.

## File Descriptions

`model_carla_viewmine.py`: This is the main model file for the SbM experiment. Here, the model fires maskrcnn on each view and propagate the confident views to the other views. This file can also be used for storing the data labels to create a dataset with SbM labels. 

`model_carla_gt.py`: This model files generates the data with ground truth labels in the required format.

`model_carla_viewmine_semisup.py`: The model file used for weak supervision experiment.

`utils/sparse_to_contour.py`: This file runs convex hull on the data generated by the above model files to prepare it in the format that `detectron2` requires.

`utils/finetune_detectron.py`: This file is used for finetuning detectron2 on the processed data generated by `sparse_to_contour.py`.

`model_carla_eval.py`: This is the evaluation model file for evaluating trained detectron2 on the test set.

## mAP Evaluations

- Clone this repository https://github.com/rafaelpadilla/Object-Detection-Metrics inside the carla folder.
- The model files creates new folders containing the txt files with detection information in the format specified in the above repository, so for mAP evaluation just execute the following command from inside the `Object-Detection-Metrics` folder. 

```
python pascalvoc.py -gt ../gt_pred/ -det ../maskrcnn_pred/ -gtformat 'xyrb' -detformat 'xyrb' -t 0.5
```

For details on the arguments of the above command, please refer this [README.md](https://github.com/rafaelpadilla/Object-Detection-Metrics/blob/master/README.md)
