# syntax = docker/dockerfile:experimental
ARG SPRYKER_PARENT_IMAGE

FROM ${SPRYKER_PARENT_IMAGE} AS assets-builder

USER spryker

COPY package.json package-lock.json ${srcRoot}/
COPY frontend ${srcRoot}/frontend
COPY tsconfig.json ${srcRoot}/
COPY config/Yves ${srcRoot}/config/Yves

ARG SPRYKER_ASSETS_MODE='development'
ENV SPRYKER_ASSETS_MODE=${SPRYKER_ASSETS_MODE}
ARG SPRYKER_PIPELINE
ENV SPRYKER_PIPELINE=${SPRYKER_PIPELINE}

RUN --mount=type=cache,id=npm,sharing=locked,target=/root/.npm \
    echo "BUILD HASH: ${SPRYKER_BUILD_HASH}" \
    && echo "MODE: ${SPRYKER_ASSETS_MODE}" \
    && vendor/bin/install -r ${SPRYKER_PIPELINE} -s build-static -s build-static-${SPRYKER_ASSETS_MODE} -vvv

# TODO add tar builder