# UI5 task for indexing cachebuster files
 UI5 Tooling Task that for indexing files to enable the cachebuster directly into the dist folder

## Install

```bash
npm install ui5-task-cachebuster-indexing --save-dev
```

## Configuration options (in `$yourapp/ui5.yaml`)

- debug: `true|false`  
  verbose logging

## Usage

1. Define the dependency in `$yourapp/package.json`:

```json
"devDependencies": {
    // ...
    "ui5-task-cachebuster-indexing": "*"
    // ...
},
"ui5": {
  "dependencies": [
    // ...
    "ui5-task-cachebuster-indexing",
    // ...
  ]
}
```

> As the devDependencies are not recognized by the UI5 tooling, they need to be listed in the `ui5 > dependencies` array. In addition, once using the `ui5 > dependencies` array you need to list all UI5 tooling relevant dependencies.

2. configure it in `$yourapp/ui5.yaml`:

```yaml
builder:
  customTasks:
  - name: ui5-task-cachebuster-indexing
    afterTask: generateVersionInfo
    configuration:
      debug: true
```

## How it works

The task will run the default generate cachebuster info task and make a clone of all resources with the timestamp from the cachebuster info in the path. This will generate the resources with a path that can be found by the cachebuster. 

Example path: 

It is not needed to run the "generateCachebusterInfo" task as this already done inside this one. Nevertheless, this task should always be executed after the cachebuster info generation "generateCachebusterInfo".

## Known limitations

only works with timestamp