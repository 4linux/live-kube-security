FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y golang-go
COPY app.go .

RUN CGO_ENABLED=0 go build app.go

FROM alpine:3.12.1

RUN chmod a-w /etc
RUN addgroup -S cksgroup && adduser -S cksuser -G cksgroup -h /home/cksuser

RUN rm -rf /bin/*

COPY --from=0 /app /home/cksuser

USER cksuser

CMD ["/home/cksuser/app"]
