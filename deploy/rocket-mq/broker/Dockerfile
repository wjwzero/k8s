# Start from a Java image.
FROM java:8

ARG version

# Rocketmq version
ENV ROCKETMQ_VERSION ${version}

# Rocketmq home
ENV ROCKETMQ_HOME  /opt/rocketmq-${ROCKETMQ_VERSION}

ENV NAMESERVER "rmqnamesrv.itms.cn:9876"

WORKDIR  ${ROCKETMQ_HOME}

RUN mkdir -p \
		/opt/logs \
	    /opt/store \
      /opt/conf
RUN curl https://dist.apache.org/repos/dist/release/rocketmq/${ROCKETMQ_VERSION}/rocketmq-all-${ROCKETMQ_VERSION}-bin-release.zip -o rocketmq.zip \
          && unzip rocketmq.zip \
          && mv rocketmq-all*/* . \
          && rmdir rocketmq-all*  \
          && rm rocketmq.zip


RUN chmod +x bin/mqbroker

RUN sed -i  "s/8g/512m/g" bin/runbroker.sh
run sed -i  "s/4g/256m/g" bin/runbroker.sh
run sed -i  "s/15g/512m/g" bin/runbroker.sh

CMD cd ${ROCKETMQ_HOME}/bin && export JAVA_OPT=" -Duser.home=/opt " && sh mqbroker -n ${NAMESERVER} -c /opt/conf/broker.properties


EXPOSE 10909 10911
VOLUME /opt/logs \
		/opt/store \
    /opt/conf
