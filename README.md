#static-app-practable-io-ed-dev-ui-david
David's development repo

## Summary

The contents of this repo are mirrored on a google cloud instance `ed-dev-ui` that is dedicated to serving development versions of user interfaces for developers.

There are four directories that are accessible from the web: 

- `./ui` at `https://app.practable.io/ed-dev-ui/david/ui`
- `./config` at `https://app.practable.io/ed-dev-ui/david/config`
- `./images` at `https://app.practable.io/ed-dev-ui/david/images`
- `./info` at `https://app.practable.io/ed-dev-ui/david/info`

Any other directories are not accessible from the web - if you need an additional directory/routing let sysadmin know.

## Usage

In short: if you can `git push` then you can upload files to the new server. 

### Mechanism 

When you push to the `main` branch of this repo on Github, a webhook alerts `ed-dev-ui` to `git pull`. The new files should be ready almost immediately after the push completes.

### Procedure 

These instructions assume you clone all your repos to some directory we can call $SOURCES, and that you wish to add the `pvna-twoport-graphical-1.0` user interface.

- clone the repo 
     ```
    cd $SOURCES`
    git clone git@github.com:practable/static-app-practable-io-ed-dev-ui-david.git
    ```
- Prepare the UI files:
    - set the base path in `.env.production` to something like `VITE_BASE='/ed-dev-ui/david/ui/pvna-twoport-graphical-1.0/'`
    - `npm run build` to build the production version
    - copy the UI files in `./dist` to `$SOURCES/static-app-practable.io-ed-dev-ui-david/ui/pvna-twoport-graphical-1.0/` 
    - `git add all`
    - `git commit -m 'ui (feat): add pvna-twoport-graphical-1.0 files'`
    - `git push origin main`
- Check your work
    - Your files should now be available immediately on the server
    - go to the booking system at the link you've been given by the sysadmin
    - book out a kit
    - choose the graphical,DEVELOPER option, see how it goes....
- If your UI is ready for deployment on the main server:
    - fork https://github.com/practable/static-app-practable-io-ed0-default
    - rebuild ui with the basepath it will have on the main server
       `VITE_BASE='/ed0/static/ui/pvna-twoport-graphical-1.0/`
    - put the files from ./dist in the appropriate ./ui directory in `$SOURCES/static-app-practable-io-ed0-default/ui`
    - commit, and make a pull request.
       

## Extra details:

- There're some symbolic links behind the scenes to ensure the contents of the ui directory are served at app.practable.io/david/ui. Those links are in place for config, images, info, and ui. Any other directories you add to the repo will not be accessible from the web - if you need something added, just let me know and I can update the script that handles the git pull task. That script is separate for each user, so changes you make to your directory structure won't affect others. 
- Anytime you need a new ui added to the manifest so the booking system can offer it, just let sysadmin know the path and any other relevant details - but that should be you sorted for two-port vna for now.

## Benefits:

- This approach reduces admin work - just build the ui, copy the dist files to the repo, and push to github
- Minimises the blast radius of any issues with developers interacting with the instance because there is no direct access - probably something we'll equip the EO with though as a back up for me.
- All developers have their own repos, but I've left permission for all ui developers to access each other's repos for now, but let's revisit if this leaves anyone feeling exposed

## Other notes
Please leave the `index.html` file in the root directory - this is essential to the correct functioning of the server.`./ui` at `https://app.practable.io/ed-dev-ui/david/ui`

