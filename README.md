# Focal Loss

An implementation of the Focal loss proposed in the paper ['Focal Loss for Dense Object Detection'](https://arxiv.org/abs/1708.02002) with PyTorch. 
The implementation presented in this notebook is prepared by taking Appendix A of the paper into consideration. 

>### Focal Loss, Focal Loss Variant & Cross-Entropy Loss

![focal-loss](https://user-images.githubusercontent.com/46245117/225941354-ce3dcd65-44d4-4d6b-8adb-451853d70287.PNG)

The starting point of the focal loss is to investigate the case of two-stage detectors accuracy is surpassing the accuracy of one-stage detectors. The authors of the paper states that the reason is encountring the foreground-background class imbalance during training process in one-stage detectors.

There are two type of models in object detectors. One-stage detectors and two-stage detectors. Two stage detectors uses (1-)Region Proposal and (2-)Classification. The first stage generates a sparse set of candidate proposals and the second stage classifies the porposals into classification. One-stage detectors on the otherhand, skips the region proposal part and run detection directly over a **dense** sampling of locations.

<img src="https://user-images.githubusercontent.com/46245117/235455888-398a1532-62eb-4092-890b-0985ea4b9b21.PNG" width=70% height=70%>

Running detection over a dense sampling  results in **foreground-background class imbalance** wihch can be described as having a high ratio of (ex: 1:100 ) foreground-background class predictions.

![focal-loss-2](https://user-images.githubusercontent.com/46245117/235457418-998dda79-e15f-409f-b2c9-0f2c31eaf359.PNG)

The loss contribution of a well-classified(model output with a probability of >0.6 for ground truth class ) background class example is non-negligible and overall they exhaust the loss with no useful learning because they have a high ratio over the foreground examples.

![focal-loss](https://user-images.githubusercontent.com/46245117/235458947-65117ba8-e39e-4994-9c76-6ab071b81738.PNG)

To address this class imbalance in one-stage detectors, researches in Facebook AI proposes Focal Loss that introduces a factor that down-weights the cross entropy loss assigned to the well-classified examples to focus on foreground examples which have rich information.

![focal-loss-4](https://user-images.githubusercontent.com/46245117/235460257-850591b8-3f94-4da1-8fc7-83ef6b945879.PNG)

The focusing parameter is γ, that controls the strength of the modulating term. When γ = 0, the loss is equivalent to the CE loss. As γ increases, the shape of the loss changes so that “easy” examples with low loss get further discounted.



