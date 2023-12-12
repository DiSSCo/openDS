FROM nginx:stable-alpine3.17-slim

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

COPY ./annotations/v0.1.0/schema/annotation.json schema-root/schemas/annotations/v0.1.0/annotation.json

COPY ./fdo-profiles/v0.1.0/digital-specimen/schema/ schema-root/schemas/fdo-profiles/v0.1.0/
COPY ./fdo-profiles/v0.1.0/doi-kernel/schema/ schema-root/schemas/fdo-profiles/v0.1.0/
COPY ./fdo-profiles/v0.1.0/handle-kernel/schema/ schema-root/schemas/fdo-profiles/v0.1.0/

COPY ./specimens-and-media/v0.1.0/digital-specimens/schema schema-root/schemas/digital-specimens/v.0.1.0/
COPY ./specimens-and-media/v0.1.0/shared-models/schema schema-root/schemas/shared-models/v.0.1.0/
COPY ./specimens-and-media/v0.1.0/digital-media-object/schema schema-root/schemas/digital-media-object/v.0.1.0/

