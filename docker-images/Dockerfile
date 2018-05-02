FROM ubuntu

#
RUN apt-get -y update && apt-get install -y --no-install-recommends apt-utils && apt-get -y install software-properties-common && add-apt-repository ppa:webupd8team/java && apt-get install -y oracle-java8-installer

#
#CMD ["bash"]
CMD ["/bin/bash"]
