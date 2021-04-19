<b>Exercise 8.1</b> The nonplanning method looks particularly poor in Figure 8.3 because it is a one-step method; a method using multi-step bootstrapping would do better. Do you think one of the multi-step bootstrapping methods from Chapter 7 could do as well as the Dyna method? Explain why or why not.

<b>Solution:</b> I do not think that multi-step bootstrapping would do as well as Dyna because Dyna does a lot more number of updates than what multi-step bootstrapping does. For an episode of length k, multi-step bootstrapping would do k updates whereas Dyna would do kn updates, n being the no. of planning steps. Also, because of more updates of Dyna, the states would have the latest values which wouldn't be the case with multi-step bootstrapping.

<b>Exercise 8.2</b> Why did the Dyna agent with exploration bonus, Dyna-Q+, perform better in the first phase as well as in the second phase of the blocking and shortcut experiments?

<b>Solution:</b> 

First Phase: Dyna depends only on epsilon greedy policy for exploration whereas Dyna Q+ explores more due to exploration bonus and hence the chance of finding optimal/better policies would be high for it. Dyna on the other hand might have ended up with a sub-optimal policy.

Second Phase: Since Dyna Q+ keeps exploring and taking obscure actions due to the bonus, it can quickly find out the change in environment and thereby optimal policy sooner. Dyna on the other hand would take sometime to find the change of environment (or may not at all) and requires more time thereafter to find an optimal policy.

<b>Exercise 8.3</b> Careful inspection of Figure 8.5 reveals that the difference between Dyna-Q+ and Dyna-Q narrowed slightly over the first part of the experiment. What is the reason for this?

<b>Solution:</b> It could be that Dyna found out an optimal policy over time which is achieved by Dyna Q+ in a lesser amount of time.

<b>Exercise 8.5</b> How might the tabular Dyna-Q algorithm shown on page 164 be modified to handle stochastic environments? How might this modification perform poorly on changing environments such as considered in this section? How could the algorithm be modified to handle stochastic environments and changing environments?

<b>Solution:</b> 

- Dyna-Q could be modified to handle stochastic environments by maintaining a count of the next state/reward for every state-action pair. The model can thereby sample the next state/reward for a state-action by weighting them according to the counts.
- Dyna-Q learns the Q values over time for the old environment and since we are following an epsilon greedy policy, we would mostly be following the same trajectories even when the environment changes.  Moreover, the longer the model is trained on the old environment the harder it would get to make changes because the state-transition probabilities would've become higher for the states that fetched well in the older environment - thereby making the consecutive transitions to less probable next states less likely.
- I think it could be modified in a similar way to Dyna-Q+, but the bonus here being "reward bonus" + "probability bonus". Reward bonus would encourage taking obscure actions and probability bonus would encourage transition to less probable states.  The idea is to somehow help refresh the old Q values to hold values for the new environment.

<b>Exercise 8.6</b> The analysis above assumed that all of the b possible next states were equally likely to occur. Suppose instead that the distribution was highly skewed, that some of the b states were much more likely to occur than most. Would this strengthen or weaken the case for sample updates over expected updates? Support your answer.

<b>Solution:</b>  It would strengthen the case for sample updates. Consider a case where b = 10,000 and only 1000 of the next states occur frequently (~99% of the time). The sample updates would back up using these samples which consider the important updates and ignore the less likely occurring ones. On the other hand, expected updates would be wasting their time to compute the value by considering the almost-never visited next states as well.

<b>Exercise 8.7</b> Some of the graphs in Figure 8.8 seem to be scalloped in their early portions, particularly the upper graph for b = 1 and the uniform distribution. Why do you think this is? What aspects of the data shown support your hypothesis?

<b>Solution:</b> The scallop is due to the reward distribution in my opinion. The values of the states are poor in the early stages for the uniform distribution case. But with time as the values get better, the reward distribution doesn't affect the values as much and hence we see a smoother curve at the later stages.