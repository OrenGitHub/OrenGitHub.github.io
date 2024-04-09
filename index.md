## `installation` (you only need `docker` and `git`)

```bash
$ git clone --recurse-submodules https://github.com/OrenGitHub/dhscanner
$ cd dhscanner

# build containers ( currently dev oriented, might take around 30 min.)
$ docker build --tag host.front.js  --file dhscanner.front.js/Dockerfile  dhscanner.front.js
$ docker build --tag host.front.rb  --file dhscanner.front.rb/Dockerfile  dhscanner.front.rb
$ docker build --tag host.parser.js --file dhscanner.parser.js/Dockerfile dhscanner.parser.js
$ docker build --tag host.parser.rb --file dhscanner.parser.rb/Dockerfile dhscanner.parser.rb

# use ports 8000 and up *consecutively*
$ docker run -p 8000:3000 -d -t --name front.js  host.front.js
$ docker run -p 8001:3000 -d -t --name front.rb  host.front.rb
$ docker run -p 8002:3000 -d -t --name parser.js host.parser.js
$ docker run -p 8003:3000 -d -t --name parser.rb host.parser.rb

# the dhscanner manager runs in docker too
$ docker build --tag host.dhscanner  --file Dockerfile .
$ docker run --network=host -d -t --name dhscanner host.dhscanner

# everything seems ready - let's do a quick health check
# what are you waiting for ? just jump inside !
$ docker exec -it dhscanner bash

# inside our cozy and comfy docker !
# let's make sure everyone's ready for work !
$ python health_check_all_components.py
```
