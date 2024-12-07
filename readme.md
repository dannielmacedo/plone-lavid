# Install Plone 6.1 with Cookieplone
This template is the recommended way to start a new Plone project using the Volto frontend. It also includes tools for development and deployment.

## Prerequisites for installation
- Python 3.10, 3.11, or 3.12
- pipx 
- nvm
- Node.js LTS 20.x
- GNU make
- Git

`python3 --version`
> Python 3.12.3

### pipx
`sudo apt install pipx`

`pipx ensurepath`

### nvm / Node.js
`touch ~/.bash_profile`
`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.40.1/install.sh | bash`
`source ~/.bashrc`
`nvm install --lts`
`corepack enable`

### GNU Make
`sudo apt install make`

## Generate the project
`pipx run cookieplone project`
> Project Title (Project Title): Lavid
> Should we use prerelease versions? (No): Yes

## Install the project
`cd lavid`

`make install`

## Start Plone
Plone 6 has two servers: one for the frontend, and one for the backend. As such, we need to maintain two active shell sessions, one for each server, to start your Plone site.

### Start Backend
`make backend-start`

### Start Frontend
Create a second shell session in a new window. Change your current working directory to project-title. Start the Plone frontend with the following command.

`make frontend-start`

# Installing Volto Light Theme
Follow the steps below to install and configure VLT in your project. VLT provides a clean and modern design with ready-to-use blocks and components.

## Step 1: Install Volto Light Theme
To install VLT, navigate to the `frontend/packages/volto-lavid` folder and run the following command:
`pnpm install @kitconcept/volto-light-theme@6.0.0-alpha.3`

While in your project package folder, add VLT to the addons list in your package.json, as follows:
`"addons": ["@kitconcept/volto-light-theme"],`

## Step 2: install block add-ons
Volto Light Theme comes with several pre-configured add-ons that provide basic blocks for your website. If you'd like to include them, you can add them in the addons section in your package.json, but this is not required.

Here is the list of recommended addons to install, including VLT, which should be the last element:

```json
"addons": [
  "@eeacms/volto-accordion-block",
  "@kitconcept/volto-button-block",
  "@kitconcept/volto-heading-block",
  "@kitconcept/volto-highlight-block",
  "@kitconcept/volto-introduction-block",
  "@kitconcept/volto-separator-block",
  "@kitconcept/volto-slider-block",
  "@kitconcept/volto-light-theme"
],
```
## Step 3: configure Volto Light Theme as the theme provider
To leverage a cohesive set of styles, components, and design patterns that align with Volto's best practices, you need to set VLT as your theme provider.

Open the `volto.config.js` file in your frontend folder, and modify it as shown below.

```javascript
const addons = ['volto-project-title'];
const theme = '@kitconcept/volto-light-theme';

module.exports = {
  addons,
  theme
};
```

Install package requirements:
`make install`

Restart frontend:
`make start`

You'll need to restart your Plone frontend to see the changes.

# VLibras

## Install
Add `@plonegovbr/volto-vlibras` to your `package.json`:

```json
"addons": [
    "@plonegovbr/volto-vlibras"
],

"dependencies": {
    "@plonegovbr/volto-vlibras": "*"
}
```

Install package requirements:
`make install`

Restart frontend:
`make start`

## Configuration
To inject the component in the project add the appextras configuration in the `index.js` file.

A suggested way is to use appExtras from settings object (docs):

```javascript
import Libras from '@plonegovbr/volto-vlibras/components/Libras';

const applyConfig = (config) => {
  config.settings.appExtras = [
    ...config.settings.appExtras,
    {
      match: '',
      component: Libras,
    },
  ];
  return config;

};
```

