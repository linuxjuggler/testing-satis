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

## Usage

Now that we set it up, we can just add the following to our `compose.json` file

```json
{
    "repositories": [{
        "type": "composer",
        "url": "https://linuxjuggler.github.io/testing-satis"
    }]
}
```

and whenever we require any of the packages it will be pulled from there, an example of the values for one of the packages

```json
{
    "name": "damascene/lumen-make",
    "version": "v5.7",
    "source": {
        "type": "git",
        "url": "https://github.com/linuxjuggler/lumen-make.git",
        "reference": "d8e90f3360a13ad84b805ca8e187bd87cfedb1cc"
    },
    "dist": {
        "type": "tar",
        "url": "https://linuxjuggler.github.io/testing-satis/dist/damascene/lumen-make/damascene-lumen-make-d8e90f3360a13ad84b805ca8e187bd87cfedb1cc-zip-33d39f.tar",
        "reference": "d8e90f3360a13ad84b805ca8e187bd87cfedb1cc",
        "shasum": "64637e258c95adf509ee40cf9a3b51d1082138d9"
    }
}
```
as you can notice, the dist is from our github pages.

## Private repositories

This will work if you have a *Pro* account, since Github Pages can be private for only *Pro* accounts.