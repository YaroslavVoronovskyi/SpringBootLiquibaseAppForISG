# Liquibase migration with MySQL DB in Java Spring Boot application.

This repository provides a simple migration MySQL DB by Liquibase in a Java and Spring Boot application.

## Prerequisites

Before starting, make sure you use Java 17 you have Docker on your computer.

## Getting Started

Clone the repository:

```git@github.com:YaroslavVoronovskyi/SpringBootLiquibaseAppForISG.git```

Before run application, you need open terminal in your project IDE, 
and run command "docker compose up"? and after that you can run application.

#### Result:

After run application you should see next liquibase logs:

 liquibase.changelog                      : Reading from Library.databasechangelog
 liquibase.ui                             : Database is up to date, no changesets to execute
 liquibase.changelog                      : Reading from Library.databasechangelog
 liquibase.util                           : UPDATE SUMMARY 
 liquibase.util                           : Run:                          4
 liquibase.util                           : Previously run:               0
 liquibase.util                           : Filtered out:                 0
 liquibase.util                           : -------------------------------
 liquibase.util                           : Total change sets:            4
 liquibase.util                           : Update summary generated
 liquibase.command                        : Update command completed successfully.
 liquibase.ui                             : Liquibase: Update has been successful. Rows 

If you stop application and than run ia again you should see next liquibase logs:

 liquibase.changelog                      : Reading from Library.databasechangelog
 liquibase.ui                             : Database is up to date, no changesets to execute
 liquibase.changelog                      : Reading from Library.databasechangelog
 liquibase.util                           : UPDATE SUMMARY
 liquibase.util                           : Run:                          0
 liquibase.util                           : Previously run:               4
 liquibase.util                           : Filtered out:                 0
 liquibase.util                           : -------------------------------
 liquibase.util                           : Total change sets:            4
 liquibase.util                           : Update summary generated
 liquibase.lockservice                    : Successfully released change log lock
 liquibase.command                        : Command execution complete

#### Rollback:

If you wanna make manual rollback, you have three options:

```rollbackTag```
We can define a particular state of our database to be a tag. 
Therefore, we can reference back to that state. 
Rolling back to the tag name “1.0” looks like:

mvn liquibase:rollback -Dliquibase.rollbackTag=1.0

This executes rollback statements of all the changesets executed after tag “1.0”.

```rollbackCount```
Here, we define how many changesets we need to be rolled back. 
If we define it to be one, the last changeset execute will be rolled back:

mvn liquibase:rollback -Dliquibase.rollbackCount=1

```rollbackDate```
We can set a rollback target as a date, therefore, any changeset executed after that day will be rolled back:

mvn liquibase:rollback "-Dliquibase.rollbackDate=Jun 03, 2017"

The date format has to be an ISO data format or should match the value of 
DateFormat.getDateInstance() of the executing platform.
