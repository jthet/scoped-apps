FROM jthet/pysep:latest

LABEL maintainer="Jackson Thetford"

RUN apt-get update --yes \
    && apt-get install -yq --no-install-recommends zlib1g-dev \
    && docker-clean

RUN cd /home/scoped \
    && git clone https://github.com/adjtomo/adjdocs \
    && git clone --branch devel https://github.com/adjtomo/seisflows \
    && git clone --branch devel https://github.com/adjtomo/pyatoa \
    && git clone --branch devel https://github.com/geodynamics/specfem2d \
    && git clone --branch devel --depth=1 https://github.com/geodynamics/specfem3d

# Copy the environment.yml file into the container and create the Conda environment
RUN cd /home/scoped/pyatoa \
    && conda env create -f environment.yml

# Activate the environment in subsequent commands
RUN echo "source activate pyatoa" > ~/.bashrc
ENV PATH /opt/conda/envs/pyatoa/bin:$PATH

RUN cd /home/scoped/seisflows \
    && conda install --file requirements.txt \
    && pip install -e . \
    && docker-clean

ADD scripts/clean_specfem2d_repo.sh /home/scoped/clean_specfem2d_repo.sh 
ADD scripts/clean_specfem3d_repo.sh /home/scoped/clean_specfem3d_repo.sh

RUN cd /home/scoped/specfem2d \
    && ./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi \
    # && make all \
    # && bash /home/scoped/clean_specfem2d_repo.sh \
    # && rm /home/scoped/clean_specfem2d_repo.sh \
    && docker-clean

RUN cd /home/scoped/specfem3d \
    && ./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi \
    # && make all \
    # && bash /home/scoped/clean_specfem3d_repo.sh \
    # && rm /home/scoped/clean_specfem3d_repo.sh \
    && docker-clean

COPY extras/startup-tacc.sh /usr/bin/
RUN chmod +x /usr/bin/startup-tacc.sh

ENTRYPOINT ["tini", "-s", "-g", "--", "/entry.sh", "/usr/bin/startup-tacc.sh"]