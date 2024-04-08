## Target: Detect and compute the deforestation square in the satellite images.

<p align="justify">
  Today it is becoming increasingly important to realize how much living forest is being cut down. Forest biodiversity is an integral and very important part of our country and the planet. Forests play a key role in maintaining ecological balance and provide unique conditions for animals, plants, and microorganisms. They also perform important functions in water supply and climate change mitigation. However, despite all this, global deforestation is happening at a rate that exceeds resource renewal. This topic is relevant because understanding the scale helps to identify the problem and ways to solve it, such as preserving forest areas, restraining resource consumption growth, developing sustainable forest management methods, and creating public awareness of the ecological value of forests. The method developed in the work allows obtaining reliable data on the area of   deforested forest using open cartographic sources and Python programming language libraries.
</p>

<p align="left">
To achieve this goal, the following tasks were set: <br />
   • Search for deforested areas <br />
   • Save the images keeping particular map scale <br />
   • Select a training image <br />
   • Perform clustering of objects to create an array of labels <br />
   • Train a classification model with the training image and label array <br />
   • Evaluate the quality and time of the classifier <br />
   • Process the entire data set to compute deforested areas square <br />
</p>

<p align="justify">
The subject of research is satellite images of forest areas obtained from the cartographic service Yandex Maps by taking screenshots. All images contain the target object represents as sections of cleared forest.
</p>

### Location: 59.086135, 111.975826

![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5fba8d94-17d1-441e-9b45-d001f80f171b)

The created data set consists of 17 pictures 1200 х 800.

![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/013d0762-ea37-4342-82d2-190cc30b5b46)
>[!NOTE]
>Considering the following square computing, it is important to keep particular map scale during screenshotting.
>In this case it's 200 meters.

>![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/18d0cb7e-eadd-4e7f-9d2e-62192d3ca39d)
>
### Train data preparation
<p align="justify">
To start with, we need to make visual analysis of the data set and select one or two images where the features of target object are easily recognizable. 
</p>

### Data Clustering and labeling
<p align="justify">
Then the chosen images are being labeled, all pixels of background are marked as zeros and the target object's - as ones. In this case it is binary clustering. Clustering can be performed with different cluster number, it is important to pay attention on how it could affect the result. The Elbow method based on intrarcluster dispersion can be used to find the right cluster quantity. Here's an example of the Elbow method method plot and comparing different cluster quantity for our train pictures.
</p>

<img src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/495098a8-e208-410f-bdc2-bd6e6d9a089a" width="350" height="300">



<img src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5e6cc88b-d0d4-4435-a3fa-a1cab64e7209" width="450" height="300">


### Median filter
The clustering results may contain some imperfections. In our case this was solved by implementing cv2 median filter.
<img width="241" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/3894833a-5a08-4c9e-8c8e-bf7062c59e31">
<img width="241" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/d44d2f5a-ba37-4408-b4bf-3a0e8b01e9aa">

Alternatively binary clustering can be performed by threshold processing at HSV color space using cv2.inRange.
<img width="202" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5cd2843c-a209-4317-8c34-a5e9aa0f16a8">
<img width="387" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/09816599-0ab3-42e0-9fde-07fa1f98c984">

### Morphological transformations
<p align="justify">
In the next step the labeling was improved by morphological transformations. In particular by combination of dilation and erosion operations. This order is commonly interpreted as Closing operation. 
</p>

![out](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/9545e880-2875-4dfd-a9d2-8133e7603b5e)

### Learning Classifiers
<p align="justify">
One of the important targets here is to minimize time and computation resource consumption. Considering this, the following classifiers were selected to perform the task of detecting and labeling the target object:
</p>

<p align="left">
   • Gaussian Naive Bayes <br />
   • K Nearest Neighbors <br />
   • Multi-layer Perceptron <br />
</p>
The following evaluation metric scores were retrieved:
<p align="left">
<img width="500" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/357ff319-a100-41bb-be61-8bda1cc73d08">

Due to quite similar results, time consumption may be taken into consideration when choosing a classifier to compute the rest of the data set.
for learning:  
</p>
<p align="left">
<img width="400" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/341d0f1a-3ffe-46cb-a05f-331693fb948a">
</p>
for data set computing:
</p>
<p align="left">
<img width="400" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/02a955b8-6f59-4633-a217-8efbcdc6d5cc">
</p>

### Computing data set
Finally the whole data set was passed to the classifier. According to visual analysis of the results, MLP was chosen for final step.

### Result:
<p align="justify">
The results are represented as two pictures and deforested area square value. Picture one is the original image, number two represents the target areas. Such representation allows to evaluate visually the result of defining the target areas and increases the data trustworthiness. 
</p>

![out](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/0284d142-31b0-445f-948c-3df03e76288c)

### Comparing with other methods
In order to compare the algorithm with other means of square calculation, the same object was measured using Google maps.

<img width="326" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/1971b6ac-6f4e-42c0-a201-a29bfab573f4">
<img width="260" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/28e0e5d7-61aa-41ba-8838-dfb826a33ca7">
<img width="281" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/294b27a6-9f42-4b91-be52-6116ea034468">

This comparison confirms that the algorithm is quite accurate.

### Conclusion
<p align="justify">
The represented method works well for purpose of detecting and computing the deforestation square in the satellite images. Also it can be used for another data sets with different target objects, the necessary instruments are provided for fast adjustment. Having a data set of 10-20 pictures it's enough to have one or two training images. It takes insignificant time to learn the classifier.
</p>


