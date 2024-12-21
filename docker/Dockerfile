# Imagem base com OpenJDK e Python
FROM openjdk:8-jdk-slim

# Definindo variáveis de ambiente para o Spark
ENV SPARK_VERSION=3.5.0
ENV HADOOP_VERSION=3
ENV SPARK_HOME=/opt/spark
ENV PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH
ENV PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
ENV PYSPARK_PYTHON=python3
ENV PYSPARK_DRIVER_PYTHON=python3

# Instalando dependências
RUN apt-get update && apt-get install -y curl wget tar python3 python3-pip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Baixando e instalando o Apache Spark
RUN wget https://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz && \
    tar -xvzf spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz && \
    mv spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION $SPARK_HOME && \
    rm spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz

# Instalando bibliotecas Python necessárias
RUN pip install pyspark==3.5.0 pandas numpy

# Instalando Jupyter
RUN pip install jupyterlab

# Expondo a porta do Jupyter
EXPOSE 8888


# Expondo portas
EXPOSE 4040 9080 7077 8888

# Entrando no shell do Spark por padrão
# CMD ["/bin/bash", "jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
