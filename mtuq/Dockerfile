FROM ghcr.io/seisscoped/mtuq@sha256:4733f4b768d506f5f56f8e1639384786ebb9b2714d44cf8baaafa5a377ece20c AS old-mtuq

FROM jthet/container-base:mtuq

LABEL maintainer="Jackson Thetford"

COPY --from=old-mtuq /home/scoped/ /home/scoped/
COPY --from=old-mtuq /opt/conda/ /opt/conda/


RUN cd /home/scoped/mtuq \
    && pip install -e . \
    && bash ./data/examples/unpack.bash\
    && docker-clean

COPY extras/startup-tacc.sh /usr/bin/
RUN chmod +x /usr/bin/startup-tacc.sh

ENTRYPOINT ["tini", "-s", "-g", "--", "/entry.sh", "/usr/bin/startup-tacc.sh"]