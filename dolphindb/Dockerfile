FROM ubuntu:22.04

RUN apt-get update
RUN apt-get install unzip -y && \
    apt install curl -y && \
    apt install unzip -y && \
    DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata && \
    apt-get install wget

WORKDIR /opt/ddb
RUN curl https://www.dolphindb.com/downloads/DolphinDB_Linux64_V1.20.5.zip --output ddb.zip && \
    unzip ddb.zip && \
    chmod 755 /opt/ddb/server/dolphindb

RUN echo "" >> /opt/ddb/server/dolphindb.cfg && \
    echo "newValuePartitionPolicy=add" >> /opt/ddb/server/dolphindb.cfg && \
    echo "persistenceDir=dbcache" >> /opt/ddb/server/dolphindb.cfg && \
    echo "subPort=8808" >> /opt/ddb/server/dolphindb.cfg && \
    echo "maxPubConnections=1280" >> /opt/ddb/server/dolphindb.cfg && \
    echo "localExecutors=2" >> /opt/ddb/server/dolphindb.cfg && \
    echo "maxConnections=1000" >> /opt/ddb/server/dolphindb.cfg && \
    echo "maxSubQueueDepth=1000000" >> /opt/ddb/server/dolphindb.cfg && \
    echo "subExecutors=2" >> /opt/ddb/server/dolphindb.cfg && \
    echo "dataSync=0" >> /opt/ddb/server/dolphindb.cfg && \
    # echo "startup=/opt/ddb/server/startup.dos" >> /opt/ddb/server/dolphindb.cfg && \
    echo "maxPartitionNumPerQuery=100000" >> /opt/ddb/server/dolphindb.cfg

RUN wget https://www.dolphindb.com/downloads/dolphindb_lic.zip --no-check-certificate -O ddb.lic.zip &&\
    unzip -o ddb.lic.zip && \
    cp dolphindb.lic server

WORKDIR /opt/ddb/server
RUN echo "./dolphindb -console 0 >> dolphindb.log" >> cmd && chmod 755 cmd


CMD ["/bin/bash", "/opt/ddb/server/cmd"]