# Resnet50 Changlog

## Attempt 1
- remove Autotune
- add normalisation and zoom to preprocessing
- use 0.9 - 0.1 split of training and validation

todo: rmsprop learning rate decay

## Attempt 2
- freeze until layer 172, 
```
Total params: 23,587,712
Trainable params: 4,096
Non-trainable params: 23,583,616
```
high training loss
