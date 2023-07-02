<h1 align="center"> AWS DeepRacer Autonomous Racing </h1>

<h3 align="center"> Reinforcement Learning Experimentation focussed on Autonomous Racing </h3>

<p align="center">

<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/67ae7619-8ec6-48d5-a1b9-10c75bf41ab0" alt="drawing" width="200" height="180"/>

<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/e4bc6d00-525e-41e9-9a6d-a18befbea0f7" alt="drawing" width="180" height="180"/>

<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/a40e3bf9-18c1-4b88-8443-a5cd5d4dd906" alt="drawing" width="200" height="180"/>

</p>

## AWS DeepRacer

AWS DeepRacer is a fully autonomous 1/18th scale race car driven by an **AWS Machine Learning** service for exploring **Reinforcement Learning** focussed on **Autonomous Racing**.

## Reinforcement Learning

Reinforcement learning is a machine learning method that is focused on **autonomous decision-making** by an **agent** in order to achieve specified goals through interactions with an **environment**. In reinforcement learning, learning is achieved through trial and error and **training does not require labeled input**. Training relies on the **reward hypothesis**, which posits that all goals can be achieved by maximizing a future reward after **action** sequences. 

*In reinforcement learning, designing the reward function is important. Better-crafted reward functions result in better decisions by the agent.*


#### Terms in Reinforcement Learning
![image](https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/be83035f-9cfa-414b-9995-ff84f493b2b3)


To encourage learning during training, the learning agent must be allowed to sometimes pursue actions that might not result in rewards. This is referred to as the **exploration and exploitation trade-off**. It helps reduce or remove the likelihood that the agent might be misguided into false destinations.

#### Reinforcement Learning in context of Autonomous Racing
For autonomous racing,
- The agent is a vehicle.
- The environment includes traveling routes and traffic conditions.
- The goal is for the vehicle to reach its destination quickly without accidents.
- Rewards are scores used to encourage safe and speedy travel to the destination. The scores penalize dangerous and wasteful driving.

 ## Reinforcement Learning Model

A reinforcement learning model is an environment in which an agent acts that establishes three things: 
- The states that the agent has [Input]
- The actions that the agent can take [Output]
- The rewards that are received by taking action.

The strategy with which the agent decides its action is referred to as a **policy**. The policy takes the environment state as input and outputs the action to take. In reinforcement learning, the policy is often represented by a **deep neural network**. We refer to this as the reinforcement learning model. Each training job generates one model. A model can be generated even if the training job is stopped early. 

*A model is **immutable** which means it cannot be modified and overwritten after it is created.* 

## Machine Learning Frameworks Used

<p align="center">
<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/3572a5ee-f2ca-42c2-9cda-034edfb6bb60" alt="drawing" height="400"/>
</p>

AWS Services used for Model Building are as follows: 
- **Amazon DeepRacer :** While it is not a framework itslef but a console, it provides a complete learning environment for Autonomous Racing. It includes a simulated racing environment, reinforcement learning algorithms and web based interface for training and evaluating models.
- **Amazon SageMaker :** Powerful Machine Learning Platform that supports popular frameworks like **RLCoach, MXNet and TensorFlow** which is used here for Autonomous Racing.
- **Amazon RoboMaker :** It helps in developing, testing and deploying robotic applications. It is used here to simulate and evaluate autonomous racing algorithms and models.
- **Amazon Kinesis Video Streams :** It is used here to share live simulation video of learning model.
- **Amazon S3 :** It is used for storage purpose.
- **Amazon CloudWatch :** It is used here to store logs related to events during model building.


## Workflow of AWS DeepRacer

<p align="center">
<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/91bea88c-84b9-414d-8bdc-17988c1ded8a" alt="drawing" />
</p>


## Steps to Model Creation

<p align="center">
<img src="https://github.com/manishkr1754/AWS_DeepRacer_Autonomous_Racing/assets/114581035/897bbe10-cfa9-42c7-b78e-4a8bd9408441" alt="drawing" />
</p>


## Concepts and Terms related to Model Building & Evaluation

- **Policy Network :** A policy network is a neural network that is trained. The policy network takes video images as input and predicts the next action for the agent. Depending on the algorithm, it may also evaluate the value of current state of the agent. Training the policy network amounts to iterating through steps that involve generating experiences based on the current policy, followed by optimizing the policy network with the newly generated experiences. The process continues until certain performance metrics meet required criteria.  
- **Optimization Algorithm :** An optimization algorithm is the algorithm used to train a model. For **supervised training**, the algorithm is optimized by **minimizing a loss function** with a particular strategy to update weights. For **reinforcement learning**, the algorithm is optimized by **maximizing the expected future rewards** with a particular reward function.
- **Hyperparameters :** Hyperparameters are algorithm-dependent variables that control the performance of neural network training. An example hyperparameter is the learning rate that controls how many new experiences are counted in learning at each step. A larger learning rate results in a faster training but may make the trained model lower quality. Hyperparameters are empirical and require systematic tuning for each training.
- **Reward Function :** A reward function is an algorithm within a learning model that tells the agent whether the action performed resulted in:
  
     - A good outcome that should be reinforced
     - A neutral outcome
     - A bad outcome that should be discouraged

  The reward function is a key part of reinforcement learning. It determines the behavior that the agent learns by incentivizing specific actions over others. The user provides the reward function by using Python. This reward function is used by an optimizing algorithm to train the reinforcement learning model.

- **Experience Episode (Experience Generating Episode) :** An experience episode is a period in which the agent collects experiences as training data from the environment by running from a given starting point to completing the track or going off the track. Different episodes can have different lengths.
- **Experience Iteration (Experience Generating Iteration) :** It is a set of consecutive experiences between each policy iteration that performs updates of the policy network weights. At the end of each experience iteration, the collected episodes are added to an experience replay or buffer. The size can be set in one of the hyperparameters for training. The neural network is updated by using random samples of the experiences.
- **Policy Iteration (Policy Updating Iteration) :** It is any number of passes through the randomly sampled training data to update the policy neural network weights during **gradient ascent**. A single pass through the training data to update the weights is also known as an **epoch**.
- **Training Job :** A training job is a workload that trains a reinforcement learning model and creates trained model artifacts on which to run inference. Each training job has two sub-processes:
    - Start the agent to follow the current policy. The agent explores the environment in a number of episodes and creates training data. This data generation is an iterative process itself.
    - Apply the new training data to compute new policy gradients. Update the network weights and continue training. Repeat Step 1 until a stop condition is met.

- **Evaluation Job :** An evaluation job is a workload that tests the performance of a model. Performance is measured by given metrics after the training job is done. The standard AWS DeepRacer performance metric is the **driving time** that an agent takes to complete a lap on a track. Another metric is the **percentage of the lap completed**. 






