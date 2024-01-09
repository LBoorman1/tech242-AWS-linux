# JPA

Java persistence API

Solves two main issues three main issues that occur with using JDBC. 
1. datasource should not matter (no-SQL databases may need to be treated differently, however the process is still simplified)
2. adds persistence to the java application, objects created such as entities will remain even if the application is stopped.
3. Simplifies programmer interaction with the database by never making them leave the OOP paradigm.

Overview
- Allows programmers to think rationally about their objects, rather than converting code to database tables and back for example.
- Write classes for entities and repositories, or use SpringJPA to generate them for us.
- Provides built in methods for common queries such as get all by id.
- Persistence means that objects outlast the application that created them.

Our Use Case
- Used the springJPA with a world sql dataset.
- Created entities such as Country, City and CountryLanguage and their associated repositories. 
- Saved us the effort of using JDBC and manually writing queries with long form SQL syntax.
- SpringJPA also provided us with a visual representation of our datasource and this meant that we could edit it manually if needed.