FROM kalilinux/kali-linux-docker

# tools from kali repo
RUN apt-get update && \
  apt-get -y dist-upgrade && \
  apt-get -y install \
  --no-install-recommends \
  zsh \
  net-tools \
  ssh \
  screen \
  aptitude \
  less \
  proxychains \
  metasploit-framework \
  netcat-traditional \
  socat \
  ncat \
  telnet \
  tftp \
  whois \
  host \
  traceroute \
  smbclient \
  tcpdump \
  masscan \
  nmap \
  amap \
  dirb \
  gobuster \
  wfuzz \
  sqlmap \
  wpscan \
  john \
  hashid \
  build-essential \
  libssl-dev \
  libffi-dev \
  python-dev \
  python-pip \
  python-setuptools \
  ldapscripts \
  unzip \
  vim \
  openjdk-8-jdk \
  python-requests \
  ipcalc \
  wordlists \
  whatweb \ 
  onesixtyone \
  snmp \
  snmpcheck \
  crackmapexec \
  file \
  python3.7 \
  python3.7-dev \
  python3-pip
# additional tools
RUN cd /tmp \
  && wget -q https://github.com/caffix/amass/releases/download/v1.5.1/amass_1.5.1_linux_amd64.zip \
  && cd /opt && git clone https://github.com/IOActive/jdwp-shellifier.git \
  && cd /opt && git clone https://github.com/CoreSecurity/impacket.git && cd impacket \
  && pip install . \
RUN cd /opt && \
  git clone https://github.com/byt3bl33d3r/SILENTTRINITY && \
  cd SILENTTRINITY/Server && \
  python3.7 -m pip install -r requirements.txt \
RUN cd /opt && wget -q https://github.com/matthiaskaiser/jmet/releases/download/0.1.0/jmet-0.1.0-all.jar \
  && wget -q https://jitpack.io/com/github/frohoff/ysoserial/master-SNAPSHOT/ysoserial-master-SNAPSHOT.jar
RUN pip install ldap3 dnspython ldapdomaindump

# make all directories
RUN mkdir -p /root/.msf4 /root/.ssh

# config files
COPY proxychains.conf /etc/proxychains.conf
COPY screenrc /root/.screenrc
COPY zshrc /root/.zshrc
COPY aliases /root/.aliases
COPY msfconsole.rc /root/.msf4

RUN echo "IPQoS lowdelay" > /root/.ssh/config

ENTRYPOINT ["/usr/bin/zsh", "-c", "screen && exit"]
WORKDIR "/data"
