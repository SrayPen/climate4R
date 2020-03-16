FROM jupyter/base-notebook:latest

RUN conda install -c defaults -c r -c conda-forge -c santandermetgroup climate4r=1.1.0 "r-classInt>=0.4.1"

USER root 
RUN apt-get update && apt-get install -y xorg git && ln -s /bin/tar /bin/gtar && \
	R --vanilla -e 'install.packages(c("crayon", "pbdZMQ"), repos = "http://cran.rediris.es/")' && \
	R --vanilla -e 'library(devtools);install_github("IRkernel/repr")' && \
	R --vanilla -e 'library(devtools);install_github("IRkernel/IRdisplay")' && \
	R --vanilla -e 'library(devtools);install_github("IRkernel/IRkernel")' && \
	R --vanilla -e 'IRkernel::installspec(); IRkernel::installspec(user = FALSE)' && \
	chown -R jovyan:users /home/jovyan
USER $NB_USER

# $NB_USER not supported in chown, see https://github.com/moby/moby/issues/35018
COPY --chown=jovyan:users examples /home/$NB_USER/examples
