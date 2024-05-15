# Release Notes

New version 0.0.2 for some of the files to include new terms.

## Verbatim Terms
Verbatim terms added such as `dwc:verbatimLocality` and `dwc:verbatimEventDate`.
The verbatim terms will be filled with the verbatim fields but not used for any further processing.
They are mainly used to keep the original value on the label.
The non-verbatim fields will be used for further processing.
For the non-verbatim fields we will first check the non-verbatim field, if this is not available we will take the verbatim field.
For example, to fill the `dwc:locality` field we will first check the `dwc:locality` field, if this is empty we will take the `dwc:verbatimLocality` field.

## ID fields
MIDS 3 requires several ID fields to be present.
These were not all included in the 0.1.0 version.

## Updated class names
Updated class names to reuse Darwin Core classes as much as possible.
Where it is not possible to reuse Darwin Core we prefixed them with `???:`.
Made them singular and camelCase.