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

## Attempt 5
- decrease decay_steps from 10000 to 1000
- now overfit `loss: 0.5694 - accuracy: 0.9903 - val_loss: 0.7080 - val_accuracy: 0.8491`

## Attempt 6 (Getting there)
- Trainable params: 65,731, dense layer 32 neurons
- Lock back model completely
- decrease decay_steps to 100

## Attempt 7
- Remove normalisation!! It normalise over the whole batch, which is bad
- `loss: 0.5911 - accuracy: 0.9914 - val_loss: 0.6393 - val_accuracy: 0.9224`


## Attempt 8
- switch to generator ImageDataGenerator
- it seems bad, in performance. and with high bias


## Attempt 9 (Good Result)
- use workers=8 to speed up
- use PiecewiseConstantDecay
- implement historam equalisation
- submission result 0.95890

## Attempt 10
- Use label smoothing for cross entropy loss
- validation now higher than training
- submission result 0.93835

## Attempt 11 (with all regularization)
- `PiecewiseConstantDecay( [800, 2000, 2400, 2800], [ 0.003, 0.001, 0.0003, 0.0001, 0.00001])`
- fine_tune_at = 171
- 3 dense layer: 128, 64, 32 with both l2 regularizer and dropout
- `loss: 0.7589 - accuracy: 0.9356 - val_loss: 0.7349 - val_accuracy: 0.9437`

## Attempt 12 (only l2 regulariztion)
- `loss: 0.6323 - accuracy: 0.9987 - val_loss: 0.6587 - val_accuracy: 0.9697`

## Attempt 13 (no regularisation)
- with a single 128 dense layer
- `loss: 0.5632 - accuracy: 0.9984 - val_loss: 0.5959 - val_accuracy: 0.9567`
- it overfits!