# Pneumonia Detection from Chest X-Rays

This project is part of the **Udacity AI for Healthcare** nanodegree program.

The **Project Overview**, **Pneumonia and X-Rays in the Wild** and **About the Dataset** sections below are taken from the starter description of the project delivered by Udacity. The **Project Steps** section has been amended and is complemendet by my comments and contains my results. 

## Project Overview

In this project, you will apply the skills that you have acquired in this 2D medical imaging course to analyze data from the NIH Chest X-ray Dataset and train a CNN to classify a given chest x-ray for the presence or absence of pneumonia. This project will culminate in a model that can predict the presence of pneumonia with human radiologist-level accuracy that can be prepared for submission to the FDA for 510(k) clearance as software as a medical device. As part of the submission preparation, you will formally describe your model, the data that it was trained on, and a validation plan that meets FDA criteria.

You will be provided with the medical images with clinical labels for each image that were extracted from their accompanying radiology reports. 

The project will include access to a GPU for fast training of deep learning architecture, as well as access to 112,000 chest x-rays with disease labels  acquired from 30,000 patients.

## Pneumonia and X-Rays in the Wild

Chest X-ray exams are one of the most frequent and cost-effective types of medical imaging examinations. Deriving clinical diagnoses from chest X-rays can be challenging, however, even by skilled radiologists. 

When it comes to pneumonia, chest X-rays are the best available method for diagnosis. More than 1 million adults are hospitalized with pneumonia and around 50,000 die from the disease every
year in the US alone. The high prevalence of pneumonia makes it a good candidate for the development of a deep learning application for two reasons: 1) Data availability in a high enough quantity for training deep learning models for image classification 2) Opportunity for clinical aid by providing higher accuracy image reads of a difficult-to-diagnose disease and/or reduce clinical burnout by performing automated reads of very common scans. 

The diagnosis of pneumonia from chest X-rays is difficult for several reasons: 
1. The appearance of pneumonia in a chest X-ray can be very vague depending on the stage of the infection
2. Pneumonia often overlaps with other diagnoses
3. Pneumonia can mimic benign abnormalities

For these reasons, common methods of diagnostic validation performed in the clinical setting are to obtain sputum cultures to test for the presence of bacteria or viral bodies that cause pneumonia, reading the patient's clinical history and taking their demographic profile into account, and comparing a current image to prior chest X-rays for the same patient if they are available. 

## About the Dataset

The dataset provided to you for this project was curated by the NIH specifically to address the problem of a lack of large x-ray datasets with ground truth labels to be used in the creation of disease detection algorithms. 

The data is mounted in the Udacity Jupyter GPU workspace provided to you, along with code to load the data. Alternatively, you can download the data from the [kaggle website](https://www.kaggle.com/nih-chest-xrays/data) and run it locally. You are STRONGLY recommended to complete the project using the Udacity workspace since the data is huge, and you will need GPU to accelerate the training process.

There are 112,120 X-ray images with disease labels from 30,805 unique patients in this dataset.  The disease labels were created using Natural Language Processing (NLP) to mine the associated radiological reports. The labels include 14 common thoracic pathologies: 
- Atelectasis 
- Consolidation
- Infiltration
- Pneumothorax
- Edema
- Emphysema
- Fibrosis
- Effusion
- Pneumonia
- Pleural thickening
- Cardiomegaly
- Nodule
- Mass
- Hernia 

The biggest limitation of this dataset is that image labels were NLP-extracted so there could be some erroneous labels but the NLP labeling accuracy is estimated to be >90%.

The original radiology reports are not publicly available but you can find more details on the labeling process [here.](https://arxiv.org/abs/1705.02315) 


### Dataset Contents: 

1. 112,120 frontal-view chest X-ray PNG images in 1024*1024 resolution (under images folder)
2. Meta data for all images (Data_Entry_2017.csv): Image Index, Finding Labels, Follow-up #,
Patient ID, Patient Age, Patient Gender, View Position, Original Image Size and Original Image
Pixel Spacing.


## Project Steps

### 1. [Exploratory Data Analysis](EDA.ipynb)

The first part of this project involve exploratory data analysis (EDA) to understand and describe the content and nature of the data. This includes:

* The patient demographic data analysis
* The distribution of other diseases that are comorbid with pneumonia
* Number of disease per patient 
* Pixel-level assessments of the imaging data

![pneumonia comorbidities](/images/Pneumonia&#32;comorbidities.png)

### 2. [Building and Training Your Model](Build&#32;and&#32;train&#32;your&#32;model.ipynb)

VGG16 pretrained on ImageNet is used. Classifier layers are added and trained, the last convolutional layer of the original VGG16 architecture is fine-tuned. After training the model performance is evaluated.

![training binary accuracy and loss](/images/Training&#32;accuracy&#32;and&#32;loss.png)

### 3. [Clinical Workflow Integration](Inference.ipynb)

This step focuses on creating a DICOM wrapper that takes in a DICOM file and outputs an image in the format appropriate for the model. There are also some checks performed of essential DICOM metadata fields.

### 4. [FDA  Submission](FDA_Submission.pdf)

The steps in FDA Submission are derived from the FDA's official guidance on both the algorithm description and the algorithm performance assessment. These include:

1.  Intended Use statement, indications for use, device limitations, clinical impact
2.  Algorithm design and function, preprocessing steps
3.  Algorithm training details and metrics
4.  Information about the training and validation datasets
5.  Ground Truth
6.  FDA Validation Plan

![flowchart](/images/Flowchart.png)
