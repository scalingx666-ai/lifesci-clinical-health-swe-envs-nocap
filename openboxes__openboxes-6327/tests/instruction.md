# Issue

**Title:** OBPIH-8089 Unwrap Hibernate proxies in the Person and Party JSON mars…

## Description

…hallers

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**

**Description:**

**Problem**

On Grails 7, JSON rendering fails for associations declared as `Person` whose row is a `User` (`requestedBy`, `recipient`, `orderedBy`, …), for example on the stock movement lists:

```
class org.pih.warehouse.core.Person$HibernateProxy$… cannot be cast to class org.pih.warehouse.core.User
```

**Why it worked on Grails 3 and fails on Grails 7**

A lazy `Person` association is loaded as a Hibernate proxy of `Person`, even when the row is a `User`. On Grails 3, GORM 6 used Groovy-aware proxies (`GroovyAwarePojoEntityTuplizer`).

- Such a proxy answered `getMetaClass()` with its own `Person` metaclass, so `person.toJson()` resolved to `Person.toJson()`.
- That call was forwarded to the loaded object, where Java dispatch ran `User.toJson()`.

GORM 7+ removed this on purpose and uses plain Hibernate (ByteBuddy) proxies (](), closed as won't fix).

- These proxies forward `getMetaClass()` to the loaded object, so Groovy gets the `User` metaclass.
- Groovy then calls `User.toJson()` on the `Person` proxy, which is not a `User`, and the call fails with `ClassCastException`.

**Fix**

The `Person` and `Party` JSON marshallers in `BootStrap` unwrap the proxy with `Hibernate.unproxy(...)` before calling `toJson()`. `Party` → `Organization` is the same case.

- `unproxy` only touches proxies; other objects are returned as they are.
- It loads just that one row, which `toJson()` reads anyway.
- It doesn't change any fetch strategy.

The `User`/`Organization` marshallers need no change: they only receive real objects or proxies of their own type, and `toJson()` works on those.

**Known similar places (not changed in this PR)**

The same pattern can still fail elsewhere. These spots are left for follow-up if they show up. Whether they fail depends on whether the same `User`/`Organization` was already loaded in the request:

- `StockMovementController.reject()`: `Comment.recipient` stays empty when a request is rejected.
- `DocumentTemplateService.renderOrderDocumentTemplate`: the vendor/buyer `Organization` variables.
- `InvoiceService.createFromOrder`: `partyFrom`.
- `StockMovementService.updateShipmentBasedStockMovement`: `shipment.createdBy`.

I decided not to fix all the places at once, because it is not known if they would even fail, because e.g. I was able to create the invoice without any error.

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa673b308cbb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.