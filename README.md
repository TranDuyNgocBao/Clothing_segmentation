# **Using Detectron2 for segmentation**
* **B1**: run from begin to line [9] (you can run plot segmented images to check the dataset) 
* **B2**: in title **Detectron**, pip install libraries needed to use detectron2
* **B3**: some lines of code to plot images that need to change link to read images from dataset saved on your devices
* **B4**: run every lines until line [29] then stop
* **B5**: depending on size of your input dataset, customize train and val set that suit to yours
* **B6**: from line [29], we divide our model to be trained by 3 metrics FPN, DC5 and C4.
* **B7**: in training code, you can change some parameters like batch-sized, iteration (minimum = 1000 to get good results),...
* **B8**: Get results and Evaluation at the end of the code. 
