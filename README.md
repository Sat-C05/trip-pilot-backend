# TripPilot backend

Coursework backend submission: Java 21, Spring Boot and MySQL 8.4. Source exported from the canonical [TripPilot project](https://github.com/Sat-C05/trip-pilot-java). The separate frontend is [trip-pilot-frontend](https://github.com/Sat-C05/trip-pilot-frontend).

## Layout and build

The root `pom.xml` is the Maven parent; `backend/` contains the application, tests and all eight Flyway migrations. Keep both directories together. This standalone parent contains only the backend module. Maven wrapper and a backend-only Docker build are included.

With Java 21 configured, run `./mvnw.cmd -B -ntp -pl backend -am -DskipTests package` on Windows (use `./mvnw` on Linux). The executable is `backend/target/backend-0.1.0-SNAPSHOT.jar`. This build skips test execution; integration tests require deliberate isolated MySQL/model/browser setup described in the canonical repository. Do not run them against personal or hosted application data.

## Local configuration

Set process environment variables described in `backend/.env.example`; Spring does not automatically load that file. Configure a dedicated fresh MySQL schema and account, then run `java -jar backend/target/backend-0.1.0-SNAPSHOT.jar`. Local defaults are backend port 8002, MySQL 13306 and pinned Ollama 11436. Do not replace other running services. Configure inference through the documented adapter; the hosted configuration uses Gemini. Never commit database passwords or API keys.

## Hosted configuration

The existing backend is https://trippilot-coursework.onrender.com, used by https://trip-pilot-java.vercel.app/. The existing deployment stays connected to the canonical repository. This repository can build independently using `infra/deployment/Dockerfile` and repository-root Docker context. See [deployment guide](docs/coursework-deployment.md) for environment variables, CA secret file, MySQL VERIFY_IDENTITY TLS, secure cookies, resource limits and account setup. Use a fresh hosted database; no local database export is included.

## Features and limits

Session authentication and CSRF, ownership checks, durable research, three shared workers with one inference slot, backend-owned retrieval/validation/budgets, per-job model snapshots, citations, SSE replay, card CRUD/restore, plan rename, selected contexts and Inspector. Guide research does not establish current commercial prices, inventory or provider policies. Booking remains disabled; the optional separate local booking simulation is available only in the canonical repository, not included here.

Public documents are preserved for technical context and historical acceptance; references to the combined repository, booking-demo and verification scripts refer to the canonical project. [Project document](project-document.md) records the design. A standalone build does not establish new hosted acceptance. No credentials, runtime data, personal records, internal notes or Git history are exported.