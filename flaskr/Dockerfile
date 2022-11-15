# syntax=docker/dockerfile:1.4
FROM --platform=$BUILDPLATFORM python:3.10-bullseye AS builder

WORKDIR /flaskr

COPY requirements.txt /flaskr
RUN --mount=type=cache,target=/root/.cache/pip \
    pip3 install -r requirements.txt

COPY . /flaskr

ENTRYPOINT ["python3"]
CMD ["flask --app flaskr"]

FROM builder as dev-envs

RUN <<EOF
apt update
apt add git
EOF

RUN <<EOF
addgroup -S docker
adduser -S --shell /bin/bash --ingroup docker vscode
EOF
# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /
