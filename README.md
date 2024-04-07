## Target: Detect and compute the deforestation square in the satellite images.

<p align="justify">
  Today it is becoming increasingly important to realize how much living forest is being cut down. Forest biodiversity is an integral and very important part of our country and the planet. Forests play a key role in maintaining ecological balance and provide unique conditions for animals, plants, and microorganisms. They also perform important functions in water supply and climate change mitigation. However, despite all this, global deforestation is happening at a rate that exceeds resource renewal. This topic is relevant because understanding the scale helps to identify the problem and ways to solve it, such as preserving forest areas, restraining resource consumption growth, developing sustainable forest management methods, and creating public awareness of the ecological value of forests. The method developed in the work allows obtaining reliable data on the area of   deforested forest using open cartographic sources and Python programming language libraries.
</p>

<p align="left">
To achieve this goal, the following tasks were set: <br />
   • Search for areas with deforested plots <br />
   • Save images of the plots with the appropriate scale <br />
   • Select a training image <br />
   • Perform clustering of objects in it to create an array of annotations <br />
   • Pass the image and annotation array data for training the classification model <br />
   • Evaluate the quality and time of the classifier's operation <br />
   • Process the entire dataset and obtain data on the area <br />
</p>

The subject of research is satellite images of forest areas obtained from the cartographic service Yandex Maps by taking a screenshots. All images contain the target object representes as sections of cleared forest.

### Location: 59.086135, 111.975826

![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5fba8d94-17d1-441e-9b45-d001f80f171b)

The created data set consists of 17 pictures 1200 х 800.

![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/013d0762-ea37-4342-82d2-190cc30b5b46)
>[!NOTE]
>Considering the following square computing, it is important to keep particular map scale during screenshoting.
>In this case it's 200 meters.

>![image](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/18d0cb7e-eadd-4e7f-9d2e-62192d3ca39d)
>
### Train data preparation
To start with, we need to make visual analisys of the data set and select one or two images where the features of target object are easily recognazible. 

### Data Clustering and labeling
Then the chosen images are being labled, all pixels of background are marked as zeros and the target object's - as ones. In this case it is binary clusterisation.
Clustriastion can be performed with different cluster number, it is important to pay attention on how ot could affect the result.
The Elbow method based on intrarclaster disperion can be used to find the right cluster quantity.
Here's an example of the Elbow method method plot and comparing different cluster quantity for our train pictures.

<img src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/495098a8-e208-410f-bdc2-bd6e6d9a089a" width="350" height="300">



<img src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5e6cc88b-d0d4-4435-a3fa-a1cab64e7209" width="450" height="300">


### Median filter
The clusterisation results may contain some imperfections. In our case this was solved by implementing cv2 median filter.
<img width="241" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/3894833a-5a08-4c9e-8c8e-bf7062c59e31">
<img width="241" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/d44d2f5a-ba37-4408-b4bf-3a0e8b01e9aa">

Alternatively binary custerisation can be performed by threshold processing at HSV color space using cv2.inRange.
<img width="202" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/5cd2843c-a209-4317-8c34-a5e9aa0f16a8">
<img width="387" alt="изображение" src="https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/09816599-0ab3-42e0-9fde-07fa1f98c984">

### Morphological transformations
In the next step the labeling was improved by morphological transformations. In particular by combination of dilation and erosion operations. This order is commonly interpreted as Closing operation. 

![out](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/9545e880-2875-4dfd-a9d2-8133e7603b5e)

### Learning Classificators
One of the important targets here is to minimaze time and computation resource consumption. Considering this, the following classificators were selected to perform the task of detecting and labeling the target object:
<p align="left">
   • Search for areas with deforested plots <br />
   • Save images of the plots with the appropriate scale <br />
   • Select a training image <br />
   • Perform clustering of objects in it to create an array of annotations <br />
</p>




## Result:
![out](https://github.com/Andrudewt/Computing-deforestation-square-in-satellite-images-using-computer-vision-and-machine-learning/assets/137271592/0284d142-31b0-445f-948c-3df03e76288c)
