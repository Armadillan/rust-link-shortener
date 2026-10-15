### Plan

1. Start in memory
   - tests
   - url validation
   - code generation
   - collision handling
   - lookup
2. HTTP
3. SQLite
4. eviction

### DB structure
Fields:
- code
- url
- creation time (unix timestamp)
- last access time (unix timestamp)

### Stats to keep track of
- number of active codes
- max number of codes (config)
- age of last evicted entry
- last access time of last evicted entry

### HTTP route contract and HTML pages

- GET / -> HTML form to submit new code
  - landing page with stats and form
  - page with code to copy on successful creation
- POST /add-link -> Create link, return 201 with the code in response body
- GET /{code} -> 307 redirect or 404
  - 404 page
