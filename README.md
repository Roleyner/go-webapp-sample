## Dockerised go-webapp for Kubernetes deployment

In favor of implementing what there is in this repository, I based in [this one](https://github.com/ybkuroki/go-webapp-sample)

## Stack

1. **GitHub Action** as our GitOps - CI/CD tool.
2. **Docker** as our container solution.
3. **Kubectl** as our mechanism to deploy the application to our GKE cluster generated by Terraform.
4. **GO** as our programming language for the application.


*Explanation*:

- There's the go-webapp that easily can be run and tested by performing:
                                  `go run main.go`
- Once the command above gets performed, the web server starts to listen on **[::]:8080** and can be accesed through **http://localhost:8080** from your web browser.

- Credentials to log in are:
    **username**: `test`
    **password**: `test`

- Also, to be able to build and run the app on Docker, it's necessary to run the following:
    1. `docker build -t go-webapp .`
    2. `docker run --rm -p 8080:8080 go-webapp`


*GitOps CI/CD*:

- There are two files inside the **.github** directory which are in charge of generating the GitHub workflows within the GitHub repository.

- **CI** workflow gets automatically triggered either from *push to main branch* or *tag generated*. This part builds and pushes to GAR the go-webapp Docker image.

- **CD** workflow, unlike *CI* doesn't get automatically generated. Instead, it's gotta be manually triggered from the GutHub UI. This part deploys the latest *tag* created to the GKE cluster.