FROM rwightman/pytorch:latest

RUN conda install --name pytorch-py35 pandas scikit-image scikit-learn jupyter

RUN mkdir /workspace/notebook

COPY jupyter_notebook_config.py /root/.jupyter/

COPY entrypoint.sh /

COPY run_jupyter.sh /

EXPOSE 8888

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/run_jupyter.sh", "--allow-root"]

