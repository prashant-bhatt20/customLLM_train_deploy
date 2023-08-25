FROM ubuntu:20.04
FROM pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime
MAINTAINER prashant.bhatt@lntinfotech.com
WORKDIR /app
COPY . .
COPY example.env .env
# COPY models /app
# COPY db /app
# COPY constants.py /app
# COPY my_req.txt /app
# COPY requirements.txt /app

RUN apt update && apt upgrade --yes

RUN DEBIAN_FRONTEND='noninteractive' apt install wget build-essential libncursesw5-dev libssl-dev \
libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev --yes 

RUN apt install software-properties-common --yes
RUN apt update
RUN add-apt-repository ppa:deadsnakes/ppa
RUN  apt install python3.11 --yes
RUN  apt-get install python3.11
#RUN  update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 1
#RUN  update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11
#RUN  update-alternatives --config python3
RUN  apt-get install --reinstall python3-distutils --yes
#RUN  apt-get install --reinstall  python3-apt4
RUN  apt-get install python3.11-distutils --yes
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.11
RUN  apt install build-essential
RUN  apt-get install manpages-dev --yes
RUN  apt-get install libpcap-dev libpq-dev --yes
# RUN python3 -m venv /opt/venv
# #RUN ./opt/venv/bin/activate
# # Enable venv
# ENV PATH="/opt/venv/bin:$PATH"

RUN pip install --upgrade pip
RUN pip install cuda-python
RUN pip install torch==2.0.1
#RUN pip install -r my_req.txt
RUN pip3 install torch torchvision torchaudio 
RUN pip install -r requirements.txt

# RUN cd /app/models
# RUN wget https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin
# RUN cd ..
#RUN mv ggml-gpt4all-j-v1.3-groovy.bin /app/models

RUN export CUDA_HOME=/usr/local/cuda
EXPOSE 5000
EXPOSE 6000
EXPOSE 8000
EXPOSE 8501
HEALTHCHECK CMD curl --fail http://localhost:8501/_stcore/health
ENV CUDA_VISIBLE_DEVICES=="1"
#RUN python ingest.py
ENTRYPOINT ["streamlit", "run", "app.py","--server.port=8501", "--server.address=0.0.0.0","--server.fileWatcherType=none"]
#ENTRYPOINT ["streamlit", "run", "app.py"]