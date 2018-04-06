FROM debian:sid-slim

RUN apt-get update && apt-get -y dist-upgrade && apt-get install -y \
  ca-certificates \
  libxrender1 \
  libxtst6 \
  libxi6 \
  libgl1-mesa-dri \
  libgl1-mesa-glx \
  ca-certificates \
  chromium \
  libnss3-tools \
  vim \
  --no-install-recommends \
  && rm -rf /var/lib/apt/lists/*

# install burp
COPY files/burpsuite_pro*.sh /tmp/burp
RUN chmod +x /tmp/burp && /tmp/burp -q && rm /tmp/burp

# copy burp preferences
RUN mkdir -p /data/project
COPY files/java /root/.java
COPY project.json /data/project.json

# import burp ca certificate
COPY files/cacert.der /data/cacert.der
RUN mkdir -p $HOME/.pki/nssdb && \
  certutil -d $HOME/.pki/nssdb -N --empty-password && \
  certutil -d sql:$HOME/.pki/nssdb -A -t "C,," -n burp -i /data/cacert.der

# copy start script
COPY start.sh /data/start.sh
RUN chmod +x /data/start.sh

EXPOSE 8080

ENTRYPOINT [ "/bin/bash" ]
WORKDIR "/data/"