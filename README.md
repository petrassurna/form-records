# form-records

**Define forms and store their data using standard field types.**

---

## What this is

`form-records` is a small, headless library for defining **forms** (schemas) and storing **records** (form instances) using a fixed set of standard field types.

It provides a clean domain model for:
- form definitions
- field definitions
- records
- values
- querying via metadata

There is **no UI**, **no admin panel**, and **no form builder**.

This library is intended to be used as a **core data engine**, not a product.

---

## Example

### Defining a form

Below is an example form definition for a **Company**.

The form defines three fields:
- `name` (text)
- `type` (select)
- `description` (long text)

```ts
import { defineForm, text, select, longText } from "form-records";

const CompanyForm = defineForm({
  id: "company",
  name: "Company",
  fields: [
    text({
      id: "name",
      label: "Name",
      required: true,
      searchable: true,
    }),

    select({
      id: "type",
      label: "Type",
      options: [
        { value: "supplier", label: "Supplier" },
        { value: "customer", label: "Customer" },
        { value: "partner", label: "Partner" },
      ],
      required: true,
      searchable: true,
    }),

    longText({
      id: "description",
      label: "Description",
    }),
  ],
});


---

## Core concepts

### Form definitions
A form is a named collection of fields.

Each field has:
- an identifier
- a type (text, number, select, date, boolean, etc.)
- optional constraints (required, searchable, options)

Form definitions describe **what data can exist**.

---

### Form records
A record is an instance of a form.

Each record:
- belongs to exactly one form
- stores values keyed by field
- represents **what data does exist**

---

## What this library does

- Models forms and records as domain objects
- Enforces standard, well-understood field types
- Separates definitions from values
- Supports storage and querying via adapters
- Treats persistence as an implementation detail

---

## What this library does *not* do

Intentionally out of scope:

- UI components
- form rendering
- visual builders
- admin dashboards
- authentication or permissions
- workflows
- low-code / no-code features
- runtime schema mutation via UI

Those concerns belong in applications built on top of this library.

---

## Architecture

Application / UI
|
form-records
|
Persistence adapter (Postgres, SQLite, memory, etc.)

The domain model does not depend on SQL, HTTP, or UI frameworks.

---

## Persistence

Storage is handled via adapters.

A typical SQL-backed implementation uses a **fixed schema** with tables for:
- forms
- fields
- records
- field values

Schema creation, migrations, and indexing are considered **infrastructure concerns**, not core domain concerns.

---

## Use cases

`form-records` is suited to:
- CMS data definition (ACF in WordPress, Umbraco etc)
- dynmaic form modelling
- systems needing flexible but controlled data models

It is **not** a CMS or a SaaS platform.

---

## Design philosophy

- Boring over clever
- Explicit over magical
- Domain first, storage second
- Reads use projections; writes use the domain
- Small surface area
- Easy to walk away from

---

## Status

Early development.  
APIs may change until the core domain stabilises.

---

## License

MIT


Conceptual layering:

