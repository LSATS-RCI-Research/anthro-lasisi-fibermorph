# OpenShift Deployment

The following instructions will guide you through deploying the FiberMorph Streamlit application on an OpenShift cluster.
This includes building the docker image, pushing it to DockerHub, and creating the necessary OpenShift resources.

In the future, a GitHub Action workflow will be added to automate the process of building, pushing, and deploying the
application whenever a yet-to-be-determined tag or release is created.

## OpenShift Setup
- Create a new project in OpenShift for the FiberMorph application.
- Create a Secret named `dockerhub-pull` with the lsatsrciresearch team DockerHub pull credentials (available in passwordstate). This will allow OpenShift to pull the image from DockerHub.

## Build and Push Docker Image
1. Build the Docker image locally:
   ```bash
   docker build --tag lsatsrciresearch/fibermorph:latest .
   ```
2. Push the Docker image to DockerHub:
   ```bash
   docker push lsatsrciresearch/fibermorph:latest
   ```

## Deploy to OpenShift
1. Install the OpenShift CLI (`oc`) if you haven't already.
2. Log in to your OpenShift cluster using the `oc login` command (the easiest way to obtain this is to log in to the OpenShift web console and copy the command from there).
3. Switch to the project you created for FiberMorph:
    ```bash
    oc project <your-project-name>
    ```
4. Install the helm chart for the FiberMorph application:
    ```bash
   helm install {release} charts/fibermorph -f charts/fibermorph/values.{release}.yaml
