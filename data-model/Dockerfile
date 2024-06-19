FROM nginxinc/nginx-unprivileged:1.26-alpine

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

# Versioned FDO Profile schemas
COPY fdo-profile/annotation/0.1.0/schema schema-root/schemas/fdo-profile/annotation/0.1.0
COPY fdo-profile/digital-specimen/0.1.0/schema/ schema-root/schemas/fdo-profile/digital-specimen/0.1.0
COPY fdo-profile/doi-kernel/0.1.0/schema schema-root/schemas/fdo-profile/doi-kernel/0.1.0
COPY fdo-profile/handle-kernel/0.1.0/schema schema-root/schemas/fdo-profile/handle-kernel/0.1.0
COPY fdo-profile/mapping/0.1.0/schema schema-root/schemas/fdo-profile/mapping/0.1.0
COPY fdo-profile/mas/0.1.0/schema schema-root/schemas/fdo-profile/mas/0.1.0
COPY fdo-profile/media-object/0.1.0/schema schema-root/schemas/fdo-profile/media-object/0.1.0
COPY fdo-profile/organisation/0.1.0/schema schema-root/schemas/fdo-profile/organisation/0.1.0
COPY fdo-profile/source-system/0.1.0/schema schema-root/schemas/fdo-profile/source-system/0.1.0
COPY fdo-profile/tettris-service/0.1.0/schema schema-root/schemas/fdo-profile/tettris-service/0.1.0
COPY fdo-profile/tombstone/0.1.0/schema schema-root/schemas/fdo-profile/tombstone/0.1.0
COPY fdo-profile/virtual-collection/0.1.0/schema schema-root/schemas/fdo-profile/virtual-collection/0.1.0

# Latest FDO Profile schemas
COPY fdo-profile/annotation/0.1.0/schema schema-root/schemas/fdo-profile/annotation/latest
COPY fdo-profile/digital-specimen/0.1.0/schema/ schema-root/schemas/fdo-profile/digital-specimen/latest
COPY fdo-profile/doi-kernel/0.1.0/schema schema-root/schemas/fdo-profile/doi-kernel/latest
COPY fdo-profile/handle-kernel/0.1.0/schema schema-root/schemas/fdo-profile/handle-kernel/latest
COPY fdo-profile/mapping/0.1.0/schema schema-root/schemas/fdo-profile/mapping/latest
COPY fdo-profile/mas/0.1.0/schema schema-root/schemas/fdo-profile/mas/latest
COPY fdo-profile/media-object/0.1.0/schema schema-root/schemas/fdo-profile/media-object/latest
COPY fdo-profile/organisation/0.1.0/schema schema-root/schemas/fdo-profile/organisation/latest
COPY fdo-profile/source-system/0.1.0/schema schema-root/schemas/fdo-profile/source-system/latest
COPY fdo-profile/tettris-service/0.1.0/schema schema-root/schemas/fdo-profile/tettris-service/latest
COPY fdo-profile/tombstone/0.1.0/schema schema-root/schemas/fdo-profile/tombstone/latest
COPY fdo-profile/virtual-collection/0.1.0/schema schema-root/schemas/fdo-profile/virtual-collection/latest

# Versioned FDO Type schemas
COPY fdo-type/annotation/0.3.0/schema schema-root/schemas/fdo-type/annotation/0.3.0
COPY fdo-type/create-update-tombstone-event/0.3.0/schema schema-root/schemas/fdo-type/create-update-tombstone-event/0.3.0
COPY fdo-type/digital-media/0.3.0/schema schema-root/schemas/fdo-type/digital-media/0.3.0
COPY fdo-type/digital-specimen/0.3.0/schema schema-root/schemas/fdo-type/digital-specimen/0.3.0
COPY fdo-type/machine-annotation-service/0.3.0/schema schema-root/schemas/fdo-type/machine-annotation-service/0.3.0
COPY fdo-type/data-mapping/0.3.0/schema schema-root/schemas/fdo-type/data-mapping/0.3.0
COPY fdo-type/shared-model/0.3.0/schema schema-root/schemas/fdo-type/shared-model/0.3.0
COPY fdo-type/source-system/0.3.0/schema schema-root/schemas/fdo-type/source-system/0.3.0
COPY fdo-type/tettris-service/0.1.0/schema schema-root/schemas/fdo-type/tettris-service/0.1.0
COPY fdo-type/virtual-collection/0.1.0/schema schema-root/schemas/fdo-type/vitual-collection/0.1.0

# Latest FDO Type schemas
COPY fdo-type/annotation/0.3.0/schema schema-root/schemas/fdo-type/annotation/latest
COPY fdo-type/create-update-tombstone-event/0.3.0/schema schema-root/schemas/fdo-type/create-update-tombstone-event/latest
COPY fdo-type/digital-media/0.3.0/schema schema-root/schemas/fdo-type/digital-media/latest
COPY fdo-type/digital-specimen/0.3.0/schema schema-root/schemas/fdo-type/digital-specimen/latest
COPY fdo-type/machine-annotation-service/0.3.0/schema schema-root/schemas/fdo-type/machine-annotation-service/latest
COPY fdo-type/data-mapping/0.3.0/schema schema-root/schemas/fdo-type/data-mapping/latest
COPY fdo-type/shared-model/0.3.0/schema schema-root/schemas/fdo-type/shared-model/latest
COPY fdo-type/source-system/0.3.0/schema schema-root/schemas/fdo-type/source-system/latest
COPY fdo-type/tettris-service/0.1.0/schema schema-root/schemas/fdo-type/tettris-service/latest
COPY fdo-type/virtual-collection/0.1.0/schema schema-root/schemas/fdo-type/vitual-collection/latest

# Versioned Developer schemas
COPY developer-schema/annotation/0.2.0/schema schema-root/schemas/developer-schema/annotation/0.2.0

# Latest Developer schemas
COPY developer-schema/annotation/0.2.0/schema schema-root/schemas/developer-schema/annotation/latest

# Versioned internal schemas
COPY internal-schema/annotation/0.1.0/schema schema-root/schemas/internal-schema/annotation/0.1.0

# Latest internal schemas
COPY internal-schema/annotation/0.1.0/schema schema-root/schemas/internal-schema/annotation/latest