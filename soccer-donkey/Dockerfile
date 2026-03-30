#
# Rserve R Server Dockerfile with DataSHIELD Soccer Donkey profile
#
# https://github.com/datashield/docker-rserver
#

# R 4.5.3, Rserver
FROM rocker/r-ver:4.5.3

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
# RUN R -q -e "install.packages('ps', 'devtools'))"
    R -q -e "install.packages(c('ps', 'devtools'))" && \
# RUN R -q -e "install.packages('remotes', 'arrow'))"
    R -q -e "install.packages(c('remotes', 'arrow'))" && \
# RUN R -q -e "update.packages()"
    R -q -e "update.packages()"

# Install BiocManager package

ENV BIOCMANAGER_VERSION="v1.30.27"
RUN installGithub.r "Bioconductor/BiocManager@${BIOCMANAGER_VERSION}" \
    && ln -s /usr/local/lib/R/site-library/littler/examples/installBioc.r /usr/local/bin/installBioc.r

# Install Platform R packages
ENV RSERVE_VERSION=master
ENV RESOURCER_VERSION=1.5.1

# Rserve
LABEL Rserve=${RSERVE_VERSION}
RUN installGithub.r "s-u/Rserve@${RSERVE_VERSION}"
# Install Resourcer package
LABEL resourcer=${RESOURCER_VERSION}
RUN installGithub.r "obiba/resourcer@${RESOURCER_VERSION}"

# Install Profile R packages

ENV DSMEDIATION_VERSION=0.0.3
ENV DSEXPOSOME_VERSION=2.0.9
ENV DSTIDYVERSE_VERSION=v1.1.1
ENV DSOMICS_VERSION=v1.0.19
ENV DSMTL_VERSION=0.9.9
ENV DSSURVIVAL_VERSION=v2.1.3
ENV DSBASE_VERSION=6.3.5

# dsMediation
LABEL dsMediation=${DSMEDIATION_VERSION}
RUN Rscript -e "remotes::install_github('datashield/dsMediation', ref = '$DSMEDIATION_VERSION', repos = c('https://cloud.r-project.org', 'https://cran.datashield.org'), upgrade = FALSE)"
# dsMTLBase
LABEL dsMTL=${DSMTL_VERSION}
RUN Rscript -e "remotes::install_github('transbioZI/dsMTLBase', ref = '$DSMTL_VERSION', dependencies = TRUE, upgrade = FALSE)"
# dsSurvival
LABEL dsMSurvival=${DSSURVIVAL_VERSION}
RUN Rscript -e "remotes::install_github('datashield/dsSurvival', ref = '$DSSURVIVAL_VERSION', dependencies = TRUE, upgrade = FALSE)"
# dsTidyverse
LABEL dsTidyverse=${DSTIDYVERSE_VERSION}
RUN Rscript -e "remotes::install_github('molgenis/ds-tidyverse', ref = '$DSTIDYVERSE_VERSION', dependencies = TRUE, upgrade = FALSE)"
# dsExposome
LABEL dsExposome=${DSEXPOSOME_VERSION}
RUN Rscript -e "BiocManager::install(c('bumphunter', 'missMethyl', 'rexposome'), update = FALSE, ask = FALSE)" \
    && Rscript -e "remotes::install_github('isglobal-brge/dsExposome', ref = '$DSEXPOSOME_VERSION', repos = c('https://cloud.r-project.org', 'https://cran.datashield.org'), upgrade = FALSE)"
# dsOmics
LABEL dsOmics=${DSOMICS_VERSION}
RUN Rscript -e "BiocManager::install(c('Biobase', 'SNPRelate', 'GENESIS', 'GWASTools', 'GenomicRanges', 'SummarizedExperiment', 'DESeq2', 'edgeR', 'MEAL'), update = FALSE, ask = FALSE)" \
    && Rscript -e "remotes::install_github('isglobal-brge/dsOmics', ref = '$DSOMICS_VERSION', repos = c('https://cloud.r-project.org', 'https://cran.datashield.org'), upgrade = FALSE)"
# dsBase
LABEL dsBase=${DSBASE_VERSION}
RUN Rscript -e "remotes::install_github('datashield/dsBase', ref = '$DSBASE_VERSION', dependencies = TRUE, upgrade = FALSE)"

# Startup the RServer
ENV RSERVE_DEBUG=FALSE
CMD ["R", "-e", "Rserve::Rserve(debug=FALSE, args='--vanilla --RS-set remote=enable --RS-set auth=disable --RS-set daemon=disable')"]
