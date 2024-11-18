# Instal·lació aproximada (per a Windows)

S'han d'instal·lar diversos components en dues fases.

- Comprovació de versions

## Steps in Python: 

1. Install anaconda from here: 

    https://repo.anaconda.com/archive/Anaconda3-2022.10-Windows-x86_64.exe

2. Open the Anaconda Prompt:

3. Setup and environment: 

  - `conda create --name EnvName python=3.6`

  - proceed: Y

  - Activate environment:
 
	- `conda activate EnvName`

	- Everytime you use mlagents, you will have to run this line

  - Check python is the right version: 

	- `python --version`

	- Should return 3.6 

4. Install packages:

	- `pip install mlagents`

	- `pip install mlagents_envs`

	- `pip install gym_unity`

	- `pip install torch`

5. run `mlagents-learn`. this should ask you permission, which you should give


- Pantalla unity-learn funcionant
![](mlagentslearn.png)

## Steps in Unity: 

1. Clone MLAgents github repository 

   - `git clone --branch release_19 https://github.com/Unity-Technologies/ml-agents.git`

2. Go to Unity

3. Open package manager -> + -> add package from disk -> com.ml-agents

4. Open package manager -> + -> add package from disk -> com.ml-agents.extensions

## Enllaç alternatiu:

[https://virajvaitha.medium.com/unity-ml-agents-2022-installation-e8af1eab2dd](https://virajvaitha.medium.com/unity-ml-agents-2022-installation-e8af1eab2dd)


