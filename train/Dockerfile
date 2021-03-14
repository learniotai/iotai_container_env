FROM iotai_infer_gpu:latest 

USER root 

# ENV DEBIAN_FRONTEND=noninteractive 
# ENV DEBCONF_NONINTERACTIVE_SEEN=true
# ENV OPT=/opt 
# ENV CONDA_HOME=${OPT}/miniconda
# ENV TMP=/tmp

# Add operating system packages 
ADD train-os-packages.txt ${TMP}/
RUN apt-get update && xargs -a ${TMP}/train-os-packages.txt apt-get install -y --no-install-recommends 

WORKDIR ${TMP}
RUN curl -o ${TMP}/code.deb -fSL https://go.microsoft.com/fwlink/?LinkID=760868 && \
    gdebi -n -q ${TMP}/code.deb && \
    wget --quiet https://dbeaver.io/files/dbeaver-ce_latest_amd64.deb -O ${TMP}/dbeaver.deb && \
    gdebi -n -q ${TMP}/dbeaver.deb
     # && \
    # rm ${TMP}/*.sh && \
    # rm ${TMP}/*.deb
 # wget --quiet https://atom.io/download/deb -O ${TMP}/atom.deb && \ 
 #   dpkg -i ${TMP}/atom.deb && apt-get install -f && \


WORKDIR ${OPT}
RUN wget --quiet https://download.jetbrains.com/python/pycharm-community-2020.1.1.tar.gz?_ga=2.1894769.1984017565.1590319299-433175914.1590319299 -O ${OPT}/pycharm-ce.tar.gz && \ 
    tar -xvzf ${OPT}/pycharm-ce.tar.gz
    # && \
    # ln -svf ${OPT}/pycharm-community-2020.1.1/bin/pycharm.sh /usr/local/bin/pycharm.sh && \
    # wget --quiet https://download.pytorch.org/libtorch/nightly/cpu/libtorch-shared-with-deps-latest.zip -O ${OPT}/libtorch-shared-with-deps-latest.zip && \
    # unzip ${OPT}/libtorch-shared-with-deps-latest.zip && \
    # wget --quiet https://github.com/QIICR/dcmqi/releases/download/latest/dcmqi-1.2.2-linux-20200602-3efde87.tar.gz -O ${OPT}/dcmqi.tar.gz && \
    # tar -xvzf ${OPT}/dcmqi.tar.gz && \
    # ln -svf ${OPT}/dcmqi-1.2.2-linux-20200602-3efde87 ${OPT}/dcmqi && \
    # rm ${OPT}/*.gz
    # && \
    # rm ${OPT}/*.zip


# RUN npm install -g create-react-app
EXPOSE 8899
EXPOSE 5006
ADD launch_jupyter_notebook.sh /usr/local/bin
ENV DISPLAY=":0"

ADD train-environment-conda.yml ${TMP}/
RUN conda env update -f ${TMP}/train-environment-conda.yml

# RUN pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/cuda/10.0 nvidia-dali
RUN ln -svf ${OPT}/pycharm-community-2020.1.1/bin/pycharm.sh /usr/local/bin/pycharm.sh
# RUN ln -svf $CONDA_HOME/lib/libopenh264.so.2.1.1 $CONDA_HOME/lib/libopenh264.so.5

