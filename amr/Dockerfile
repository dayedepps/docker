FROM centos:7 as amrbuild
#FROM ubuntu:17.10

ARG VERSION

USER root
WORKDIR /root/

#RUN apt-get -y -m update && apt-get install -y build-essential wget
#RUN wget ftp://ftp.ncbi.nlm.nih.gov/pub/slottad/amr/fam.tab
RUN yum -y groupinstall 'Development Tools'

COPY src src

WORKDIR src
RUN make

FROM centos:7
#FROM ubuntu:17.10

COPY VERSION .

USER root
WORKDIR /root
COPY --from=amrbuild /root/src/amr_report /usr/bin
COPY --from=amrbuild /root/fam.tab /

CMD ["/bin/bash"]
