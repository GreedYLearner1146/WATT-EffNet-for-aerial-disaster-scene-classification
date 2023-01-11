# WATT-EffNet-for-aerial-disaster-scene-classification
This is a github repository for our work on "A Novel Wider ATTention EFFicientNet (WATT-EffNet) for Classifiying Aerial Disaster Images" by Gao Yu Lee, Tanmoy Dam, Md Meftahul Ferdaus, Daniel Puiu Poenar and Vu N. Duong.

Our proposed algorithmic structure are designed with applications to UAV-based aerial image disaster scene classification.
Submitted to IEEE Geoscience and Remote Sensing letters (2023).

Unmanned aerial vehicles (UAVs) embedded with a deep learning (DL) classification model can be utilized for search-and-rescue operations, as well as monitoring and mitigating the effects of natural disasters. In such cases, the UAV must quickly comprehend the crisis scenario to limit search areas. This ensures that the UAV's limited power and processing resources are used properly and effectively. To achieve such goal, an effective and lightweight method for scene classification must be developed. Existing approaches, on the other hand, prioritize achieving the highest possible accuracy on classification-based benchmark datasets while ignoring computationally efficient observations. To mitigate such research gap, we have introduced a novel Wider ATTention EFFicientNet (WATT-EffNet) to achieve higher accuracy with a lighter architecture than the baseline EfficientNet. Implementation of width-wise incremental feature module and attention mechanism over width-wise features in WATT-EffNet contributes to the network's light structure. UAV-based aerial disaster image classification dataset is considered for analysing the effectiveness of the purposed WATT-EffNet. Our method surpassed baseline by up to a factor of 15 in terms of classification accuracy and by 38.3% in terms of computing efficiency measured by the Floating Point Operations per second (FLOPs). An ablation study is also conducted by varying the width of WATT-EffNet to examine a higher accuracy at a lower FLOPs. 

See WATT-EffNet Structure FINAL.png for an illustration of our algorithmic architecture design.

# Some Results
