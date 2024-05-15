setup: setup-workspace clone install
update: pull install build
dev: switch-dev update

# setup repos
clone:
	if [ ! -d "core" ]; then git clone https://github.com/satellite-earth/core.git; fi
	if [ ! -d "desktop" ]; then git clone https://github.com/satellite-earth/desktop.git; fi
	if [ ! -d "public-node" ]; then git clone https://github.com/satellite-earth/public-node.git; fi
	if [ ! -d "private-node" ]; then git clone https://github.com/satellite-earth/private-node.git; fi
	if [ ! -d "community-ui" ]; then git clone https://github.com/satellite-earth/community-ui.git; fi

setup-workspace:
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/package.json -O package.json

update-make:
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/Makefile -O Makefile

# pull all changes
pull:
	cd core && git pull
	cd desktop && git pull
	cd public-node && git pull
	cd private-node && git pull
	cd community-ui && git pull

# install all dependencies
install:
	yarn install

# build all packages
build:
	cd core && yarn build
	cd desktop && yarn build
	cd public-node && yarn build
	cd private-node && yarn build
	cd community-ui && yarn build

# login to the github registry using your github username and private access token
# this is only nessisary if you want to publish package versions from your local machine
npm-login:
	if ! npm whoami --registry=http://npm.pkg.github.com; then echo "Login to npm.pkg.github.com using github username and access token" && npm login --scope=@satellite-earth --auth-type=legacy --registry=https://npm.pkg.github.com; fi

# general cleanup task
clean:
	rm -rf node_modules

watch:
	cd core && yarn build --watch > /dev/null &\
	cd desktop && yarn build --watch > /dev/null &\
	cd public-node && yarn build --watch > /dev/null &\
	cd private-node && yarn build --watch > /dev/null &\
	cd community-ui && yarn build --watch > /dev/null &\
	wait

switch-dev:
	cd core && git checkout dev
	cd desktop && git checkout dev
	cd public-node && git checkout dev
	cd private-node && git checkout dev
	cd community-ui && git checkout dev
