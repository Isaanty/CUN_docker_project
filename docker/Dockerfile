FROM debian:latest
RUN	apt -y update \
    && apt -y install curl \
    && curl -sL https://deb.nodesource.com/setup_18.x | bash - \
    && apt -y install nodejs \
    && apt -y install wget \
        build-essential \
        net-tools

RUN npm install -g pnpm

# Set the global bin directory for pnpm
ENV PNPM_HOME="/usr/local/pnpm"
RUN mkdir -p $PNPM_HOME
ENV PATH="/usr/local/pnpm:$PATH"

RUN pnpm install -g pm2

ENV TZ=America/Bogota
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone		
    
RUN mkdir -p /home/cun_repository_docker/ && touch /home/cun_repository_docker/
RUN chown -R root:root /home/cun_repository_docker/

WORKDIR /home/cun_repository_docker/

CMD pnpm install --force \
    && pm2 install pm2-logrotate \
    && pm2-runtime ./start.json --time 