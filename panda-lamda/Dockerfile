#
# Rserver R Server Dockerfile with DataSHIELD Panda Lamda profile
#
# https://github.com/datashield/docker-rserver-panda-lamda
#

# R 4.5.2
FROM rocker/r-ver:4.5.2

# Update of packages
# RUN apt-get update -y
RUN apt-get update -y && \
# RUN apt-get install littler -y
    apt-get install littler -y && \
# RUN apt-get install cmake -y
    apt-get install cmake -y && \
# RUN R -q -e "install.packages('remotes', 'arrow'))"
    R -q -e "install.packages(c('remotes', 'arrow'))" && \
# RUN R -q -e "update.packages()"
    R -q -e "update.packages()"

# Install new R packages
# dsBase
ENV RSERVER_VERSION=master
LABEL Rserve=${RSERVER_VERSION}
RUN installGithub.r "StuartWheater/Rserve@${RSERVER_VERSION}"
# RUN install2.r --error "https://registry.molgenis.org/repository/r-hosted/src/contrib/MolgenisRserve_${RSERVER_VERSION}.tar.gz" --repos NULL

# Install Resourcer package
ENV RESOURCER_VERSION=1.4.0
LABEL resourcer=${RESOURCER_VERSION}
RUN installGithub.r "obiba/resourcer@${RESOURCER_VERSION}"

# Install new R packages
# dsBase
ENV DSBASE_VERSION=6.3.4
LABEL dsBase=${DSBASE_VERSION}
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"

# Startup the RServer
ENV RSERVE_DEBUG=TRUE
CMD R -e "MolgenisRserve::Rserve(debug=${RSERVE_DEBUG}, args='--vanilla --RS-set remote=enable --RS-set auth=disable --RS-set daemon=disable')"
