FROM jupyter/pyspark-notebook

ADD requirements.txt /build/requirements.txt

WORKDIR /build/

USER root

RUN  apt-get update && apt-get install -y apt-utils lsb-release && apt-get clean all
RUN  apt-get -y install curl ca-certificates gnupg 
RUN  curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
RUN  sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
RUN  sudo apt-get update
RUN  sudo apt-get -y install postgresql
RUN  sudo apt -y install libpq-dev python3-dev
RUN  cd /usr/local/spark/jars
RUN  wget https://jdbc.postgresql.org/download/postgresql-42.2.18.jar
RUN  conda create -y --name torch1.8.1-cudacu102
ENV  PATH /opt/conda/envs/mro_env/bin:$PATH
RUN  /bin/bash -c "source activate torch1.8.1-cudacu102"
# RUN  conda activate torch1.8.1-cudacu102
RUN  pip install -U pip
RUN  pip install -r requirements.txt
RUN  pip install torch torchvision torchaudio
RUN  pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.8.0+cu102.html
RUN  pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.8.0+cu102.html
RUN  pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.8.0+cu102.html
RUN  pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.8.0+cu102.html
RUN  pip install torch-geometric

WORKDIR /mnt/
