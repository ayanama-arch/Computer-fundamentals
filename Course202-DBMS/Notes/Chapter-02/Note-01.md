# Normalization

It is technique to remove or Reduce Redundancy from a table.

There are two types of duplicacy in table:-

1. Row Level
   Use primary key to remove row level redundancy

2. Column Level:-

Probelems with Column level redundancy

`Insertion Anamoly`: You need to have some mandatory field before inserstion.
`Deletion Anamoly`: More than required information gets deleted.
`Updation Anamoly`: Integrity might lost while updating throughout the table.

## First Normal Form

Table should not contain any multivalued attribute.
If there is multivalued attribute create two table and refrenced that table from second table.

## Closure Method

Closure method is fundamental in database theory as it helps in identifying candidate keys, superkeys, and understanding the overall dependency structure within a database schema.

- A candidate key is a minimal set of attributes in a relational database that can uniquely identify a tuple

`Example:01`
FD = {A->B,B->C,C->D}
Here A can determine all the other attribute so {A} is candidate key.
Prime Attribute: {A}
Non-Prime Attribute: {B,C,D}

- NOTE: (AB) can also determine {A,B,C,D} But AB is not candidate key because A is already C.K which is minimal here, AB is super key.

`Example:02`
FD={A->B,B->C,C->D,D->A}
Here all the keys can determine ever other attribute so all of them are canidate key
C.K. = {A,B,C,D}
**Prime Attribute** It is a key which is used to determine canidate key
Here Prime Attribute are {A,B,C,D}
and Non Prime Attribute = {null}

`Example:03`
FD = {a->B,BC->D,E->C,D->A}
C.K. = {AE, DE, BE}
Prime Attribute: {A,B,D,E}
Non-Prime Attribute: {C}

## Functional Dependency(FD)

Relationship between attributes

X(Determinent) -> Y(Dependent Attribute): X Determines Y

`Trivial Functional Dependency:`
X->Y, then Y is subset of X

`Non-Trivial FD:`
X->Y, Y is not subset of X

### Properties of FD

`Reflexivity`: If Y is subset of X then X->Y.
`Augmentation`: If X->Y, then XZ->YZ
`Transitive`: If X->Y and y->Z, then X->Z
`Union`: If X->Y and X->Z then X->YZ
`Decomposition`: If X->YZ then X->Y, X->Z
`Pseudotransitivity`: If X->Y and WY->Z then WX->Z
`Composition`: If X->Y and Z->W then XZ->WY

## Second Normal Form

- Table or Relation must be in 1st Normal Form.
- All the non-prime attributes should be fully functional dependent on Candidate key.
- There should be No partial dependency in the relation in subset of C.K to non-prime attribute.

## Third Normal Form

- Table or relation must be in Second normal form.
- There should be no transitive dependency in table.
- No non-prime attribute should not determine non-prime attribute.

A table is in 3rd Normal form if LHS of all FD is CK/SK OR RHS is prime attribute.

## BNCF(Boyce Codd Normal Form)

BCNF is a normalization form that ensures no non-trivial functional dependency violates the rule where the left-hand side must be a superkey. It helps in reducing redundancy and maintaining data integrity.

In BNCF Complete C.K must determine non-prime attribute not partially.

`Example`
If AB is C.K. and AB->D, then D should not be a partial dependency of either A or B unlike 3rd normal form.

`Note:` In BCNF lHS of FD must be Candidate Key(C.K)

- Third Normal form always ensures 'Dependency Preserving decomposition' but not in BNCF.
- Both Third & BNCF ensures lossless decomposition.
