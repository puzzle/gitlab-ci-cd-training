FROM alpine:latest

RUN apk add curl

#Download kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
RUN chmod +x kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

#Download helm
RUN curl -LO https://get.helm.sh/helm-v3.6.3-linux-amd64.tar.gz
RUN tar -zxvf helm-v3.6.3-linux-amd64.tar.gz
RUN mv linux-amd64/helm /usr/local/bin/helm
RUN chmod +x /usr/local/bin/helm