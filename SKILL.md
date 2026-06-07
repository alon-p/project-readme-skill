---
name: Project Readme Editor
description: >
  Create and edit a README.md file for a project, describing how to setup, the tech used, guidelines, examples, and more.
  Makes the README.md easy to read and understand for newcomers.
  Use when a user asks to create or update a README.md file, or to edit an existing one.
  Also use when a user asks to document project sections like installation, setup, models, and more.
license: MIT
---

# Project Readme Editor

## Instructions

### step 1: [Review current Readme.md]

Review the current Readme.md file to understand the project structure and how to setup.
Ask the user if they need to update the current Readme.md file or create a new one.

### step 1: [Reslove language and framework]

Analyze pacakge manager files like package.json, pyproject.toml, requirements.txt, and similar files.
Identify the programming language and framework used in the project.
Example: Python with Django 6, React with Next.js 13, Express with Node.js 18, and so on.

### step 2: [review project files structure]

Review the project structure according to the language and framework.
Note if using a docker-compose file to run some services.

### step 3: [Write a heading section]

In the Readme.md file, write a heading section that describes the project. what tech is used, how the project is
orgenaized.

### step 4: [Write Setup section]

In the Readme.md file, write a section that describes how to setup the project.
Make sure to include the steps to install the dependencies, according to each operating system.
If there is a dockerfile, use that as a context on how to setup the project, at least on the opreationg system mentioned
in the dockerfile.
If there is a docker-compose file, detail each service and how to run it, the user might not need all services, usally
he needs data storage services like postgres, redis, influx, and so on.

### step 5: [Write a section for models]

If the project has a database, write a section that describes the models used in the project.
Write where each model is stored, and what is the purpose of each model.

### step 6: [Write a section for API]

If the project has an API, write a section that describes the API endpoints and how to use them.
See if there is a swagger file or similar file that describes the API.
See if there is a documentation page for the API.
If there is, write a section that describes how to run/disaply the swagger or similar documentaion.
Example: run the main service and browse to http://localhost:8000/docs

### step 6: [Write a section for tests]

If the project has tests, explain how to run them.
Use bash formatting for the commands.
Example:
```bash
python manage.py test
```
If no tests are found, explain that the project does not have tests.


### step 7: [Write a section for contributing]
If there are contribution guidelines, write a section that describes how to contribute to the project.
If there isn't, ask the user if they want to add a section for contributing.
If they do, write a section that describes how to contribute to the project.





