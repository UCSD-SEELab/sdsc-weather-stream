### Creator: Lori
### Date: May 1 and May 2
### purpose: document model parameters tryout
This is the file for model tryout history.
####### NOTE: #1 to # 8 tryout focused on 4/20 dataset only/
#1 
Weather and Stationary are the same. 
Weather: layer 1 = 32, layer 2 = 32, layer 3 = 32. All activation = relu, optimizer = adam. Decay = 0, batch=10, epoch=100
Dataset use: 4_20

Weighted function: layer 1 = 50. Activation = relu, optimizer = adam. Decay = 0, batch = 10, epoch = 150.
Weather prediction mse: 370710
Stationary prediction mse: 16135
Combined prediction mse: 101970

#2
Weather and Stationary: add decay = 0.1 to adam optimizer for Weather, Stationary, Weighted.
With epoch = 100, don't converge. Even 10000 epochs couldn't converge

Weather: epoch = 2000 converge, decay = 0.01
Stationary: epoch = 2000, decay = 0.001
Weighted: epoch = 2000, decay = 0.001
Weather prediction mse: 427015
Stationary prediction mse: 15871
Combined prediction mse: 169491 

#3
Use Lasso to train and predict stationary. Seem like more valid.
Weather and weighted structure remain the same as #2   
Weather prediction mse: 427015
Stationary prediction mse: 6554
Combined prediction mse: 11901

#4
Keep using Lasso for stationary prediction. Change the optimizer of Weather and Weighted to sgd, no decay using.
sgd(lr=0.01, momentum=0.0,decay=0.0,nesterov=false)
Weather prediction: 984412
Stationary prediction: 6554
Combined prediction mse: 984421

#5
Strcucture remains the same as #4. Change sgd to adagrad
adagrad(lr=0.01,epsilon=None,decay=0.0)
Weather prediction mse: 359158
Stationary prediction mse: 6554
Combined prediction mse: 6536

#6
Structure remains the same as #5. Change adagrad to adadelta. 
adadelta(lr=1.0,rho=0.95,epsilon=None,decay=0.0)
change the Weighted epoch to 1500
Weather prediction mse: 281233 ( adadelta significantly more suitable for handling the weather data prediction. The training error was really small. might overfit)
Stationary prediction mse: 6554
Combined prediction mse: 6775
#7
Same as before
change Weighted epoch=500
Combined prediction mse: 7459

#8 
Weighted and stationary reamins the same as before. 
Change Weather model to random forest.
Weather prediction mse: 281233
Combined prediction mse: 7685

### Date: May 7
###### Below tryout focused on 5/1 dataset
# 9
Model structure remains the same as #8. I change the optimizer back to default adam.
Weather prediction mse: 25840549
Stationary Prediction mse: 118289950 ### it caused by some n/a in the dataset, fixed in #10
Combined prediction mse: 24158090
# 10
Change the weather model parameter: optimizer = adam (lr=0.001,beta_2=0.999,epsilon=None,decay=0.01,amsgrad=False). Change batch size to 16.
Weather Prediction mse: 649174739 ### loss hasn't flatened completely
Stationary Prediction mse: 154188213
Combined Prediction mse: 80830834

# 11
Change the epoch size of weather model to 20000. structure remains the same.
Change the model for stationary to mlp again: layer1=32, layer2=32, layer3=32, activation = relu. using adam optimizer as in #10, epoch set to 20000, batch size set to 16.
Change the weighted model optimizer to adam as in #10, epoch is stil 500
Weather prediction mse: 231409711
Stationary prediction mse: 136445471
Combined prediction mse:130199285
