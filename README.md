
# UE5-Build-Project

This GitHub Action is designed to cook, stage, and package projects for Unreal Engine. It provides a streamlined and configurable way to automate the preparation of your Unreal Engine projects for distribution.

## How it Works

The action wraps the `RunUAT.bat` script provided by Unreal Engine, allowing you to specify various options such as whether to build, cook, stage, package, create .pak files, or include the server in your builds.

## Inputs

- `RUNUAT_PATH`: The path to your `RunUAT.bat` file. This is typically found in the `Engine/Build/BatchFiles` directory of your Unreal Engine installation.
- `UPROJECT_PATH`: The full path to your Unreal Engine project `.uproject` file.
- `BUILD_CONFIG`: The build configuration to use, such as `Development` or `Shipping`.
- `PLATFORM`: The target platform for your build, such as `Win64` or `Linux`.
- `COOK`: Set to `true` if the cooking process should be included in the build process.
- `STAGE`: Set to `true` if you want to stage your project.
- `PACKAGE`: Set to `true` if the packaging process should be executed.
- `PAK`: Set to `true` if you want to create .pak files.
- `SERVER`: Set to `true` if you need to include a dedicated server in your build.

## Using the Action

To use this action in your workflow, include it as a step in your `.github/workflows/main.yml` file like so:

```yaml
- name: Cook, Stage & Package UE Project
  uses: OrchidIsle/UE5-Build-Project@latest
  with:
    RUNUAT_PATH: 'C:/Unreal Engine/UE5.3_Source/Engine/Build/BatchFiles/RunUAT.bat'
    UPROJECT_PATH: ${{ github.workspace }}/YourGameFolder/MyGame.uproject
    BUILD_CONFIG: Development
    PLATFORM: Win64
    COOK: true
    STAGE: true
    PACKAGE: false
    PAK: false
    SERVER: false
```

## Outputs

The action does not explicitly output any variables, as it is designed to perform actions rather than provide information. However, the success or failure of the build process can be used as a trigger for subsequent workflow steps.

## Typical Usage

This action can be used anytime you want to automate the preparation of your Unreal Engine project for distribution. It can be configured to match the needs of different environments such as development, testing, or production.

## Additional Information

-   Ensure that your Unreal Engine project is correctly set up for the desired build configuration and platform.
-   It's recommended to use the actions/checkout step before this action to clone the repository into the GitHub Actions runner.
-   Verify that the paths provided to the `RUNUAT_PATH` and `UPROJECT_PATH` inputs are correct and accessible within the GitHub Actions runner environment.
-   The action is designed for use with Unreal Engine projects and may not be suitable for other types of projects or build systems.

By integrating this action into your CI/CD pipeline, you can automate and streamline the process of getting your Unreal Engine project ready for distribution and testing.

