# WATT-EffNet-for-aerial-disaster-scene-classification

(Another github page on the same project can be found at: https://github.com/TanmDL/WATT-EffNet/tree/main)

This is a github repository for our work on "A Novel Wider ATTention EFFicientNet (WATT-EffNet) for Classifiying Aerial Disaster Images" by Gao Yu Lee, Tanmoy Dam, Md Meftahul Ferdaus, Daniel Puiu Poenar and Vu N. Duong.

Our proposed algorithmic structure are designed with applications to UAV-based aerial image disaster scene classification.
Accepted by IEEE Geoscience and Remote Sensing letters (IEEE GRSL) (2023). A version of the paper is available at arxiv: https://arxiv.org/pdf/2304.10811.pdf 

Unmanned aerial vehicles (UAVs) embedded with a deep learning (DL) classification model can be utilized for search-and-rescue operations, as well as monitoring and mitigating the effects of natural disasters. In such cases, the UAV must quickly comprehend the crisis scenario to limit search areas. This ensures that the UAV's limited power and processing resources are used properly and effectively. To achieve such goal, an effective and lightweight method for scene classification must be developed. Existing approaches, on the other hand, prioritize achieving the highest possible accuracy on classification-based benchmark datasets while ignoring computationally efficient observations. To mitigate such research gap, we have introduced a novel Wider ATTention EFFicientNet (WATT-EffNet) to achieve higher accuracy with a lighter architecture than the baseline EfficientNet. Implementation of width-wise incremental feature module and attention mechanism over width-wise features in WATT-EffNet contributes to the network's light structure. UAV-based aerial disaster image classification dataset is considered for analysing the effectiveness of the purposed WATT-EffNet. Our method surpassed baseline by up to a factor of 15 in terms of classification accuracy and by 38.3% in terms of computing efficiency measured by the Floating Point Operations per second (FLOPs). An ablation study is also conducted by varying the width of WATT-EffNet to examine a higher accuracy at a lower FLOPs. 

See WATT-EffNet Structure FINAL.png for an illustration of our algorithmic architecture design.

**The training weights of the optimal configuration are contained in the weights file.**

**The necessary updates for this repository has been done, but may still be updated in the future.**

# Dataset

Our work is trained and evaluated on the Aerial Image Database for Emergency Response (AIDER) subset by Kyrkou and Theocharides [1]. The dataset comprised of images illustrating four major types of disasters: fire, floods, afermath of building collapses and traffic collisions, as well as images of non-disasters (normal class) in a relatively larger amount than the other four to replicate real-world scenario as close as possible. Some samples of the images of each class is shown in AIDER Images Examples.png. Unlike the original dataset which comprised of a total of 8540 images, the subset only contained 6433 images. The AIDER subset can be downloaded from https://zenodo.org/record/3888300.

AIDER subset image sets distribution in our approach:

| Class | Train | Valid | Test | Total per Class |
| ------ | ------| ------| ------| ------|
|**Collapsed Building**| 367 | 41 | 103 | 511 |
|**Fire**| 249 | 63 | 209 | 521 |
|**Flood**| 252 | 63 | 211 | 526 |
|**Traffic**| 232 | 59 | 194 | 485 |
|**Normal**| 2107 | 527 | 1756 | 4390 |
|**Total per Set**| 3207 | 753 | 2473 | **6433** |


# Some Results

Due to the imbalance class distribution of the AIDER subset, we utilized the mean F1 scores for the classification effectiveness evaluation and the floating point operations per second (FLOPs) for the efficiency computation.

We experimented with 1, 3 and 5 MBConv blocks in the EfficienNetB0 architecture, utilizing a width of 12 for 1MBConv block, widths of 2 to 7 for 3MBConv blocks and width factors of 2 and 3 for 5MBConv blocks. Possible combinations of our WATT-EffNet architecture can be written in the form WATT-EffNet-*d*-*k*, where *d* is the number of MBConv blocks and *k* is the width factor per block. Each variant is ran for 10 times during the evaluation and its mean F1 scores and corresponding standard deviation are recorded.

WATT-EffNet model variants:

| Model variant | F1 (%) | FLOPs | Parameters |
| ------ | ------| ------| ------|
| WATT-EffNet-1-12| 83.5 | 22 | 106,501 |
| WATT-EffNet-3-2| 84.2 | 22 | 106,629 |
| WATT-EffNet-3-3| 83.3 | 22 | 205,673 |
| WATT-EffNet-3-4| 86.0 | 22 | 335,693 |
| WATT-EffNet-3-5| 85.2 | 22 | 496,689 |
| **WATT-EffNet-3-6**| **88.5** | **22** | **688,661** |
| WATT-EffNet-3-7 | 87.3 | 22 | 911,609 |
| WATT-EffNet-5-2 | 86.8 | 22 | 371,493 |
| WATT-EffNet-5-3 | 86.4 | 22 | 720,233 |

All the SOTA and our approach are trained from scratch on the AIDER subset and serves as a baseline. The SOTA evaluated include MobileNetV1 [2], MobileNetV2 [3], SqueezeNet [4], ShuffleNet [5], EfficientNetB0 [6] and EmergencyNet [2]. The optimal variant of our propsoed approach is the WATT-EffNet-3-6, which comprised of 3 MB Conv blocks and a width factor of 6. 

| SOTA Model | F1 (%) | FLOPs | Parameters |
| ------ | ------| ------| ------|
| MobileNetV1 [2]| 84.0 | 972 | 3,233,861 |
| MobileNetV2 [3]| 82.0 | 625 | 2,282,629 |
| SqueezeNet [4]| 87.3 | 531 | 725,073 |
| ShuffleNet [5]| 84.7 | 972 | 4,023,865 |
| EfficientNetB0 [6]| 80.0 | 774 | 3,499,453 |
| EmergencyNet [2]| 84.5 | 185 | **94,420** |
| **WATT-EffNet-3-6** | **88.5** | **22** | 688,661 |

# Code Instructions
1) Run Data_loading.py. This would load the AIDER data subset, sort the images and labels into the five respective classes, and split them into train, valid and test set.
2) Run one_hot_encode.py to convert the numerical labels into one-hot encoded label. **Note: Due to tensorflow/Keras version update, sparse=False has become sparse_output=False. Please use the latest syntax**.
3) Run Attention.py for the attention module. **Note: tf.keras.ops has been used instead of tf.keras on certain keras operation, as the latter is obsolete in the newest version. Also, tf_keras instead of tf.keras in the Sequential syntax has been used.**
4) Run the MBConvblocks.py. **Note: tf.keras.ops has been used instead of tf.keras on certain keras operation, as the latter is obsolete in the newest version. Also, tf_keras instead of tf.keras in the Sequential syntax has been used.**
5) Run the watt-effnet-3-6.py. Note that based on our experiment, the WATT-EffNet-3-6 is the ideal WATT-EffNet configuration. The attention is imbued in the architecture. **Note: tf.keras.ops has been used instead of tf.keras on certain keras operation, as the latter is obsolete in the newest version. Also, tf_keras instead of tf.keras in the Sequential syntax has been used.**
6) Proceed to train the model. This is found under train.py.
7) Finally, run the F1 metrics.py to output the F1 score, and the compute_flops.py to output the flops value.

