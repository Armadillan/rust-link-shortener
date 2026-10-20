# rust-link-shortener
Practice project.

### Goals:

- Rust HTTP server
- Three simple html pages
  - / html form to add codes
  - / with the newly created short url (code) for copying
  - /{code} renders 404 page when returning 404
- Redirects GET /{code}
  - Returns 307
  - Handles db misses with 404
- Adds codes by POST to /add-link
  - Duplicate destinations allowed
  - Handles code collisions by retrying
  - Random short codes (base62)
  - URL validation (of destination link)
  - returns 201 with new short URL in response
- SQLite database
  - Set max size with LRU eviction (last access time)
    - Minimum age since creation to evict
- Tests throughout
  - Integration tests & unit tests
  - HTTP routes
  - SQLite integration
- ENV config
  - code length
  - address and port to bind listener to
  - max db size
  - min age to evict
  - db config
- Handle errors! no/minimal `unwrap`
  - Crashing on for example failing to bind to port is ok, but not on for example a malformed request

#### Stretch goals:

- Support redirecting all request types
- Optional commandline config (overrides ENV)
- Switch to MySQL from SQLite
- Optimize db transactions
  - atomic
  - combined insertion and eviction
  - batch db writes (dont write on every redirect), configurable

#### Non-goals / design limitations:
- Designed to run behind reverse proxy
  - no need to handle HTTPS/terminate TLS
  - no auth
  - no rate limiting
- Designed to be run in container
