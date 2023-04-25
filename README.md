1.1. Chess

States: 2-d vector (state representation using FEN notation, bool - checkmate)

Actions: tuple (piece, move) = (piece, (# of steps, direction))
*** special moves (e.g. pawn promotion, kingside/queenside castling) could e.g. be expressed by a tuple of pieces and a tuple of moves.

State transition (probability) function p: the probability distribution over all possible board states S’ that can be reached from the current state s, taking action a

Reward function:
capturing an opponent’s piece: reward is based on piece value
- pawn: +1
- knight: +3
- bishop: +3
- rook: +5
- queen: +9
- king: +∞
losing a piece:
- pawn: -1
- knight: -3
- bishop: -3
- rook: -5
- queen: -9
- king: -∞
making a move: -0.5 (punishment to prefer quick games)
pawn promotion: reward amount depends on piece chosen
- pawn: +0
- knight: +2
- bishop: +2
- rook: +4
- queen: +8

Policy: The probability distribution over all possible actions, given an initial state that gets optimized during learning such that higher probability is assigned to better move options. This probability also depends on the opponent player’s move.



1.2. LunarLander
 
States: 
state in 8-dimensional vector: coordinates (x,y) of lander, lander’s linear velocities in (x,y), angle, angular velocity, bool-left leg in contact with ground, bool-right leg in contact with ground

Actions: 4 actions - do nothing, fire left orientation engine, fire main engine, fire right orientation engine

State transition (probability) function p: maps the probability distribution of the resulting state, based on an action (moving the lander) and initial state (previous lander position)
-> transition probability is determined/influenced by the physics of the simulation (e.g. firing main engine will increase velocity in the direction of its orientation, but also consume fuel)

Reward function:
moving from top of screen to landing pad and coming to rest: 100-140 points
moving away from the landing pad: - ???
lander crashes (body, i.e. neither leg, contacts moon):  -100 points
lander comes to rest: +100 points
left/right leg has ground contact: +10
firing main engine: -0.3 points each frame
firing side engine: -0.3 points each frame
solved (both legs on moon within landing pad): +200 points

Policy: the probability distribution over all possible actions (to move the lander) that can be taken from a specific state of the lander



1.3 

Policy Evaluation =

Policy Iteration =

—---------------------------

Environment Dynamics = the rules that govern how the agent interacts with the environment. The environment dynamics include 2 functions -  reward function and state transition function. Both determine the consequences of an agent’s action and guide its decision-making/learning process. The agent needs to have an accurate model of the environment dynamics to make good (or even optimal) decisions.
If the Environment Dynamics are fully known, then the agent is able to learn an optimal policy. 

Reward function = maps a specific (expected) reaction of the environment (positive/negative reward) to the action taken in a specific state. The reaction/reward describes the “goodness” of the action & therefore makes learning possible.

State transition function = probability distribution that describes the probabilities of all possible transitions from initial state s to another state s’, when making a certain action a (all possible actions). 

Example 1:
Example 2:

—------------------------
Are the environment dynamics generally known?
In most RL problems, the environment dynamics (or parts of it) are unknown (e.g. other agent’s decision making processes) and therefore must be learned by the agent through interaction with the environment (trial-and-error), i.e. the agent takes an action and observes the resulting states and rewards. These observations are used to estimate/update/optimize the environment dynamics.
Also, the environment dynamics might change through time and might not be even accessible.

Can environment dynamics practically be used to solve a problem with RL? 
Generally yes, but environment dynamics may not be practical to use for solving a RL problem, if the state/action space is too large (or even continuous), because it makes estimation/optimization of the environment dynamics unfeasible. 
