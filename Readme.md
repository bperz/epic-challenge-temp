# EPiC 2023: The Emotion Physiology and Experience Collaboration

This repository contains data and helpful code for the EPiC 2023 competition.

## 1. The goal of the EPiC 2023 competition
We aim to (1) establish the best approaches to moment-to-moment inference of valence and arousal from physiology, (2) compare how model accuracy scores vary across different validation scenarios, and (3) promote open science much needed to accelerate the affective science research.

## 2. Your task
Your task is to predict continuous values of valence and arousal based on the available physiological data. Formally, this is a regression problem.

## 3. Experiment description
Some details on the experiments were concealed in order to avoid bias. All information will be disclosed after the competition resolution.

We use data from the experiment on emotion annotation conducted in laboratory conditions. Study participants watched emotional stimuli and annotated their emotions continuously in arousal-valence space. During the experiment, the following physiological activity was measured:

- Cardiac activity:
	- with photoplethysmography (bvp)
	- with electrocardiograph (ecg)

- Muscle activity:
	- corrugator supercilii (emg_coru)
	- trapezius (emg_trap)
	- zygomaticus major (emg_zygo)

- Electrodermal activity (gsr)

- Respiration trace (rsp)

- Skin Temperature (skt)

All physiological signals were recorded with the sampling frequency of 1kHz, and annotations were recorded with the frequency of 20Hz.

## 4. Data structure
All the data is stored in `releases` section of the repository (on github website it should appear to the right of this text). Data is divided into four scenarios, each representing a different validation approach:
1. Across-time scenario corresponds to the hold-out validation approach that respects chronology. Each sample is divided into training and test parts based on the time. A sample represents a single person watching a single video - first part of the activity is in the train set and the later part in the test set.
This scenario analyzes how well a model utilizes knowledge obtained from the past data to the new data from the same set of participants and stimuli.
2. Across-subject scenario matches the leave-N-subjects-out validation approach. Participants are divided into random groups. All the samples of a given group of participants belong either to the train or test set, depending on the fold. There are 5 folds in this scenario and each fold leaves out a different set of subjects.
This scenario validates a model’s ability to generalize knowledge obtained from a group of people to other, previously unseen, people.
3. Across-elicitor scenario follows the leave-one-stimuli-out validation approach. There are two samples (videos) per each quadrant in arousal-valence space, and both are excluded in a given fold. There are 4 folds in total, each excluding one arousal-valence quadrant.
This scenario validates how well models trained on three arousal-valence quadrants can infer states experienced in the fourth quadrant.
4. Across-version scenario resembles the hold-out validation approach that doesn’t necessarily respect chronology. There are two samples per arousal-valence quadrant, so one will be used to train the model while the other to test it. Thus, this scenario has 2 folds.
This scenario validates how well models trained on one version of the quadrants can infer states experienced in the other version of the quadrants.
Similarly to the first scenario, this scenario analyzes how well a model performs for the same set of participants and a similar task.

In each scenario you will find train and test data sets. You can further divide the train set into train and validation sets, if you find it reasonable.
In the test set, the length of the physiology is 20 seconds longer than the length of the self-annotation part (ground truth). This is to allow building models that utilize time windows of up to 20 seconds long – 10 seconds of physiology before and 10 seconds after the annotation timestamp. Please note, this is your sole decision what architecture, which physiological signals, which features, what window size, to use.

Data files in test sets have columns (arousal and valence) and timestamps defined. Your taks is to predict arousal and valence levels for all of the provided timestamps. You can use the files as a template that you have to fill with predictions produced by your solution.

To extract the data you can use any software supporting encrypted zip files. For Windows operating system we recommend 7-Zip.

For a more visual explanation of how the dataset is constructed and organized, you can see the attached example notebook `explain_data.ipynb`. It shows how to load data, and what do data look like when stored in memory and plotted. 

## 6. Requirements and submission procedure

TBD
-no cheating
-clean code, comments
-easy to recreate
-performance measure
-how to prepare solution files, especially in scenarios with folds - naming convention, format, zipped or not, etc.

## 7. Additional information and materials
Using Python is not required but we strongly encourage it.