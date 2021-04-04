
Source: [Utilizing the Kaggle Python Docker Container image](https://github.com/stefan-bergstein/Utilizing-the-Kaggle-Python-Docker-Container-image)

# 0. Create data folder
Docker container will map this folder.
>`mkdir data`

# 1. Run the container based on `kaggle/python`image:
```bash
docker run --restart always -v ${PWD}/data:/tmp/working -w=/tmp/working -p 8800:8888 --name kaggle \
   -d kaggle/python jupyter notebook --no-browser --ip="0.0.0.0" --notebook-dir=/tmp/working --allow-root
```

# 2. Access the log to get the http token for accessing Jupyter:
>`docker logs kaggle`

CURRENT TOKEN:
> 40119a2f87c125c72f7603945ca6b1561e0fb9ed45929234

For example:
>`http://640b804c545b:8888/?token=8e28bf1201d83f3f43521fba4b0cf382107781a4955ecf93&token=8e28bf1201d83f3f43521fba4b0cf382107781a4955ecf93`

- Replace 640b804c545b with `localhost`or the IP of the machine where Kaggle image is running.
- Replace port 8888 (container) by 8800 (host)

Everything can be done with the bash script `./kaggle.sh`

## Using the Jupyter token
In the http line above:
>`token=40119a2f87c125c72f7603945ca6b1561e0fb9ed45929234`

### Don't know why the next procedure does not set the password
So if you want to set a password for accessing Jupyter, after launching the container go to:
`http://localhost:8888`

Enter your token and change the password.

# 3. SSH into the container
`docker exec -it kaggle bash`

# 4. ANOMALY DETECTION ANALYSIS
## S1.A [`./`] Z-score for anomaly detection
Source tutorial: [Z-score for anomaly detection](https://towardsdatascience.com/z-score-for-anomaly-detection-d98b0006f510)

**DATASET**: Gearbox fault raw signals `./input/gearbox-fault-diagnosis/`

> **Notebook:** `Zscore.GearboxFault-anomaly_detection.ipynb`

## [WITH ERRORS, SOLVED IN S1.D] S1.B [`./MultivariateGaussian`] Multivariate Gaussian Analisis
Source tutorial: [Wondering how to build an anomaly detection model?](https://towardsdatascience.com/wondering-how-to-build-an-anomaly-detection-model-87d28e50309)

- Gists here https://gist.github.com/abhishek-Kumar009 
- Dataset from [Github](https://github.com/abhishek-Kumar009/Machine-Learning/tree/master/AnomalyDetectionScratch)

**DATASET**: Servers' throughput (mb/s) & latency (ms)
- `anomalyData.mat` & `anomalyDataTest.mat`

> **Notebook:** `MGD.server-anomaly_detection.ipynb`

## S1.C Mixture Gaussian models
Source tutorial: [Anomaly Detection in Python with Gaussian Mixture Models](https://towardsdatascience.com/understanding-anomaly-detection-in-python-using-gaussian-mixture-model-e26e5d06094b)

We can see that Multivariate Gaussian performs not quite good.

- Same dataset as above

> **Notebook:** `GaussianMixtureModels.server-anomaly_detection.ipynb`

## S1.D Mixture Gaussian models
Source tutorial: [Anomaly Detection in Python with Gaussian Mixture Models](https://towardsdatascience.com/understanding-anomaly-detection-in-python-using-gaussian-mixture-model-e26e5d06094b)

- Same dataset as above

> **Notebook:** `GMM.server-anomaly_detection.ipynb`: GMM testing against validation set

## S2.A Detecting outliers using KNN algorithm: Gearbox dataset
Source tutorial: [gearbox dataset requires to compute standard deviation for equal size samples of acceleration signal](https://www.geeksforgeeks.org/machine-learning-for-anomaly-detection/)
 - Using Python `pyod` packages for KNN analysis
> **Notebook with dummy data:** `pyodKNN.DummyDataset-anomaly_detection.ipynb`

**DATASET**: Gearbox fault gearbox of standard deviation of equal size samples of acceleration signal `./input/gearbox-fault-diagnosis/stdev/`

> This dataset is computed here:
- `dataset.GearboxFault-stdev.ipynb`

> **Notebook:** `pyodKNN.GearboxFault-anomaly_detection.ipynb`

## S2.B: NASA Bearing Dataset: EDA & PCA analysis
Using dataset of experiment 2. Raw data is proccessed in Kaggle:
 - (private) https://www.kaggle.com/brjapon/nasa-bearing-dataset-merging

> **Notebook:** `NASAbearingDataset-EDA_PCA.ipynb`

## S2.C Detecting outliers using KNN algorithm: NASA bearing dataset
- Applying the same analysis in S2.A
- Same dataset as in S2.B
- Analysis is based on the PCA dimensionality reduction computed in S2.B

> **Notebook:** `NASAbearingDataset-pyodKNN.ipynb`