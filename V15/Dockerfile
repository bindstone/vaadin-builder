FROM ubuntu:18.04
MAINTAINER bindstone
USER root

# JDK
RUN apt-get update
RUN apt-get install software-properties-common -y
RUN apt-get install wget -y
#RUN wget https://download.java.net/java/GA/jdk14/076bab302c7b4508975440c56f6cc26a/36/GPL/openjdk-14_linux-x64_bin.tar.gz
RUN wget https://download.java.net/java/GA/jdk13/5b8a42f3905b406298b72d750b6919f6/33/GPL/openjdk-13_linux-x64_bin.tar.gz
RUN tar -xzvf *.tar.gz
ENV JAVA_VERSION="jdk-13"
RUN mv $JAVA_VERSION /usr/local/share/
RUN rm *.tar.gz
ENV JAVA_HOME=/usr/local/share/$JAVA_VERSION
ENV PATH="$JAVA_HOME/bin:$PATH"

# MAVEN
ENV MAVEN_VERSION 3.5.0
ENV MAVEN_ROOT /var/lib/maven
ENV MAVEN_HOME $MAVEN_ROOT/apache-maven-$MAVEN_VERSION
ENV MAVEN_OPTS -Xms256m -Xmx512m
RUN echo "# Installing Maven " && echo ${MAVEN_VERSION} && \
    wget --no-verbose -O /tmp/apache-maven-$MAVEN_VERSION.tar.gz \
    http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    mkdir -p $MAVEN_ROOT && \
    tar xzf /tmp/apache-maven-$MAVEN_VERSION.tar.gz -C $MAVEN_ROOT && \
    ln -s $MAVEN_HOME/bin/mvn /usr/local/bin && \
    rm -f /tmp/apache-maven-$MAVEN_VERSION.tar.gz

# NODE JS & NPM
RUN apt-get install --yes curl && \
    curl --silent --location https://deb.nodesource.com/setup_13.x | bash - && \
    apt-get install --yes nodejs && \
    apt-get install --yes build-essential

RUN npm install npm@latest -g

# VALIDATE
RUN java --version
RUN mvn --version
RUN node --version
RUN npm --version
