# train
```sh
python train.py --img 640 --batch 64 --epochs 100 --data data/sl_coco.yaml --cfg ./yolov5n.yaml --weights ./yolov5n.pdparams --noautoanchor

```
# convert to pdmodel
```sh
# paddle-bfloat          0.1.7
# paddle2onnx            1.0.6
# paddlelite             2.11
# paddlepaddle-gpu       2.4.2.post117
# docker exec -it paddle bash

nvidia-docker run --name paddle -it --shm-size=8g  -v /home/server/yolov5n:/paddle paddlepaddle/paddle:2.5.0-gpu-cuda11.7-cudnn8.4-trt8.4 /bin/bash
python convert_static.py --weights runs/train/exp/weights/best.pdparams --cfg ./yolov5n.yaml --data data/sl_coco.yaml --source crop.jpg
```
# convert to paddlelite opencl
```sh
paddle_lite_opt --model_file=./simple_net.pdmodel --param_file=simple_net.pdiparams  --optimize_out_type=naive_buffer --optimize_out=./yolov5n_gpu --valid_targets=opencl
```

# cpp code
```sh
https://github.com/PaddlePaddle/Paddle-Lite-Demo/tree/develop/object_detection/android/shell/cxx/yolov5n_detection
```
