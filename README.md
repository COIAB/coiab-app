# CoiabApp

Aplicativo da Coordenação das Organizações Indígenas da Amazônia Brasileira
(COIAB) para coleta de dados territoriais indígenas, desenvolvido pela Transistir.
CoiabApp é o nome provisório do projeto, também referido como Kutary e Ekanâdyby.

## Base tecnológica: CoMapeo

Este aplicativo é uma versão derivada do software livre
[CoMapeo Mobile](https://github.com/digidem/comapeo-mobile), do projeto
[CoMapeo](https://comapeo.app/). As adaptações para a COIAB incluem identidade
visual, navegação, uma camada de organizações com áreas de Monitoramento e
Alertas, e informações de etnia e aldeia no cadastro e nos metadados das
observações. O núcleo de dados e colaboração utiliza os componentes do CoMapeo.

O desenvolvimento é acompanhado em
[transistir/coiab-app](https://github.com/transistir/coiab-app); o repositório
institucional é [COIAB/coiab-app](https://github.com/COIAB/coiab-app).
Consulte [LICENSE](./LICENSE) para a licença GNU GPL v3 e preserve os avisos
aplicáveis ao projeto original e às suas dependências.

Para gerar e obter um APK, consulte [docs/ApkBuild.md](./docs/ApkBuild.md).
As instruções técnicas abaixo são mantidas a partir da documentação do CoMapeo;
use o repositório e a revisão correspondentes à versão que pretende executar.

## Getting started

1. Clone repository

   ```sh
   git clone https://github.com/COIAB/coiab-app.git
   ```

2. Set up the development environment
   1. Install [Node](https://nodejs.org), ideally through a proper node version manager such as [nvm](https://github.com/nvm-sh/nvm), [fnm](https://github.com/Schniz/fnm), [asdf](https://asdf-vm.com/), or [mise](https://mise.jdx.dev/)
      - This project uses **Node v24.13.0+** with **npm v11.6.2** (LTS)

   2. Follow the React Native instructions for setting up the development environment: https://reactnative.dev/docs/environment-setup
      - Note that **Java 17** is the minimum version required for this project.

      - When setting up the Android-specific tooling, you will also need to install the [Android NDK](https://developer.android.com/ndk/). This can be installed using Android Studio by going to the `SDK Tools` tab in the `SDK Manager`. This project uses **NDK 26.1.10909125**.

   3. Copy the [`.env.template`](./.env.template) file to a file called `.env`. Replace any placeholder `<replace_me>` values with the relevant ones:

      `MAPBOX_ACCESS_TOKEN`: a [Mapbox access token](https://docs.mapbox.com/android/maps/guides/install/#configure-credentials). If you do not have access to a Mapbox account, reach out to the maintainers about getting access to an access token.

      `COMAPEO_METRICS_URL`: URL pointing to a hosted CoMapeo metrics server. Reach out to the maintainers about getting access to this credential.
      `COMAPEO_METRICS_API_KEY`: API key needed for accessing a CoMapeo metrics server. Reach out to the maintainers about getting access to this credential.

3. To enable Sentry source map uploads from the backend when developing locally, create a file `.env.sentry-build-plugin` with a `SENTRY_AUTH_TOKEN`. This is only necessary when trying to debug source map uploads.

4. Run the app locally
   1. Install dependencies
      - This project requires the following system dependencies. Make sure they are available on your `PATH`.
        - curl
        - tar

      - Install NPM-based project dependencies

        ```sh
        npm install
        ```

   2. Generate the native code
      - This project uses [Expo Prebuild](https://docs.expo.dev/workflow/prebuild/) for generating the relevant native code. If you update [`app.json`](./app.json) or [`app.config.js`](./app.config.js), or install/update any dependencies that provide native code, you should run the following command to make sure the project is up-to-date:

      ```sh
      npx expo prebuild
      ```

      If you have made any manual changes to the generated directories (e.g. `android/` or `ios/`), you may need to specify the `--clean` flag with the command.

   3. Start the Metro bundler process

      ```sh
      npm start
      ```

      Leave this running in a separate terminal window.

   4. Build and run the app (Android)
      - For this project, using a physical device is more convenient and reliable to work with. It is recommended that you follow React Native's [setup instructions](https://reactnative.dev/docs/running-on-device) for running an app on a device.

      - Run the following command to build and run the Android app with Expo:

        ```sh
        npm run android
        ```

   5. Build and install on a physical iOS device
      - To build a standalone, offline-capable build and install it directly onto a connected iPhone (e.g. for field testing without Metro), see [docs/iOSDeviceBuilds.md](./docs/iOSDeviceBuilds.md).

## Ethos and Guidelines

[See documentation](./docs/EthosAndGuidelines.md)

## E2E Testing

This project is tested with BrowserStack.
