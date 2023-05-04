# Virtual environemnts and installing packages



Today, we will work in our machines, **not in the google colab or kaggle** and see how to do that. 

Now, we will create a `virtual environment`. A virtual enviro­nment is a Python tool for `dependency management` and `project isolation`. They allow Python third party libraries to be installed locally in an isolated directory for a particular project. *So it works like an isolated box insode your machine for python.*

<!-- We will create **virtual environments** inside our machine so that different projects and versions of the packages do not get mmixed up. Virtual environments are like separate boxes inside your machine which do not intearct between each other.  -->

To install libraries, we will use `conda`, which will also be used to create virtual environments. Other ways of doing that will be using `Pip` to install packages and `venv` or some other method to create virtual environment,

After that, we will try to run n example repository from github (about nanoGPT). 

# Conda

`conda cheatsheet`: https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf


## Install conda
Goto https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html#regular-installation and install conda (miniconda for smaller size)

Install Anaconda or Miniconda normally, and let the installer add the conda installation of Python to your PATH environment variable. There is no need to set the PYTHONPATH environment variable.

To see if the conda installation of Python is in your PATH variable:
* On Windows, open an Anaconda Prompt and run `echo %PATH%`
* On macOS and Linux, open the terminal and run `echo $PATH`



## After Installation, create virtual environement
We will try `nanoGPT` (https://github.com/karpathy/nanoGPT) and run somse of the examples - we will not create new code but use another person's code. 

To do that, we will create a new virtual environment:
* Create environment
```bash
conda create --name ENVNAME
```
* Activate that environment
```bash
conda activate ENVNAME
```

## Install packages: 

* First, install pytorch according to this website: https://pytorch.org/get-started/locally/
```bash
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```
* Then other packages according to the readme file of the `nanoGPT`:
```bash
conda install transformers datasets tiktoken wandb tqdm -c conda-forge
```
(Some of the package need the extra channel `conda-forge`)



## Go to nanoGPT page and download the package
* Download or clone:
```bash
git clone https://github.com/karpathy/nanoGPT.git --depth 1
```
* Go inside the folder
```bash
cd nanoGPT
```

We will not train the whole model as it would take time. We would `fine-tune` the model, already script is ready. 

Configure to prepare the models:
```bash
python data/shakespeare/prepare.py --device=cpu
```
Fine tune (skip it for now, you can fine tune more, see the readme of the `nanoGPT` github repo):
```bash
python train.py config/finetune_shakespeare.py --device=cpu --init_from=gpt2 --eval_iters=10
```


Sample from it
```bash
python sample.py --device=cpu\
    --init_from=gpt2 \
    --start="What is the answer to life, the universe, and everything?" \
    --num_samples=5 --max_new_tokens=100
```


Deactivate the environment
```bash
conda deactivate
```




# PIP
The other common way to use the virtual environment is via `venv` and `Pip`. First, we have to install `pip`.
"Pip is a thing that installs packages, pip itself is a package that someone might want to install..." 
```sh
# Download PIP globally
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

# Install it
python get-pip.py

# Veirfy
pip --version
```


For windows users, you have to add path of the pip and python to the environment variable. 
You can check the link: `https://www.activestate.com/resources/quick-reads/how-to-install-pip-on-windows/`
and go to `Adding PIP to Windows Environment Variables` section.

One of the most common problems with running Python tools like pip is the “not on PATH” error. This means that Python cannot find the tool you’re trying to run in your current directory. In most cases, you’ll need to navigate to the directory in which the tool is installed before you can run the command to launch it. 

If you’d rather run pip (or other tools) from any location, you’ll need to add the directory in which it’s installed as a PATH environment variable by doing the following:  
* Open up the Control Panel and navigate to System and Security > System
* Click on the Advanced system settings link on the left panel
* Click Environment Variables.
* Under System Variables, double-click the variable PATH.
* Click New, and add the directory where pip is installed, e.g. C:Python33Scripts, and select OK.


----------------------------------------------------
## Virtual environments

We will create **virtual environments** inside our machine so that different projects and versions of the packages do not get mmixed up. 
Cheatsheet: https://gist.github.com/ryanbehdad/858b47b54be441a684efb7ae6ca98a75


We will use `venv` function which is already shipped with python.
```sh
# creates a virtualenv
python -m venv venv1

# activates the virtualenv
source venv1/bin/activate

# or, for windows
.\venv1\Scripts\activate
```


### Install packages
```bash
pip install transformers datasets tiktoken wandb tqdm
#or 
python -m pip install -U transformers datasets tiktoken wandb tqdm
```




## Other ways for virtual environment using `virtualenv`

Cheatsheet: https://cheatography.com/ilyes64/cheat-sheets/python-virtual-environments/

### Installing virtualenv
* macOS and Linux
```bash
python3 -m pip install --user virtualenv
```

* Windows
```bash
py -m pip install --user virtualenv
```

## Creating a virtual enviro­nment
* macOS and Linux
```bash
python3 -m virtualenv my-env
```

* Windows
```bash
py -m virtualenv my-env
```

### Activating a virtual enviro­nment
* macOS and Linux
```bash
source my-env­/bi­n/a­ctivate
```

* Windows
```bash
.\my-e­nv­\Scr­ipt­s\a­ctivate
```

### Leaving the virtual enviro­nment
```bash
deactivate
```

### Installing packages
```bash
pip install transformers
```