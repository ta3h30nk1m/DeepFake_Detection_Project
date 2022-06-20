# DeepFake_Detection_Project

2022 Spring Yonsei Univ. CSI4108 course Project  - Deep Learning Practice

Topic: DeepFake Detection

train and inference data from https://dacon.io/competitions/official/235655/overview/description)

Final result: 91.463% (Accuracy)

1. Image Selector
- Train dataset: About 1.7 millions real&fake images (127GB)
- Choose randomly - fake: 169868 images, real: 134967 images

2. MTCNN
- Crop the face from images by using MTCNN (https://github.com/ipazc/mtcnn)
- Give a little margin from the target(face) box

3. EfficientNetB4+RectifiedAdam
- Apply various data augmentations to reduce overfitting - Horizontal Flip, Gaussian Blur, Gaussian Noise, Image Compression
- Apply one more augmentation - mask part of the face by using dlib face landmark
- Batch Size: 6 - used RTX2080, cannot run larger batch size when using EfficientNet
- Input Size: 224 x 224 x 3
- Model: EfficientNetB4 + FC(512) + Dropout(0.5) + output(1)
- Optimizer: RectifiedAdam, Loss: CE
- Train on 5~6 epochs
