# pnpm monorepo for multiple cdk apps.

## Create a new app

1. mkdir src/apps/<app-name>
2. cd src/apps/<app-name>
3. pnpm cdk init --language=typescript
4. delete the tsconfig.json file
5. cd ../../..

## Complete Process to Build, Synth and Deploy CDK App

Build

- `pnpm tsc -noEmit && pnpm esbuild --bundle --platform=node src/apps/app-1/bin/app-1.ts --outdir=src/apps/app-1/dist`

- `pnpm tsc -noEmit && pnpm esbuild --bundle --platform=node src/apps/app-2/bin/app-2.ts --outdir=src/apps/app-2/dist`

- TODO: - use build scripts per app: https://esbuild.github.io/getting-started/#build-scripts

Synth

- `pnpm cdk synth -a src/apps/app-1/dist/app-1.js -o cloud-assembly/app-1`
- `pnpm cdk synth -a src/apps/app-2/dist/app-2.js -o cloud-assembly/app-2`

Deploy

- `pnpm cdk deploy -a cloud-assembly/app-1 --all`
- `pnpm cdk deploy -a cloud-assembly/app-2 --all`

Destroy

- `pnpm cdk destroy -a cloud-assembly/app-1 --all`
- `pnpm cdk destroy -a cloud-assembly/app-2 --all`

DOES THIS WORK WITH CACHED VALUES IN cdk.json?
