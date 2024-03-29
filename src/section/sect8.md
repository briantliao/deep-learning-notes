# Section 8: Fairness, MDP, Imitation Learning

## Fairness
* We don't the model to bias irrelevant features including those legally protected
    * race, sex, citizenship
* biases:
    * learning algorithms rely on data
    * bias from data collection and selection
    * if bias is 0, variance is infinity

### Notation:
* \\( X \\): vector of the features of an individual
* \\( A \\): the protected attributes such as national origin
* \\( Y \\): label such as received loan or not
* \\( \hat{Y} = f(X, A) \\): model output

### Definitions:
* `Unawareness`: \\(f(X, A) = f(X) \\) a model without A does the same as a model with A
    * however features are usually correlated, so A camn be predicted by other attributes in X
* `Demographic Parity`: \\( P[\hat{Y} = 1 | A = 0] = P[\hat{Y} = 1 | A = 1] \\) or \\( \hat{Y}  ~ \bot ~ A \\) (the predicted Y is __conditionally independent__ of A).
    * since we have A, this solves the feature correlation problem
    * problem of __Laziness__, accept qualified candidate for \\( A = 0 \\) and randomly accept for \\( A = 1 \\) (with the same probability?), demographic parity is maintained
*   `Separation`: \\( \hat{Y} ~ \bot ~ A | Y \\) given that the candidate is qualified, the predicted Y output is independent of protected attributed.
    * equal opportunity
    * ?
* What is `Sufficiency`?
    * \\( Y ~ \bot ~ A | \hat{Y} \\) given the predictors output, it should reflect the true score?

### Optimizing for Fairness
* How do you optimize for fairness?
    * minimize Jenson-Shannon divergence optimizing like a GAN

![](https://i.imgur.com/A57FfFX.png)

* How does this work again?

## Markov Decision Processes (MDP)
* What is a `Markov Decision Process`?
    * for games, where you have states, actions, and rewards
    * at every time step we are in state s. the agent must choose an action a for that state. Then we transition to a new state s' based on some probability distribution. On transition a reward r is generated.

* What is a `trajectory`?
    * sequence of transitions
    * \\( \tau = ((s_0, a_0), (s_1, a_1), ..., (s_t, a_t, r_t))

* How can you mathematically define a MDP?
    * A 4-tuple: \\( (S, A, T, r) \\)
        * \\( S \\): set, set of states
        * \\( A \\): set, set of actions A[s] given state, these are the actions you can take
        * \\( T(s, a) \\): function(S, A) -> S, transition function that takes current state adn action that returns a new state. In a __stochastic MDP__ the new state is returned from some distribution \\( P(s_new | s_old, a) \\) prob of each new state given old state and action taken
        * \\( r(s, a, s') \\): function(S, A, S) -> real, reward function for the state you are in, action you took, and state you will be in. This can also be r(s, a) where s is actually the new state s'. It's confusing sorry.

* What is `policy`?
    * Our attempt at a solution to the MDP.
    * \\( \pi(\tau) \\)
    * it attempts to maximized expected reward for it's given state and action

![](https://i.imgur.com/EogyJKY.png)

* trajectory generated by the policy

* How would you explain it if the environment was fully deterministic?
    * you know what action to take, the one that maximizes reward
* What is \\( \tau \~ p_{\pi}(\tau) \\)?
    * weighed sum and and prob of starting at that given state

* What is the `discount factor`?

![](https://i.imgur.com/jNVeL9M.png)

* rewards in the present are worth more.

### Other questions
* What is Jenson-Shannon Divergence?
* Why is \\( r_t \\) in the trajectory?
* What is an example run of argmaxing the policy?
