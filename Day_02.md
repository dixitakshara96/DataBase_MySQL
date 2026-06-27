# DBMS Learning: Functional Dependencies & Keys

This repository contains learning notes and core concepts for an introductory Database Management Systems (DBMS) course, heavily inspired by the GeeksforGeeks curriculum. The focus of this module is on Functional Dependencies (FDs), attribute closures, and schema refinement.

## Table of Contents
1. [Attribute Closure](#attribute-closure)
2. [Equivalence of Functional Dependencies](#equivalence-of-functional-dependencies)
3. [Canonical Cover (Minimal Cover)](#canonical-cover)

---

## Attribute Closure

**Definition:**
The set of all attributes that can be functionally determined from a specific attribute or set of attributes is called the **Attribute Closure**. For a given attribute set `X`, its closure is denoted as `X⁺`.

Finding the attribute closure is essential for identifying candidate keys, super keys, and testing whether a specific functional dependency holds.

### Algorithm to find Attribute Closure (`X⁺`)
1. Initialize the result set `Result = X` (the attribute itself is always part of its closure due to trivial dependency).
2. Loop through the given set of Functional Dependencies (`F`).
3. For each functional dependency `A → B` in `F`:
   - If `A` is a subset of `Result` (`A ⊆ Result`), add `B` to the `Result` (`Result = Result ∪ B`).
4. Repeat Step 2 and 3 until the `Result` set stops changing (no new attributes can be added).

### Example
Given `R = (A, B, C, D)` and `F = {A → B, B → C, C → D}`.
To find `A⁺`:
- **Initial:** `Result = {A}`
- **A → B:** `Result = {A, B}`
- **B → C:** `Result = {A, B, C}`
- **C → D:** `Result = {A, B, C, D}`

`A⁺ = {A, B, C, D}`. Since `A` can determine all attributes, `A` is a Super Key.

---

## Equivalence of Functional Dependencies

**Definition:**
Two sets of Functional Dependencies, say `F` and `G`, are considered equivalent if they enforce the exact same constraints on a relational schema. If `F` and `G` are equivalent, they can imply each other, which is denoted as `F ≡ G`.

To prove equivalence, you must show that:
1. Every functional dependency in `F` can be inferred from `G` (i.e., `F ⊆ G⁺`).
2. Every functional dependency in `G` can be inferred from `F` (i.e., `G ⊆ F⁺`).

### How to check equivalence
- **Check `F ⊆ G⁺`:** For every dependency `X → Y` in `F`, calculate the attribute closure of `X` using the dependencies in `G`. If `Y` is present in the computed closure, then `G` can determine `F`.
- **Check `G ⊆ F⁺`:** Conversely, for every dependency `X → Y` in `G`, calculate the attribute closure of `X` using the dependencies in `F`. If `Y` is present, then `F` can determine `G`.

If both conditions hold true, the sets `F` and `G` are equivalent.

---

## Canonical Cover

**Definition:**
A Canonical Cover (also known as a Minimal Cover or Irreducible Set) is the simplest, most reduced form of a set of functional dependencies. It is obtained by removing all redundant dependencies and extraneous attributes without losing any information from the original set.

Computing a canonical cover is crucial for database normalization and ensuring dependency-preserving decomposition.

### Steps to find the Canonical Cover
1. **Split Right-Hand Side (RHS) Attributes:** Break down dependencies so that every RHS contains only a single attribute.
   - *Example:* Convert `A → BC` into `A → B` and `A → C`.
2. **Remove Redundant Functional Dependencies:** Check each dependency to see if it is implied by the remaining dependencies.
   - Temporarily remove a dependency `X → Y`.
   - Calculate `X⁺` using the remaining dependencies.
   - If `Y` is still in `X⁺`, the dependency `X → Y` is redundant and should be permanently removed.
3. **Remove Extraneous Attributes (Left-Hand Side):** If a dependency has multiple attributes on the LHS (e.g., `AB → C`), check if one of the attributes is unnecessary.
   - *Check if `A` is extraneous:* Calculate `B⁺` using all FDs. If `C` is in `B⁺`, `A` is extraneous and `AB → C` becomes `B → C`.
   - *Check if `B` is extraneous:* Calculate `A⁺`. If `C` is in `A⁺`, `B` is extraneous.

### Example
Given `F = {A → B, B → C, A → C}`.
- **Step 1:** All RHS attributes are single. No splitting needed.
- **Step 2:** Check for redundancy.
  - Let's check `A → C`. If we temporarily remove it, the remaining FDs are `{A → B, B → C}`.
  - Calculate `A⁺` using the remaining FDs: `A⁺ = {A, B, C}`.
  - Since `C` is in the closure without needing `A → C` (due to transitivity `A → B → C`), `A → C` is redundant.

**Minimal Cover = `{A → B, B → C}`.**
