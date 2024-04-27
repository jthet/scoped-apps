FROM jthet/container-base:latest
## This is meant for TACC's Tapis

LABEL maintainer="Jackson Thetford"

RUN mkdir -p /home/scoped
WORKDIR /home/scoped/

# Clone the repository
RUN cd /home/scoped \
    && git clone https://github.com/adjtomo/pysep.git

# Create the conda environment and install packages
### Gives user command line tool -> https://pysep.readthedocs.io/en/latest/pysep.html 
RUN conda create -n pysep cartopy -y \
    && echo "source activate pysep" > ~/.bashrc \
    && /bin/bash -c "source activate pysep" 

RUN conda install -n pysep cartopy -y
RUN pip install pysep-adjtomo

# Clean up any unnecessary files and packages
RUN docker-clean

ENV TERM=xterm-256color

COPY extras/startup-tacc.sh /usr/bin/
RUN chmod +x /usr/bin/startup-tacc.sh

ENTRYPOINT ["tini", "-s", "-g", "--", "/entry.sh", "/usr/bin/startup-tacc.sh"]
