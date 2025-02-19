# DeepSelectNet requires Python 3.5 >= version <= 3.8
FROM --platform=linux/amd64 python:3.8 AS build

WORKDIR /app

RUN apt-get update
RUN apt-get install -y --no-install-recommends build-essential gcc

RUN git clone https://github.com/AnjanaSenanayake/DeepSelectNet

RUN pip3 install -r ./DeepSelectNet/requirements.txt

# Workaround "generated code is out of date and must be regenerated with protoc >= 3.19.0" error in trainer.py
RUN pip install protobuf==3.20.*

# Workaround "module 'numpy' has no attribute 'object'" error in trainer.py
RUN pip install numpy==1.19.5

# Workaround "Matplotlib requires numpy>=1.20; you have 1.19.5" error in trainer.py
RUN pip install matplotlib==3.6

# Workaround Pyslow "ValueError: numpy.ndarray size changed, may indicate binary incompatibility." error in inference.py
# (Rebuild pyslow5 using older numpy)
RUN pip uninstall pyslow5 -y
RUN pip install pyslow5 --no-binary pyslow5

RUN useradd -m user

ENV PATH=$PATH:/app/DeepSelectNet/scripts:/app/DeepSelectNet/support

RUN chmod +x /app/DeepSelectNet/scripts/inference.py
RUN chmod +x /app/DeepSelectNet/scripts/preprocessor.py
RUN chmod +x /app/DeepSelectNet/scripts/trainer.py
RUN sed -i '1i#!/usr/bin/env python3' /app/DeepSelectNet/scripts/inference.py
RUN sed -i '1i#!/usr/bin/env python3' /app/DeepSelectNet/scripts/preprocessor.py
RUN sed -i '1i#!/usr/bin/env python3' /app/DeepSelectNet/scripts/trainer.py

USER user

WORKDIR /workspace
