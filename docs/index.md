# CivRealm

CivRealm is a reinforcement learning environment for the open-source strategy game [Freeciv-web](https://github.com/freeciv/freeciv-web) based on [Freeciv](https://www.freeciv.org/). The goal is to provide a simple interface for AI researchers to train agents on Freeciv.

## Install and Setup

### System Requirements

Civrealm requires Python version >=3.8.

In order to test the civrealm on <http://localhost>, please download the docker image from: https://drive.google.com/file/d/1tf32JpwqGN7AtUPe0Q4fIRkE4icSM-51/view?usp=sharing.

> :warning:
> Please make sure you have installed **the latest** docker engine and docker-compose.
> Using older versions of docker may result in unexpected erorrs.


### Installation
> We suggest using Conda to create a clean virtual environment for installation.

Installation through the source code in the civrealm folder:

```bash
cd civrealm
pip install -e .
```

### Testing the installation

To test if the installation is successful, run

```bash
test_civrealm 
```

To test with multiple players, run

```bash
test_civrealm --minp=2 --username=myagent --client_port=6001
```

Then start another terminal and run:

```bash
test_civrealm --username=myagent1 --client_port=6001
```
> :warning:
> Note that to run multiple agents in the same game, you need to make them connect to the same port (specified by client_port). The available client_port range is 6001, 6300~6331.

> :warning:
> Note that when a game finishes on a port, the server on that port will take some time (around 10 seconds) to restart itself. If you start a new game on that port before the server is ready, the program will encounter expected errors and may stop/halt.

To observe the game play, you can access http://localhost:8080/ on a browser. Then, please click the "Online Games" button. You can find the running game under the "MULTIPLAYER" tab.

### Trouble Shooting

The following are some common issues that you may encounter when running the code. If you encounter any other issues, please feel free to open an issue.

* Note that each game corresponds to one port on the server. If one game just stops and you immediately start a new game connecting to the same port as the stopped game, the new game may encounter errors and exit. Our training has used ''Ports.get()'' in ''civrealm/freeciv/utils/port_utils.py'' to avoid the situation. If you want to configure the client port and start a client manually, you need to find the available ports by checking the 'Online Games/MULTIPLAYER' tab in localhost:8080.

* If firefox keeps loading the page, please try to add the following line to `/etc/hosts`:

    ```bash
    127.0.0.1 maxcdn.bootstrapcdn.com
    127.0.0.1 cdn.webglstats.com
    ```