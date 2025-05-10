# USVTrack

USVTrack is a benchmark for tracking multiple objects in complex water surface scenes.

<div align="center"><img src="images/demo.png" ></div>

## Overview
- [News](#News)
- [Dataset](#Dataset)
- [Evaluation](#Evaluation)

## News

- May 10, 2025: A subset of USVTrack and Evaluation code are released.

## Dataset
### Introduction
Multi-object tracking (MOT) in water surface scenes is crucial for the autonomous navigation of Unmanned Surface 
Vehicles (USVs). However, existing MOT datasets rarely focus on these scenes. Moreover, the few available water surface 
MOT datasets contain limited data shot onboard and concentrate narrowly on specific marine scenes, creating a significant 
gap from real-world USV navigation applications. To promote research on USV autonomous navigation, we introduce USVTrack, 
a multi-object tracking benchmark collected entirely onboard. It covers diverse and complex water-surface scenes, 
including both inland and marine surface scenes, and is characterized by a high proportion of small objects and varied backgrounds.
Specifically, USVTrack consists of 27 video sequences, comprising a total of 8,283 annotated frames and over 100k bounding boxes. 
Among them, 3,223 frames are from inland scenes (sequence_1 to sequence_13), and 5,060 frames are from maritime scenes (sequence_14 to sequence_27).

### Dataset Link

The complete dataset will be available at [ORCA-UBOAT Datasets](https://orca-tech.cn/datasets) soon.

### Dataset Structure

The USVTrack dataset is organized as follows:

~~~
{USVTrack ROOT}
|-- usvtrack
|   |-- train
|   |   |-- sequence_1
|   |   |   |-- img1
|   |   |   |   |-- 000001.jpg
|   |   |   |   |-- ...
|   |   |   |-- gt
|   |   |   |   |-- gt.txt            
|   |   |   |-- seqinfo.ini
|   |   |-- ...
|   |-- test
|   |   |-- ...
|   |-- label.txt
~~~

### Dataset Annotation Format

We follow the annotation format of [MOTChallenge](https://motchallenge.net/).

~~~
<frame>, <id>, <bb_left>, <bb_top>, <bb_width>, <bb_height>, <conf>, <cls>, <vis>
~~~

USVTrack includes a total of 15 object categories, listed as follows:

~~~
Format: <cls_id>-<cls_name>
1-boat, 2-speedboat, 3-duckboat, 4-speedboat, 5-yacht, 6-cruise, 7-oceanLiner, 8-aquaplane,
9-buoy, 10-person, 11-disruptors, 12-reflection, 13-building, 14-occlusion, 15-shine
~~~


## Evaluation

We use [Evaluation/TrackEval](./Evaluation/TrackEval) for evaluation based on a more user-friendly version of
[TrackEval](https://github.com/JackWoo0831/Easier_To_Use_TrackEval/blob/main/README_ENG.md). 

To do evaluation with our provided code, we organize the track results as follows:
~~~
{Track Results ROOT}
|-- usvtrack (split name)
|   |-- TRACKER_NAME
|   |   |-- sequence_x.txt
|   |   |-- ...
|   |-- ...
~~~

sequence_x.txt is the tracking result of sequence_x, and its format should be:

~~~
<frame>, <id>, <bb_left>, <bb_top>, <bb_width>, <bb_height>, <conf>, -1, -1, -1
~~~

Then update the dataset path, result path and tracker name in the config file [Evaluation/TrackEval/configs/usvtrack.yaml](./Evaluation/TrackEval/configs/usvtrack.yaml). 
We have provided a template.

Finally, run the following command to evaluate:

```
cd Evaluation/TrackEval
python scripts/run_custom_dataset.py --config_path ./configs/usvtrack.yaml
```

The evaluation result will be saved to output path in the config file.