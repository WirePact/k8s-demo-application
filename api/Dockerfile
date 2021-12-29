FROM golang:1.16-alpine as build

WORKDIR /app

ENV GOOS=linux \
    GOARCH=amd64 \
    USER=appuser \
    UID=1000

RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "${UID}" \
    "${USER}"

COPY go.mod go.sum ./
RUN go mod download && go mod verify

COPY . .

RUN go build -ldflags="-w -s" -o /go/bin/app


FROM alpine

ARG COMMIT_SHA

LABEL org.opencontainers.image.source="https://github.com/WirePact/k8s-demo-application" \
    org.opencontainers.image.authors="cbuehler@rootd.ch" \
    org.opencontainers.image.url="https://github.com/WirePact/k8s-demo-application" \
    org.opencontainers.image.documentation="https://github.com/WirePact/k8s-demo-application/blob/main/README.md" \
    org.opencontainers.image.source="https://github.com/WirePact/k8s-demo-application/blob/main/api/Dockerfile" \
    org.opencontainers.image.revision="${COMMIT_SHA}" \
    org.opencontainers.image.licenses="Apache-2.0" \
    org.opencontainers.image.title="WirePact Kubernetes Demo Api" \
    org.opencontainers.image.description="Demo Basic Auth Api for WirePact in Kubernetes."

ENV GIN_MODE=release

COPY --from=build /etc/passwd /etc/group /etc/
COPY --from=build /go/bin/app /go/bin/app

USER appuser:appuser

ENTRYPOINT ["/go/bin/app"]
