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
azure site create [name] --git
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







