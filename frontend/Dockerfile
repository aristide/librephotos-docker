FROM node:20-slim as builder

RUN apt-get update && apt-get install -y git
RUN npm config set fetch-retry-maxtimeout 60000

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
ENV CLI_WIDTH 80
RUN git clone https://github.com/LibrePhotos/librephotos-frontend /usr/src/app
RUN npm install --legacy-peer-deps
RUN npm run postinstall
RUN npm run build

FROM halverneus/static-file-server
ENV PORT 3000
EXPOSE 3000

COPY --from=builder /usr/src/app/dist /web

ENTRYPOINT ["/serve"]
CMD []
