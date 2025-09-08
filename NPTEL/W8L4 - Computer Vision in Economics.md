This lecture explores how **computer vision** is applied to economics, a field that uses algorithms to enable computers to analyze visual data like images. The core challenge is representing an image in a way that allows a computer to "understand" its contents and draw meaningful conclusions.

---

### Understanding Computer Vision

* **Image Representation:** A digital image is a **matrix** of numbers. For a color image, it's a 3D matrix ($m \times n \times l$), where $m$ is the height, $n$ is the width, and $l$ (usually 3) represents the Red, Green, and Blue (RGB) color channels. Each pixel's value is an integer, typically from 0 to 255, representing the intensity of that color channel at that location.
* **Computer Vision Tasks:**
    * **Image Classification:** Assigning a class label (e.g., "dog," "cat") to an entire image. The challenge lies in **intra-class variation** (different dogs can look very different) and **inter-class similarity** (a wolf can look like a dog).
    * **Object Detection:** Finding specific objects within an image and drawing a **bounding box** around them. This requires not only classifying objects but also localizing them and handling different sizes and orientations.
    * **Image Segmentation:** Dividing an image into different regions based on the objects they contain. This is a form of **pixel clustering**, where pixels of the same object are grouped together.

---

### The Challenge of Feature Representation

To perform these tasks, a computer needs a meaningful way to represent an image.

* **Raw Pixels:** Simply using raw pixel values as features is problematic because it loses **spatial information** (neighboring pixels are no longer next to each other when the image is flattened into a vector) and is sensitive to noise and irrelevant details.
* **Hand-Engineered Features:** For a long time, researchers used **filters** to extract features like edges, corners, and textures. However, this was a difficult and manual process because a researcher had to guess and design the right filters for the task.
* **Deep Learning Revolution:** The advent of **convolutional neural networks (CNNs)** revolutionized computer vision by solving this problem. Instead of being manually designed, the filters (or masks) are **learned automatically** during the training process. A CNN's multiple layers create hierarchical "feature maps" that represent the image in increasingly abstract ways, from basic edges in early layers to complex object parts in later layers. This allows the network to learn the most discriminative features for a given task. 

---

### Computer Vision for Economics

Economists and researchers are now using computer vision to analyze visual data to measure economic activity and well-being. This is particularly useful in regions where traditional data sources like surveys are scarce or unreliable.

* **Proxy Variables:** Since images often don't contain direct economic data, computer vision is used to find **proxy variables**—visual indicators that correlate with economic activity.
    * **Nighttime Lights:** Satellite images of the Earth at night show bright spots where there's a lot of economic activity (cities, factories) and dark spots where there's less (rural areas, forests). The intensity of light serves as a powerful proxy for a region's **Gross Domestic Product (GDP)**.
    * **High-Resolution Imagery:** Images from Google Street View or satellites can be used to count or detect objects that indicate development, such as:
        * **Cars and Buildings:** The density and quality of cars and buildings can be an indicator of wealth.
        * **Roads and Infrastructure:** The presence and quality of roads can indicate a region's development level.
        * **Vegetation and Agricultural Land:** Analyzing vegetation can provide insights into a region's agricultural output.

* **Case Studies:**
    * **"Are Nighttime Lights Good Proxies...?"** This paper validates the strong correlation between satellite-measured nighttime light intensity and regional GDP in Colombia, even at a local municipal level.
    * **"Poverty from Space..."** Researchers used high-resolution satellite imagery of Sri Lanka to estimate poverty rates. They trained a model to detect objects like cars, buildings, and roads, and used these counts as features to predict economic well-being, finding that they were good indicators.
    * **"Transfer Learning..."** This work addresses a key challenge: the lack of ground-truth data. Researchers trained models on regions where survey data was available and used a technique called **transfer learning** to apply the trained model to other regions where ground-truth data was not available. This makes the models highly scalable and useful for creating "poverty maps" for vast areas like the entire African continent.

These studies demonstrate that computer vision, particularly deep learning models, can be a valuable tool for economists to bypass traditional data collection methods and get new insights into economic development and inequality.