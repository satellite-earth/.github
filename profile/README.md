# Satellite


## Setup Local development

If you want to setup all the repos and play around with them locally you can use the handy [Makefile](https://github.com/satellite-earth/.github/blob/master/tools/Makefile)

```sh
# download the Makefile
wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/Makefile
# clone, install, link, and build repos
make setup dev
```

Avaliable commands
- `make setup` Clone all repos, install dependencies, and build all packages
- `make update` Pull all repos
- `make dev` Pull and checkout dev branch
- `make link` Link package dependencies
- `make watch` Build all packages and watch for changes
- `make clean` Remove npm links
