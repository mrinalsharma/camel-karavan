FROM docker.io/jbangdev/jbang-action

ENV CAMEL_VERSION=3.21.0-SNAPSHOT
ENV KARAVAN="/karavan"
ENV JBANG_REPO="$KARAVAN/.jbang/cache/.m2"
ENV JBANG_DIR="$KARAVAN/.jbang"
ENV KAMELETS_DIR="$KARAVAN/kamelets"
ENV CODE_DIR="$KARAVAN/code"
ENV CAMEL_DIR="$KARAVAN/camel"

RUN mkdir -p $KARAVAN \
    && mkdir -p $JBANG_REPO \
    && mkdir -p $CODE_DIR \
    && mkdir -p $KAMELETS_DIR \
    && mkdir -p $CAMEL_DIR \
    && mkdir -p $CAMEL_DIR/.camel \
    && chown -R 1001 $KARAVAN \
    && chmod -R "g+rwX" $KARAVAN 

USER 1001
RUN jbang trust add https://github.com/apache/camel \
    && jbang app install camel@apache/camel

EXPOSE 8080
WORKDIR $KARAVAN

ENTRYPOINT jbang -Duser.home=$CAMEL_DIR -Dcamel.jbang.version=$CAMEL_VERSION camel@apache/camel run --source-dir=$CODE_DIR --console --local-kamelet-dir=$KAMELETS_DIR 