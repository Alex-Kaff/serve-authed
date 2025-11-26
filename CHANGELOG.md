# serve-authed

## 14.3.0

### Minor Changes

- Added authentication support via `--token` flag
  - Supports token authentication via Authorization header (with or without Bearer prefix)
  - Supports token authentication via `authentication` query parameter
  - Returns 403 Forbidden for unauthenticated requests when token is configured
  - Backward compatible - works without authentication when no token is provided

## 14.2.5

### Patch Changes

- f4b6fbd: Update compression to v1.8.1
