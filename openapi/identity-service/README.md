# Identity Service OpenAPI Contract

`openapi.yaml` defines the Spring Boot Identity and Access Service contract.

The service owns the business logic for owner and staff authentication, password and three digit PIN verification, sessions, staff access management, password recovery, account lockout, and current-user context. It never connects directly to MongoDB; it calls the private Identity Data Service for all persistence.

There are no public device add, remove, or modify endpoints. On successful login, the service revokes every earlier session for the same user. The API Gateway validates the JWT session ID on every authenticated request, so the previous device receives `401` on its next request and returns to login.

Shared, cross-service schemas are referenced from `../common/common.yaml`. Future microservices should add a sibling directory under `openapi/` and reference the same common contract rather than duplicating errors, headers, or pagination rules.
