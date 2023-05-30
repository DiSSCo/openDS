# Living or Preserved

## openDS
Will be harmonised to `ods:livingOrPreserved`
This is a new field used also in the FDO Profile.

## Mapping
Before calculating livingOrPreserved with the below logic, we will first check if a default value or explicit mapping has been set.

## Mapping
This field is created based on the [`dwc:basisOfRecord`](./basisOfRecord.md).
If the `dwc:basisOfRecord` is LivingSpecimen then this field will contain `Living`.
In all other cases this field will be filled with `Preserved`.