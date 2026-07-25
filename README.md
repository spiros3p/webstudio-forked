<section align="center">
  Webstudio is an Open Source Visual Development Platform for developers, designers, and cross-functional teams. You own the data, components, and infrastructure. You can use the hosted version or roll out your own.
</section>
<br /><br />

## Learning Resources

- [Blog](https://webstudio.is/blog)
- [Documentation](https://docs.webstudio.is/)
- [Brand and Product Design](https://docs.webstudio.is/contributing/contributing-for-designers)
- [Contributing Guide for Devs](https://docs.webstudio.is/contributing/contributing-for-developers)
- [Github Discussions](https://github.com/webstudio-is/webstudio-community/discussions)
- [Wishlist](https://github.com/webstudio-is/webstudio-community/discussions/categories/wishlist)
- [Builder Issues Tracker](https://github.com/webstudio-is/webstudio/issues)
- [Roadmap](https://github.com/orgs/webstudio-is/projects/11)

## Social Media

- [Twitter](https://twitter.com/getwebstudio)
- [Youtube](https://www.youtube.com/@getwebstudio)
- [Discord](https://wstd.us/community)

## Thanks

<a href="https://www.lost-pixel.com/"><img src="https://user-images.githubusercontent.com/29632358/168112844-77e76a0d-b96f-4bc8-b753-cd39f4afd428.png" width="50" height="50" alt="Lost Pixel" /></a>

Thanks to [Lost Pixel](https://www.lost-pixel.com/) for providing the visual testing platform that helps us review UI changes and catch visual regressions.

## License

- **Webstudio core** (all functionality in this repository) is free/open-source under AGPL-3.0-or-later.
- **sdk-components-animation** package (optional) is proprietary. You must accept the Webstudio, Inc. EULA located in [sdk-components-animation/LICENSE](./packages/sdk-components-animation/LICENSE) before using it.

## Custom instructions

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
- push apps/<project name> content to new repo
- in root level run `git submodule add -f <repo url> ./apps/<project dir>`
- push the changes to your parent repo's proejct branch

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
