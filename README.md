# vault-csi-provider w/ kustomize
<div id="top"></div>

<!-- TABLE OF CONTENTS -->
<details open>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
        <li><a href="#configuration">Configuration</a></li>
      </ul>
    </li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>
</br>



<!-- ABOUT THE PROJECT -->
## About The Project
This project allows you to deploy [vault-csi-provider](https://github.com/hashicorp/vault-csi-provider) on Kubernetes with Kustomize binary.

<p align="right">(<a href="#top">back to top</a>)</p>


### Built With
* [Kubernetes](https://kubernetes.io/)
* [Kustomize](https://kustomize.io/)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

You need to have :
* An operational Kubernetes cluster
* Kustomize binary

### Installation
1. Clone the repo:
   ```sh
   git clone https://github.com/aamoyel/vault-csi-provider.git && cd vault-csi-provider
   ```
2. Create csi namespace:
   ```sh
   kubectl create ns csi
   ```
3. Deploy the project on your cluster
   ```sh
   kustomize build . | kubectl apply -f -
   ```

<p align="right">(<a href="#top">back to top</a>)</p>

### Configuration
To configure your vault kubernetes auth backend you need to have your cluster CA cert, your kubernetes api endpoint and a Reviewer JWT token.
1. First, get your Token Reviewer JWT:
   ```sh
   kubectl get secret -n kube-system vault-auth -o=jsonpath='{.data.token}' | base64 --decode
   ```
2. Get your kubernetes api url:
   ```sh
   kubectl config view --raw --minify --flatten -o=jsonpath='{.clusters[].cluster.server}'
   ```
3. Get your cluster CA certificate:
   ```sh
   kubectl config view --raw --minify --flatten -o=jsonpath='{.clusters[].cluster.certificate-authority-data}' | base64 --decode
   ```
4. Create your vault auth backend with previous information
5. Use the CSI Provider with this examples: https://www.vaultproject.io/docs/platform/k8s/csi/examples

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- CONTACT -->
## Contact

Alan Amoyel - [@AlanAmoyel](https://twitter.com/AlanAmoyel)

Project Link: [https://github.com/aamoyel/vault-csi-provider](https://github.com/aamoyel/vault-csi-provider)

<p align="right">(<a href="#top">back to top</a>)</p>
