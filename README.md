
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
## 4.1 Multivariate Gaussian Analisis
[Wondering how to build an anomaly detection model?](https://towardsdatascience.com/wondering-how-to-build-an-anomaly-detection-model-87d28e50309)

- Gists here https://gist.github.com/abhishek-Kumar009 
- Dataset from [Github](https://github.com/abhishek-Kumar009/Machine-Learning/tree/master/AnomalyDetectionScratch)

## 4.2 Detecting outliers using KNN algorithm
Based on [this tutorial](https://www.geeksforgeeks.org/machine-learning-for-anomaly-detection/)
 - Using Python `pyod`packages for KNN analysis