FROM nginxinc/nginx-unprivileged:alpine3.18-slim

RUN

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

COPY ./annotations/0.1.0/schema/annotations.json schema-root/schemas/annotations/0.1.0/annotation.json

COPY ./fdo-profiles/0.1.0/doi-kernel/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/handle-kernel/schema/ schema-root/schemas/fdo-profiles/0.1.0/

COPY digitalobjects/0.1.0/digital-specimens/schema schema-root/schemas/digitalobjects/0.1.0/digital-specimens
COPY digitalobjects/0.1.0/shared-models/schema schema-root/schemas/digitalobjects/0.1.0/shared-models
COPY digitalobjects/0.1.0/digital-media-objects/schema schema-root/schemas/digitalobjects/0.1.0/digital-media-objects

