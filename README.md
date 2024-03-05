# Exception

## spring-core 6.1.3 has issue with xml-based.xml file

If we use dependency:

        <dependency>

            <groupId>org.springframework</groupId>

            <artifactId>spring-core</artifactId>

            <version>6.1.3</version>

        </dependency>

Bean below produces exception:

    <bean id="personBean"
          name="person"
          class="ru.job4j.xmlbased.Person"
          lazy-init="true">
        <constructor-arg name="canary" ref="canary"/>
        <constructor-arg name="cat" ref="cat"/>
        <constructor-arg name="dog" ref="dog"/>
        <constructor-arg name="parrot" ref="parrot"/>
        <constructor-arg name="name" value="Man"/>
    </bean>

*"Exception in thread "main" org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'personBean' defined in class path resource [xml-based.xml]: Unsatisfied dependency expressed through constructor parameter 0: Could not convert argument value of type [ru.job4j.xmlbased.Canary] to required type [java.lang.String]: Failed to convert value of type 'ru.job4j.xmlbased.Canary' to required type 'java.lang.String'; Cannot convert value of type 'ru.job4j.xmlbased.Canary' to required type 'java.lang.String': no matching editors or conversion strategy found"*

Fix: change bean to:

    <bean id="personBean"
          name="person"
          class="ru.job4j.xmlbased.Person"
          lazy-init="true">
        <constructor-arg ref="canary"/>
        <constructor-arg ref="cat"/>
        <constructor-arg ref="dog"/>
        <constructor-arg ref="parrot"/>
        <constructor-arg name="name" value="Man"/>
    </bean>