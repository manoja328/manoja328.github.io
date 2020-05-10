---
layout: post
title:  "Debugging you ML models"
excerpt: debuggin ML models
comments: true
date:   2020-5-10 18:02:00 +0545
categories: ML 
---

1. Always check your data
   - Visuzalize outputs/labels  and the  inputs

   - Visualize the distribution and try to find patterns
   - May also try if simple methods like  Kernel SVM , Random Forest work reasonably. If not then some problem with the dataset

   - Duplicated examples , bad data , corrupted labels
   - Do you need to do Data processing ?
     - Mean centering , Whitening etc.
   - Look for dataset imbalance and biases
     - Up-sample or Down-sample if you see imbalance
2. Start by overfitting on few samples by turning of regularization. If the loss doesnot converge to zero then there  is a problem.
3. Start with simple model then gradually increase model complexity.
4. Is the model underfitting or overfitting?  Simple checks can be done using k-Fold cross validation and seeing train and val losses. Run on small version or mini-validation data especially if you are running huge datasets. Use Tensorboard or other solutions to visualize the  losses.

   - Underfitting: both train and test errors are high. Solutions:
     1. Increase model complexity
   - Overfitting: train error low but test error high. Solutions:
     1. Collect more data
     2. Decrease model complexity eg. fewer units, reduce no. of  hidden layers
     3. Regularize:
        - Dropout 
        - Batchnorm 
        - Early stopping 
        - L2 weight decay
        - Ensemble
5. See that scales of losses are OK

   - check for anamoly in gradient values
     -  If you find that gradient are blowing-up then you can perform gradient clipping.
   - check if there are NaNs or Infs or really weird values. Below, I describe a scenario that I faced. I was getting  NaNs  while running a Faster-RCNN model. I checked all the losses and found that my loss for classification was fine. But, I was getting NaNs just for co-ordinate regressors. Upon digging deep I find that  something like below could be happeing:

``` @super-wcg

1. (x,y) of bounding boxes > H / W of the image. 
2. xmin = xmax or ymin = ymax
3. Small sized bounding boxes

Easy fixes could be something like not loading small boxes i.e ensuring |xmax -xmin| >= 10 in your dataloader. 
```

Additionally to debug during  the backward pass you will need to add few hooks and print statements.
Fortunately, you can also use pytorch anomaly detection for the latest version of pytorch code.

    class MyModel(nn.Module):
        def __init__(self):
            super(MyModel, self).__init__()
            self.model = models.resnet18(pretrained = True)
            self.gradients = []
            ## your layers
            self.model.avgpool.register_backward_hook(self.save_gradients)
            
        def forward(self, x):
            ## your forward pass
            return self.model(x)
    
        def save_gradients(self, module, grad_input, grad_output):
            name = module._get_name()
            self.gradients.append(grad_output)
            
    model = MyModel()
    x = torch.rand(1,3,224,224)
    output = model(x)
    output.backward()
    print(model.gradients)


6. Code Sanity checks 

- Conditional logic **if-conditions** in your code  and be sure they are really doing intended things
- Deliver clear error messages 
  - eg. I made a silly mistake where I   dont initilialize a model if the checkpoint is not found. I forgot to add an error message to show the  *folder not found  error*. So, I was unaware if the model is being initialized or not.
- Have asserts in dataloader to prevent  absolutely ridiculous things from happering
  - E.g. check if bounding box min and max are same or if  box coordinates are larger than  image
7. Learn how to use a debugger.  **ipdb or pdb**  for python to trace the points where you keep gettings errors. Its better than using *print* debugging since you can examine each steps. Also, It might come handy to learn some pdb commands.



##  Resources: 

1. 37 Reasons why your Neural Network is not working: https://blog.slavv.com/37-reasons-why-your-neural-network-is-not-working-4020854bd607 
2. A Recipe for Training Neural Networks http://karpathy.github.io/2019/04/25/recipe/
3. https://sebastianraschka.com/faq/docs/nnet-debugging-checklist.html
4. https://medium.com/machine-learning-world/how-to-debug-neural-networks-manual-dc2a200f10f2
5. https://blog.cardiogr.am/4-ways-to-debug-your-deep-neural-network-e5edb14a12d7
6. https://www.semantics3.com/blog/debugging-neural-networks-a-checklist-ca52e11151ec/#inputs
7. http://210.28.132.67/weixs/project/CNNTricks/CNNTricks.html
8. https://medium.com/@jonathan_hui/debug-a-deep-learning-network-part-5-1123c20f960d



