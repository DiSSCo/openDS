FROM nginxinc/nginx-unprivileged:1.26-alpine

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

COPY ./annotations/0.1.0/schema/annotation.json schema-root/schemas/annotations/0.1.0/annotation.json
COPY ./annotations/0.1.0/schema/annotation-for-mas.json schema-root/schemas/annotations/0.1.0/annotation-for-mas.json
COPY ./annotations/0.1.0/schema/annotation-event.json schema-root/schemas/annotations/0.1.0/annotation-event.json

COPY ./fdo-profiles/0.1.0/annotation/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/digital-specimen/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/doi-kernel/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/handle-kernel/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/mapping/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/mas/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/media-object/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/organisation/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/source-system/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/tettris-service/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/tombstone/schema/ schema-root/schemas/fdo-profiles/0.1.0/
COPY ./fdo-profiles/0.1.0/virtual-collections/schema/ schema-root/schemas/fdo-profiles/0.1.0/

COPY ./annotations/0.1.0/schema/annotation.json schema-root/schemas/fdo-types/0.1.0/annotation.json
COPY ./fdo-types/0.1.0/digital-specimens/schema schema-root/schemas/fdo-types/0.1.0/digital-specimens
COPY ./fdo-types/0.1.0/shared-models/schema schema-root/schemas/fdo-types/0.1.0/shared-models
COPY ./fdo-types/0.1.0/digital-media-objects/schema schema-root/schemas/fdo-types/0.1.0/digital-media-objects
COPY ./fdo-types/0.1.0/machine-annotation-services/schema schema-root/schemas/fdo-types/0.1.0/machine-annotation-services
COPY ./fdo-types/0.1.0/mappings/schema schema-root/schemas/fdo-types/0.1.0/mappings
COPY ./fdo-types/0.1.0/source-systems/schema schema-root/schemas/fdo-types/0.1.0/source-systems
COPY ./fdo-types/0.1.0/virtual-collections/schema schema-root/schemas/fdo-types/0.1.0/vitual-collections

COPY ./fdo-types/0.2.0/digital-specimens/schema schema-root/schemas/digitalobjects/0.2.0/digital-specimens

COPY ./fdo-types/0.3.0/digital-specimens/schema schema-root/schemas/fdo-types/0.3.0/digital-specimens
COPY ./fdo-types/0.3.0/shared-models/schema schema-root/schemas/fdo-types/0.3.0/shared-models
COPY ./fdo-types/0.3.0/digital-media-objects/schema schema-root/schemas/fdo-types/0.3.0/digital-media-objects