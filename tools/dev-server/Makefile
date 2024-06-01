setup: clone checkout install build
update: checkout restore pull install build

start-public:
	cd public-node && pnpm rebuild && pnpm start

start-personal:
	cd personal-node && pnpm rebuild && pnpm dev

clone:
	if [ ! -d "core" ]; then git clone https://github.com/satellite-earth/core.git; fi
	if [ ! -d "web-ui" ]; then git clone https://github.com/satellite-earth/web-ui.git; fi
	if [ ! -d "public-node" ]; then git clone https://github.com/satellite-earth/public-node.git; fi
	if [ ! -d "personal-node" ]; then git clone https://github.com/satellite-earth/personal-node.git; fi

pull:
	cd core && git pull
	cd web-ui && git pull
	cd public-node && git pull
	cd personal-node && git pull

install:
	pnpm install

build:
	cd core && pnpm build
	cd web-ui && pnpm build
	cd public-node && pnpm build
	cd personal-node && pnpm build

restore:
	cd core && git restore .
	cd public-node && git restore .
	cd personal-node && git restore .
	cd web-ui && git restore .

checkout:
	cd core && git checkout dev
	cd public-node && git checkout dev
	cd personal-node && git checkout dev
	cd web-ui && git checkout dev
