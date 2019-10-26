# Adventures in making a game in python

## Project set up

Step one : Create environment with conda

I'm using Miniconda version (4.7.9) with python 3.7.3 on Windows.

```sh
conda create -n STG python=3.7
conda activate STG
```

Step two : install pygame (1.9.6)

```sh
(STG) $ python -m pip install pygame
```

Check if it's been properly installed by running `python -m pygame.examples.aliens`

