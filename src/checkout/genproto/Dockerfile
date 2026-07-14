# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

FROM docker.io/library/golang:1.27rc2-alpine@sha256:7870fdc211100210e7380f487953c4188fcbeac99646a56926a973161a3eedcd

WORKDIR /build

RUN apk add --no-cache protobuf-dev

COPY ./src/checkout/go.mod go.mod
COPY ./src/checkout/go.sum go.sum

RUN go install tool
