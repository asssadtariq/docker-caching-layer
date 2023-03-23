# Docker Layer Caching

<h2>What is Docker?</h2>
<p> Docker is a platform as a service that build, ship and run applications using containers. Containers are isolated process. Containers provides application-level virtualization. VMs take a lot of space most probably in gigabytes whereas containers take size in megabytes. Containers require very few resources in order to build, deploy, run and manage. </p>

<h2>What is Caching?</h2>
Caching is a process of storing frequently used data in way that it is quickly available to CPU or any application. However, in DevOps, Caching is a technique to improve the performance of applications and services.

<h2>Problems that occur without layer caching</h2>
When working with Docker, one of the most time-consuming parts of the process can be building and rebuilding your images. Each time you make a change, Docker has to re-execute all the steps in your Dockerfile, which can take a lot of time, especially if you have a complex image with many dependencies.

<h2>Possible solutions to improve build times</h2>

<ul>
<li>Multi-stage builds</li>
<li>Using smaller base images</li>
<li>Docker Layer Caching</li>
</ul>

<h2>Docker Layer Caching</h2>
One way to speed up your builds is by taking advantage of Docker's layer caching. Layer caching allows Docker to reuse layers from previous builds if they haven't changed, rather than executing the entire Dockerfile from scratch each time.
Docker layer caching mainly work with RUN, COPY, and ADD commands. RUN command allows to create a layer if the layer exist then the RUN command executes only once. COPY command inside Dockerfile allows to import one or more external files into a Docker image. Similarly, ADD command is used to import external files in Dockerfile.

<h2>What are Layers?</h2>
Layer in Docker is a file system that is read-only, each instruction in a Dockerfile is executed it results in the creation of a new layer.
Docker caches each layer separately, if one layer has been changed then Docker only rebuild that particular layer and the layers that are depended on it. 

<h2>How Does Layer Caching Work?</h2>
When you build a Docker image, Docker uses the cached layers from previous builds, as long as they haven't changed. This means that if you have a Dockerfile with several dependencies that don't change frequently, Docker can reuse those layers across multiple builds, greatly reducing the time it takes to build your image.
However, if any layer has changed, Docker will rebuild that layer and any layers that depend on it. This ensures that your image is up to date with any changes you've made.

To take advantage of layer caching, it's important to structure your Dockerfile in a way that takes advantage of layers. For example,
<ul>
<li>FROM xyz-base-image</li>
<li>RUN [run-command dependency-1 dependency-2 dependency-3 …]</li>
<li>COPY [copy-path]</li>
<li>CMD [cmd run command]</li>
</ul>

<ul>
<li>FROM python:3.9-slim-buster</li> 
<li>RUN pip install flask requests tensorflow</li>
<li>COPY app.py /app/</li> 
<li>CMD ["python", "/app/app.py"]</li>
</ul>

<ul>
<li>Version: N</li>
<li>Jobs:</li>
<li>Build_elixir</li>
<li>Machine:</li>
<li>	Image: any image</li>
<li>	Docker_layer_caching: true/false</li>
<li>Steps:</li>
<li>-----</li>
<li>-----</li>
</ul>

<h2>Conclusion</h2>
If you have a complex Dockerfile with many dependencies then Docker layer caching can greatly help you to speed up the builds. Structuring of Dockerfile in a way that takes advantage of layers, you can greatly reduce the time it takes to build the Dockerfile

<h2>References</h2>
https://circleci.com/blog/config-best-practices-docker-layer-caching/
https://medium.com/@asadtariq.at66/docker-layer-caching-2b1ea9132611
