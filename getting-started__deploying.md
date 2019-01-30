# Deploying

Installing your website for the first time is with OffbeatWP no different than with any other Wordpress + Theme. But for deploying ongoing work we advice you the following approach:

## 1. Have a GIT repository containing your OffbeatWP theme.

## 2. Setup an automated tool like Jenkins, Gitlab CI or DeployHQ to handle the deployment process for you.

On a regular project we have a script like this in our deployment tool (deployment tool handles ssh connection):

```
cd {$theme-folder-of-your-website}
git pull
composer install
yarn install
yarn offbeatwp production
rm -rf ../../cache/twig/*
```

### Explanation per line:
1. `cd {$theme-folder-of-your-website}`
Getting into your theme folder

2. `git pull`
Getting the latest content from the GIT

3. `composer install`
Updating composer packages based on the composer.lock in your theme

4. `yarn offbeatwp production`
Updating npm packages based on the yarn.lock in your theme

5. `rm -rf ../../cache/twig/*`
Clearing the Twig compiled files  

## 3. Run deployment (semi-)automatically on commit to a specific branch or pushing a "build/deploy" button in your deployment tool.

