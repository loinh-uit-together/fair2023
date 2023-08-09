#Download từ github
git clone https://github.com/loinh-uit-together/fair2023.git

# YOLO v5
cd /fair2023/yolov5
python train.py --data ./data/coco.yaml --epochs 300 --weights yolov5x.pt --cfg ./models/yolov5x.yaml  --batch-size 8 --device 0
python val.py --task 'test' --weights ./runs/train/exp/weights/best.pt --data ./data/coco.yaml --img 640 --verbose
python detect.py --weights ./runs/train/exp/weights/best.pt --img 640 --conf 0.25 --source ../aeriau/images/test/

# YOLO v6
cd /fair2023/YOLOv6
pip3 install numpy==1.23.5
python ./tools/train.py --batch 8 --conf ./configs/yolov6l_finetune.py --epochs 300 --data ./data/coco.yaml --device 0
python ./tools/eval.py --task 'test' --data ./data/coco.yaml --weights ./runs/train/exp/weights/best_ckpt.pt --verbose
python ./tools/infer.py --weights ./runs/train/exp/weights/best_ckpt.pt --source ../aeriau/images/test/

# YOLO v7
cd /fair2023/yolov7
python train.py --epochs 300 --batch-size 8 --data data/coco.yaml --img 640 640 --cfg cfg/training/yolov7x.yaml --weights yolov7x.pt --device 0
python test.py --task 'test' --weights ./runs/train/exp/weights/best.pt --data data/coco.yaml --img 640 --verbose
python detect.py --weights ./runs/train/exp/weights/best.pt --img 640 --source ../aeriau/images/test/

# Nếu thử nghiệm trên bộ dữ liệu aeriau 
# Copy đoạn sau vào file ./data/coco.yaml 
train: ../aeriau/images/train/
val: ../aeriau/images/test/
test: ../aeriau/images/test/

nc: 4
names: ['car', 'truck', 'bus', 'motor']

# Nếu thử nghiệm trên bộ dữ liệu visdrone
# Copy đoạn sau vào file ./data/coco.yaml 
train: ../visdrone/images/train/
val: ../visdrone/images/test/
test: ../visdrone/images/test/

nc: 10
names: [ 'pedestrian', 'person', 'bicycle', 'car', 'van', 'truck', 'tricycle', 'awning-tricycle', 'bus', 'motor'] 

# Download Model chúng tôi đã train tại đây:
https://drive.google.com/drive/folders/1gPI8u_q6h-x7ULhYdpody66sZUi21kNv?usp=sharing