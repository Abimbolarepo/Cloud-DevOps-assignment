# react-and-spring-data-rest

The application has a react frontend and a Spring Boot Rest API, packaged as a single module Maven application.

You can build the application running (`./mvnw clean verify`), that will generate a Spring Boot flat JAR in the target folder.

To start the application you can just run (`java -jar target/react-and-spring-data-rest-*.jar`), then you can call the API by using the following curl (shown with its output):

---

\$ curl -v -u greg:turnquist localhost:8080/api/employees/1
{
"firstName" : "Frodo",
"lastName" : "Baggins",
"description" : "ring bearer",
"manager" : {
"name" : "greg",
"roles" : [ "ROLE_MANAGER" ]
},
"\_links" : {
"self" : {
"href" : "http://localhost:8080/api/employees/1"
}
}
}

---

To see the frontend, navigate to http://localhost:8080. You are immediately redirected to a login form. Log in as `greg/turnquist`
