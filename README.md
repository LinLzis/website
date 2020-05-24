# Serverless Plus Website

This website is built using [Docusaurus 2](https://v2.docusaurus.io/), a modern static website generator.

### Installation

```bash
$ yarn
```

### Local Development

```bash
$ yarn start
```

This command starts a local development server and open up a browser window. Most changes are reflected live without having to restart the server.

### Build

```bash
$ yarn build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

### Deployment

```bash
$ sls deploy
```

> Notice: If you don't want to scan QR code, you can setup credentials for Tencent Cloud in `.env` file like `.env.example`.

### Continuous Integration

Some common defaults for linting/formatting have been set for you. If you integrate your project with an open source Continuous Integration system (e.g. Travis CI, CircleCI), you may check for issues using the following command.

```bash
$ yarn ci
```

### CDN Refresh

Copy `cdn/serverless.example.yml` to `cdn/serverless.yml`, and change it to your Tencent CDN Domain, then run:

```bash
$ yarn cdn:refresh
```

### License

MIT License

Copyright (c) 2020 Serverless Plus
