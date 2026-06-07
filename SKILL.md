---
name: project-readme-skill
description: >
  Create, update, or audit a README.md file for a project, covering setup, tech stack, models, API, tests, and more.
  Makes the README.md easy to read and understand for newcomers.
  Use when a user asks to create or update a README.md file, review and improve an existing one, or document
  specific sections like installation, setup, models, API endpoints, and more.
license: MIT
---

# Project README Editor

## General Guidelines

- Do not use emojis anywhere in the README.md output.
- **Document only what you can verify.** Base every section on what you can confirm by reading the code, config, or schema. Never invent endpoints, model fields, environment variables, commands, or versions. If something cannot be verified, omit it or leave a clearly marked placeholder (e.g. `<!-- TODO: confirm -->`) for the user to fill in.
- After completing a step, if there is something material the user could improve — a section that is missing detail, unclear, or would trip up a newcomer — note it as a short bulleted list before moving on. Skip the suggestions when a section is already complete and accurate rather than inventing feedback for every step.
- When setup steps genuinely differ by operating system, provide separate instructions for Windows and for Linux/macOS. If the steps are identical across platforms, give them once rather than duplicating them.
- **Watch for native dependencies with OS-specific prerequisites.** Some packages require system-level libraries or build tools that are installed differently per OS — e.g. `psycopg`/`psycopg2` needs the PostgreSQL client tools (`libpq`) and a C compiler, which on Windows often means installing the PostgreSQL CLI tools while on Debian/Ubuntu it is `apt install libpq-dev`, and on macOS `brew install libpq`. Scan the dependency list for packages like this (database drivers such as `psycopg`/`mysqlclient`, image libraries such as `Pillow`, and others that compile native extensions) and document the required system packages per OS so the install does not fail with a cryptic build error.
- When referencing Docker, link to or mention the Docker Engine only — do not recommend Docker Desktop. Leave the choice of a Docker GUI to the user.
- **Update mode:** When the user chooses to update an existing README rather than replace it, apply every section step as an audit-and-patch operation: locate the corresponding section in the current file, check it for accuracy and completeness against the project as it exists now, and edit only what is wrong, missing, or outdated. Do not remove content that is still correct. If a section is absent entirely, add it. Preserve any custom sections or prose the user has written that fall outside these steps.
- **Scale depth to project size:** Match the level of detail to the complexity of the project. A small utility script needs only brief setup instructions and a short description. A multi-service application warrants full model, API, and environment variable documentation. Use judgment — avoid padding small projects with empty sections, and avoid skimping on large ones.
- **Keep the Table of Contents in sync:** After writing or updating each section, update the Table of Contents so links remain accurate throughout the README.
- **Monorepos:** If the project contains multiple packages or services in subdirectories, document the top-level README at a high level (what the repo contains and how the parts relate) and link to per-package or per-service READMEs for the detail. Do not try to document all packages exhaustively in a single file.

## Instructions

### Step 1: Review current README.md

Check whether a README.md file exists at the project root. If it does not exist, inform the user
that no README.md was found and that one will be created at the project root (`./README.md`).

Then ask the user the following questions in a single prompt, so the writing phase is not
interrupted later:
- If a README already exists: **Update** (audit and patch each section in place, preserving what
  is correct — update mode) or **Replace** (discard the existing content and write from scratch)?
- Should a **Contributing** section be added? (used in Step 9)
- Should a **License** file and section be added if none is found? (used in Step 10)

Wait for the user's answers before proceeding to Step 2. Do not begin analyzing or writing until
they respond.

### Step 2: Resolve language and framework

Analyze package manager files like package.json, pyproject.toml, requirements.txt, and similar files.
If no package manager file is present, check for a Dockerfile and read the `FROM` directive to infer the language and runtime version.
Identify the programming language and framework used in the project.
Example: Python with Django 6, React with Next.js 13, Express with Node.js 18, and so on.

### Step 3: Review project file structure

Review the project structure according to the language and framework.
Note if using a docker-compose file to run some services.
Check for CI/CD configuration files (e.g. `.github/workflows/`, `.gitlab-ci.yml`) — note what checks run so
the reader knows how to run the same checks locally.
Check whether the project has a user-facing UI (e.g. frontend framework, templates, static assets) so Step 4
knows whether to add a screenshots or demo section.

After completing this step, report a brief summary to the user before proceeding:
- Language and framework detected (from Step 2)
- Key directories and their roles
- Services found (docker-compose, external DBs, caches, etc.)
- CI/CD checks found, if any
- Whether the project has a UI
- Which README sections will be written based on what was found

Stop and wait for the user to confirm or correct this summary before moving to Step 4. Do not begin
writing the README until they respond — this is the user's chance to correct any wrong assumptions
before writing begins.

### Step 4: Write or update heading section

This is the step that first creates the file. If no README.md exists, create `./README.md` now with
the heading section below; later steps then patch and append to it. (In update mode the file already
exists — edit the existing heading in place.)

