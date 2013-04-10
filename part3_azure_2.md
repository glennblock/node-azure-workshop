# Deploying node.js applications to Windows Azure Websites

## What are Azure Websites
A website is an application container in Windows Azure for running your code. The way it works is you create a website and then deploy your application to it. Windows Azure then takes care of hosting your app in the cloud, allowing it to scale, etc.
 
Azure Websites have some really nice benefits for node development

* Cheap - 10 free sites out of the box
* Fast - Deploy really quickly using git, github, mercurial, dropbox or FTP!
* Scalable - Easily scale up number of instances and underlying hardware
* Great for node
	* Fully supports hosting node apps
	* Downloads npm packages on the fly
	* Streaming of node output logs
	* Debugging support

	
## Deploying your first app - Express

### Create an express app
```bash
npm install express -g
express
```

### Create a Website to deploy with git
```bash
azure site create *site* --git
```
This automatically provisions a new Website and creates a local git repo

### Deploy your website
```bash
git add .
git commit -am "first commit"
git push azure master
```

### View the app
```bash
azure site browse
```

### Make an edit
Go update one of the files like the index.jade file
```bash
git commit -am "another update"
git push azure master
azure site browse
```

### List sites
```bash
azure site list
```

### Delete sites
```bash
azure site delete [site]
```
### Show site details
```bash
azure site show [site]
```

## Github deployment (supports SSH)
Create a site that is connecting to a github repo
```bash
azure site create *site* --github
```
This will create a website that is linked to a github repo. Every time you push to github the site will be updated.

## Debugging

### Configuring
* Edit your iisnode.yml and set "koggingEnabled" and "devErrorsEnabled" to true.
* Make an error in your code like requiring a module that does not exist.

### Commit and browse to see debugger errors

```bash
git commit -am "setting debug"
git push azure master
azure site browse
```

### Stream the output
```bash
azure site log tail
```

## Managing deployments
### List out your deployments
```bash
azure site deployment list
```

### Redeploy
```bash
azure site deployment redeploy *deployment_id*
```

## Configuring environment variables
You can use the CLI to set environment variables which instantly propagate to your app. Very useful for staging / production like settings which you don't want hard coded.

Make a change in your index.jade to display a "foo" environment variable i.e.

```jade
#{process.env.foo}
```

### Commit

```bash
git commit -am "adding env"
git push azure master
```

### Set the environment var

```bash
azure site config add foo=bar
```

### View the site

```bash
azure site browse
```
