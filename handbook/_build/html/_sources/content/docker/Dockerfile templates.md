# Dockerfile templates

#docker #DockerFile #DataScience #template #setup #CodeSnippet

```python
FROM image-name
WORKDIR "dir-to-start"
```

## Container for python project

`Dockerfile`

```docker
FROM python:3.8.7

# creating an environment variable that holds the project directory
ENV PYTHONPATH="/workspace"
WORKDIR "${PYTHONPATH}"

# install python dependencies
RUN pip install pipenv
COPY Pipfile .
COPY Pipfile.lock .
RUN pipenv install --system --deploy --ignore-pipfile 
CMD ["pipenv", "shell"]
```

Script to create and start the container:

```bash
export NAME="my-project"
docker build -f Dockerfile -t $NAME .
docker run -it -d -v $PWD:/workspace --name=$NAME $NAME
```

Example `Pipfile.lock` with:

- pandas
- matplotlib
- numpy
- sklearn
- seaborn
- scipy
- jupyterlab

## Container for data science with Jupyter Lab

`Dockerfile`

```docker
FROM python:3.8.7

# creating an environment variable that holds the project directory
ENV PYTHONPATH="/workspace"
WORKDIR "${PYTHONPATH}"

COPY requirements.txt requirements.txt

# installing the necessary dependencies for the operation of the project
# RUN sudo apt-get update 
RUN pip install jupyterlab numpy pandas sklearn matplotlib seaborn
RUN pip install -r requirements.txt 
RUN echo "alias jp=\"jupyter lab --no-browser --allow-root --ip=0.0.0.0\""  >> ~/.bashrc

# comment this to turn off autostart of jupyter lab
CMD ["jupyter", "lab", "--no-browser", "--allow-root", "--ip=0.0.0.0"]
```

Script to create and start container:

```bash
export NAME="name-place-holder"
docker build -t $NAME -f Dockerfile .
docker stop $NAME
docker rm $NAME
docker run -it -p 8888-9000:8888-9000 -v $PWD:/work --name=$NAME $NAME
```


```docker
FROM python:3.8.7

# creating an environment variable that holds the project directory
ENV PYTHONPATH="/workspace"
WORKDIR "${PYTHONPATH}"

COPY requirements.txt requirements.txt

# installing the necessary dependencies for the operation of the project
# RUN sudo apt-get update 
RUN pip install jupyterlab numpy pandas sklearn matplotlib seaborn
RUN pip install -r requirements.txt 
RUN echo "alias jp=\"jupyter lab --no-browser --allow-root --ip=0.0.0.0\""  >> ~/.bashrc

# comment this to turn off autostart of jupyter lab
CMD ["jupyter", "lab", "--no-browser", "--allow-root", "--ip=0.0.0.0"]
```

```docker
FROM python:3.8.7 AS base

# creating an environment variable that holds the project directory
ENV PYTHONPATH="/workspace"
WORKDIR "${PYTHONPATH}"

# other environment variables
ENV DATADIR="/data"

# install python dependencies
COPY Pipfile .
COPY Pipfile.lock .
RUN python -m pipenv install --system --deploy --ignore-pipfile --dev

# Copying project files to the container

```