FROM vladohor/spark-driver


# Install Jupyter and Data Science libraries
USER root
RUN ln -sv /usr/bin/pip3 /usr/bin/pip \
        && pip install numpy pandas
RUN pip install notedown plotly seaborn matplotlib
RUN pip install bokeh xlrd yellowbrick
RUN pip install scikit-learn scikit-image
RUN pip install scipy
RUN pip install jupyterlab s3contents \
        && mkdir -p /home/public && chmod 777 /home/public
RUN pip install py4j \
        && ln -s /opt/spark/python/pyspark /usr/local/lib/python3.7/dist-packages/pyspark \
        && ln -s /opt/spark/python/pylintrc /usr/local/lib/python3.7/dist-packages/pylintrc

# Install Jupyter Spark extension
RUN pip install jupyter-spark \
        && jupyter serverextension enable --py jupyter_spark \
        && jupyter nbextension install --py jupyter_spark \
        && jupyter nbextension enable --py jupyter_spark \
        && jupyter nbextension enable --py widgetsnbextension

# Configure Jupyter User
ARG NB_USER="jovyan"
ARG NB_UID="1000"
ARG NB_GROUP="analytics"
ARG NB_GID="777"
RUN groupadd -g $NB_GID $NB_GROUP \
        && useradd -m -s /bin/bash -N -u $NB_UID -g $NB_GID $NB_USER \
        && mkdir -p /home/$NB_USER/work \
        && mkdir -p /home/$NB_USER/.jupyter \
        && chown -R $NB_USER:$NB_GROUP /home/$NB_USER


# Configure Working Directory
USER $NB_USER
WORKDIR /home/$NB_USER/work
