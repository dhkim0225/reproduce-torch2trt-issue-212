### Build Pytorch docker with torch2trt (CUDA 10.2)
```
sudo docker build -f Dockerfile.pytorch -t='test/test:torch2trt_cu102' .
```

Run pytorch docker and make .engine outputs with make_engine.py.
```
sudo docker run --rm -v$(pwd):/home/ --gpus all test/test:torch2trt_cu102 python3 /home/make_engine.py
```

Run pytorch docker and deserialize model.plan.
```
sudo docker run --rm -v$(pwd):/home/ --gpus all test/test:torch2trt_cu102 python3 /home/deserialize_engine.py
```

### Build TRTIS docker (CUDA 10.2)
```
sudo docker build -f Dockerfile.trt -t test/test:TRTIS .
```

Run TRTIS
```
sudo docker run --rm -v$(pwd):/home/ --gpus all --shm-size=1g --ulimit memlock=-1 --ulimit stack=67108864 -p8000:8000 -p8001:8001 -p8002:8002 test/test:TRTIS
```
