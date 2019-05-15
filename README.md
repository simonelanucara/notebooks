## Planet Interactive Guides

[![Join the chat at https://gitter.im/planetlabs/notebooks](https://badges.gitter.im/planetlabs/notebooks.svg)](https://gitter.im/planetlabs/notebooks?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

In this repository, you'll find a collection of [Jupyter notebooks](http://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html) from the software developers, data scientists, and developer advocates at [Planet](https://www.planet.com/). These interactive, open-source (APLv2) guides are designed to help you explore Planet data, work with our APIs and tools, and learn how to extract information from our massive archive of high-cadence satellite imagery. We hope these guides will inspire you to ask interesting questions of Planet data. Need help? Find a bug? Please [file an issue](https://github.com/planetlabs/notebooks/issues/new) and we'll get back to you.

### The basics: search, activate, download	
* [Explore the Planet Data API with Python](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/data-api-tutorials/planet_data_api_introduction.ipynb)
* [Search, activate, and download imagery with the Planet Python Client](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/data-api-tutorials/planet_cli_introduction.ipynb)
* [Planet API reference](https://docs.planet.com/v1/reference)

### Process Planet data
* [Create a mosaic from multiple PlanetScope scenes](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/mosaicing/basic_compositing_demo.ipynb)
* [Calculate a vegetation index from 4-band satellite imagery](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/ndvi/ndvi_planetscope.ipynb)
* [Convert PlanetScope metadata from radiance to reflectance](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/toar/toar_planetscope.ipynb)
* [Visualize and convert a UDM to a binary mask](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/udm/udm.ipynb)

### Analyze and visualize Planet data
* [Detect, count, and visualize ships in Planet imagery](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/ship-detector/01_ship_detector.ipynb)
* [Python examples for remote sensing](https://github.com/kscottz/PythonFromSpace)
* [Pixel-by-pixel comparison of PlanetScope and Landsat Scenes](https://github.com/planetlabs/notebooks/blob/master/jupyter-notebooks/landsat-ps-comparison/landsat-ps-comparison.ipynb)

Soon we hope to add notebooks from the researchers, technologists, geographers, and entrepreneurs who are already using Planet data to ask interesting and innovative questions about our changing Earth. If you're working with our imagery and have a notebook (or just an idea for a notebook) that you'd like to share, please [file an issue](https://github.com/planetlabs/notebooks/issues) and let us know.

## Install and use these notebooks

### System Prerequisites
* [Docker](https://store.docker.com/search?type=edition&offering=community)
* [Planet Account](https://www.planet.com/explorer/?signup=1)
* [Planet API Key](https://www.planet.com/account/#/)

### Clone the repo:
```bash
git clone https://github.com/planetlabs/notebooks.git
cd notebooks
```

## Run Planet Notebooks in Docker
Planet Notebooks relies on a complex stack of technologies that are not always easy to install and properly 
configure. To ease this complexity we provide a docker container for running the notebook on docker compatible 
systems. To install docker on your system please see docker's [documentation](https://docs.docker.com/engine/installation/)
for your operating system.

### Build the Docker image
First you must build the docker image. Note, this only has to be done the first time you use it. After checking out the
this repository, you run:
```bash
cd planet-notebook-docker
docker build --rm -t planet-notebooks .
cd ..
```

This will build and install the Docker image on your system, making it available to run. This may take some 
time (between 10 and 20 minutes) depending on your network connection.

### Run the container
To run the container (after building it), add your Planet API key below and issue the following command from the git repository root directory:
```bash
docker run -it --rm -p 8888:8888 -v $PWD:/home/jovyan/work -e PL_API_KEY='[YOUR-API-KEY]' planet-notebooks
```
```bash
RUN THE CONTAINER AND MAP TO host directory agr10/planet_test_data
docker run -it --rm -p 8888:8888 -v /home/agr10/planet_test_data:/home/jovyan/work -e PL_API_KEY='[YOUR-API-KEY]' planet-notebooks
```
```bash
RUN THE CONTAINER AND MAP TO host directory agr10/planet_test_data AND ADD SUDO PRIVILEGES
docker run -it --rm -p 8888:8888 -v /home/agr10/planet_test_data:/home/jovyan/work -e GRANT_SUDO=yes PL_API_KEY='[YOUR-API-KEY]' planet-notebooks
```
This does several things:  

1. Maps the docker container's ```8888``` port to your system's ```8888``` port.  This makes the 
container available to your host systems web browser.

1. Maps a host system path ```$PWD``` to the docker containers working  directory.
This ensures that the notebooks you create, edit, and save are available on your host system under the
`jupyter-notebooks` sub-directory and are not *destroyed* when the you exit the container.
This also allows for running tests in the `tests` sub-directory.

1. Starts in an interactive terminal and is accessible through http://localhost:8888.

1. Sets an environment variable with your unique Planet API key for authenticating against the API.

1. Include the ```--rm``` option to clean up the notebook after you exit the process.

### Open Jupyter notebooks
Once the Docker container is running, the CLI output will display a URL that you will use to access Jupyter notebooks
with your browser.
```
http://localhost:8888/?token=<UNIQUE-TOKEN>
```

NOTE: This security token will change every time you start your Docker container.
