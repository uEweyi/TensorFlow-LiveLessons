# Step-by-Step Instructions for Mac OS X

## Install

1. open the Terminal application ([like this](http://www.wikihow.com/Open-a-Terminal-Window-in-Mac))
2. to install in your home directory (this is my recommended default):
	* type `cd ~` into the command-line prompt and 
	* *execute* the line by pressing the **return** key on your keyboard
3. retrieve all of the code for this LiveLessons by executing `git clone https://github.com/the-deep-learners/TensorFlow-LiveLessons.git` (if you haven't used `git` before, you may be prompted to install Xcode -- do it!)
4. [install the Docker "Stable channel"](https://docs.docker.com/docker-for-mac/install/)
5. start Docker, e.g., by using Finder to navigate to your Applications folder and double-clicking on the Docker icon
6. back in Terminal, execute `source TensorFlow-LiveLessons/installation/let_jovyan_write.sh` so that you can write to files in the *TensorFlow-LiveLessons* directory from inside the Docker container we'll be creating momentarily 
7. move into the *TensorFlow-LiveLessons* directory by executing `cd TensorFlow-LiveLessons`
8. build the Docker container by executing `sudo docker build -t tensorflow-ll-stack .` (you'll get an error if you miss the final `.`!)
9. when that build process has finished, run the Docker container by executing `sudo docker run -v ~/TensorFlow-LiveLessons:/home/jovyan/work -it --rm -p 8888:8888 tensorflow-ll-stack`
10. in the web browser of your choice (e.g., Chrome), copy and paste the URL created by Docker (this begins with `http://localhost:8888/?token=` and should be visible near the bottom of your Terminal window) 

## Shutdown

You can shutdown the Jupyter notebook by returning to the Terminal session that is running it and hitting the **control** and **c** keys simultaneously on your keyboard. 

## Restart

You can restart the Jupyter notebook later by following steps nine and ten alone. 

## Bonus: Training Models with an Nvidia GPU

You don't need to train your Deep Learning models with a GPU for these LiveLessons, but some of the later notebooks in these LiveLessons will run much more quickly if you do. 

1. install an [Nvidia GPU](http://www.nvidia.com/content/global/global.php) on your machine or spin up a cloud instance that includes one (typically a Tesla K80)
1. install CUDA and cuDNN, e.g., per the **Installing CUDA Toolkit** and **Installing cuDNN** sections of [this blog post](https://hackernoon.com/launch-a-gpu-backed-google-compute-engine-instance-and-setup-tensorflow-keras-and-jupyter-902369ed5272) (this step may be tricky if you're relatively new to working with the Unix command line)
2. in the `TensorFlow-LiveLessons/installation/docker-stack-scripts` directory:
	* run `chmod 777 jupyter_notebook_config.py start*.sh`
3. replace step eight of my **Install** section above with `sudo docker build -f Dockerfile-gpu -t tfll-gpu-stack .`
4. replace step nine with `sudo nvidia-docker run -v ~/TensorFlow-LiveLessons:/home/jovyan/work -it --rm -p 8888:8888 tfll-gpu-stack`
