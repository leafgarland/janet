FROM alpine:3.12 as alpine-dev
RUN apk add --no-cache gcc musl-dev make git

FROM alpine-dev as build
WORKDIR /build
COPY . .
RUN make PREFIX=/app -j
RUN make test
RUN make PREFIX=/app install

FROM alpine-dev as dev
COPY --from=build /app /app
ENV PATH="/app/bin:$PATH"
WORKDIR /app
CMD ["ash"] 

FROM alpine as core
COPY --from=build /app/ /app/
ENV PATH="/app/bin:$PATH"
WORKDIR /app
CMD ["janet"] 
