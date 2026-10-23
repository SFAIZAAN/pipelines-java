
# Run the web app with Docker

Docker builds the WAR inside a container, so Java and Maven do not need to be installed on your PC. Install and start Docker Desktop, then run these commands from the repository folder:

```powershell
docker build -t helloworld .
docker run --rm -p 8080:8080 helloworld
```

Open http://localhost:8080/ in your browser. Stop the server with Ctrl+C in the terminal.

# Deploy from Azure Pipelines

The pipeline tests the project, builds and pushes a Docker image, then deploys it to Azure App Service for Containers. Before running it:

1. Create an Azure Container Registry and a Linux Web App configured for a custom container. The web app needs an App Service plan that supports custom containers.
2. Enable the web app's system-assigned managed identity, grant it the **AcrPull** role on the container registry, and configure the web app to use that identity when pulling from the registry.
3. In Azure DevOps, create a Docker Registry service connection for the ACR and an Azure Resource Manager service connection with permission to deploy to the web app.
4. Update the service connection names, registry hostname, and web app name in `azure-pipelines.yml`. Authorize both service connections for the pipeline.
5. Push a change to `main` to build and deploy. Once the pipeline succeeds, browse to `https://<your-web-app-name>.azurewebsites.net/`.

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Legal Notices

Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all others rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
