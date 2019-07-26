FROM python:slim-stretch as making_wheels
ENV NVIDIA_VISIBLE_DEVICES=all

RUN apt-get update && \
    apt-get install -y gcc && \
    rm -rf /var/lib/apt/lists/*

COPY ./requirements.txt ./gpustat/
RUN pip install -r   ./gpustat/requirements.txt

#------------------------------------------------------------------------
FROM python:slim-stretch
ENV NVIDIA_VISIBLE_DEVICES=all

# we take the wheels we compiled in the previous image
COPY --from=making_wheels /root/.cache/pip/wheels /root/.cache/pip/wheels

COPY ./requirements.txt ./gpustat/
RUN pip install -r ./gpustat/requirements.txt

COPY ./ ./gpustat
RUN pip install ./gpustat

ENTRYPOINT ["gpustat"]
