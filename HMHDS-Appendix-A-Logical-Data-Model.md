# HMHDS Appendix A

# Logical Data Model

## Version 1.0

### Draft

### June 2026

---

## 1. Purpose

This appendix defines the logical data model for the Historical Marker & Heritage Data Standard.

The model is technology-neutral, but designed to map cleanly to PostgreSQL/PostGIS, modern APIs, and graph-based search or discovery systems.

---

## 2. Missing Data, Unknown Values, and Null Handling

The model distinguishes between:

- No value supplied
- Unknown value
- Not applicable
- Withheld or restricted information
- Inferred information

These states are not interchangeable.

### NULL

NULL indicates that no value exists in the field.

### Unknown

Unknown is a valid value within a controlled vocabulary. It indicates that the field is applicable, was evaluated, and the correct value cannot currently be determined.

### Not Applicable

Not applicable indicates that a field does not logically apply to the entity.

### Withheld

Withheld indicates that information exists but is intentionally restricted.

### Inferred Values

Inferred values are derived from available evidence rather than explicitly supplied by a source. They require confidence metadata and supporting rationale.

---

## 3. Core Entities

The logical model includes:

- historical_resource
- resource_instance
- condition_history
- external_identifier
- name
- location
- external_geographic_identifier
- place
- person
- organization
- event
- resource_text
- source_subject
- normalized_subject
- subject_mapping
- resource_subject
- source
- source_record
- field_confidence
- media
- media_link
- contributor
- contribution
- review
- knowledge_note
- collection
- collection_item
- educational_resource
- reuse_policy
- entity_relationship
- change_log

---

## 4. Historical Resource

Represents the conceptual historical object or subject being documented.

Required fields include:

- resource_id
- resource_type
- preferred_name
- status
- created_at
- updated_at

---

## 5. Resource Instance

Represents a specific physical manifestation of a Historical Resource.

Required fields include:

- instance_id
- resource_id
- instance_type
- physical_type
- material
- current_status
- created_at
- updated_at

Date and year fields remain nullable when no value is supplied.

---

## 6. Location

The location model is internationalized and does not embed U.S.-specific geography in the core entity.

Core fields include:

- location_id
- instance_id
- latitude
- longitude
- geometry
- original_coordinate_text
- original_coordinate_system
- location_description
- address_full
- admin_level_1_name
- admin_level_1_type
- admin_level_2_name
- admin_level_2_type
- admin_level_3_name
- admin_level_3_type
- country_code
- country_name
- postal_code
- location_precision
- is_current
- effective_date
- expiration_date
- source_id

U.S. FIPS, GNIS, GeoNames, Wikidata, OSM, ISO, Statistics Canada, UK ONS, and similar identifiers belong in `external_geographic_identifier`.

---

## 7. Source and Provenance

Every significant fact must be traceable to a source.

Source records are immutable and preserve original source payloads.

---

## 8. Community Contribution and Knowledge Notes

Contributors should contribute knowledge, not data structures.

Knowledge notes capture observations, memories, leads, and research notes before they become structured data.

---

## 9. Minimum Viable Texas Implementation

For Phase 1 Texas, required entities include:

- historical_resource
- resource_instance
- location
- resource_text
- source
- source_record
- external_identifier
- external_geographic_identifier
- source_subject
- normalized_subject
- subject_mapping
- resource_subject
- condition_history
- media
- media_link
- field_confidence
- change_log

---

## 10. Implementation Notes

Recommended physical implementation:

- PostgreSQL
- PostGIS
- JSONB for immutable source payloads
- GIN indexes for full-text search
- Geometry indexes for map queries
- Role-based access control for contribution and review workflows

---

END OF DOCUMENT
