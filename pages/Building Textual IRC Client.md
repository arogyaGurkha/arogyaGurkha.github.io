# Building Textual IRC Client

[Textual](https://www.codeux.com/textual/) is often the most recommended IRC client for macOS. You can buy it for $7.99 or you can simply build it from source. Let us look at how to do exactly that.

# Prerequisites

Your mac needs to have Xcode 10.0 or newer.

## Cloning the source

Clone the source from `[https://github.com/Codeux-Software/Textual](https://github.com/Codeux-Software/Textual)` whereever you desire. Don't forget to download the submodules used by Textual. If submodules aren't downloaded, Xcode will give `the directory <directory> does not contain a xcode project` build error.

```bash
$ git clone https://github.com/Codeux-Software/Textual.git
$ cd Textual
$ git submodule update --init --recursive
```

## Setup code signing certificates

- Launch Keychain Access.app and use Certificate Assistance to Create a Certificate.

![Untitled](Building%20Textual%20IRC%20Client/Untitled.png)

- Enter your name, set Identity Type to "Self Signed Root" and set Certificate Type to "Code Signing" and create the certificate.

 

![Untitled](Building%20Textual%20IRC%20Client/Untitled%201.png)

- Your certificate should be visible in the "My Certificates" section of "login" Keychain

# Changing config files

You will need to change two files: `Code Signing Identity.xcconfig` and 

`Enabled Features.xcconfig`.

## Code Signing Identity configuration

- Open `Code Signing Identity.xcconfig` with a text editor of choice. It should be located at `Textual/Configurations/Build/`.
- For `CODE_SIGN_IDENTITY`, type the name that was used to create the Certificate above.
- Leave `DEVELOPMENT_TEAM`, `PROVISIONING_PROFILE_SPECIFIER` empty.

![Untitled](Building%20Textual%20IRC%20Client/Untitled%202.png)

## Enabled Features configuration

- Open `Enabled Features.xcconfig` with a text editor of choice. It should be located at `Textual/Configurations/Build/Standard Release/`.
- Set `TEXTUAL_BUILT_WITH_LICENSE_MANAGER` to 0. This prevents the trial period countdown.

![Untitled](Building%20Textual%20IRC%20Client/Untitled%203.png)

# Building Textual

Open Textual in Xcode by launching `Textual.xcworkspace` file in Textual root. Xcode will start indexing and processes source files. Once that is complete, follow these steps:

1. On your Xcode menu bar, click Product > Scheme and select **Textual (Standard Release).**
2. Similarly, click on Product > Build to start building the app. This should start the build process.

![Untitled](Building%20Textual%20IRC%20Client/Untitled%204.png)

1. Navigate to `Textual/Build Results/Release` and you should see a shiny new Textual.app. Drag this to your Applications folder.

You should now have a working Textual app with no trial countdown that you built yourself!