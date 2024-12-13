<div align="center">
<img src="assets/Group 21.png" width="50%" alt='Sparky-ml-pets'>
<h1 align="center">Sparky-ml-pets</h1>
<h3 align="center">Framework for training and deploying AIs for Super Auto Pets</h3>

[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7834142.svg)](https://doi.org/10.5281/zenodo.7834142)
[![PEP8](https://img.shields.io/badge/code%20style-pep8-orange.svg)](https://www.python.org/dev/peps/pep-0008/)
[![codecov](https://codecov.io/gh/andreped/super-ml-pets/branch/main/graph/badge.svg?token=9YF7NANQTE)](https://codecov.io/gh/andreped/super-ml-pets)
![GitHub repo size](https://img.shields.io/github/repo-size/AndrePedersenDev/SparkyAIPet)
![GitHub issues](https://img.shields.io/github/issues/AndrePedersenDev/SparkyAIPet)
![GitHub stars](https://img.shields.io/github/stars/AndrePedersenDev/SparkyAIPet?style=social)
 
Train AIs for Super Auto Pets through a simulated environment and test the trained model against real opponents in the actual game! AI is trained using reinforcement learning and a machine vision system is used to capture the screen to give information to the AI.

Sparky is a unique AI-driven pet represented as a $sparky token on the Solana blockchain. Its core parameters—Health, Energy, Food, and Happiness—dynamically evolve over time, reflecting the pet’s overall state. Users can monitor Sparky’s condition through a dedicated web interface and interact with it on Twitter, encouraging community engagement and widespread interest. The technology stack utilizes React and Node.js for the web application, PostgreSQL for data management, and Solana integration for token verification and updates. Future developments may include more advanced AI-driven behavior, additional features, and integration with external data sources. Sparky’s key value lies in offering an original, entertaining, and interactive digital pet experience powered by cutting-edge technology.

</div>

## [Introduction](https://github.com/andreped/super-ml-pets#introduction)

Framework supports Python `3.7-3.11` and works cross-platform (Ubuntu, Windows, macOS). Deployment is also compatible with the [web app](https://teamwood.itch.io/super-auto-pets).

Training has also been tested with [GitHub Codespaces](https://github.com/features/codespaces) and [Google Colab](https://colab.research.google.com/). A demonstration of model training can be seen in [this gist](https://colab.research.google.com/gist/andreped/cc0789bd711874f792c0991978b2f981/super-ml-pets-test.ipynb).

We recommend using **Windows for deployment** as the UNIX-based systems require root permissions to launch the program out-of-the-box.

## [Getting started](https://github.com/andreped/super-ml-pets#getting-started)

1. Clone the repo:
```
git clone https://github.com/AndrePedersenDev/SparkyAIPet.git
```

2. Setup virtual environment:
```
cd super-ml-pets/
virtualenv -ppython3 venv --clear
./venv/Scripts/activate
```

To activate the virtual environment on UNIX-based systems, instead of the last line run `source venv/bin/activate`

3. Install requirements:
```
pip install -r requirements.txt
```

4. Download all pets, food, and misc icons
```
wget https://github.com/AndrePedersenDev/SparkyAIPet/releases/download/pets-01-2024/pets.zip -O pets.zip; Expand-Archive pets.zip -DestinationPath ./; Remove-Item pets.zip
wget https://github.com/AndrePedersenDev/SparkyAIPet/releases/download/food-01-2024/food.zip -O food.zip; Expand-Archive food.zip -DestinationPath ./; Remove-Item food.zip
wget https://github.com/AndrePedersenDev/SparkyAIPet/releases/download/misc-01-2024/misc.zip -O misc.zip; Expand-Archive misc.zip -DestinationPath ./; Remove-Item misc.zip
```

<details>
<summary>Additional setup for Ubuntu only</summary>

```
sudo apt install python3-tk
sudo su
source venv/bin/activate
xhost +
export DISPLAY=:0.0
```

Note that the command `sudo su` enables administrator rights. This seems to be required by `keyboard` as mentioned in issue https://github.com/andreped/super-ml-pets/issues/23. The xhost + DISPLAY stuff is needed as the screen might not be found, hence, initializing one solves this issue.

</details>

## [Usage](https://github.com/AndrePedersenDev/SparkyAIPet#usage)
This framework currently supports training and deploying RL models for SAP.

<details open>
<summary>Training</summary>

For training in simulated environment, using default arguments, simply run:
```
python main.py --task train
```

Given an existing model, it is also possible to finetune it by (with example):
```
python main.py --task train --finetune /path/to/model_sap_gym_sb3_180822_checkpoint_2175_steps
```

The script supports other arguments. To see what is possible, run:
```
python main.py --help
```

</details>

<details open>


</details>

<details>
<summary>Training history</summary>

To plot training history, run:
```
python smp/plot_history.py --log /path/to/history/history_rl_model/progress.csv
```

<p align="center">
  <img src="assets/training_history_example.png" width="60%" alt='super-auto-pets'>
</p>

</details>

<details>
<summary>Troubleshoot</summary>

To install virtualenv, run:
```
pip install virtualenv
```

If you do not have virtualenv in the path, you can access it by:
```
python -m virtualenv -ppython3 venv --clear
```

To activate virtual environment on UNIX-based systems (e.g., macOS or Ubuntu), run:
```
source venv/bin/activate
```

If you are using newer versions of Python (e.g., `3.10`), you might have issues with installing and/or using `numpy` with the other dependencies. If that happens, try downgrading numpy by:
```
pip install numpy==1.23.2 --force-reinstall
```
 
On both Ubuntu and macOS, it might require sudo permissions to run deployment. This has to do with keyboard events not being able to be recognized without
sudo rights. On Windows, administrative rights is **not needed**. For more information, see [here](https://pynput.readthedocs.io/en/latest/limitations.html).
 
On macOS, when you are downloading the models (.zip files) from [Releases](https://github.com/andreped/super-ml-pets/releases), they might be unzipped automatically. This is **bad** as the model extension is `.zip`. To fix this, disable the `Open safe files after downloading` in the Safari Preferences (see [here](https://www.lifewire.com/disable-open-safe-files-after-downloading-in-safari-446562) for more information).
 
If deployment fails to start (no mouse movements or events), it may be because your screen resolution differ from the expected resolution. The current machine vision system expects the screen resolution to be `1920x1080`. Please, adjust the resolution to this. This will be fixed in the future.

</details>

## [Acknowledgements](https://github.com/andreped/super-ml-pets#acknowledgements)
This implementation is based on multiple different projects. The core implementation is derived from [GoldExplosion](https://github.com/GoldExplosion/SuperAutoPets-RL-Agent), which further was based upon the super auto pets engine [sapai](https://github.com/manny405/sapai) and RL training through [sapai-gym](https://github.com/alexdriedger/sapai-gym).

All credit to [jpdefrutos](https://github.com/jpdefrutos) for designing the amazing [header figure](https://github.com/andreped/super-ml-pets/blob/main/assets/SMLP.svg).

## [Citation](https://github.com/andreped/super-ml-pets#citation)
If you found this project relevant for your research, please, cite the following:
```
@software{andre_pedersen_2024_7834142,
  author       = {André Pedersen},
  title        = {andreped/super-ml-pets: v0.0.9},
  month        = dec,
  year         = 2024,
  publisher    = {Zenodo},
  version      = {v0.0.9},
  doi          = {10.5281/zenodo.7834142},
}
```
