## A test for using Github Pages with Satis

Since am using the docker image, the `output-dir` config value in `satis.json` has no value, so to clean up and
produce everything within the `docs` dir we run the following command:

```bash
docker run --rm --init -it \       
  -u $(id -u):$(id -g) \
  -v $(pwd):/build \
  -v "${COMPOSER_HOME:-$HOME/.composer}:/composer" \
  composer/satis build /build/satis.json /build/docs

``` 

We specify the path to `satis.json` within the docker image, and we also specify the `output-dir` too.