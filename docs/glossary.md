---
title: Glossary
description: List of common terms in machine learning
---

# Basic ML / RL Glossary

This glossary is aimed at the kinds of concepts that come up when training an agent to play a game like Asteroids.

## Core Concepts

* **Model** — A learned function that maps inputs to outputs. In your case, it might take the current game state and output which controls to press.

* **Parameters / Weights** — The learned numbers inside a model. Training adjusts these values.

* **Inference** — Running a trained model to get an output. No learning happens during inference.

* **Training** — The process of adjusting model weights based on examples, rewards, or other feedback.

* **Dataset** — A collection of examples used for training or evaluation.

* **Sample** — One individual training example.

* **Feature** — An input value given to the model, such as ship velocity, asteroid position, or angle to a target.

* **Label / Target** — The correct or desired output for a training example.

* **Prediction** — The output produced by the model.

* **Loss** — A number measuring how wrong the model's prediction was. Training tries to minimize loss.

* **Gradient** — Information describing how each model parameter should change to reduce loss.

* **Optimizer** — The algorithm that updates model weights using gradients. Examples include Adam and SGD.

* **Learning Rate** — Controls how large each training update is.

* **Epoch** — One complete pass through the training dataset.

* **Batch** — A group of samples processed together during one training step.

* **Batch Size** — The number of samples in a batch.

---

## Agent / Game Terminology

* **Agent** — The thing making decisions in an environment. Your neural-network-controlled ship is the agent.

* **Environment** — The world the agent interacts with. Your Asteroids simulation is the environment.

* **State** — The information describing the environment at a particular moment.

  Example:

  `ship position + velocity + heading + asteroid positions + bullet positions`

* **Observation** — What the agent is actually allowed to see. The full environment state and the observation may be different.

* **Action** — A decision made by the agent.

  Examples:

  * rotate left
  * rotate right
  * thrust
  * fire
  * no-op

* **Action Space** — The complete set of actions available to the agent.

* **Episode** — One complete game or attempt, usually from initial state until death, timeout, or victory.

* **Step / Timestep** — One interaction cycle:

  `observe → choose action → update game → observe again`

* **Trajectory** — A sequence of states, actions, and possibly rewards from an episode.

  Conceptually:

  `state₀ → action₀ → state₁ → action₁ → state₂ ...`

* **Rollout** — Running an agent through the environment to generate a trajectory.

---

## Policies

* **Policy** — The rule used by an agent to decide what action to take given an observation.

  Mathematically:

  `action = policy(observation)`

  Your hand-written Asteroids bot is a policy.

  Your trained neural network will also be a policy.

* **Deterministic Policy** — Always chooses the same action for the same state.

* **Stochastic Policy** — Produces probabilities over actions and may choose differently when given the same state.

  Example:

  ```
  left   5%
  right 10%
  thrust 20%
  fire   60%
  none    5%
  ```

* **Policy Network** — A neural network whose output represents the agent's policy.

* **Behavior Policy** — The policy actually generating the data.

  For behavioral cloning, your scripted bot is the behavior policy.

* **Target Policy** — The policy you ultimately care about learning or evaluating.

---

## Teacher / Student Terminology

* **Teacher** — A stronger system that generates examples or guidance for another model.

  In your Asteroids project, the hand-written bot can act as the teacher.

* **Student** — The model being trained to imitate or learn from the teacher.

* **Expert** — Usually another name for a high-quality teacher policy.

* **Demonstration** — A recorded example of an expert acting in the environment.

  A demonstration might contain:

  `observation → expert action`

* **Imitation Learning** — Training an agent using demonstrations of another agent.

* **Behavioral Cloning / Behavior Cloning** — The simplest form of imitation learning. Treat agent decisions as a supervised-learning problem.

  Dataset:

  ```
  game state → teacher action
  game state → teacher action
  game state → teacher action
  ```

  Then train:

  ```
  neural network(game state) ≈ teacher action
  ```

* **Distillation** — Training a smaller model to imitate the outputs of a larger or more complicated model.

  For example:

  `large teacher network → tiny ESP32 policy network`

---

## Supervised Learning

* **Supervised Learning** — Training using examples where the correct answer is already known.

  Example:

  ```
  input: game state
  target: FIRE
  ```

