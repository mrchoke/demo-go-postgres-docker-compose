FROM golang:1.18 AS build
WORKDIR /work
COPY go.mod .
RUN go mod tidy
COPY . .
ENV CGO_ENABLED=0
RUN go build -a -installsuffix cgo -o backend .


FROM alpine:3.16.0
RUN apk --no-cache add tzdata
COPY --from=build /work ./
CMD [ "./backend" ]
