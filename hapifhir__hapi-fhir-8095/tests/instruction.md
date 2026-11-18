# Issue

**Title:** Rename copied bean name methods to avoid collisions

## Description

ImportCustomTerminologyJobAppCtx has two methods with name overlaps to ImportIcdJobAppCtx:

importIcdStepChunkConceptsForClosureGeneration
importIcdStepGenerateConceptClosures

This resulted in exceptions trying to load configurations in hapi-fhir-jpaserver-starter:

```
Caused by: org.springframework.beans.factory.support.BeanDefinitionOverrideException: Invalid bean definition with name 'importIcdStepChunkConceptsForClosureGeneration' defined in ca.uhn.fhir.jpa.batch2.jobs.term.custom.ImportCustomTerminologyJobAppCtx: Cannot register bean definition [Root bean: class=null; scope=; abstract=false; lazyInit=null; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; fallback=false; factoryBeanName=ca.uhn.fhir.jpa.batch2.jobs.term.custom.ImportCustomTerminologyJobAppCtx; factoryMethodName=importIcdStepChunkConceptsForClosureGeneration; initMethodNames=null; destroyMethodNames=[(inferred)]; defined in ca.uhn.fhir.jpa.batch2.jobs.term.custom.ImportCustomTerminologyJobAppCtx] for bean 'importIcdStepChunkConceptsForClosureGeneration' since there is already [Root bean: class=null; scope=; abstract=false; lazyInit=null; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; fallback=false; factoryBeanName=ca.uhn.fhir.jpa.batch2.jobs.term.icd.ImportIcdJobAppCtx; factoryMethodName=importIcdStepChunkConceptsForClosureGeneration; initMethodNames=null; destroyMethodNames=[(inferred)]; defined in ca.uhn.fhir.jpa.batch2.jobs.term.icd.ImportIcdJobAppCtx] bound.
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.registerBeanDefinition(DefaultListableBeanFactory.java:1263)
        at org.springframework.context.annotation.ConfigurationClassBeanDefinitionReader.loadBeanDefinitionsForBeanMethod(ConfigurationClassBeanDefinitionReader.java:305)
        at org.springframework.context.annotation.ConfigurationClassBeanDefinitionReader.loadBeanDefinitionsForConfigurationClass(ConfigurationClassBeanDefinitionReader.java:144)
        at org.springframework.context.annotation.ConfigurationClassBeanDefinitionReader.loadBeanDefinitions(ConfigurationClassBeanDefinitionReader.java:120)
        at org.springframework.context.annotation.ConfigurationClassPostProcessor.processConfigBeanDefinitions(ConfigurationClassPostProcessor.java:430)
        at org.springframework.context.annotation.ConfigurationClassPostProcessor.postProcessBeanDefinitionRegistry(ConfigurationClassPostProcessor.java:290)
        at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanDefinitionRegistryPostProcessors(PostProcessorRegistrationDelegate.java:349)
        at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(PostProcessorRegistrationDelegate.java:118)
        at org.springframework.context.support.AbstractApplicationContext.invokeBeanFactoryPostProcessors(AbstractApplicationContext.java:792)
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:610)
        at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:146)
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:752)
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:439)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:318)
        at org.springframework.boot.test.context.SpringBootContextLoader.lambda$loadContext$3(SpringBootContextLoader.java:152)
        at org.springframework.util.function.ThrowingSupplier.get(ThrowingSupplier.java:58)
        at org.springframework.util.function.ThrowingSupplier.get(ThrowingSupplier.java:46)
        at org.springframework.boot.SpringApplication.withHook(SpringApplication.java:1461)
        at org.springframework.boot.test.context.SpringBootContextLoader$ContextLoaderHook.run(SpringBootContextLoader.java:595)
        at org.springframework.boot.test.context.SpringBootContextLoader.loadContext(SpringBootContextLoader.java:152)
        at org.springframework.boot.test.context.SpringBootContextLoader.loadContext(SpringBootContextLoader.java:111)
        at org.springframework.test.context.cache.DefaultCacheAwareContextLoaderDelegate.loadContextInternal(DefaultCacheAwareContextLoaderDelegate.java:225)
        at org.springframework.test.context.cache.DefaultCacheAwareContextLoaderDelegate.loadContext(DefaultCacheAwareContextLoaderDelegate.java:152)
        ... 19 more
```

The methods are named according to their enclosing class in this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1134df6fa9fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.