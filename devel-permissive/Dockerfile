#
# R Server Dockerfile with DataSHIELD Margin Gypsum Permissive profile
#
# https://github.com/datashield/docker-rock
#

# R 4.5.2, RServe
FROM datashield/rserver-devel:latest

ENV DSBASE_VERSION=v6.3.4-permissive

ENV ROCK_LIB=/var/lib/rock/R/library

# Update of packages
RUN apt-get update -y
RUN apt-get upgrade -y
RUN R -q -e "update.packages()"

# Install new R packages
# dsBase
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"
