#
# Rserver R Server Dockerfile with DataSHIELD Soccer Donkey Permissive profile
#
# https://github.com/datashield/docker-rserver
#

# R 4.5.3, Rserver
FROM datashield/rserver_soccer-donkey:1.0.0

ENV DSBASE_VERSION=v6.3.5-permissive

# Update of packages
RUN apt-get update -y
RUN apt-get upgrade -y
RUN R -q -e "update.packages()"

# Install new R packages
# dsBase
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"
