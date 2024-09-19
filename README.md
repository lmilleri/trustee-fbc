# Trustee FBC

The file based catalog (**FBC**) for trustee.


## Install `opm`

You need v1.46.0 or greater.

Download the binary from [Github releases](https://github.com/operator-framework/operator-registry/releases).


## Update the FBC

1. Run `./update.sh` to update the digests in the template.
1. Run `./render.sh` to update the actual catalog.
1. Open a pull request with your changes.


## Add a new OpenShift version

In examples that follow, the latest release is `v4.16` and you want to release for `v4.17` too.

### New Konflux component

You can add a new component from the web UI.

### New PipelineRuns

Create the PipelineRuns to build the new FBC:
1. Enter the `.tekton` folder.
1. Copy the pull-request PipelineRun.

   Example: copy `trustee-fbc-4-16-pull-request.yaml` to `trustee-fbc-4-17-pull-request.yaml`.

1. Copy the push PipelineRun.

   Example: copy `trustee-fbc-4-16-push.yaml` to `trustee-fbc-4-17-push.yaml`.

1. Update all occurrences of the version in the new PipelineRuns. For example, run:
   ```
   sed -i 's/v4.16/v4.17/' trustee-fbc-4-17-*.yaml
   sed -i 's/4-16/4-17/' trustee-fbc-4-17-*.yaml
   ```

### New FBC

Create the new FBC:
1. Copy the folder. For example, copy `v4.16` to `v4.17`.
1. Update the base image version in the Dockerfile. For example, run:
   ```
   sed -i 's/v4.16/v4.17/' v4.17/Dockerfile
   ```
1. Run `./render.sh` to update the actual catalog. Note that this command will not make any changes, if they are not needed.
