# Deploy Godot Game Action

|[Website](https://appsinacup.com)|[Discord](https://discord.gg/56dMud8HYn)|
|-|-|

![example](docs/example.png)

Reusable Action that deploys a Godot game. This action deploys a game already built using [appsinacup/action_export_godot_game](https://github.com/appsinacup/action_export_godot_game). The resulting build needs to be uploaded as an artifact.

This action can deploy to:
- itch.io
- Play Store
- iOS App Store
- macOS App Store
- Steam

For instructions on how to generate the secrets, go to the [appsinacup/action_export_godot_game](https://github.com/appsinacup/action_export_godot_game) repo.

## Usage

- Itchio Deploy:

```yml
deploy-itchio:
    uses: appsinacup/action_deploy_godot_game/.github/workflows/deploy-itchio.yml@main
    strategy:
        fail-fast: false
        max-parallel: 1
        matrix:
            artifact-name: ["Linux x86_64", "Linux x86_32", "Web", "macOS", "Windows Desktop x86_64", "Windows Desktop x86_32", "Windows Desktop arm64"]
    with:
        artifact-name: ${{ matrix.artifact-name }}
        itchio-game: itch-game-name
        itchio-username: itch-username
    secrets:
        butler-credentials: ${{ secrets.BUTLER_CREDENTIALS }}
```

- Android Deploy:

```yml
deploy-android:
    uses: appsinacup/action_deploy_godot_game/.github/workflows/deploy-android.yml@main
    with:
        artifact-name: Android
        android-package: com.example.game
        game-name: GameName
    secrets:
        service-account-json-base64: ${{ secrets.SERVICE_ACCOUNT_JSON_BASE64 }}
```

- iOS Deploy:

```yml
deploy-ios:
    uses: appsinacup/action_deploy_godot_game/.github/workflows/deploy-ios.yml@main
    with:
        artifact-name: iOS-apple-store
        game-name: GameName
    secrets:
        apple-id: ${{ secrets.APPLE_ID }}
        app-specific-password: ${{ secrets.APP_SPECIFIC_PASSWORD }}
```

- macOS Deploy:

```yml
deploy-macos:
    uses: appsinacup/action_deploy_godot_game/.github/workflows/deploy-macos.yml@main
    with:
        artifact-name: macOS
        game-name: GameName
        macos-package: com.example.game
    secrets:
        apple-id: ${{ secrets.APPLE_ID }}
        apple-team-id: ${{ secrets.APPLE_TEAM_ID }}
        app-specific-password: ${{ secrets.APP_SPECIFIC_PASSWORD }}
        deploy-certificate-base64: ${{ secrets.BUILD_CERTIFICATE_BASE64 }}
        install-certificate-base64: ${{ secrets.INSTALL_CERTIFICATE_BASE64 }}
        p12-password: ${{ secrets.P12_PASSWORD }}
        deploy-provisioning-profile-mac-base64: ${{ secrets.DEPLOY_PROVISION_PROFILE_MAC_BASE64 }}
        keychain-password: ${{ secrets.KEYCHAIN_PASSWORD }}
```

- Steam Deploy:

```yml
deploy-steam:
    uses: appsinacup/action_deploy_godot_game/.github/workflows/deploy-steam.yml@main
    with:
        game-version: 1.0
        steam-win64-depot-id: 123456
        steam-win32-depot-id: 123457
        steam-linux64-depot-id: 123458
        steam-linux32-depot-id: 123459
        steam-mac-depot-id: 123460
        steam-app-id: 123455
    secrets:
        steam-username: ${{ secrets.STEAM_USERNAME }}
        steam-password: ${{ secrets.STEAM_PASSWORD }}
        steam-shared-secret: ${{ secrets.STEAM_SHARED_SECRET }}
```
