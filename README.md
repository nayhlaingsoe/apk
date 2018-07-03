# apk
snc
language: android 
jdk: 
  - oraclejdk8 
android: 
  components: 
    - tools 
    - build-tools-24.0.0 
    - android-24 
    - Extra-android-support 
    - extra-google-google_play_services 
    - extra-android-m2repository 
    - extra-google-m2repository 
    - addon-google_apis-google-24 
BEFORE_INSTALL: 
- ​​chmod + x gradlew 
- export JAVA8_HOME = / usr / lib / jvm / java-8-oracle 
- export JAVA_HOME = $ JAVA8_HOME 
after_success: 
- chmod + x ./upload-gh-pages. sh 
- ./upload-apk.sh 
script: 
- ./gradlew build
#create the new directory will contain que October generated apk
  mkdir $ HOME / buildApk / 
  #copy generated apk from build folder to the folder just created
  cp -R app / build / outputs / apk / app-debug.apk $ HOME / android / 
  #go to home and git setup  
  cd $ HOME 
  git config --global user.email "useremail@domain.com" 
  git config --global user.name "Your Name" 
  # Clone the repository in the folder buildApk
  git clone --quiet --branch master = https: // user-name: $GITHUB_API_KEY@github.com/user-name/repo-name master> / dev / null 
  #go into directory and copy data we're interested
  cd master cp -Rf $ HOME / android / *. 
  #add, commit and push files
  git add -f. 
  git remote rm origin 
  git remote add origin https: // user-name: $GITHUB_API_KEY@github.com/user-name/repo-name.git
   . git add -f 
  git commit -m "Travis build $ TRAVIS_BUILD_NUMBER pushed [skip ci] " 
  git push origin master -fq> / dev / null 
  echo -e" Done \ n "
