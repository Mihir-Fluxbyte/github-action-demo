To create your own GitHub Action in TypeScript, start by setting up a new project with TypeScript and necessary dependencies. First, create a `package.json` file and install the required dependencies:

```bash
npm init -y
npm install typescript ts-node @types/node -D
```

Next, create a `tsconfig.json` file for TypeScript configuration. Now, create a `src` folder and an `index.ts` file inside it. This file will contain the main logic for your GitHub Action.

Install the `@actions/core` and `@actions/github` dependencies to interact with the GitHub Actions environment:

```bash
npm install @actions/core @actions/github
```

In the `src/index.ts` file, write your custom logic using the installed dependencies. For example, you can create a simple greeting action:

```ts
import { getInput } from "@actions/core";
const inputName = getInput("name");
greet(inputName);

function greet(name: string) {
  console.log(`Hello ${name}! You are running a GH Action!`);
}
```

Create an `action.yml` file in the project root to define your action's metadata and entry point:

```yaml
name: 'My Custom Action'
description: 'Custom GH action with TypeScript'
inputs:
  name:
    description: 'Name to greet'
    required: false
    default: 'GitHub User'
runs:
  using: 'node16'
  main: 'dist/index.js'
```

Finally, compile your TypeScript code and create a workflow file (`.github/workflows/test.yml`) to test your custom action:

```yaml
name: Test
on: push
jobs:
  run-action:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
          node-version: 16.x
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Run my action
        uses: ./
        with:
          name: 'GitHub User'
```

Now, when you push changes to your repository, the workflow will run and execute your custom GitHub Action ([Source 0](https://www.thisdot.co/blog/creating-your-own-github-action-with-typescript/)).