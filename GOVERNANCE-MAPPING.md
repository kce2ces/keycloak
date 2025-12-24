# Governance Mapping — Keycloak IAM

This document maps governance authority defined by the 
WSI Governance Canon to the operational scope of this Keycloak system.

## 1. Governance Authority

Ultimate authority for identity governance resides with
accountable human governance bodies operating under
the WSI Governance Canon.

AI systems have no authority to define, modify, or approve
identity governance decisions.

## 2. Human Authority Boundaries

The following authority boundaries apply:

- Governance Authority (Human)
  - Defines identity principles and constraints
  - Approves realm-level authority delegation

- System Administrators (Human)
  - Configure Keycloak realms, clients, and roles
  - Operate strictly within approved governance boundaries

- Application Owners (Human)
  - Request identity integrations and access scopes
  - Do not define identity governance rules

## 3. System Boundary (Keycloak)

Keycloak functions as:
- An identity execution system
- A policy enforcement point
- A credential and session authority

Keycloak does not function as:
- A governance decision-maker
- An autonomous authority
- A policy originator

## 4. AI Constraint

Any AI-assisted tooling interacting with this system:
- Acts in executor-only capacity
- Requires explicit human authorization
- Produces auditable and reversible changes

## 5. Canon Supremacy

In all cases of ambiguity or conflict:
WSI Governance Canon prevails.
