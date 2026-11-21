# Education Analytics Lakehouse — Dataset v2

Four synthetic CSV source datasets, 300 raw rows each:
- universities.csv
- courses.csv
- students.csv
- applications.csv

## Important usage guidance
These are deliberately imperfect RAW source files for Bronze/Silver engineering practice.
They contain nulls, blank/whitespace values, duplicate primary keys, malformed values,
invalid domain values, and selected orphan foreign keys.

Do not clean these files manually. Preserve them as source data and implement validation,
quarantine/reject handling, deduplication, type casting and referential-integrity checks
in your Silver processing.

## Existing project schema compatibility
- universities: university_id, university_name, country, city, ranking, tuition_fee,
  currency, is_partner, updated_at
- courses: course_id, university_id, course_name, degree_level, duration_years,
  annual_tuition_fee, currency, is_active, updated_at
- students: student_id, student_name, email, nationality, education_level,
  graduation_year, created_at
- applications: application_id, student_id, course_id, intake, application_date,
  application_status, application_fee_paid, updated_at

## Data quality scenarios seeded
- Duplicate identifiers in all four datasets.
- Null identifiers and required attributes.
- Invalid integer, decimal, boolean and date values.
- Invalid categorical/domain values.
- Empty and whitespace-only strings.
- Invalid email formats.
- Orphan university, student and course references.

## Recommended ingestion
For the raw Bronze landing step, read CSV columns as strings (inferSchema=False)
or use an explicit raw schema. This prevents malformed values from causing the
entire CSV read to fail and preserves source values for later validation.
Cast to typed columns in Silver using safe casts and record rejected rows with
a rejection_reason, source_file and ingestion_timestamp.

All names, institutions and records are synthetic. Do not treat this as real student data.
