# Engineer: Pagination & Sorting

Role: Engineer
Purpose: Best practices for paginated endpoints and stable sorting in Laravel.
Inputs: Query parameters (`page`, `per_page`, `sort`, `direction`).
Constraints: Limit `per_page` with sane max; prevent SQL injection via whitelists.
Outputs: Controller/query examples and FormRequest validation rules.
