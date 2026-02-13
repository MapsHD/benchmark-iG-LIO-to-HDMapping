# iG-LIO to HDMapping simlified instruction

## Step 1 (prepare data)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)).

File 'reg-1.bag' is an input for further calculations.
It should be located in '~/hdmapping-benchmark/data'.


## Step 2 (prepare docker)
```shell
mkdir -p ~/hdmapping-benchmark
cd ~/hdmapping-benchmark
git clone https://github.com/MapsHD/benchmark-iG-LIO-to-HDMapping.git --recursive
cd benchmark-iG-LIO-to-HDMapping
git checkout Bunker-DVI-Dataset-reg-1
docker build -t ig-lio_noetic .
```

## Step 3 (run docker, file 'reg-1.bag' should be in '~/hdmapping-benchmark/data')
```shell
cd ~/hdmapping-benchmark/benchmark-iG-LIO-to-HDMapping
chmod +x docker_session_run-ros1-ig-lio.sh 
cd ~/hdmapping-benchmark/data
~/hdmapping-benchmark/benchmark-iG-LIO-to-HDMapping/docker_session_run-ros1-ig-lio.sh reg-1.bag .
```

## Step 4 (Open and visualize data)
Expected data should appear in ~/hdmapping-benchmark/data/output_hdmapping-ig-lio
Use tool [multi_view_tls_registration_step_2](https://github.com/MapsHD/HDMapping) to open session.json from ~/hdmapping-benchmark/data/output_hdmapping-ig-lio.

You should see following data

lio_initial_poses.reg

poses.reg

scan_lio_*.laz

session.json

trajectory_lio_*.csv

## Movie
[[movie]](https://youtu.be/KlZf7nHeVmI)

## Contact email
januszbedkowski@gmail.com