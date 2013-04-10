# Windows Azure and the Azure CLI
## Windows Azure
Windows Azure is Microsoft's cloud platform. At high level it provides two things:

### Compute
Deploy your application workloads to public / private cloud and let them run in Windows Azure. We support multiple models including:
* Infrastructure As a Service [IAAS] through Virtual Machines
* Platform As a Service [PAAS] via Web sites and Cloud Services
* Backend As a Service [BAAS] via Azure Mobile Services. Node is supported in ALL :-)

### Services
Capabilities provided by Windows Azure that you can use within your applications whether they are running on premise or in the cloud
* Storage Services (Tables, Blobs, SQL)
* Messaging (Queues and Service Bus)
* Media Services, CDN, etc.
* Add-ons, 3rd part services like MongoDB, Pusher

# Azure CLI
A cross platform command line tool for managing Windows Azure Compute and Services

![cli image](https://photos-4.dropbox.com/t/0/AAAEjk4FcKQ8lG7M6RlqqTfsCIWVD3bUxEGWbtaBFl8csA/12/6860088/png/32x32/3/_/1/2/cli.png/MVbb579GQQMggCN0G0evxWcsZ1BVvZr0P3pRpvQGOLU?size=1024x768)

## Installing
The azure-cli is available as an npm package.

```bash
sudo npm install azure-cli -g
```

## Test it out
```bash
azure
```

## Downloading your credentials (publishsettings)

```bash
azure account download
```

This will take you to the Azure portal to login and download a publish settings file.

## Importing credentials

```bash
azure account import [publishsettings]
```

You should change to the directory where the publishsettings file was downloaded. Once you have imported you are now ready to go work with Azure.

## Test it out

```bash
azure site list
azure vm list
azure sb namespace list
azure sql list
