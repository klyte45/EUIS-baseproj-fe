# Basic Single SPA project for EUIS

## Instructions

- Clone this repository
- In `package.json`, change the field `name` to `@<modderID>/<projectID>`. Use this name when registering your app in the EUIS. Both just can have lowercase letters, numbers and hyphens; `<modderID>` must be 3-10 letters long and `<projectID>` must be 3-30 letters long.
  - **NOTE:** The `<projectID>` will always start with the mod acronym defined in the `IEUISAppRegister` implementation that will load this app, plus an hyphen (`-`).
  After this, any name matching the the constraints above are allowed. Ex: `xy-main` will be valid for a mod with acronym `xy`, as well `xy-30-letters-and-numbers-name`, but `main-xy`, `main` and `xy-main/123` won't.
- Install the project using `npm i`

## Testing the application for development

The application to be registered in C# side must implement `IEUISModRegister` (one class each mod) to register the delegates which will bind the events from/to the mod backend, and `IEUISAppRegister` (one class each application) with informations specifics to the current application, like name and files to load explained right below.

Configure the registration for EUIS (field `UrlJs`) to point to `http://localhost:8500/<modderID>-<projectID>.js`. Do the same for `UrlCss` pointing to `http://localhost:8500/<modderID>-<projectID>.css`. Then, the EUIS screen will load searching by the file there.
The icon in the EUIS taskbar must be defined at `UrlIcon`, and the application display name must be set at `DisplayName` field.

Run the project using `npm start -- --port 8500` to serve the packed project in that place. Be sure to keep a button in the app screen to reload the page while in development mode.

## Building the application

Use the command `npm run build:webpack` to generate the bundled js file to `dist/` folder. Don't forget packing it along when distributing the application. As well, you will need to change both `UrlJs` and `UrlCss` in EUIS registration to point the bundled JS/CSS instead of the localhost.

## Note about css

This basic project is setted up to support SCSS. You may change this by following the instructions of Webpack for other css processors.

The EUIS isolates the css by each application, and ignores any styles not set in the url set in `UrlCss` field. So you might need to copy shared styles between projects if necessary.

Don't forget importing all css files into your react files. Only linked css files are bundled by Webpack.