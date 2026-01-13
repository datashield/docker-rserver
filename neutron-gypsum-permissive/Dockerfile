#
# Rock R Server Dockerfile with DataSHIELD Margin Gypsum Permissive profile
#
# https://github.com/datashield/docker-rock
#

# R 4.5.0, Rock 2.1.4
FROM datashield/rserver-neutron-gypsum:latest

ENV DSBASE_VERSION=v6.3.1-permissive

ENV ROCK_LIB=/var/lib/rock/R/library

# Update of packages
RUN apt-get update -y
RUN apt-get upgrade -y
RUN R -q -e "update.packages()"

# Install new R packages
# dsBase
# RUN install2.r --error "https://registry.molgenis.org/repository/r-hosted/src/contrib/MolgenisRserve_${RSERVER_VERSION}.tar.gz" --repos NULL
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"
