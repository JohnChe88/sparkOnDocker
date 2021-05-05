

# Building Spark on Docker Image
Let us do a simple example of Spark on Docker. In this package, we are creating a small Spark REST API using Flask library and then hosting it on a Docker container. The REST API can be accessed via the HTTP endpoint. The package for the sample docker image is available on my git hub at the location <Location>

## Prerequisite:
Any Operating system. Python 3.x installed. Install the docker and expose the daemon on TCP. 

## Dockerfile
The Dockerfile uses Base image variants of python and OpenJDK. The version of PySpark used is 3.1.x. All the dependency libraries are mentioned in the requirements.txt
For cloud platforms like AWS, Azure, and GCP they may have their own version of OpenJDK, Linux operating system, and it will be maintained and upgraded by the platform. Here, in our example, I am using an OpenJDK image from the docker hub( keeping it cloud-agnostic). 

## Spark application on Flask
The python script Main.py, is using the Spark framework to read sample data from a dataset downloaded from data.gov and converting it into HTML format. The Flask framework is used APIfy the Spark application. The Flask library is hosting the application on port 5000(by default). The HTTP request can be Posted to view the generated dataframe in HTML format on the browser or OS commands

## Requirements.txt
The requirements file is used to install the dependencies like flask, pandas, and HTML libraries. The Flask is used to host the spark function as a REST API, pandas to convert the spark dataframe to HTML and HTML libraries to display on a web page(when accessed via localhost:5000).]

## Docker Image
A Docker image is a combination of a file system and parameters needed to run an application as containers such as code, config file, the environment variable, and run time. It comprises multiple layers and used to execute code on Docker container. Once the image is deployed on the Docker environment it can be executed as a Docker container. The docker images are immutable but can be copied and shared which makes it an excellent candidate for testing new applications and configurations. The docker image starts with a base image consisting of dependent libraries, OS, and executable code. More you configure the docker file the base image is cached and a new layer is formed which helps in fast set up and execution.
Once the package is downloaded from GitHub into a folder using the command prompt log in to the folder and run the below commands.
docker build -t sparkRestDocker:latest .
The above command creates a docker image from the docker file package. This image will have all dependencies installed and required files copied.

## Docker container
The Docker container is a unit of packaged code and its dependencies that runs platform or environment agnostic. It is generated using the docker run command from a docker image.

docker run -d -p 5000:5000 sparkRestDocker
docker container ls

Once the docker run command is used to run the images then the docker container is created and the port is exposed on 5000. Check if the container is running using the container ls command. Use the browser or curl command to access the REST API end point.
http://localhost:5000/sparkdf

## Access Docker and REST spark API function
Confirm the docker container running the command docker container ls. The docker container can be accessed from the below link on your localhost at port 5000 using any browser or curl commands.
The below link accesses the spark method in main.py and displays the dataframe in HTML format. Data using is downloaded from data.gov.
Browser - http://127.0.0.1:5000/readdf?location=/main/COVID-19_Hospital_Capacity.csv
Or
curl http://127.0.0.1:5000/readdf?location=/main/COVID-19_Hospital_Capacity.csv
For each cloud platform, the images might vary so please refer to the guidelines in the documentation. Use the cloud platform images so that all the OS and security updates will be automatic. The cloud platform has its own version of the Kubernetes cluster and Container registry repository. Upload the image to the Container repository and host it on the Kubernetes cluster.
