# FCN for Semantic Image Segmentation on TensorFlow

This is an implementation of Fully Convolutional Networks (FCN) on Python 3 and TensorFlow achieving **68.5 mIoU** on the PASCAL VOC 2012 test set. The model generates semantic masks for each object class in the image using a VGG16 backbone. It is based on the work by E. Shelhamer, J. Long and T. Darrell described in the [PAMI FCN](https://arxiv.org/abs/1605.06211) and [CVPR FCN](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Long_Fully_Convolutional_Networks_2015_CVPR_paper.html) papers.

![Semantic Segmentation Sample](assets/sample1.png)

The repository includes:

* Source code of FCN built on VGG16

* Training code for PASCAL VOC

* Pre-trained weights for PASCAL VOC

* Code to download the PASCAL VOC 2012 dataset and extra data from [Hariharan et al.](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/), and prepare datasets for training and validation

* Data augmentation code based on OpenCV

* Jupyter notebook to visualize the data augmentation pipeline with PASCAL VOC 2012

* Other examples of training with the Kitty Road and CamVid datasets

* Evaluation of trained models for several datasets

The code is documented and designed to be easy to extend for your own dataset. If you use it in your projects, please consider citing this repository (bibtex below).



# Getting started

* [demo.ipynb](demo.ipynb): This notebook is the easiest way to start. It provides an example of using a FCN model pre-trained on PASCAL VOC to segment object classes in your own images. It includes code to run object class segmentation on arbitrary images.

* [data_augmentation.ipynb](fcn/data_augmentation.ipynb): This notebook visualizes the different pre-processing steps to prepare the training data. The augmentation process is built on OpenCV.

* ([fcn_run_loop.py](fcn/fcn_run_loop.py), [fcn_model.py](fcn/fcn_model.py))): These files contain the main VGG16 FCN implementation details.

* [fcn_training.ipynb](fcn/fcn_training.ipynb): This notebook reports training results for several datasets and can be used to reproduce them.

 

# Validation Results

This section reports validation results for several datasets on the following experiments:
 * **One-off** end to end training of the **FCN-32s** model starting from the pre-trained weights of VGG16.
 * **One-off** end to end training of **FCN-16s** starting from the pre-trained weights of VGG16.
 * **One-off** end to end training of **FCN-8s** starting from the pre-trained weights of VGG16.
 * **Staged** training of **FCN-16s** using the pre-trained weights of FCN-32s.
 * **Staged** training of **FCN-8s** using the pre-trained weights of FCN-16s. 
 
The models are evaluated against standard metrics, including **pixel accuracy** (PixAcc), **mean class accuracy** (MeanAcc), and **mean intersection over union** (MeanIoU). All training experiments were done with the Adam optimizer. Learning rate and weight decay parameters were selected using grid search.
 

## Kitty Road

