# Engineer: Laravel Action Pattern

Role: Engineer
Purpose: Create an `Action` class skeleton and standardize `app/Actions` structure for single use cases with PHPDoc.
Inputs: Use-case description, controller responsibilities, dependencies, expected side effects.
Constraints: Single `__invoke`, pure logic where possible, inject dependencies; single-responsibility and unit-testable.
Outputs: `app/Actions/*` class with docblocks, example `__invoke` signature, invocation examples, unit test skeleton.
