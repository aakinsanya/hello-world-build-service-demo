# hello-world-build-service-demo

An overly simplified use case showing the shortcomings of DockerFiles and the value of kpack/Tanzu Build Service.

Leverages the cartographer to stitch together a Continuous Delivery process.

Scenarios
1. Build image using good and bad docker file
2. Build image using TBS
2. Compare content using dive
3. Create supplychain using Cartographer
4. Try out Continuous Delivery with source code update
5. Update stack and watch your app get rebased

Useful links
https://cartographer.sh/docs/v0.6.0/
https://github.com/wagoodman/dive
https://paketo.io/docs/
https://github.com/vmware-tanzu/kpack-cli
https://github.com/pivotal/kpack
https://buildpacks.io/
https://fluxcd.io/flux/
