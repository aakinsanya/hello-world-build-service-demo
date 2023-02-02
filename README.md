# hello-world-build-service-demo

An overly simplified use case showing the shortcomings of DockerFiles and the value of kpack/Tanzu Build Service. **NOT FOR PRODUCTION USE!**

Uses the cartographer to stitch together a Continuous Delivery process. Source -> Build -> Deploy

#### Scenarios
1. Build image using the good and bad docker file. Compare sizes and content using dive
```
    docker build -t hello-world:1.0.0-BAD -f ./hello-world-dotnet/Dockerfile_BAD ./hello-world-dotnet
    docker build -t hello-world:1.0.0-GOOD -f ./hello-world-dotnet/Dockerfile_GOOD ./hello-world-dotnet
```
2. Build image using TBS
```
    kp image create hello-world-dotnet --tag <IMAGE REPO/IMAGENAME:TAG> --git <GIT_REPO> -n default
    kp build logs hello-world-dotnet
    docker image pull <IMAGE REPO/IMAGENAME:TAG>
```
2. Compare content using dive
```
    dive <IMAGE REPO/IMAGENAME:TAG>
```
3. Apply image manually and view running app
```
    kubectl apply -f ./k8s/manual/hello-world-deployment.yml
    kp image delete hello-world-dotnet
```
3. Create a supplychain using Cartographer and deploy workload
```
    kubectl apply -f ./k8s/cartographer/
```
4. Try out Continuous Delivery with source code update
5. Update stack and watch your app get rebased
```
    kp clusterstack update base --build-image registry.pivotal.io/tanzu-base-bionic-stack/build:1.2.40-base-cnb --run-image registry.pivotal.io/tanzu-base-bionic-stack/run:1.2.40-base-cnb
    
    kp build status hello-world
    
    kubectl get all
```

Please ensure that your default service account has your registry and git secrets mounted. Enjoy!

Useful links
1. https://cartographer.sh/docs/v0.6.0/
2. https://github.com/wagoodman/dive
3. https://paketo.io/docs/
4. https://github.com/vmware-tanzu/kpack-cli
5. https://github.com/pivotal/kpack
6. https://buildpacks.io/
7. https://fluxcd.io/flux/
