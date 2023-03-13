# Build & Release APK via Github Actions

## Usage
- To use this action simply create the YML file at this specified path at a root level. for example: `.github/workflows/android.yml`
- Copy paste the below YML in your YML file
- Provide the required Secrets (check below) and Environment variables (check below)
- After doing the above, whenever you are ready, make a commit from your Android Project to Github Repo
- Create and push the tag
- As soon as you push the tag this github action will be initiated and generated apk build will be released under releases with the same tag, which you can check in your github - code - releases

#### YML
```yml
name: Build & Publish Release APK

on:
  push:
    tags:
      - '*'

jobs:
  Gradle:
    runs-on: ubuntu-latest
    steps:
    - name: checkout code
      uses: actions/checkout@v2
    - name: setup jdk
      uses: actions/setup-java@v1
      with:
        java-version: 11
    - name: Make Gradle executable
      run: chmod +x ./gradlew
    - name: Build Release APK
      run: ./gradlew assembleRelease
    - name: Releasing using Hub
      uses: r0user/release-apk@main
      env:
       GITHUB_TOKEN: ${{ secrets.TOKEN }}
       APP_FOLDER: app
```
