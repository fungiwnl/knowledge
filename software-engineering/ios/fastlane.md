# Fastlane

Fastlane is an open resource toolchain that simplifies both Android and iOS deployment. In particular, it provides the great benefit of simplying codesigning for iOS, which has historically been a personal pain to manage with CI platforms that don't do all the work for you (i.e buddybuild, bitrise). 


## Pre-requiresites 

- Apple developer account 


## Set up

- Appfile

- Fastfile

- Matchfile 

  

## Match 

- Git repo

- --readonly flag for CI 

  

## Import existing certificates 

```bash
fastlane match import \
    --username example@email.com \
    --git_url git@bitbucket.org:example/example-fastlane.git \
    --app_identifier com.brianfung.example \
    --team_name "Brian Fung" \
    --type appstore 
```



## Testflight deployment

```bash
fastlane pilot upload --username "$FASTLANE_APPLE_LOGIN" --ipa "myapp.ipa"
```



## Resources

- The [official documentation]([https://docs.fastlane.tools/getting-started/ios/setup/) for fastlane is clear and concise and a good resource worth referencing 
