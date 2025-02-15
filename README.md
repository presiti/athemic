# DataIgnite Athemic Project
## Project Structure
    - BOLTZMAN : Web Engine to control AI Module (classification, regression, statistics)
    - ENTROPY : data ingestion engine for BOLTMAN SYSTEM
    - AI Module : This project supply general machine learning algorithm
              Now you can use randomforest classification / regression / descriptive statistics

![](/features/archi.png)

BOLTZMAN Machine Learning
![](/features/BOLTZMAN.png)

ENTROPY Data Manager
![](/features/ENTROPY.png)

## 1. How to Run 
### Run without build process 
    This Project, each systems run on Docker

    1. Clone this repository
        git clone https://github.com/dataignitelab/athemic
        If you want to use sample data, you must clone this repository

    2. Network
        docker network create dataignite
    
    3. Run Storage Container 
            cd BOLTZMAN
            docker-compose --file docker-compose-storage.yaml up -d
	    	    
	
    4. Run from docker hub
            cd BOLTZMAN
            docker-compose --file docker-compose.yaml up -d
        
            Open
            http://localhost:8501/

             
     5. Run ML Container from docker hub
		A. Statistics
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name statistic dataignitelab/statistic:0.0.1
		
		B Randomforest Classification
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name randomforestclassifier dataignitelab/randomforestclassifier:0.0.1

		C Randomforest Regression
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name randomforestregression dataignitelab/randomforestregression:0.0.1
	
     6. Run ENTROPY DataEngine Container from docker hub
		cd ENTROPY
	    
		docker-compose --file docker-compose.yaml up -d
		open
		http://localhost:8502/

	
### Run with build process
    1. BOLTZMAN Machine Learning web engine
		A. Build
			i. image build
				cd BOLTZMAN/streamui/
				docker build --tag boltzman -f Dockerfile .
				
		B. Run from local image
				docker run -d -p 8501:8501 --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage -e mongo_host=mongodb -e mongo_user=dataignite -e mongo_passwd=dataignite -e auth_source=datastore --name boltzman boltzman
				
	2. ENTROPY Data Engine web engine
		A. Build
			i. image build
				cd ENTROPY
				docker build --tag entropy -f Dockerfile .

		B. Run from local image
				docker run -d -p 8501:8501 --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage -e mongo_host=mongodb -e mongo_user=dataignite -e mongo_passwd=dataignite -e auth_source=datastore --name entropy entropy
				

    3. Statistics
        A. image build
            cd algorithm_process/statistics
            docker build --tag statistic -f Dockerfile .
			
	    B. Run from local image
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name statistic statistic
			

    4. Randomforest Classification
        A. image build
            cd algorithm_process/classification/RandomForestClassifier
            docker build --tag randomforestclassifier -f Dockerfile .
			
	    B. Run from local image
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name randomforestclassifier randomforestclassifier			


    5. Randomforest Regression
        A. image build
            cd algorithm_process/regression/RandomForestRegression
            docker build --tag randomforestregression -f Dockerfile .
			
	    B. Run from local image
            docker run -d --network dataignite -e mqbroker=rabbitmq_disage -e minio_host=minio:9000 -e redis_host=redis_disage --name randomforestregression randomforestregression						
	
### Manual 
<a href="https://dataignite.notion.site/BOLTZMAN-bc707971d89f42e2aeccb31e1deadff0?pvs=4" target="_blank">BOLTZMAN Machine Learning web engine manual</a>

#### 
<a href="https://dataignite.notion.site/ENTROPY-8dac96c869db43fabf0eca97d685fcab?pvs=4" target="_blank">ENTROPY Data Engine web engine manual</a>

### Algorithm interface
<a href="https://dataignite.notion.site/Algorithm-Interface-8674cb944a6d4464b57b0dc3afb1953b?pvs=4" target="_blank">BOLTZMAN and Machine Learning Servie Interface</a>

### Communication
<a href="https://github.com/dataignitelab/athemic/issues" target="_blank">GitHub Issues: mainly for bug reports, new feature requests, question asking, etc. </a>




