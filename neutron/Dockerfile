#
# Rserver R Server Dockerfile with DataSHIELD Neutron profile
#
# https://github.com/datashield/docker-rserver-neutron
#

# R 4.4.3
FROM rocker/r-ver:4.4.3

# Update of packages
RUN apt-get update -y
# RUN apt-get upgrade -y
RUN apt-get install cmake -y
# RUN R -q -e "update.packages()"

# Install system libraries

RUN apt-get install zlib1g-dev libssl-dev libcurl4-openssl-dev -y

# RUN apt-get install -qq libxml2-dev libcurl4-openssl-dev libssl-dev libgsl-dev libgit2-dev -y
# RUN apt-get install -qq libharfbuzz-dev libfribidi-dev libmagick++-dev -y

# Install R packages
RUN install2.r --error RANN stringr lme4 dplyr reshape2 polycor gamlss gamlss.dist --repos "https://cloud.r-project.org/"
RUN install2.r --error httr DescTools remotes childsds --repos "https://cloud.r-project.org/"
RUN install2.r --error haven mitml mice --repos "https://cloud.r-project.org/"

# Install dsBase package
ENV DSBASE_VERSION="6.3.1"
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"

# Install new R packages
# dsBase
ENV RSERVER_VERSION="0.1.2"
RUN install2.r --error "https://registry.molgenis.org/repository/r-hosted/src/contrib/MolgenisRserve_${RSERVER_VERSION}.tar.gz" --repos NULL

# Startup the RServer
CMD R -e "MolgenisRserve::Rserve(debug=${DEBUG}, args='--vanilla --RS-set remote=enable --RS-set auth=disable --RS-set daemon=disable')"
