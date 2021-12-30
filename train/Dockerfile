FROM iotai_infer_gpu:latest 

USER root 

# Add operating system packages 
ADD train-os-packages.txt ${TMP}/
RUN apt-get update && xargs -a ${TMP}/train-os-packages.txt apt-get install -y --no-install-recommends 

WORKDIR ${TMP}
RUN curl -o ${TMP}/code.deb -fSL https://go.microsoft.com/fwlink/?LinkID=760868 && \
   gdebi -n -q ${TMP}/code.deb && \
   wget --quiet https://dbeaver.io/files/dbeaver-ce_latest_amd64.deb -O ${TMP}/dbeaver.deb && \
   gdebi -n -q ${TMP}/dbeaver.deb && \
   rm ${TMP}/*.sh && \
   rm ${TMP}/*.deb


WORKDIR ${OPT}
ENV PYCHARM_VERSION=pycharm-community-2021.1
RUN wget --quiet https://download.jetbrains.com/python/${PYCHARM_VERSION}.tar.gz -O ${OPT}/pycharm-ce.tar.gz && \ 
    tar -xvzf ${OPT}/pycharm-ce.tar.gz && \
    ln -svf ${OPT}/${PYCHARM_VERSION}/bin/pycharm.sh /usr/local/bin/pycharm.sh && \
    wget --quiet https://download.pytorch.org/libtorch/nightly/cpu/libtorch-shared-with-deps-latest.zip -O ${OPT}/libtorch-shared-with-deps-latest.zip && \
    unzip ${OPT}/libtorch-shared-with-deps-latest.zip && \
    rm ${OPT}/*.gz  && \
    rm ${OPT}/*.zip

ADD launch_jupyter_notebook.sh /usr/local/bin
ENV DISPLAY=":0"
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

ADD train-environment-conda.yml ${TMP}/
RUN conda env update -f ${TMP}/train-environment-conda.yml
WORKDIR ${TMP}
RUN curl -sL https://deb.nodesource.com/setup_16.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh
RUN apt-get install -y nodejs