* **Classification** — Predicting one category from several possibilities.

  Choosing `LEFT / RIGHT / FIRE / THRUST` is classification.

* **Regression** — Predicting continuous numbers.

  Example:

  ```
  desired steering angle = -0.34
  desired thrust = 0.81
  ```

* **Cross-Entropy Loss** — A common loss function for classification.

* **Mean Squared Error / MSE** — A common loss function for regression.

---

## Reinforcement Learning

* **RL / Reinforcement Learning** — Training an agent by letting it interact with an environment and rewarding or penalizing its behavior.

  Instead of telling it:

  `You should press FIRE here.`

  you tell it something like:

  `+10 for destroying an asteroid.`

* **Reward** — A numeric signal telling the agent how desirable something was.

  Example:

  ```
  +10 destroy asteroid
  +1 survive another second
  -100 die
  ```

* **Reward Function** — The rules determining how rewards are assigned.

* **Return** — The total accumulated reward over some future period.

* **Discount Factor / Gamma / γ** — Controls how strongly the agent values future rewards versus immediate rewards.

* **Credit Assignment** — Figuring out which earlier actions deserve credit or blame for later rewards.

* **Sparse Reward** — Rewards happen rarely.

  Example: only awarding points when the game ends.

* **Dense Reward** — Rewards happen frequently.

  Example: rewarding survival, aiming, dodging, and asteroid destruction individually.

* **Reward Shaping** — Adding intermediate rewards to make learning easier.

* **Policy Gradient** — A family of RL methods that directly adjust a policy to increase expected reward.

* **PPO / Proximal Policy Optimization** — A very popular policy-gradient RL algorithm. Often a good baseline for game-playing agents.

* **DQN / Deep Q-Network** — An RL algorithm that learns the value of taking particular discrete actions.

---

## Value-Based RL

* **Value Function** — Estimates how good a state is in terms of expected future reward.

  `V(state)`

* **Q-Value / Action Value** — Estimates how good it is to take a particular action from a state.

  `Q(state, action)`

* **Q-Function** — The function that predicts Q-values.

* **Q-Learning** — An RL approach that learns the expected value of actions.

* **Bellman Equation** — A mathematical relationship connecting current value estimates to future rewards and value estimates.

---

## Exploration

* **Exploration** — Trying actions that may not currently appear optimal so the agent can discover better behavior.

* **Exploitation** — Choosing the action the agent currently believes is best.

* **Exploration vs. Exploitation** — The tradeoff between trying new behavior and using known good behavior.

* **Epsilon-Greedy** — A simple exploration technique:

  ```
  95% choose best known action
  5% choose random action
  ```

* **Entropy** — A measure of how random or spread-out a policy's action distribution is. RL algorithms sometimes encourage entropy to prevent premature convergence.

---

## Training Data Concepts

* **Train Set** — Data used to update model weights.

* **Validation Set** — Data used during development to measure generalization and tune training decisions.

* **Test Set** — Data reserved for final evaluation.

* **Train/Test Split** — Dividing data so the model is evaluated on examples it did not train on.

* **Generalization** — The ability to perform well on situations not seen during training.

* **Overfitting** — Learning the training examples too specifically and performing poorly on new situations.

* **Underfitting** — The model is too simple or insufficiently trained to capture useful patterns.

* **Distribution** — The statistical pattern of the data the model encounters.

* **Distribution Shift** — When the situations encountered during deployment differ from the training data.

---

## Important Imitation-Learning Problem

* **Compounding Error** — A major issue with behavioral cloning.

  During training, the student sees states produced by the teacher.

  During actual play, the student makes small mistakes.

  Those mistakes lead to states the teacher rarely encountered.

  The student may then make even worse decisions.

  This can snowball:

  ```
  small error
      ↓
  unfamiliar state
      ↓
  larger error
      ↓
  even stranger state
      ↓
  death
  ```

* **Covariate Shift** — The technical term for the student's runtime state distribution differing from the training distribution.

* **DAgger** — Dataset Aggregation. An imitation-learning technique that addresses this problem.

  Basic idea:

  1. Train student from teacher data.
  2. Let student play.
  3. Record the states the student reaches.
  4. Ask the teacher what it would do in those states.
  5. Add those examples to the dataset.
  6. Retrain.
  7. Repeat.

