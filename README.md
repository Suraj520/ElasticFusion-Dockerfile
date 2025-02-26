# Modified README
1. This has been modified for building co_fusion(https://github.com/martinruenz/co-fusion). Evaluation on pre-recorded samples have been done.
2. The Co_fusion binary is located inside the docker in the path : /opt/Co_fusion/build/GUI/build; One can then execute original readme's command by replacing Co_Fusion by ElasticFusion.
3. Pre-recorded sample's link: https://github.com/martinruenz/co-fusion#real-asus-xtion-sequences-in-klg-format
4. Output on pre-recorded sample: https://drive.google.com/file/d/1tmQ22s7O1N1cy9Tmoa8suvP0j8MIkqAd/view?usp=sharing
# ElasticFusion Dockerfile

Dockerfile for use of [ElasticFusion](https://github.com/mp3guy/ElasticFusion) with RealSense

## Requirements

- Docker
  - from: https://docs.docker.com/get-docker/
- NVIDIA Container Toolkit
  - from: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html

### My environment (ref.)

- Ubuntu 20.04
- CUDA 11.2 (host)

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 460.32.03    Driver Version: 460.32.03    CUDA Version: 11.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  GeForce GTX 1080    On   | 00000000:01:00.0  On |                  N/A |
| 46%   52C    P2    67W / 180W |   3900MiB /  8116MiB |     26%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```

## Docker build and run

```terminal
$ docker build -t <image_name> ./docker
$ xhost local:
$ ./opendocker.sh <image_name>
$ xhost -local:
```

## Run with RealSense

I tested only with RealSense D435.

```terminal
$ ElasticFusion
# data is saved as `/opt/ElasticFusion/GUIlive.ply`
```

## Run with sample data

```terminal
$ wget http://www.doc.ic.ac.uk/~sleutene/datasets/elasticfusion/dyson_lab.klg -P ./workspace
# in container
$ ElasticFusion -l dyson_lab.klg
```

![image](https://user-images.githubusercontent.com/25898373/70848804-1d25fa80-1eba-11ea-92c3-2295a08984d8.png)

## Visualize result

```terminal
$ pipenv sync
$ pipenv shell
$ python visualize.py --ply <path/to/.ply>
```

![image](https://user-images.githubusercontent.com/25898373/70864791-f7235780-1f98-11ea-8367-738205205726.png)
