FROM arm64v8/alpine

WORKDIR /opt/rancher
ENV PATH $PATH:/opt/rancher

RUN \
  apk add --update bash ca-certificates && \
  rm -rf /var/cache/apk/* && \
  wget -q -O /opt/rancher/giddyup https://github.com/kyamazawa/giddyup/releases/download/v0.18.0/giddyup-linux-arm64 && \
  chmod +x /opt/rancher/giddyup

RUN \
  wget -q -O - https://github.com/coreos/etcd/releases/download/v3.3.1/etcd-v3.3.1-linux-arm64.tar.gz | tar xzf - -C /tmp && \
  mv /tmp/etcd-*/etcd /opt/rancher/etcd && \
  mv /tmp/etcd-*/etcdctl /opt/rancher/etcdctl && \
  rm -rf /tmp/etcd-* && rm -f /etcd-*.tar.gz

ADD etcdwrapper run.sh disaster delete /opt/rancher/

ENTRYPOINT ["/opt/rancher/run.sh"]
CMD ["node"]
