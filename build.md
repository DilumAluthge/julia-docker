# How to create the tarballs

Run the following commands in Bash:

```bash
export JULIA_VERSION="1.11.6"
export IMAGE="julia:${JULIA_VERSION:?}-trixie"
export TARBALL_NAME="julia-${JULIA_VERSION:?}-trixie"

docker pull "${IMAGE:?}"

mkdir MY_WORKING_DIR

cd MY_WORKING_DIR

docker export --output="${TARBALL_NAME:?}.tar" "$(docker container create julia:1.11.6-trixie)"

ls julia-1.11.6-trixie.tar

gzip julia-1.11.6-trixie.tar

ls julia-1.11.6-trixie.tar.gz
```

Now, upload the `.tar.gz` file as a release asset in the GitHub Releases section of this repo. Copy the URL.

Now, open Julia and run the following:

```julia
# Required deps:
# ] add ArtifactUtils Artifacts

import Artifacts
import ArtifactUtils

artifacts_toml = "Artifacts.toml"
name = "julia-1.11.6-trixie"
tarball_url = "https://github.com/DilumAluthge/julia-docker/releases/download/julia-1.11.6-trixie/julia-1.11.6-trixie.tar.gz"

# This will create the Artifacts.toml file:
ArtifactUtils.add_artifact!(artifacts_toml, name, tarball_url)
```
