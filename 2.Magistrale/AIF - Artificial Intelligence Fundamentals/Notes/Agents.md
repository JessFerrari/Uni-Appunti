---
Subject: "[[Indice - Artificial Intelligence Fundamentals|AIF]]"
tags:
  - AIF
Creation: 2024-10-01
Papers:
  - "[[On the measure of intelligence.pdf]]"
Chapter:
  - AIMA (2)
  - "[[02_agents.pdf]]"
---
An ***Agent*** is something that acts: operate autonomously, perceive their environment, persist over a prolonged time period, adapt to change and create and pursue goals.


An ***agent*** is anything that can be viewed as perceiving its ***environment***  through ***sensors*** and acting upon that environment through ***actuators***.
How well an agent behave depends for the environment
![[Pasted image 20241001222632.png]]

An agent **percepts** things from the environment with *sensors* and do **action** on the environment wit the *actuator*.
A ***percept sequence*** is the complete history of everything the agent has perceived.

An agent's choice depends on built-in knowledge and on the all percept sequence, but not on anything it doesn't observed yet.

The agent has an *external characterisation*, that is a possible tabulation of the agent's possible action, and an ***Agent program*** that is the function of the agent.

The agent function maps from percept history to action :
$$f:P^*\to A$$
The agent program runs on the physical architecture to produce $f$.


*Rational* means exploration, learning and autonomy

A ***Rational agent*** is one that acts so as to achieve the best outcome, or the best expected -> Is the one who does the right thing, but we evaluate an agent not for what it does but for its consequences. 

As a general rule, it is better to design performance measures according to what one actually wants to be achieved in the environment, rather than according to how one thinks the agent should behave.

For each possible percept sequence, a rational agent should select an action that is expected to maximize its performance measure, given the evidence provided by the percept sequence and whatever built-in knowledge the agent has.

In some cases the environment is completely known a priori and, for consequence, completely predictable. In these cases the agent doesn't need to learn anything but only acts correctly. In the other hands, these agents are extremely fragile.

# PEAS

To design a rational agent we must specify the task environment.
The rational agent must has for elements:
- Performance measure 
- Environment
- Actuators 
- Sensors

## Environments types
 An environments could be:
 - Observable / Partially-observable /Unobservable : if an agent's sensors give it access to the complete state of the environments at each point in time then the environment is fully observable, otherwise is partially observable. Is convenient having a fully observable environments because the agent need not maintain any internal state to keep track of the world.  An environment could be partially observable because of noisy and inaccurate sensors. If the agent has no sensor at all the environment is unobservable.
 - Deterministic / Non-deterministic : If the next state is predictable or not from the current state of environment. If an environment is fully observable then is deterministic.
 - Episodic / Sequential : In an episodic task environment, the agent’s experience is divided into atomic episodes.
 - Static / Dynamic / Semi dynamic : f the environment can change while an agent is deliberating, then we say the environment is dynamic for that agent; otherwise, it is static. Static environments are easy to deal with because the agent need not keep looking at the world while it is deciding on an action, nor need it worry about the passage of time. Dynamic environments, on the other hand, are continuously asking the agent what it wants to do. If the environment itself does not change with the passage of time but the agent’s performance score does, then we say the environment is semi dynamic.
 - Discrete / Continuous : depends for the numbers/types of the states
 - Single-agent / Multi-agent : If in the environment acts one or more agents.

e.g. :![[Pasted image 20241002010450.png]]


The environment type determines the agent design.
The hardest case is partially observable, multiagent, nondeterministic, sequential, dynamic, continuous.

The job of AI is to design an agent program that implements the agent function (so the mapping function from percepts to actions)


The ***Agent architecture*** is the computing device, with physical sensors and actuators, in which the agent program runs on.

The agent structure is compose by agent program and architecture.
The program that we choose needs to be appropriate for the architecture.
```
function TABLE-DRIVEN-AGENT(percept) returns an action 
	persistent: percepts, a sequence, initially empty table, a table of actions, indexed by percept sequences, initially fully specified 

	append percept to the end of percepts 
	action : LOOKUP(percepts, table) 
	return action

```


# Agent types
There's four basic type in order of increasing generality:
- *simple reflex agents*
- *reflex agents with state*
- *goal-based agents*
- *utility-based agents*

Each kind of agent program combines particular components in particular way to generate actions.

## Simple reflex agent
![[Pasted image 20241002021432.png]]
These agents select actions on the basis of the current state, ignoring the rest of percept history.

![[Pasted image 20241002022631.png]]
Far better the table driven agent :
- the most obvious reduction comes from ignoring the percept history, which cuts down the number of relevant percept sequences from $4^T$ to just $4$.
- decision depends not on the position on the current percept 
This type of agent works only if decisions can be made on just the current percept and the environment is fully observable.
## Reflex agents with state 


## Goal-based agent
![[Pasted image 20241002023348.png]]
Sometimes goal-based action selection is straightforward—for example, when goal satisfaction results immediately from a single action. Sometimes it will be more tricky. Search and planning are the subfields of AI devoted to finding action sequences that achieve the agent’s goals
## Utility-based agent
![[Pasted image 20241002023411.png]]
A performance measure assigns a score to any given sequence of environment states, so it can easily distinguish between more and less desirable ways of getting to the taxi’s destination. An agent’s utility function is essentially an internalization of the performance measure.

## (Model based ?)
![[Pasted image 20241002023239.png]]
The most effective way to handle partial observability is for the agent to keep track of the part of the world «it can’t see now».

![[Pasted image 20241002023309.png]]Example The details of how models and states are represented vary widely depending on the type of environment and the particular technology used in the agent design.

## (Learning agent ?)
![[Pasted image 20241002023508.png]]The most important distinction is between the learning element, which is responsible for making improvements, and the performance element, which is responsible for selecting external actions.