[Kitty Road](http://www.cvlibs.net/datasets/kitti/eval_road.php) is a road and lane prediction task consisting of 289 training and 290 test images. It belongs to the KITTI Vision Benchmark Suite. As test images are not labelled I have done a 80/20 split of the training set to evaluate the model. You will need to request a download link by going to the website. Click to download the base kit and provide an email address to receive your link.

|                                                                | PixAcc      | MeanAcc     | MeanIoU     |
|----------------------------------------------------------------|-------------|-------------|-------------|
| [FCN-32s](results/kitty_road_fcn32s.png)                       | 98.1        | 97.3        | 93.8        |
| [FCN-16s-oneoff](results/kitty_road_fcn16s_oneoff.png)         | 98.6        | 97.9        | 95.6        |
| [FCN-8s-oneoff](results/kitty_road_fcn8s_oneoff.png)           | **98.8**    | **98.5**    | **96.2**    |
| [FCN-16s-staged](results/kitty_road_fcn16s_staged.png)         | **98.8**    | 98.0        | 96.0        |
| [FCN-8s-staged](results/kitty_road_fcn8s_staged.png)           | 98.6        | 98.2        | 95.3        |
 

## CamVid

The [Cambridge-driving Labeled Video Database](http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamVid/) (CamVid) is the first collection of videos with object class semantic labels, complete with metadata. The database provides ground truth labels that associate each pixel with one of 32 semantic classes. I have used a modified version of CamVid with 11 semantic classes and all images reshaped to 480x360. The training set has 367 images, the validation set 101 images and is known as [CamSeq01](http://mi.eng.cam.ac.uk/research/projects/VideoRec/CamSeq01/).

|                                                                | PixAcc      | MeanAcc     | MeanIoU     |
|----------------------------------------------------------------|-------------|-------------|-------------|
| [FCN-32s](results/cam_vid_fcn32s.png)                          | 92.6        | 73.4        | 65.0        |
| [FCN-16s-oneoff](results/cam_vid_fcn16s_oneoff.png)            | 93.9        | 79.2        | 70.4        |
| [FCN-8s-oneoff](results/cam_vid_fcn8s_oneoff.png)              | 94.5        | 81.0        | **73.2**    |
| [FCN-16s-staged](results/cam_vid_fcn16s_staged.png)            | 93.8        | 77.9        | 69.7        |
| [FCN-8s-staged](results/cam_vid_fcn8s_staged.png)              | **94.6**    | **81.5**    | 72.9        |
 

## PASCAL VOC 2012

The [PASCAL Visual Object Classes Challenge](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/) includes a segmentation challenge with the objective of generating pixel-wise segmentations giving the class of the object visible at each pixel, or "background" otherwise. There are 20 different object classes in the dataset. It is one of the most widely used dataset for research.

|                                                                | PixAcc      | MeanAcc     | MeanIoU     |
|----------------------------------------------------------------|-------------|-------------|-------------|
| [FCN-32s](results/pascal_voc_2012_fcn32s.png)                  | 90.7        | 69.3        | 60.0        |
| [FCN-16s-oneoff](results/pascal_voc_2012_fcn16s_oneoff.png)    | 91.0        | 72.9        | 61.9        |
| [FCN-8s-oneoff](results/pascal_voc_2012_fcn8s_oneoff.png)      | **91.1**    | **73.6**    | **62.5**    |
| [FCN-16s-staged](results/pascal_voc_2012_fcn16s_staged.png)    | **91.1**    | 72.3        | 61.9        |
| [FCN-8s-staged](results/pascal_voc_2012_fcn8s_staged.png)      | 91.0        | 72.1        | 61.7        |
 

## PASCAL Plus

PASCAL Plus refers to the PASCAL VOC 2012 dataset augmented with the annotations from [Hariharan et al](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/).

|                                                                | PixAcc      | MeanAcc     | MeanIoU     |
|----------------------------------------------------------------|-------------|-------------|-------------|
| [FCN-32s](results/pascal_plus_fcn32s.png)                      | 91.3        | 79.3        | 64.5        |
| [FCN-16s-oneoff](results/pascal_plus_fcn16s_oneoff.png)        | 92.4        | 78.1        | 67.3        |
| [FCN-8s-oneoff](results/pascal_plus_fcn8s_oneoff.png)          | **92.6**    | 77.1        | **68.5**    |
| [FCN-16s-staged](results/pascal_plus_fcn16s_staged.png)        | 92.3        | **78.5**    | **67.5**    |
| [FCN-8s-staged](results/pascal_plus_fcn8s_staged.png)          | 92.4        | 77.9        | 67.2        |

 
# Training on PASCAL VOC
To make it easier to start, I've provided weights pre-trained with the augmented PASCAL VOC dataset. You can use those weights as a starting point to train your own variation of the network. The training and evaluation code is in `fcn_run_loop.py`. You can import this module in a Jupyter notebook (see the provided notebook for examples) or you can run it directly from the command line as such:

```
# Train a new model starting from pre-trained PASCAL VOC weights
python3 samples/coco/coco.py train --dataset=/path/to/coco/ --model=coco

# Train a new model starting from VGG16 weights
python3 fcn/fcn_run_loop.py train --fcn_version=FCN32 --dataset=pascal_voc_2012 --data_dir=[dataset root directory] --vgg16_dir=[vgg16 weights directory] --model_name=[the model's name]  -- n_epochs=50 --optimizer=adam --learning_rate=1e-5 --weight_decay=1e-6

# Continue training a model that you had trained earlier
python3 samples/coco/coco.py train --dataset=/path/to/coco/ --model=/path/to/weights.h5

# Continue training the last model you trained. This will find
# the last trained weights in the model directory.
python3 samples/coco/coco.py train --dataset=/path/to/coco/ --model=last
```

You can also run the COCO evaluation code with:
```
# Run PASCAL VOC evaluation on a trained model
python3 fcn/fcn_run_loop.py evaluate --dataset=pascal_voc_2012 --data_dir=[dataset root directory] --model_name=[the model's name]
```


## Differences from the Official Paper
This implementation follows the FCN paper for the most part, but there are a few differences. Please let me know if I missed anything important.

* **Optimizer:** The paper uses SGD with momentum and weight decay. I've used Adam with a learning rate of 1e-5 with weight decay of 1e-6 for all versions of FCN (FCN-32s, FCN-16s, FCN-8s) and both for one-off and staged training. I did not double the learning rate for biases in the final solution.

* **Image Resizing:** To support training multiple images per batch we resize all images to the same size. For example, 512x512px on PASCAL VOC. As the largest side of any image is 500px, all images are center padded with zeros. I find this approach more convinient than having to pad or crop features after each up-sampling layer to re-instate their initial shape before the skip connection.

* **Data Augmentation**: The original publication does not augment the data. Finding no noticeable improvement. It is not possible to prevent overfitting with the standard PASCAL VOC dataset, even with data augmentation. 

To validate this approach, we compared our computed bounding boxes to those provided by the COCO dataset.
We found that ~2% of bounding boxes differed by 1px or more, ~0.05% differed by 5px or more, 
and only 0.01% differed by 10px or more.

 

 

## Citation
Use this bibtex to cite this repository:
```
@misc{fmahoudeau_fcn_2019,
  title={FCN methods for semantic image segmentation on TensorFlow},
  author={Florent Mahoudeau},
  year={2019},
  publisher={Github},
  journal={GitHub repository},
  howpublished={\url{https://github.com/fmahoudeau/fcn}},
}
