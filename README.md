# Synthetic_Dataset_Generator
The aim of this Unity project is to generate synthetic datasets for training and evaluating, mainly but not limited to, Active Perception/Vision methods. It utilises a modified version 0.9.0-preview.1 of the [Unity Perception Package](https://github.com/Unity-Technologies/com.unity.perception) along with some additional scripts and Randomizers that were developed for the purpose of this work.

This project was used in my [diploma thesis](https://www.researchgate.net/publication/362093799_Generation_of_a_Synthetic_Annotated_Dataset_for_Training_and_Evaluating_Active_Perception_Methods) for generating [ActiveHumans](https://zenodo.org/record/8359766), a synthetic dataset that contains RGB images, semantic segmentation images and JSON annotations for every valid combination of 8 environments, 33 humans, 4 lighting conditions, 7 camera distances (1m - 4m away from the human) and 36 camera angles (0° - 360° with 10° increments, rotating around the human). A combination is rendered invalid if camera GameObject is colliding with another object. The project also supports the addition of animations to the humans with two Randomizers that control the changing of the animations and the proper playing of each one. 

Using the additional scripts, a second dataset, [ActiveFace](https://github.com/opendr-eu/datasets/tree/main/active_face), that contains only facial RGB images, was generated.

The main dataset generation algorithm can be described by a sequence of nested for-loops:

```
For each Environment e
  For each Human h
    For each Lighting Condition l
      For each Animation a
        For each Animation Frame f
          For each Camera Position p
            For each Camera Angle a
              Capture and output images and metadata
```

## Image Examples
For each valid capture, the project generates an RGB image and its semantic segmentation counterpart.

### RGB Images
![Images](https://user-images.githubusercontent.com/72664246/177645117-ee686ab1-d043-44ab-a06a-1fc8c44d96f6.jpg)

### Semantic Segmentation Images
![Semantic](https://user-images.githubusercontent.com/72664246/177645984-ee049d24-fd7e-451b-a547-849ee49bfd28.png)

## Generated Folders
The Unity project generates 3 folder:
- Dataset Data: Contains the JSON files that are generated during the Simulation.
- RGBImages: Contains the RGB images.
- SemanticSegmentationImages: Contains the semantic segmentation images.

### Dataset Data
During the Simulation, the Perception package generates JSON files which contain ground truth annotations that describe each captured image. The package's source code was modified so that each JSON file contains annotations for one environment, one human and one lighting condition. If animations are enabled, each JSON file contains annotations for one environment, one human, four lighting conditions and one animation.

The dataset that was generated in my diploma thesis contained 2D Bounding Box, 3D Bounding Box and Keypoint annotations.

### Image Naming
If animations are enabled, each image is named: *e_h_l_a_f_d_r.jpg*, where
-  **e** denotes the id of the environment.
-  **h** denotes the id of the human.
-  **l** denotes the id of the lighting condition.
-  **a** denotes the id of the animation.
-  **f** denotes the frame of the animation.
-  **d** denotes the camera's distance from the human.
-  **r** denotes the rotation degrees of the camera.

If animations are disabled, each image is named: *e_h_l_d_r.jpg*.

## Used Assets
The Unity project that was developed for my diploma thesis included 8 environments created from free assets downloaded from the [Unity Asset Store](https://assetstore.unity.com/?gclid=Cj0KCQjw5ZSWBhCVARIsALERCvw1Bhpyz7oRJ-wyDHO-6OJuqiU-nU1S0uTIDNy_6Mbz9tNTsrmLGsIaAuUrEALw_wcB&gclsrc=aw.ds). 29 out of the 33 human models were downloaded from the [Asset Store](https://assetstore.unity.com/?gclid=Cj0KCQjw5ZSWBhCVARIsALERCvw1Bhpyz7oRJ-wyDHO-6OJuqiU-nU1S0uTIDNy_6Mbz9tNTsrmLGsIaAuUrEALw_wcB&gclsrc=aw.ds), [Mixamo](https://www.mixamo.com/#/) and [Turbosquid](https://www.turbosquid.com/?&utm_source=google&utm_medium=cpc&utm_campaign=RoEUAF-en-TS-Brand&utm_content=ts%20brand&utm_term=turbosquid&mt=e&dev=c&itemid=&targid=kwd-297496938642&loc=9061579&ntwk=g&dmod=&adp=&gclid=Cj0KCQjw5ZSWBhCVARIsALERCvx-98mKydP7qVEzkzbkv1eKZioniGXh6Mx24qUdCa4lmnYCegmD8H0aAlvpEALw_wcB&gclsrc=aw.ds). Due to [Mixamo](https://www.mixamo.com/#/) and [Turbosquid's](https://www.turbosquid.com/?&utm_source=google&utm_medium=cpc&utm_campaign=RoEUAF-en-TS-Brand&utm_content=ts%20brand&utm_term=turbosquid&mt=e&dev=c&itemid=&targid=kwd-297496938642&loc=9061579&ntwk=g&dmod=&adp=&gclid=Cj0KCQjw5ZSWBhCVARIsALERCvx-98mKydP7qVEzkzbkv1eKZioniGXh6Mx24qUdCa4lmnYCegmD8H0aAlvpEALw_wcB&gclsrc=aw.ds) Terms of Service, the human models and animations downloaded from these sources are not included in this repository, however the ones from [Turbosquid](https://www.turbosquid.com/?&utm_source=google&utm_medium=cpc&utm_campaign=RoEUAF-en-TS-Brand&utm_content=ts%20brand&utm_term=turbosquid&mt=e&dev=c&itemid=&targid=kwd-297496938642&loc=9061579&ntwk=g&dmod=&adp=&gclid=Cj0KCQjw5ZSWBhCVARIsALERCvx-98mKydP7qVEzkzbkv1eKZioniGXh6Mx24qUdCa4lmnYCegmD8H0aAlvpEALw_wcB&gclsrc=aw.ds) are linked below:
- [3D Claudia Rigged 002](https://www.turbosquid.com/3d-models/3d-photorealistic-human-rig-1422551)
- [Carla Rigged 001 3D](https://www.turbosquid.com/3d-models/photorealistic-human-rig-3d-1422548)
- [Eric Rigged 001 3D](https://www.turbosquid.com/3d-models/photorealistic-human-rig-3d-1422553)

Four additional humans (one male adult, one male baby, one female adult, one female baby) were designed using [MakeHuman](http://www.makehumancommunity.org). Since, I created these models, they are included in this repository in the *Assets/MyModels* folder.

### Animation Controllers
The animation controllers located in the *Assets/Resources* folder were created for the following animations from [Mixamo](https://www.mixamo.com/#/):
- Arm Stretching (used for frames 0-250)
- Crawling
- Dying (used as a falling animation from frames 35-90)
- Having Seizure (used for frames 10-150)
- Push Ups (used for frames 0-45)
- Shoulder Rubbing (used for frames 0-140)
- Sit Ups (used for frames 0-65)
- Yelling (used for frames 10-200)

One additional [Coughing](https://assetstore.unity.com/packages/3d/animations/idle-mocap-28345) animation (used for frames 165-339) was downloaded from the [Asset Store](https://assetstore.unity.com/?gclid=Cj0KCQjw5ZSWBhCVARIsALERCvw1Bhpyz7oRJ-wyDHO-6OJuqiU-nU1S0uTIDNy_6Mbz9tNTsrmLGsIaAuUrEALw_wcB&gclsrc=aw.ds).

# ActiveFace Dataset
A second dataset, ActiveFace, was generated containing only the face images for each human. This was achieved by adding a transparent cube on each human's head and labeling it as "head". Then, the 2D Bounding Box coordinates of each head were extracted and used to crop the original images in order to retain only the faces. However, since the labeled head GameObject overlaps with the "person" label which cover the whole human model, if both *Labeling* components are active the 2D Bounding Box Labeler would sometimes capture false coordinates for a person's head. For that reason, the transparent head cubes are by default disabled when opening this project. As a result, if one wants to create a face image dataset using this project they should:
- Disable the *Labeling* component of each human.
- Disable the Keypoint Labeler, since without any labeled humans the Labeler will not capture any data.
- Enable the **Head** GameObject which is a child GameObject of the head skeleton parent GameObject of each human.

The face images were used to train and evaluate an [existing enbedding-based active face recogniser](https://ieeexplore.ieee.org/document/9287085) which demonstrated how the extensive pan and distance range that the dataset provides can yield impressive results when training an Active Perception model using this dataset.

## Face Image Examples
![Faces](https://user-images.githubusercontent.com/72664246/178233325-417f6717-db24-403b-a8b6-c494c8c5eb03.png)

# Additional Scripts
Two additional Python scrips were created in order to get the face images and to store them in an organised manner:
- **face_cropper**: Parses the *captures_xyz.json* files located in the **Dataset Data** folder and stores the 2D Bounding Box coordinates and dimensions of the head GameObject of each image. Based on those values, the original images are cropped in order to retain only the heads.
- **generate_dataset_folders**: Creates 33 folders named *Person_x*, one for each individual human. For each person multiple subfolders named *y_z* are created, one for each combination of environment and lighting condition where:
  - **y** denotes the id of the environment.
  - **z** denotes the id of the lighting condition. 

# Important Notes
- When opening the project, if the default scene is empty, go to the *Scenes* folder and double-click on *MyScene.unity* in order to load the project's scene.
- If an environment is added to the project, it should be added as a child GameObject to the *Environments* parent GameObject.
- If a human is added to the project, it should be added as a child GameObject to the *Humans* parent GameObject.
- If a new *AnimationControler* is created, it should be added in the *Assets/Resources/MyAnimatorControllers* folder.

# Citation
 If you find this project useful, consider citing it using:
 ```
 @inproceedings{ActiveFace,
  title={ActiveFace: A Synthetic Active Perception Dataset for Face Recognition},
  author={Georgiadis, Charalampos and Passalis, Nikolaos and Nikolaidis, Nikos},
  booktitle={Proceedings of the IEEE 25th International Workshop on Multimedia Signal Processing},
  year={2023},
}
```
