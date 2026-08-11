# NovaCRM — Angular + NestJS + GraphQL + MongoDB

> 🚧 **Status: In Progress** — this project is being built incrementally as
> part of an ongoing portfolio effort. See the [Roadmap](#roadmap) below for
> current progress.

A full-stack CRM (Customer Relationship Management) application built to
demonstrate a modern, production-style MEAN-adjacent stack: **Angular** on
the frontend, **NestJS** on the backend, **GraphQL** as the API layer, and
**MongoDB** for persistence — end to end, containerized with Docker.

Unlike my [.NET-based projects](https://github.com/KTajerbashi), this one
is deliberately built on a different stack to show the same architectural
thinking (modular design, clear separation of concerns, testable services)
applied outside of .NET.

## What this demonstrates

- **NestJS** backend organized in feature modules (Contacts, Companies,
  Deals, Activities, Auth), each with its own resolver, service, schema,
  and DTOs — a Clean-Architecture-style separation adapted to Node.js
- **GraphQL API** (via `@nestjs/graphql` + Apollo) instead of REST —
  a single flexible endpoint, strongly typed schema, resolvers instead of
  controllers
- **MongoDB** with Mongoose schemas, modeling a real relational-ish domain
  (Contacts ↔ Companies ↔ Deals ↔ Activities) in a document database
- **JWT authentication** with route/resolver guards and basic role
  separation (Admin / Sales Rep)
- **Angular frontend** consuming the GraphQL API via Apollo Angular, with a
  feature-based folder structure (`core` / `shared` / `features`)
- Fully containerized with **Docker Compose** — Angular, NestJS, and
  MongoDB run together with one command

## Domain overview

A CRM for managing a sales pipeline:

- **Contacts** — people associated with deals and companies
- **Companies** — organizations a contact belongs to
- **Deals** — sales opportunities moving through a pipeline
  (`Lead → Qualified → Proposal → Won / Lost`)
- **Activities** — notes, calls, and meetings logged against a contact or
  deal
- **Auth** — user accounts with role-based access (Admin, Sales Rep)

```graphql
type Contact {
  id: ID!
  firstName: String!
  lastName: String!
  email: String!
  phone: String
  company: Company
  deals: [Deal!]
}

type Deal {
  id: ID!
  title: String!
  value: Float!
  stage: DealStage!   # LEAD, QUALIFIED, PROPOSAL, WON, LOST
  contact: Contact!
  activities: [Activity!]
}
```

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Angular, Apollo Angular |
| Backend | NestJS |
| API | GraphQL (Apollo Server) |
| Database | MongoDB (Mongoose) |
| Auth | JWT, Guards |
| Container | Docker, Docker Compose |

## Project Structure

```
angular-nestjs-crm/
├── backend/                        # NestJS
│   ├── src/
│   │   ├── modules/
│   │   │   ├── contacts/
│   │   │   │   ├── contacts.module.ts
│   │   │   │   ├── contacts.resolver.ts
│   │   │   │   ├── contacts.service.ts
│   │   │   │   ├── schemas/contact.schema.ts
│   │   │   │   └── dto/
│   │   │   ├── companies/
│   │   │   ├── deals/
│   │   │   ├── activities/
│   │   │   └── auth/
│   │   ├── common/                 # guards, filters, interceptors
│   │   └── main.ts
│   └── test/
├── frontend/                       # Angular
│   └── src/app/
│       ├── core/                   # auth, interceptors, guards
│       ├── shared/
│       └── features/               # contacts, deals, dashboard...
├── docker-compose.yml
└── README.md
```

## Roadmap

- [ ] Backend: `contacts` module (schema, service, basic CRUD)
- [ ] Backend: GraphQL resolvers replacing REST-style CRUD
- [ ] Backend: `companies`, `deals`, `activities` modules
- [ ] Backend: JWT auth + role guards
- [ ] Frontend: Angular app shell + Apollo Client setup
- [ ] Frontend: Contacts & Companies views
- [ ] Frontend: Deals pipeline (Kanban-style board)
- [ ] Docker Compose: Angular + NestJS + MongoDB
- [ ] Tests: unit tests for backend services/resolvers
- [ ] Deployment: live demo link

## Getting Started

> Setup instructions will be added once the initial backend module is in
> place. Planned flow:
>
> ```bash
> docker compose up --build
> ```
>
> This will start MongoDB, the NestJS API (GraphQL Playground at
> `/graphql`), and the Angular app together.

## Related projects

- [CleanArchitecture.AngularHost](https://github.com/KTajerbashi/CleanArchitecture.AngularHost) — .NET + Angular integrated hosting template with .NET Aspire
- More flagship projects linked from my [profile](https://github.com/KTajerbashi)
