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

## General Guidelines

- Do not use emojis anywhere in the README.md output.
- After completing each step, briefly suggest improvements the user could make to that section — things that are missing, could be clearer, or would help newcomers. Present suggestions as a short bulleted list before moving on to the next step.
- When writing setup or installation instructions, always provide separate instructions for Windows and for Linux/macOS.
- When referencing Docker, link to or mention the Docker Engine only — do not recommend Docker Desktop. Leave the choice of a Docker GUI to the user.

## Instructions

### step 1: [Review current README.md]

Review the current README.md file to understand the project structure and how to set up.
Ask the user if they need to update the current README.md file or create a new one.

### step 2: [Resolve language and framework]

Analyze package manager files like package.json, pyproject.toml, requirements.txt, and similar files.
Identify the programming language and framework used in the project.
Example: Python with Django 6, React with Next.js 13, Express with Node.js 18, and so on.

### step 3: [Review project file structure]

Review the project structure according to the language and framework.
Note if using a docker-compose file to run some services.
Check for CI/CD configuration files (e.g. `.github/workflows/`, `.gitlab-ci.yml`) — note what checks run so
the reader knows how to run the same checks locally.

### step 4: [Write a heading section]

In the README.md file, write a heading section that describes the project: what tech is used, how the project is
organized.
Add relevant badges (build status, license, version) if a CI/CD pipeline or package registry is present.
If the project has a UI, add a screenshots or demo section with a placeholder or link to a live demo.

### step 5: [Write Setup section]

In the README.md file, write a section that describes how to set up the project.
Make sure to include the steps to install the dependencies, according to each operating system.
If there is a dockerfile, use that as context on how to set up the project, at least on the operating system
mentioned in the dockerfile.
If there is a docker-compose file, detail each service and how to run it. The user might not need all services;
usually they need data storage services like postgres, redis, influx, and so on.
Check for environment variable usage:
- Look for a `.env.example` or `.env.sample` file — if found, list every variable it defines and explain its purpose.
- If no example file exists, grep the codebase for `os.environ`, `process.env`, `dotenv`, `getenv`, or similar patterns to discover what variables are expected.
- If any `.env`-related variables are found, instruct the reader to copy the example file (`cp .env.example .env`) and fill in their own values.
- Note which variables are required vs. optional, and flag any that need secrets (API keys, database passwords) so the reader knows not to commit them.

### step 6: [Write a section for models]

If the project has a database, write a section that describes the models used in the project.
Write where each model is stored, and what is the purpose of each model.

### step 7: [Write a section for API]

If the project has an API, write a section that describes the API endpoints and how to use them.
See if there is a swagger file or similar file that describes the API.
See if there is a documentation page for the API.
If there is, write a section that describes how to run/display the swagger or similar documentation.
Example: run the main service and browse to http://localhost:8000/docs

### step 8: [Write a section for tests]

If the project has tests, explain how to run them.
Use bash formatting for the commands.
Example:
```bash
python manage.py test
```
If a CI/CD config was found in step 3, mention how to run the same checks locally.
If no tests are found, explain that the project does not have tests.

### step 9: [Write a section for contributing]

If there are contribution guidelines, write a section that describes how to contribute to the project.
If there aren't, ask the user if they want to add a section for contributing.
If they do, write a section that covers: branch naming conventions, how to open a pull request, code style
requirements, and how to run tests before submitting.

### step 10: [Write a license section]

Check for a LICENSE or LICENSE.md file. If present, add a short license section at the bottom of the README
that names the license and links to the file.
If no license file exists, ask the user if they want to add one.

### step 11: [Write a changelog section]

If a CHANGELOG.md or CHANGELOG file exists, add a brief note in the README linking to it so readers know
where to find version history.
