setup: setup-workspace clone install
update: pull install build
dev: switch-dev update

# setup repos
clone:
	if [ ! -d "core" ]; then git clone git@github.com:satellite-earth/core.git; fi
	if [ ! -d "desktop" ]; then git clone git@github.com:satellite-earth/desktop.git; fi
	if [ ! -d "public-node" ]; then git clone git@github.com:satellite-earth/public-node.git; fi
	if [ ! -d "personal-node" ]; then git clone git@github.com:satellite-earth/personal-node.git; fi
	if [ ! -d "web-ui" ]; then git clone git@github.com:satellite-earth/web-ui.git; fi
	if [ ! -d "multiplexer" ]; then git clone git@github.com:satellite-earth/multiplexer.git; fi

setup-workspace:
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/pnpm-workspace.yaml -O pnpm-workspace.yaml
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/.npmrc -O .npmrc

update-make:
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/Makefile -O Makefile

# pull all changes
pull:
	cd core && git pull
	cd desktop && git pull
	cd public-node && git pull
	cd personal-node && git pull
	cd multiplexer && git pull
	cd web-ui && git pull

# install all dependencies
install:
	pnpm install

# build all packages
build:
	cd core && pnpm build
	cd desktop && pnpm build
	cd public-node && pnpm build
	cd personal-node && pnpm build
	cd multiplexer && pnpm build
	cd web-ui && pnpm build

# login to the github registry using your github username and personal access token
# this is only nessisary if you want to publish package versions from your local machine
npm-login:
	if ! npm whoami --registry=http://npm.pkg.github.com; then echo "Login to npm.pkg.github.com using github username and access token" && npm login --scope=@satellite-earth --auth-type=legacy --registry=https://npm.pkg.github.com; fi

switch-dev:
	cd core && git checkout dev
	cd desktop && git checkout dev
	cd public-node && git checkout dev
	cd personal-node && git checkout dev
	cd multiplexer && git checkout dev
	cd web-ui && git checkout dev

dev-desktop:
	cd core && pnpm build --watch > /dev/null &\
	cd personal-node && pnpm build --watch > /dev/null &\
	cd web-ui && pnpm dev > /dev/null &\
	cd desktop && pnpm rebuild && OVERRIDE_UI=http://localhost:5173 pnpm dev > /dev/null &\
	wait

dev-node:
	cd core && pnpm build --watch > /dev/null &\
	cd web-ui && pnpm dev > /dev/null &\
	cd personal-node && pnpm rebuild && REDIRECT_APP_URL=http://localhost:5173 pnpm dev > /dev/null &\
	wait
