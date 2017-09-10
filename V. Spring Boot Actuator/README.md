### Spring Boot执行器：Production-ready特性

Spring Boot包含很多其他特性，可用来帮你监控和管理发布到生产环境的应用。你可以选择使用HTTP端点，或者JMX来管理和监控应用。审计（Auditing），健康（health）和数据采集（metrics gathering）会自动应用到你的应用。

Actuator HTTP端点只能用在基于Spring MVC的应用，特别地，它不能跟Jersey一块使用，除非你也[启用Spring MVC](https://docs.spring.io/spring-boot/docs/2.0.0.M2/reference/htmlsingle/#howto-use-actuator-with-jersey)。