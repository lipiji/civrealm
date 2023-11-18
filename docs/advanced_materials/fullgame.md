The full game is the original game mode provided by the Freeciv game. In the full game, each player acts as a civilization leader. Besides the players controlled by our agents, the other players are controlled by built-in AI algorithms. The objective of players is to guide their civilization from its humble beginnings to the greatest civilization and one full game can last from several hours to several days. Civilizations evolve through eras from the Bronze Age to the Space Age and the number of controllable objects (units, cities, diplomatic relations, etc.) explodes as the game progresses. In addition, each decision made typically carries a multi-faceted impact, encompassing both long-term strategic consequences and short-term tactical outcomes.

For a full game, the most essential settings are the username and client_port. The username specifies the name of the agent logged in to the game and the client_port specifies the port where the game server is hosted on. For the same port, two agents with the same username cannot be logged in to the game simultaneously. To start a full game, you may take the code in "civrealm/src/civrealm/random_game.py" as an example:

The following line initializes a Freeciv environment:
``` 
env = gymnasium.make('freeciv/FreecivBase-v0')
```
followed by creating an agent (ControllerAgent just randomly chooses actions. You may create your own agent class):
```
agent = ControllerAgent()
```
Then, the environment is reset to get the first observation and information:
```
observations, info = env.reset(client_port=fc_args['client_port'], minitask_pattern=None)
```
Given the observation and information, the agent starts to play the game (by calling its act method) until the game terminates:
```
while not done:
        try:
            action = agent.act(observations, info)
            observations, reward, terminated, truncated, info = env.step(action)
            print(
                f'Step: {step}, Turn: {info["turn"]}, Reward: {reward}, Terminated: {terminated}, '
                f'Truncated: {truncated}, action: {action}')
            step += 1
            done = terminated or truncated
        except Exception as e:
            fc_logger.error(repr(e))
            raise e
    env.close()
```