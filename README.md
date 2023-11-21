### FrozenLake-V1

> ![frozen_lake](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/c35aa364-5e8c-4a30-b7dc-ec37fc677a23)

This environment is part of the Toy Text environments which contains general information about the environment.

> ![Web yakalama_21-11-2023_224210_gymnasium farama org](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/5b832ed6-d7ee-4659-8ca2-52dbf18e2d05)

Frozen lake involves crossing a frozen lake from start to goal without falling into any holes by walking over the frozen lake. The player may not always move in the intended direction due to the slippery nature of the frozen lake.

**Description**
The game starts with the player at location [0,0] of the frozen lake grid world with the goal located at far extent of the world e.g. [3,3] for the 4x4 environment.

Holes in the ice are distributed in set locations when using a pre-determined map or in random locations when a random map is generated.

The player makes moves until they reach the goal or fall in a hole.

The lake is slippery (unless disabled) so the player may move perpendicular to the intended direction sometimes (see is_slippery).

Randomly generated worlds will always have a path to the goal.

Elf and stool from https://franuka.itch.io/rpg-snow-tileset. All other assets by Mel Tillery http://www.cyaneus.com/.

**Action Space**
The action shape is (1,) in the range {0, 3} indicating which direction to move the player.

- 0: Move left

- 1: Move down

- 2: Move right

- 3: Move up

**Observation Space**
The observation is a value representing the player’s current position as current_row * nrows + current_col (where both the row and col start at 0).

For example, the goal position in the 4x4 map can be calculated as follows: 3 * 4 + 3 = 15. The number of possible observations is dependent on the size of the map.

The observation is returned as an int().

**Starting State**
The episode starts with the player in state [0] (location [0, 0]).

**Rewards**
Reward schedule:

- Reach goal: +1

- Reach hole: 0

- Reach frozen: 0

**Episode End**
The episode ends if the following happens:

- Termination:
The player moves into a hole.

The player reaches the goal at max(nrow) * max(ncol) - 1 (location [max(nrow)-1, max(ncol)-1]).

- Truncation (when using the time_limit wrapper):
The length of the episode is 100 for 4x4 environment, 200 for FrozenLake8x8-v1 environment.

**Information**
step() and reset() return a dict with the following keys:

- p - transition probability for the state.
See is_slippery for transition probability information.

**Arguments**

> ![Web yakalama_21-11-2023_224457_gymnasium farama org](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/e428cf97-7a01-4db5-8e81-fedfea02b3d2)

desc=None: Used to specify maps non-preloaded maps.

Specify a custom map.

> ![Web yakalama_21-11-2023_224542_gymnasium farama org](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/28a2821f-e006-4649-8f54-8d19f95fc9fa)

A random generated map can be specified by calling the function generate_random_map.

![Web yakalama_21-11-2023_224617_gymnasium farama org](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/d2ec9489-bb54-4270-912b-62f165db55a1)

map_name="4x4": ID to use any of the preloaded maps.

> ![Web yakalama_21-11-2023_224658_gymnasium farama org](https://github.com/tekgulburak/FrozenLake-v1/assets/108903426/ba4e5760-343d-43b7-acfb-3794b7f61b50)

If desc=None then map_name will be used. If both desc and map_name are None a random 8x8 map with 80% of locations frozen will be generated.

is_slippery=True: If true the player will move in intended direction with probability of 1/3 else will move in either perpendicular direction with equal probability of 1/3 in both directions.

For example, if action is left and is_slippery is True, then:

- P(move left)=1/3  

- P(move up)=1/3

- P(move down)=1/3
