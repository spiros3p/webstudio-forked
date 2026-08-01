# Instructions - Local Self Host

### Init builder locally

- open the repo in devcointainer (vscode extension)
- wait for the process to complete
- create `apps/builder/.env.development` and add:

```
DEV_LOGIN=true
AUTH_SECRET=my secret here
```

- run `pnpm dev`
- access `https://wstd.dev:5173/` locally (vite link encounters https issues)

### Create new project and serve it with Docker

- in the webstudio dashboard, create new project
- in the project, click "Share" button and provide builder permissions
- copy the link
- cd into `./apps/<project name dir>` (create it if not already exists)
- in the vs code terminal run `npx webstudio@0.267.0 link`
- paste the shared link in the prompt
- in the vs code terminal run `npx webstudio0.267.0 sync`
- in the webstudio UI project, click publish for the project
- in the vs code terminal run `npx webstudio0.267.0`
- choose docker
- all project app related files should be created inside your child directory

<hr>
***consider not uploading these files in the parent repo or branch***

- add to `.gitingore`

```
/apps/*
!/apps/builder
```

### Setup submodule

- create new github repo
- cd apps/<project-name>
- git init && git remote add origin <link> && git branch -M main && git add . && git commit -m "first commit" && git push -u origin main
- in root level run `git submodule add -f <repo url> ./apps/<project dir>`
- push the changes to your parent repo's project branch

### git submodule update workflow

```
cd <submodule_path>
# Make and push changes to the submodule
git add .
git commit -m "Update submodule"
git push

cd ..
# Update parent repository to point to the new submodule commit
git add <submodule_path>
git commit -m "Update submodule reference"
git push
```

### Webstudio builder project update workflow

- after completing modifications in the UI builder, click **PUBLISH**
- in the app repo, run `npx webstudio sync`, `npx webstudio --template docker`
- push your changes
