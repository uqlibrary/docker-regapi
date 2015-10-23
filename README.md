# docker-regapi
Simple bash script for performing basic API calls to Docker Private Registry v2 

The purpose is to provide some basic visibility to the contents of your v2 Private Registry (in lieu of a web Frontend/UI that supports v2 API with token auth service).

For reference, I am using to query a [v2.1 Docker Registry](https://docs.docker.com/registry/) which is using [Cesanta docker_auth](https://github.com/cesanta/docker_auth) token-based authentication server.

_Credit:_ Some of the core functionality of this script (auth service header inspection, subsequent token generation) was directly inspired by a test script posted by [Konrad Kleine](https://github.com/kwk) in an [issue](https://github.com/docker/distribution/issues/1092) on the the docker github. Thanks kwk! :)

### Usage:

    Required arguments:
        -r | --registry         private docker registry (Format: -r [domain][:port])
                                (can be preset with ENV "DOCKER_REGISTRY_HOST")

    Optional arguments:
        -p | --pass-token       password token to use with auth service (overrides ~/.docker/config.json)
        -v | --verbose          verbose output

    Commands:
        -c | --catalog          Request the Catalog (list of all images).
        -t | --tags             Get list of tags for provided image name. (Format: -t [image])

    Examples:
      Simple (Using ENV for registry and config.json for docker auth password token):
        docker-regapi -c
        docker-regapi -r registry.mydomain.com:5000 -c
        docker-regapi -r registry.mydomain.com:5000 -t repo/myimage
      All options:
        docker-regapi -r registry.mydomain.com:5000 -p "aBcDeFgH123456" -t "repo/myimage"
        
