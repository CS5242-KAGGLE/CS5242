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


## Attempt 3
- add 2 layers of dense layer, with BN and dropout
- freeze until layer 172

`loss: 0.6429 - accuracy: 0.9142 - val_loss: 0.7063 - val_accuracy: 0.8362`

## Attempt 4
- change back to global average pooling (easier to train, less parameters)
- shuffle training batch