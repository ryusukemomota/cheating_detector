# cheating_detector

## Motivations
Students may feel cheating in exams is a quick solution, but it surely ruins their self-esteem and causes distrust among teachers as well as colleagues, compromising learning atmosphere. Surveillance by an intelligent machine eye can be a great preventative measure. This AI detects suspicious eye movements in the exam.

![cheating_detector](https://user-images.githubusercontent.com/7350397/152345617-904af23c-4945-42f3-b38b-bb59f1b34b5b.jpg)

## Demo movie on YouTube
https://youtu.be/2bgxs5Pk06Q

## Hardwares
- NVIDIA Jetson Development Kit series (verified on Jetson Xavier NX Development Kit)
- USB Web Camera or Raspberry pi camera module (V2)

## Set Up and Docker
- Follow the "Setting up Jetson with JetPack" and "Running the Docker Container" steps in "HELLO AI WORLD" (https://github.com/dusty-nv/jetson-inference#hello-ai-world).
- Git clone this project.

        $ git clone https://github.com/ryusukemomota/cheating_detector
        $ cd jetson-inference
        $ docker/run.sh -v /my/host/cheating_detector:/my/container/path #Please use your local git clone absolute path.
        $ cd /my/container/path
        $ python3 cheater_detector.py /dev/video0 # csi://0 if using RaspberryPi CSI camera
    
## How it works?
- The program is based on the demo program for the Pose Estimation with PoseNet (posenet.py) of "HELLO AI WORLD" and the pre-trained pose estimation model "Pose-ResNet18-Body".
- This program evaluates the triangular shape by nose (Keypoint: 0), left_eye (Keypoint: 1) and right_eye (Keypoint: 2) to estimate the direction of the gaze.
- The side of the triangle between the left_eye and right_eye were evenly divided into three parts: right, middle and left.
- If the value of nose.x is within the range of x-value of the middle part, it returns "front: OK". Otherwise, it will return "right" or "left".

<img width="935" alt="cheating_detector" src="https://user-images.githubusercontent.com/7350397/152495301-3a1556d7-aa98-490e-86e2-3638c375b361.png">

## Issues
- ~~Never tested in real exams.~~ Follow your organization's privacy policy. Use with cautions!

## Future directions
- Currently, working on changing the color for "ALERT" message from white to red or orange.
- "ALERT" will be notified by light, sounds and  e-mail to staffs.
