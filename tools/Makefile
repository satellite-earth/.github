setup: clone link install build
update: pull link install build

# setup repos
clone:
	if [ ! -d "core" ]; then git clone https://github.com/satellite-earth/core.git; fi
	if [ ! -d "desktop" ]; then git clone https://github.com/satellite-earth/desktop.git; fi
	if [ ! -d "public-node" ]; then git clone https://github.com/satellite-earth/public-node.git; fi
	if [ ! -d "private-node" ]; then git clone https://github.com/satellite-earth/private-node.git; fi
	if [ ! -d "community-ui" ]; then git clone https://github.com/satellite-earth/community-ui.git; fi
	if [ ! -d "dashboard-ui" ]; then git clone https://github.com/satellite-earth/dashboard-ui.git; fi

# pull all changes
pull:
	cd core && git pull
	cd desktop && git pull
	cd public-node && git pull
	cd private-node && git pull
	cd community-ui && git pull
	cd dashboard-ui && git pull

# create links then attach them
link: link-create link-attach

# create links for packages that need it
link-create:
	cd core && yarn link
	cd private-node && yarn link
	cd community-ui && yarn link
	cd dashboard-ui && yarn link

# attach the links to packages the depend on them
link-attach:
	cd public-node && yarn link "@satellite-earth/core"
	cd public-node && yarn link "@satellite-earth/community-ui"
	cd private-node && yarn link "@satellite-earth/core"
	cd private-node && yarn link "@satellite-earth/dashboard-ui"
	cd desktop && yarn link "@satellite-earth/private-node"
	cd desktop && yarn link "@satellite-earth/community-ui"
	cd desktop && yarn link "@satellite-earth/dashboard-ui"

# install all dependencies
install:
	cd core && yarn install
	# cd desktop && yarn install
	cd public-node && yarn install
	cd private-node && yarn install
	cd community-ui && yarn install
	cd dashboard-ui && yarn install

# build all packages
build:
	cd core && yarn build
	# cd desktop && yarn build
	cd public-node && yarn build
	cd private-node && yarn build
	cd community-ui && yarn build
	cd dashboard-ui && yarn build

# login to the github registry using your github username and private access token
# this is only nessisary if you want to publish package versions from your local machine
npm-login:
	if ! npm whoami --registry=http://npm.pkg.github.com; then echo "Login to npm.pkg.github.com using github username and access token" && npm login --scope=@satellite-earth --auth-type=legacy --registry=https://npm.pkg.github.com; fi

# general cleanup task
clean: unlink

# remove all linked packages
unlink:
	cd core && yarn unlink
	cd private-node && yarn unlink
	cd community-ui && yarn unlink
	cd dashboard-ui && yarn unlink

watch:
	cd core && yarn build --watch > /dev/null &\
	cd public-node && yarn build --watch > /dev/null &\
	cd private-node && yarn build --watch > /dev/null &\
	cd community-ui && yarn build --watch > /dev/null &\
	cd dashboard-ui && yarn build --watch > /dev/null &\
	wait
