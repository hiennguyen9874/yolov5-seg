# Export Yolov5-seg to ONNX and TensorRT

This implimentation is based on [yolov5](https://github.com/ultralytics/yolov5).

## Install

- [TensorRT OSS Plugin](https://github.com/hiennguyen9874/TensorRT)

- [onnx-graphsurgeon](https://github.com/NVIDIA/TensorRT/tree/main/tools/onnx-graphsurgeon)

## Usage

### Download model

### Export with roi-align

#### Export ONNX

- `python3 segment/export.py --data ./data/coco128-seg.yaml --weights ./weights/yolov5m-seg.pt --batch-size 1 --device cpu --simplify --opset 14 --workspace 8 --iou-thres 0.65 --conf-thres 0.35 --include onnx --end2end --cleanup --dynamic-batch --roi-align`

- [scripts](tools/onnx_mask-roialign.ipynb)

#### Export TensorRT

- `python3 segment/export.py --data ./data/coco128-seg.yaml --weights ./weights/yolov5m-seg.pt --batch-size 1 --device cpu --simplify --opset 14 --workspace 8 --iou-thres 0.65 --conf-thres 0.35 --include onnx --end2end --trt --cleanup --dynamic-batch --roi-align`

- `/usr/src/tensorrt/bin/trtexec --onnx=./weights/yolov5m-seg.onnx --saveEngine=./weights/yolov5m-seg-nms.trt --workspace=8192 --fp16 --minShapes=images:1x3x640x640 --optShapes=images:1x3x640x640 --maxShapes=images:8x3x640x640 --shapes=images:1x3x640x640`

- [scripts](tools/trt_mask-roialign.ipynb)

### Export without roi-align

#### Export ONNX

- `python3 segment/export.py --data ./data/coco128-seg.yaml --weights ./weights/yolov5m-seg.pt --batch-size 1 --device cpu --simplify --opset 14 --workspace 8 --iou-thres 0.65 --conf-thres 0.35 --include onnx --end2end --cleanup --dynamic-batch`

- [scripts](tools/onnx_mask.ipynb)

#### Export TensorRT

- `python3 segment/export.py --data ./data/coco128-seg.yaml --weights ./weights/yolov5m-seg.pt --batch-size 1 --device cpu --simplify --opset 14 --workspace 8 --iou-thres 0.65 --conf-thres 0.35 --include onnx --end2end --trt --cleanup --dynamic-batch`

- `/usr/src/tensorrt/bin/trtexec --onnx=./weights/yolov5m-seg.onnx --saveEngine=./weights/yolov5m-seg-nms.trt --workspace=8192 --fp16 --minShapes=images:1x3x640x640 --optShapes=images:1x3x640x640 --maxShapes=images:8x3x640x640 --shapes=images:1x3x640x640`

- [scripts](tools/trt_mask.ipynb)
