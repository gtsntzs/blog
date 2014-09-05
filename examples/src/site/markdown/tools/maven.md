
---

## Apache Maven

Build tool


## Tips & Tricks

* Change the version of of a project, if project is a parent or aggregator will change the version to all subsequent child project.
```sh
mvn versions:set -DnewVersion=0.43-SNAPSHOT
```
