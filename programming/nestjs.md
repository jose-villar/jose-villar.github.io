# NestJS

## Installation

```.sh
sudo npm i -g @nestjs/cli
```

## Initialization

```.sh
nest new project-name

# Create a new TypeScript project with stricter feature set
nest --strict new project-name
```

## Running the app

```.sh
# To speed up the development process (x20 times faster builds), you can use
# the SWC builder by passing the -b swc flag to the start script, as follows
npm run start -- -b swc

# To watch for changes in your files
npm run start:dev -- -b swc

```

## Commands

- `nest g resource` command not only generates all the NestJS building blocks
  (module, service, controller classes) but also an entity class, DTO classes as
  well as the testing (.spec) files.

```.sh
nest g resource
```
