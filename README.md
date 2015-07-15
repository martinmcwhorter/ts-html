# ts-html
Type check JavaScript like expressions in HTML attributes against TypeScript

# Short Term Goals 
Validate types in Angular 1.x templates using  the TypeScript compiler service. 

# Long Term Goals
* Work with a variety of templating systems: Handlebars, Mustache, Jade, etc
* provide Gulp and Grunt wrappers. 
* support angular2 templates 

# Proposed Example
In `views/login.html`

    <!-- ts-html vm: LoginController -->
    <div>
        <input ng-model="vm.request.user" />
        <input ng-model="vm.request.password />
    </div>
    
In `LoginController.ts`

    export class LoginController() {
        
        public request: ILoginRequest = {};
    }
    
And we have a shared contract with a backend

    declare interface ILoginRequest {
        user: string;
        password: string;
    }

Now if we changed `user` in `ILoginRequest` to `userName` without updating the view, ts-html should report an error. Ideally we would have a watch running as part of the developers workflow and ts-html would be able to break builds in CI. 
