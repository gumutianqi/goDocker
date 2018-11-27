# Version 2.0.0
# Data 2018-11-23
FROM weteam/java:8

LABEL maintainer="koo@weteam.me"

ENV APP_NAME="sentinel-dashboard"
ENV APP_VERSION="2.0.0" \
    APP_ENV="dev" \
    SENTINEL_DASHBOARD_SERVER="localhost:8849" \
    SENTINEL_LOG_DIR="/logs/${APP_NAME}" \
    SENTINEL_METRIC_FILE_SINGLE_SIZE="52428800" \
    SENTINEL_METRIC_FILE_TOTAL_COUNT="6" \
    JVM_LOG_HOME="/logs/${APP_NAME}" \
    JAVA_TIMEZONE="Asia/Shanghai" \
    JAVA_MEM_OPTS="-XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m -Xss256K -XX:SurvivorRatio=8 \
        -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap \
        -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:+CMSParallelRemarkEnabled \
        -XX:+ScavengeBeforeFullGC -XX:+CMSScavengeBeforeRemark" \
    JAVA_JVM_OPTS="-Xms128m -Xmx256m -Xmn64m"

ENV SENTINEL_OPTS="-Dserver.port=8849 \
        -Dproject.name=${APP_NAME} \
        -Dcsp.sentinel.dashboard.server=${SENTINEL_DASHBOARD_SERVER} \
        -Dcsp.sentinel.log.dir=${SENTINEL_LOG_DIR} \
        -Dcsp.sentinel.metric.file.single.size=${SENTINEL_METRIC_FILE_SINGLE_SIZE} \
        -Dcsp.sentinel.metric.file.total.count=${SENTINEL_METRIC_FILE_TOTAL_COUNT}" \
    JAVA_OPTS="-Djava.security.egd=file:/dev/./urandom \
        -Duser.timezone=$JAVA_TIMEZONE \
        -Djava.awt.headless=true \
        -Djava.net.preferIPv4Stack=true \
        -Xloggc:/logs/gc.log \
        -XX:GCLogFileSize=10M \
        -XX:NumberOfGCLogFiles=10 \
        -XX:+UseGCLogFileRotation \
        -XX:+PrintGCDateStamps \
        -XX:+PrintGCTimeStamps \
        -XX:+PrintGCDetails \
        -XX:+PrintGCApplicationStoppedTime \
        -XX:+DisableExplicitGC \
        -XX:+HeapDumpOnOutOfMemoryError \
        -XX:HeapDumpPath=/logs/heapdump.hprof "

VOLUME /logs

COPY sentinel-dashboard.jar ${APP_NAME}.jar

EXPOSE 8849

ENTRYPOINT exec java -server $JAVA_JVM_OPTS $JAVA_MEM_OPTS ${SENTINEL_OPTS}  $JAVA_OPTS -jar /${APP_NAME}.jar \
    --spring.profiles.active=$APP_ENV
