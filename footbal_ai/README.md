# Object Detection, Tracking and Clustering on Computer Vision for Football
This project aims at developing a small project capable of capturing the movement of each player and ball in a football game.
![image](https://github.com/user-attachments/assets/cdcab277-79e2-482c-9419-45e7673ab82a)

Proposed Architecture:

1. The raw video is received and splitted into frames
   
2. Object detector: finds each player, goalkepeers, refereers and the ball

    a. Tracking: detection for all classes except the ball receives a unique tracking id and is then tracked
    
   b. Embedding analysis: divide the players in 2 teams (Youmap, KMeans)
    
**Prep Up:**

The original dataset was obtained from Kaggle (https://www.kaggle.com/competitions/dfl-bundesliga-data-shootout).

The dataset was then splitted into frames and through Roboflow it was then properlly labeled (https://universe.roboflow.com/roboflow-jvuqo/football-players-detection-3zvbc).

* A second dataset related to this one is that of keypoint detector which is aimed at the footbal field itself (https://universe.roboflow.com/roboflow-jvuqo/football-field-detection-f07vi)


**Needed API:**

In order to run this project it is a must to have the Roboflow APIs configured.

Open your Roboflow Settings page. Click Copy. This will place your private key in the clipboard.
In Colab, go to the left pane and click on Secrets (🔑). Store Roboflow API Key under the name ROBOFLOW_API_KEY.

-----------------------
## 1. Training Object Detection

The training of the object detection happened on Google Collab with help of Roboflow services. Different YOLOV models were tested and the final results are:
![image](https://github.com/user-attachments/assets/4b1a1d9d-3e74-46eb-b260-6a947b3e7d82)

The model is capable of detecting and tracking objects and segment them into different classes (ball, players and referee)

![image](https://github.com/user-attachments/assets/522e35c0-3c82-4e5b-838e-a35d3864fc15)


## 2. Clusterizing Players into Teams

![image](https://github.com/user-attachments/assets/2b319cbc-7ba1-4bed-b9c0-b0f23dc16707)

How to create training data for the model? Detect players on different frames and crop them out.

CLIP is an algorithm of Image Embedding which looks for similar images. Embeddings captures the semantic meaning of an image such as lightning, and look for images that have similar characteristicas. SigLIP is the choice.

After detecting the players, SigLIP will analyze each player and place them in an embedding vector.

UMAP is applied to reduce the dimensions into a 3D space.

KMeans will divide players into two clusters.
