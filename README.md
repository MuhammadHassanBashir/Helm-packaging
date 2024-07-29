# Helm-packaging

## Duplicating Helm Charts for etcd and Redis from Bitnami to Your Own GitHub Repository

### Introduction
This guide will help you duplicate the etcd and Redis Helm charts from Bitnami to your own GitHub repository. You will learn how to download, modify, package, and host the charts using GitHub Pages.

### Prerequisites
Helm installed on your local machine.
A GitHub account and a repository where you will host the Helm charts.
Steps
Step 1: Download the Helm Charts
Add the Bitnami Helm repository:

    
    helm repo add bitnami https://charts.bitnami.com/bitnami
    Download and unpack the etcd and Redis charts:

    
    helm pull bitnami/etcd --untar
    helm pull bitnami/redis --untar
    
This will create directories named etcd and redis containing the Helm charts.

Step 2: Modify the Charts
Navigate to the etcd directory and edit the values.yaml file as needed:


    cd etcd
    nano values.yaml

Navigate to the redis directory and edit the values.yaml file as needed:


    cd ../redis
    nano values.yaml

Make any other necessary modifications to the chart templates or metadata.

    Step 3: Create Your Own Helm Repository
    Using GitHub Pages to Host Your Helm Repository
    Create a GitHub repository to host your Helm charts.

Package the Helm charts:


    helm package etcd
    helm package redis

This will create .tgz files for the charts in the current directory.

Create an index.yaml file for your repository:


    helm repo index . --url https://<your-github-username>.github.io/<your-repo-name>   or you can use repo https URL. 

Replace <your-github-username> and <your-repo-name> with your GitHub username and repository name, respectively. This will generate an index.yaml file in the current directory.

Initialize a Git repository and push the packaged charts and index.yaml to GitHub:

    git init
    git remote add origin https://github.com/<your-github-username>/<your-repo-name>.git
    git add .
    git commit -m "Add etcd and redis Helm charts"
    git push -u origin master

Set up GitHub Pages for your repository:

    Go to your repository on GitHub.
    Click on "Settings".
    Scroll down to "GitHub Pages".
    Select the source branch and folder (e.g., main branch and /docs folder(by selecting this you will be notifing that our one page is live)).
    Verify that the index.yaml file is accessible via your browser by visiting:


    https://<your-github-username>.github.io/<your-repo-name>/index.yaml

Step 4: Use Your Helm Repository
Add your Helm repository:


    helm repo add myrepo https://<your-github-username>.github.io/<your-repo-name>  or you can use repo https URL. 
    helm repo update

Install the etcd and Redis charts from your repository:


    helm install my-etcd myrepo/etcd
    helm install my-redis myrepo/redis

Summary
These steps will help you duplicate the etcd and Redis Helm charts from Bitnami to your own repository. You'll download the charts, make any necessary modifications, create a Helm repository using GitHub Pages, and then use your repository to install the charts.

By following this guide, you can easily manage and customize your own versions of the etcd and Redis Helm charts.

Feel free to copy and use this document for creating a GitHub repository and hosting your customized Helm charts. Let me know if you need any further adjustments!
