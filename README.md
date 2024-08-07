# UE5-Build-Project

This GitHub Action, "UE5-Build-Project," is tailored for automating the build processes of Unreal Engine projects. It efficiently handles tasks such as cooking, staging, packaging, creating .pak files, and even archiving projects, offering a robust solution for developers looking to streamline their workflow.

## How it Works

The action leverages Unreal Engine's `RunUAT.bat` script, providing a flexible interface to configure various build aspects, including the ability to build, cook, stage, package, create .pak files, include a server, and archive the build output.

## Inputs

-   `RUNUAT_PATH`: Path to your `RunUAT.bat` file, typically in the `Engine/Build/BatchFiles` directory of your Unreal Engine installation.
-   `UPROJECT_PATH`: Full path to your Unreal Engine project `.uproject` file.
-   `BUILD_CONFIG`: Build configuration to use, e.g., `Development` or `Shipping`.
-   `PLATFORM`: Target platform for your build, such as `Win64` or `Linux`.
-   `CLEAN`: Set to `true` to have your project cleaned before rebuild (default: `false`).
-   `COOK`: Set to `true` to include cooking in the build process.
-   `STAGE`: Set to `true` to stage your project.
-   `PACKAGE`: Set to `true` to execute the packaging process.
-   `PAK`: Set to `true` to create .pak files.
-   `SERVER`: Set to `true` to include a dedicated server in your build.
-   `ARCHIVE`: Set to `true` to archive the build output.
-   `ARCHIVE_PATH`: Specify the path where the archive should be stored (used only if `ARCHIVE` is `true`).
-   `NULLRHI`: Set to `true` if you don't have a video output (i.e. a screen) such as when running this action in a container on the cloud (default: `false`).
-   `EDITOR` : Set to `true` to compile the editor as well. Useful for builds requiring editor functionality.
-   `ENCRYPT_INI`: Set to `true` to encrypt INI files.
-   `RELEASE`: Enter new release version number to create a release version.
-   `PATCH`: Enter the base release version number to generate a patch.
-   `MAPS`: Comma separated list of maps to build and package, leave empty to build all maps.
-   `DELETE_PDB`: Set to `true` to have any PDB files in the StagedBuilds directory purged (default: `false`).
-   `ANTICHEAT_ENABLED`: Set to `true` to enable anticheat functionality (default: `false`).
-   `ANTICHEAT_PRIVATE_KEY`: Base64 encoded private key for anticheat (required if `ANTICHEAT_ENABLED` is `true`).
-   `ANTICHEAT_PUBLIC_CERT`: Base64 encoded public certificate for anticheat (required if `ANTICHEAT_ENABLED` is `true`).

## Using the Action

Include this action in your workflow by adding it as a step in your `.github/workflows/main.yml` file:

```yaml
- name: Cook, Stage & Package UE Project
  uses: OrchidIsle/UE5-Build-Project@latest
  with:
    RUNUAT_PATH: 'C:/Unreal Engine/UE5.3_Source/Engine/Build/BatchFiles/RunUAT.bat'
    UPROJECT_PATH: ${{ github.workspace }}/YourGameFolder/MyGame.uproject
    BUILD_CONFIG: Development
    PLATFORM: Win64
    CLEAN: true
    COOK: true
    STAGE: true
    PACKAGE: false
    PAK: false
    SERVER: false
    ARCHIVE: false
    ARCHIVE_PATH: 'C:/Archives/MyGame'
    NULLRHI: true
    EDITOR: true
    ENCRYPT_INI: true
    RELEASE: '1.0.0'
    PATCH: '0.9.0'
    MAPS: 'Map1,Map2'
    DELETE_PDB: true
    ANTICHEAT_ENABLED: true
    ANTICHEAT_PRIVATE_KEY: 'base64encodedprivatekey'
    ANTICHEAT_PUBLIC_CERT: 'base64encodedpubliccert'
```

## Outputs

This action primarily executes build tasks and does not output variables. The success or failure of the build process can trigger subsequent workflow steps.

## Typical Usage

Use this action to automate your Unreal Engine project's preparation for various environments, including development, testing, or production.

## Additional Information

-   Ensure your Unreal Engine project is properly set up for the intended build configuration and platform.
-   Use the actions/checkout step before this action to clone your repository into the GitHub Actions runner.
-   Verify the accuracy and accessibility of paths provided to `RUNUAT_PATH` and `UPROJECT_PATH`.
-   Designed specifically for Unreal Engine projects; may not suit other project types or build systems.

Integrating this GitHub Action into your CI/CD pipeline automates the preparation of your Unreal Engine project for distribution and testing, enhancing efficiency and reliability.
