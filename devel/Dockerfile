#
# Rserver R Server Dockerfile with DataSHIELD Devel profile
#
# https://github.com/datashield/docker-rserver-devel
#

# R 4.5.1
FROM rocker/r-ver:4.5.1

# Update of packages
# RUN apt-get update -y
RUN apt-get update -y && \
# RUN apt-get install littler -y
    apt-get install littler -y && \
# RUN apt-get install cmake -y
    apt-get install cmake -y && \
# RUN apt-get install cmake -y
    apt-get install git -y && \
# RUN apt-get upgrade -y
    apt-get upgrade -y && \
# RUN R -q -e "install.packages('ps', 'devtools'))" **** Check "devtools" needed ****
    R -q -e "install.packages(c('ps', 'devtools'))" && \
# RUN R -q -e "install.packages('remotes', 'arrow'))"
    R -q -e "install.packages(c('remotes', 'arrow'))" && \
# RUN R -q -e "update.packages()"
    R -q -e "update.packages()"

# Install new R packages
# Rserve
ENV RSERVE_VERSION=master
LABEL Rserve=${RSERVE_VERSION}
RUN installGithub.r "s-u/Rserve@${RSERVE_VERSION}"
# RUN install2.r --error "https://registry.molgenis.org/repository/r-hosted/src/contrib/MolgenisRserve_${RSERVER_VERSION}.tar.gz" --repos NULL

# Install Resourcer package
ENV RESOURCER_VERSION=1.5.0
LABEL resourcer=${RESOURCER_VERSION}
RUN installGithub.r "obiba/resourcer@${RESOURCER_VERSION}"

# Install new R packages
# dsBase
ENV DSBASE_VERSION=6.3.4
LABEL dsBase=${DSBASE_VERSION}
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"

# Install new R packages
# dsTidyverse
ENV DSTIDYVERSE_VERSION=v1.1.1
LABEL dsTidyverse=${DSTIDYVERSE_VERSION}
RUN installGithub.r "molgenis/ds-tidyverse@${DSTIDYVERSE_VERSION}"

# Startup the RServer
ENV RSERVE_DEBUG=TRUE
CMD ["R", "-e", "Rserve::Rserve(debug=TRUE, args='--vanilla --RS-set remote=enable --RS-set auth=disable --RS-set daemon=disable')"]
