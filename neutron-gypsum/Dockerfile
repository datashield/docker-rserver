#
# Rserver R Server Dockerfile with DataSHIELD Neutron Gypsum profile
#
# https://github.com/datashield/docker-rserver-neutron-gypsum
#

FROM datashield/rserver-neutron:latest

# Install BiocManager dependencies
ENV BIOCMANAGER_VERSION="v1.30.25"
RUN installGithub.r "Bioconductor/BiocManager@${BIOCMANAGER_VERSION}"
RUN ln -s /usr/local/lib/R/site-library/littler/examples/installBioc.r /usr/local/bin/installBioc.r

# Install new R packages
# dsMediation
ENV DSMEDIATION_VERSION=0.0.3
RUN installGithub.r "datashield/dsMediation@${DSMEDIATION_VERSION}"
# dsMTLBase
ENV DSMTL_VERSION=0.9.9
RUN installGithub.r "transbioZI/dsMTLBase@${DSMTL_VERSION}"
# dsSurvival
ENV DSSURVIVAL_VERSION=v2.1.3
RUN installGithub.r "datashield/dsSurvival@${DSSURVIVAL_VERSION}"
# dsTidyverse
ENV DSTIDYVERSE_VERSION=v1.0.4
RUN installGithub.r "molgenis/ds-tidyverse@${DSTIDYVERSE_VERSION}"
# dsExposome
ENV DSEXPOSOME_VERSION=2.0.9
RUN installBioc.r 'bumphunter'
RUN installBioc.r 'missMethyl'
RUN installBioc.r 'rexposome'
RUN installGithub.r "isglobal-brge/dsExposome@${DSEXPOSOME_VERSION}"
# dsOmics
ENV DSOMICS_VERSION=v1.0.18-2
RUN installBioc.r 'Biobase'
RUN installBioc.r 'SNPRelate'
RUN installBioc.r 'GENESIS'
RUN installBioc.r 'GWASTools'
RUN installBioc.r 'GenomicRanges'
RUN installBioc.r 'SummarizedExperiment'
RUN installBioc.r 'DESeq2'
RUN installBioc.r 'edgeR'
RUN installBioc.r 'MEAL'
RUN installGithub.r "isglobal-brge/dsOmics@${DSOMICS_VERSION}"
# dsBase
ENV DSBASE_VERSION=6.3.1
RUN installGithub.r "datashield/dsBase@${DSBASE_VERSION}"
