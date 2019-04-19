# Simbotic AirSim

Machine learning, physics and controls development environment:

- airsim rosnode
- python airsim and tensorflow scripts
- C++ and tensorflow applications
- AirSim lib developemnt - physics models and APIs
- PX4 missions


# Setup

Clone this repo recursively:
```
git clone --recursively git@github.com:VertexStudio/simbotic-airsim.git
```

## Docker Setup

CPU-based docker build:
```
./docker_build.sh
./docker_run.sh
```

GPU-based docker build.
You will need [nvidia-docker](https://github.com/NVIDIA/nvidia-docker).
```
./docker_build.sh gpu
./docker_run.sh gpu
```

## Inside Docker Image


### Python Client

```
cd $AIRSIM_ROOT/scripts
python hello_drone.py
```

### C++ Client

Setup AirSim:
```
$AIRSIM_ROOT/setup.sh
```

Build C++ app:
```
cd $AIRSIM_ROOT/app
./cmake_build/bin/cmake -G "Unix Makefiles"
make -j`nproc`
./air-app
```

## Advanced Docker Setup

### CPU-based image
```
cd simbotic-airsim # into this repo clone
docker build --build-arg USER_ID=$(id -u ${USER}) --build-arg GROUP_ID=$(id -g ${USER}) -t simbotic-airsim/cpu .
docker run --runtime=nvidia -ti -v $(pwd):/sim --network=host -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --cap-add=SYS_PTRACE simbotic-airsim/cpu
```

### GPU-based image
You will need [nvidia-docker](https://github.com/NVIDIA/nvidia-docker).
```
cd simbotic-airsim # into this repo clone
docker build --build-arg USER_ID=$(id -u ${USER}) --build-arg GROUP_ID=$(id -g ${USER}) -t simbotic-airsim/gpu .
docker run --runtime=nvidia -ti -v $(pwd):/sim --network=host -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --cap-add=SYS_PTRACE simbotic-airsim/gpu
```