---

## Evaluation

* **Metric** — A number used to measure performance.

* **Accuracy** — Percentage of predictions matching the expected answer.

  Useful for behavioral cloning, but not sufficient by itself.

* **Top-1 Accuracy** — Whether the model's highest-probability action matches the teacher action.

* **Confusion Matrix** — Shows which actions the model commonly confuses.

  For example, it may frequently predict `THRUST` when the teacher predicts `NONE`.

* **Win Rate / Survival Time / Score** — Environment-level metrics measuring actual gameplay performance.

* **Offline Evaluation** — Evaluating the model using recorded data without running the game.

* **Online Evaluation** — Running the trained policy inside the environment.

For this project, online evaluation is especially important. A model with 95% imitation accuracy may still play badly if the missing 5% happens at critical moments.

---

## Model Architecture Terms

* **Neural Network** — A parameterized mathematical model consisting of layers.

* **Layer** — One stage of computation in a neural network.

* **Input Layer** — Receives the observation.

* **Hidden Layer** — Intermediate computation inside the model.

* **Output Layer** — Produces the prediction.

* **Activation Function** — A nonlinear function applied between layers. Common examples include ReLU, GELU, sigmoid, and tanh.

* **MLP / Multilayer Perceptron** — A basic feed-forward neural network. Likely one of the first architectures worth trying for your Asteroids state representation.

* **CNN / Convolutional Neural Network** — A network commonly used for image inputs.

* **RNN / Recurrent Neural Network** — A network designed to process sequences.

* **LSTM / GRU** — Types of recurrent networks designed to retain information over time.

* **Transformer** — An architecture based primarily on attention. Extremely powerful, but probably unnecessary for the first versions of this project.

---

## Model Size / Deployment

* **Parameter Count** — Number of trainable weights in a model.

  Examples:

  ```
  10K parameters
  100K parameters
  1M parameters
  10M parameters
  ```

* **Model Size** — How much storage the model weights require.

  Roughly:

  ```
  FP32 = 4 bytes per parameter
  FP16 = 2 bytes per parameter
  INT8 = 1 byte per parameter
  ```

* **Quantization** — Representing model weights using lower-precision numbers.

  Example:

  `FP32 → INT8`

  This can make a model much smaller and faster, which matters for an ESP32-S3.

* **Latency** — How long one inference takes.

* **Throughput** — How many inferences can be performed in a given amount of time.

* **Memory Footprint** — Total RAM/flash required by the model and inference system.

---

## Common Training Workflow Terms

* **Checkpoint** — A saved copy of model weights during training.

* **Hyperparameter** — A training setting chosen by you rather than learned by the model.

  Examples:

  * learning rate
  * batch size
  * number of layers
  * hidden-layer size

* **Hyperparameter Tuning** — Experimenting with different hyperparameters.

* **Seed / Random Seed** — A value used to initialize pseudorandom processes so experiments can be reproduced.

* **Deterministic Training** — Training configured so the same setup produces identical or nearly identical results.

* **Baseline** — A simple reference system used to judge whether a new method is actually better.

  For this project, good baselines include:

  * random policy
  * scripted policy
  * behavioral-cloning policy

* **Ablation** — An experiment where one feature or component is removed to see how much it mattered.

---

## Terms Especially Relevant to the Asteroids Project

A useful mental model for the project is:

```text
Environment
    ↓
Observation / State
    ↓
Policy
    ↓
Action
    ↓
Environment advances
```

For behavioral cloning:

```text
Scripted Teacher Policy
        ↓
 thousands/millions of
(state, action) examples
        ↓
Supervised Training
        ↓
Student Policy Network
        ↓
Run inside Asteroids
        ↓
Compare gameplay with teacher
```

For reinforcement learning:

```text
Policy
   ↓
plays Asteroids
   ↓
receives rewards
   ↓
RL algorithm
   ↓
updates policy
   ↓
plays again
```

And eventually a useful progression for this project is:

```text
Random Agent
    ↓
Hand-Written Teacher
    ↓
Behavioral Cloning
    ↓
DAgger / Improved Imitation
    ↓
Reinforcement Learning
    ↓
Distillation / Quantization
    ↓
Tiny Embedded Policy
```
