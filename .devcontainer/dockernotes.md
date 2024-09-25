```bash

# test if docker container can build 
wsl
cd .devcontainer 

docker build -t mmdetimage:dev . --no-cache
docker run -dit mmdetimage:dev /bin/bash 

```
### Devcontainer 
open folder in container 