FROM rwightman/pytorch:v0.1.12

ENV PATH /opt/conda/envs/pytorch-py35/bin:$PATH

# This is missing from the v0.1.12 branch official Dockerfile
WORKDIR /opt/pytorch
RUN git clone https://github.com/pytorch/vision.git && cd vision && pip install -v .

WORKDIR /workspace

RUN conda install --name pytorch-py35 -c pandas scikit-image scikit-learn jupyter

RUN mkdir /workspace/notebook

COPY jupyter_notebook_config.py /root/.jupyter/

COPY entrypoint.sh /

COPY run_jupyter.sh /

EXPOSE 8888

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/run_jupyter.sh", "--allow-root"]

