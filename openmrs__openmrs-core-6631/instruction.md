# Issue

**Title:** Ensure core service advisors apply when modules declare FactoryBean services

## Description

.

Adds `ProxyFactoryBeanObjectTypePostProcessor`, a `BeanFactoryPostProcessor` registered as a static `@Bean` in `AOPConfig`. Before any bean is created, it visits every `AbstractSingletonProxyFactoryBean` definition (that is, `TransactionProxyFactoryBean`):
- It resolves the target's class from the `target` bean reference or inner bean.
- It computes the proxy class that the factory will produce.
- It records that class as `FactoryBean.OBJECT_TYPE_ATTRIBUTE`, Spring's documented way to declare a factory bean's type up front.

By-type lookups made while the auto-proxy advisors are being built can then match these definitions without instantiating them. As a result, module targets and the core services they reference are no longer created, and proxied without advisors, ahead of those advisors.

Definitions that set `proxyInterfaces`, whose target is itself a `FactoryBean`, or that can't be resolved are left alone, so they keep today's behaviour.

**Tests:**
- `ModuleFactoryBeanServiceAdvisorsTest` adds two fixture beans to the test context:
  - A metadatamapping-style `ref` target with `conceptService`/`adminService` properties.
  - A queue-style inner-bean target with an `@Autowired OrderService`.
- Without the fix, those core services lack the authorization, required-data and transaction advice, and a logged-out `conceptService.getConcept(3)` does not throw. With the fix, all 4 tests pass.
- The full default api suite passes: 5451 tests, 0 failures.

**Runtime:**
- On master, OpenMRS with 17 Platform-3-upgraded O3 modules fails to start with the error in #6630.
- With this branch running the same 17 modules (`mvn jetty:run`, MySQL 8):
  - All modules start.
  - UI login works.
  - Anonymous REST calls to core services are again refused with 401.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Fp7T1pGYEMrMVp1M7AW9Fg

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34dc604e6eea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.