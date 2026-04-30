*NOTE:* Nest aims to be a platform-agnostic framework. => the core application logic is decoupled from the underlying HTTP server, allowing developers to switch between platforms like `Express` or `Fastify` without changing business code.

### Nest Factory
**Decorators**
    - Decorators are fn's -> that can be applied to classes, methods and parameters
    - Decorators can take arguments to control behaviour of on what it is applied (classesm methods, parameters)
**Modules**
    - Every Nest Js App has a root module, that module can depend on other modules and in turn they depend on others.
    - App module -> Root module
**Controllers**
    - Without the controller app can't handle any incoming requests
    - Controller has methods to handle requests e.g findAll, create
**Services**
    - Business logic of the modules resides here, e.g database calls and interaction

Questions : 
1. What are linters and formatter => Eslint and Prettier tbp
2. To speed up the development process (x20 times faster builds), you can use the SWC builder by passing the -b swc flag to the start script, as follows npm run start -- -b swc.  => Why use SWC ? What is it ?
3. What is decorators ?
4. Why is classes used ?