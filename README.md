# DynamicComponents

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.3.1.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

## Reference URL
https://developer.okta.com/blog/2021/12/08/angular-dynamic-components

### Add authentication
To begin with,  free Okta developer account, install the Okta CLI and run `okta register` to sign up for a new account.
 * macOS installation [https://cli.okta.com/manual/]
    1. `brew install --cask oktadeveloper/tap/okta` 
    2. To update to a new version:`brew reinstall okta`    
    3. To register : `okta register` , An account activation email has been sent to you.
    4. Bash / Zsh Completion, If you have “bash-completion” installed run one of the following commands:
        `okta generate-completion > /usr/local/etc/bash_completion.d/okta`
    5. run the following commands:
       `okta generate-completion > ~/okta.bash`
       `echo `. ~/okta.bash` >> ~/.bash_profile`
    6. if you would like to use an existing account, use `okta login` instead.
        An existing Okta Organization (https://dev-41109427.okta.com) was found in ../.okta/okta.yaml
        Overwrite configuration file? [Y/n]n
    7. Run `okta apps create --app-name dynamic-components`
    8. Use `http://localhost:4200/login/callback` for the Redirect URI and set the Logout 
        Redirect URI  to `http://localhost:4200`.
    
* Install okta package on angular app: `npm install @okta/okta-angular@4 @okta/okta-auth-js@5.8 --save`
    Open `srcs/app/app.module.ts` and create an OktaAuth instance by adding the following before the      
    NgModule and replacing the placeholders with the Issuer and Client ID from earlier.
    
* Next, add OktaAuthModule to the imports array and configure the provider for the OKTA_CONFIG token, as 
  shown : ` providers: [ { provide: OKTA_CONFIG, useValue: { oktaAuth } }]`

* Okta has a component for the login callback, but we need to add the route. Open src/app/app- 
   `routing.module.ts` and add the following to your routes array. 
   `{ path: 'login/callback', component: OktaCallbackComponent }`

* We also want to guard the Protected component route to authenticated users. Okta has a guard we can use. 
   Open `src/app/protected/protected-routing.module.ts` to add a `canActivate` guard to the default route. 
   Your routes array will look like the code snippet below.
   `const routes: Routes = [{ path: '', component: ProtectedComponent, canActivate: [OktaAuthGuard] }];`
