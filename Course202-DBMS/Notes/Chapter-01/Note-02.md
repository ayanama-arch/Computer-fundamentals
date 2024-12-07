# DBMS Basics

## Refrenced table vs Refrencing table

**Refrenced Table**
`Insert`: No Violation
`Delete`: May cause Violation
`Update`: May cause violation

**Refrencing Table**
`Insert`: May Cause Violation
`Delete`: No Violation
`Updation`: May cause violation

## Super Key

A super key is a combination of all possible attributes which can uniquely identify two tuples in a table.

- Super set of any candidate key is Super Key.

Number of super keys when:-
`one candidate key(A1)`: 2^n-1
`Two candidate key(A1,A2)`: 2^n-1 + 2^n-1 - 2^n-2
`Two candidate key of two keys combined (A1A2,A3A4)`: 2^n-2 + 2^n-2 - 2^n-4

## Entity Relationship Model (ER Model)

Conceptual view of data.

`Entity`: Rectangle
`Attribute`: Eclipse
`Relationship`: Diamond

### Types of Attributes

1. Single: Single Value (Single Eclipse)
2. Multivalued: More than one values possible (Double Ecllipse)
3. Simple: which can't be divided further
4. Composite Attribute: Made up of more than two attributes
5. Stored Attributes: Exact value
6. Derived Attribute: Which can be derived from attributes (Dotted Eclipse)
7. Key Attribute: Attribute which uniquely identifies tuple (Registration Number) represent with underline
8. Non-Key Attribute: Not necessary unique
9. Required Attribute: Whose value is mandatory
10. Optional Attribute: whose value can be skipped
11. Complex Attribute: (Composite + Multivalue)

## Degree of Relationship (Cardinality)

Relationship will be also a table which has foreign key from the both tables.
Relationship table can also have attribute called `Descriptive attribute`.

**1-1**: One to One, (Where one tuple will be related to one tuple ony or vice-versa).
`Example`: Husband <-> Wife

**1-M**: One to Many, When One Entity is related to many Entity
`Example`: Customer <-> Order

**M-N**: Many to Many, When One entity relates to many entity or vice-versa
`Example`: Student <-> Course

- You can't reduce relationship table.
- Primary key will be compisite key of both foreign key.