In the README.md file, write a heading section that describes the project: what tech is used, how the project is
organized. Include a one- or two-sentence project description immediately under the title so a newcomer knows
what the project does at a glance.
Add relevant badges (build status, license, version) if a CI/CD pipeline or package registry is present.
If the project has a UI, add a screenshots or demo section with a placeholder or link to a live demo.
After the heading section, add a Table of Contents that links to every major section in the README.
Update the Table of Contents whenever a new section is added.

### Step 5: Write or update Setup section

In the README.md file, write a section that describes how to set up the project.

**Prerequisites** — open the setup section with a short list of required runtimes and tools with their minimum versions (e.g. Node >= 20, Python >= 3.11, Docker >= 24). Derive versions from package manager files, Dockerfile `FROM` directives, or CI configuration. Only list what the reader must install before following the steps below.

Make sure to include the steps to install the dependencies, according to each operating system.
Derive the actual commands from the project itself — `package.json` scripts, a Makefile, `pyproject.toml`,
`manage.py`, or CI configuration — rather than assuming conventional defaults. Do not document a command you
cannot trace to a real script or entry point.
If there is a dockerfile, use that as context on how to set up the project, at least on the operating system
mentioned in the dockerfile.
If there is a docker-compose file, detail each service and how to run it. The user might not need all services;
usually they need data storage services like postgres, redis, influx, and so on.
**Never write real secret values into the README.** This is a hard rule. Document only variable
*names* and descriptions, never their values. A `.env.example` (or `.sample`/`.dist`) file is
intended to be safe and may be read normally. A real `.env` file is not — do not read it to harvest
values, and never copy any value from it (or from any other source containing live credentials) into
the README. Even when a `.env.example` carries placeholder values, list only the variable name and
its purpose, not the placeholder, so a real secret can never leak through a file that was committed by
mistake. If you encounter what looks like a live secret, mask it (e.g. `API_KEY=<your-api-key>`) and
flag it to the user rather than reproducing it.

Check for environment variable usage:
- Look for a `.env.example`, `.env.sample`, or `.env.dist` file — if found, list every variable it defines and explain its purpose (names only, not values, per the rule above).
- If no example file exists, grep the codebase for `os.environ`, `process.env`, `dotenv`, `getenv`, or similar patterns to discover what variables are expected.
- If any `.env`-related variables are found, instruct the reader to copy the example file (`cp .env.example .env`) and fill in their own values.
- Note which variables are required vs. optional, and flag any that need secrets (API keys, database passwords) so the reader knows not to commit them.

### Step 6: Write or update models section

If the project has a database, write a section that describes the models used in the project.
For each model include:
- The model name and which data store it lives in (e.g. PostgreSQL table, MongoDB collection, Redis key)
- A one-sentence description of its purpose
- Its key fields: name, type, and a short description — focus on fields that are non-obvious or important
  to understand the data shape; omit boilerplate fields like `id`, `created_at`, `updated_at` unless they
  carry domain significance
- Any notable relationships to other models (foreign keys, embedded documents, references)

If the project uses migrations, note where the migration files are located.

### Step 7: Write or update API section

If the project has an API, write a section that describes the API endpoints and how to use them.
For each endpoint include:
- HTTP method and path (e.g. `POST /api/users`)
- A one-sentence description of what it does
- Request parameters or body shape (required fields, types)
- Response shape (key fields returned, status codes)
- A short example request using `curl` or a similar tool

If there are many endpoints, group them by resource (e.g. Users, Orders) and document the most important ones;
note where the reader can find the full list.

Check for a Swagger/OpenAPI file or a documentation page for the API. If one exists, write a short note on how
to access it (e.g. "run the main service and browse to `http://localhost:8000/docs`") and refer the reader there
for the complete reference instead of duplicating all endpoints manually.

### Step 8: Write or update tests section

If the project has tests, explain how to run them.
Use bash formatting for the commands.
Example:
```bash
python manage.py test
```
If a CI/CD config was found in Step 3, mention how to run the same checks locally.
If no tests are found, skip this section entirely — do not add a note saying the project has no tests.

### Step 9: Write or update contributing section

If there are contribution guidelines, write a section that describes how to contribute to the project.
Otherwise, use the decision collected in Step 1:
- If the user said yes, write a section that covers: branch naming conventions, how to open a pull request, code style
  requirements, and how to run tests before submitting.
- If the user said no, skip this section and move on to Step 10.

### Step 10: Write or update license section

Check for a LICENSE or LICENSE.md file. If present, add a short license section at the bottom of the README
that names the license and links to the file.
If no license file exists, use the decision collected in Step 1: if the user said yes, prompt them for the
license type, create the LICENSE file, and add the section. If they said no, skip this section.

### Step 11: Write or update changelog section

If a CHANGELOG.md, CHANGELOG, HISTORY.md, or RELEASES.md file exists, add a brief note in the README linking
to it so readers know where to find version history.
