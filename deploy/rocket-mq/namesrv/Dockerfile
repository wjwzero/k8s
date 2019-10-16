# Start from a Java image.
FROM java:8

ARG version

# Rocketmq version
ENV ROCKETMQ_VERSION ${version}

# Rocketmq home
ENV ROCKETMQ_HOME  /opt/rocketmq-${ROCKETMQ_VERSION}

WORKDIR  ${ROCKETMQ_HOME}

RUN mkdir -p \
		/opt/logs \
		/opt/store

RUN curl https://dist.apache.org/repos/dist/release/rocketmq/${ROCKETMQ_VERSION}/rocketmq-all-${ROCKETMQ_VERSION}-bin-release.zip -o rocketmq.zip \
          && unzip rocketmq.zip \
          && mv rocketmq-all*/* . \
          && rmdir rocketmq-all*  \
          && rm rocketmq.zip


RUN chmod +x bin/mqnamesrv



run sed -i "s/4g/1g/g" bin/runserver.sh
run sed -i "s/2g/512m/g" bin/runserver.sh

CMD cd ${ROCKETMQ_HOME}/bin && export JAVA_OPT=" -Duser.home=/opt -Xmx1g -Xms1g -Xmn512m " && sh mqnamesrv


EXPOSE 9876
VOLUME /opt/logs \
		/opt/store