Please use the new weights file with "...weights.h5" as per the newly updated version requirement of keras.

# Citation Information

Please cite the following paper if you find it useful for your work: \

G. Y. Lee, T. Dam, M. M. Ferdaus, D. P. Poenar and V. N. Duong, "WATT-EffNet: A Lightweight and Accurate Model for Classifying Aerial Disaster Images," in *IEEE Geoscience and Remote Sensing Letters*, vol. 20, pp. 1-5, 2023, Art no. 6005205, doi: 10.1109/LGRS.2023.3270227.

@article{lee2023watt, \
  title={Watt-effnet: A lightweight and accurate model for classifying aerial disaster images}, \
  author={Lee, Gao Yu and Dam, Tanmoy and Ferdaus, Md Meftahul and Poenar, Daniel Puiu and Duong, Vu N}, \
  journal={IEEE Geoscience and Remote Sensing Letters}, \
  volume={20}, \
  pages={1--5}, \
  year={2023}, \
  publisher={IEEE}
}

# Some References

[1] C. Kyrkou and T. Theocharides, “Emergencynet: Efficient aerial image
classification for drone-based emergency monitoring using atrous convolutional feature fusion,” *IEEE Journal of Selected Topics in Applied
Earth Observations and Remote Sensing*, vol. 13, pp. 1687–1699, 2020.

[2] A. G. Howard, M. Zhu, B. Chen, D. Kalenichenko, W. Wang, T. Weyand, M. Andreetto, and H. Adam, “Mobilenets: Efficient convolutional neural networks for mobile vision applications,” *arXiv preprint arXiv:1704.04861*, 2017.

[3] M. Sandler, A. Howard, M. Zhu, A. Zhmoginov, and L.-C. Chen, “Mobilenetv2: Inverted residuals and linear bottlenecks,” in *Proceedings
of the IEEE conference on computer vision and pattern recognition*, 2018, pp. 4510–4520.

[4] F. Iandola, S. Han, M. Moskewicz, K. Ashraf, W. Dally, and K. Keutzer, “Squeezenet: Alexnet-level accuracy with 50× fewer parameters and 
0.5 mb model size”, *arXiv preprint arXiv:1602.07360*, 2016.

[5] N. Ma, X. Zhang, H.-T. Zheng, and J. Sun, “Shufflenet v2: Practical guidelines for efficient cnn architecture design”, in *Proceedings of the
European conference on computer vision (ECCV)*, 2018, pp. 116–131.

[6] M. Tan and Q. Le, “Efficientnet: Rethinking model scaling for convolutional neural networks,” in *International conference on machine
learning*, PMLR, 2019, pp. 6105–6114.



