## DevP2P Node Scrapper

Connects as a peer of the devp2p network, storing information of the visited peers into the DB.

_Useful if you want to have your service of status of the network, or if you want to keep your table of byzantium-fork nodes_.

### Very Quick Start

You need to give it:

* _devp2p_ nodes to bootstrap the network (we are providing you with a file, `./services/bootnodes-devp2p`)
* How to reach your redis DB.

Then, from the **root** of this very repository

```
make devp2p-node-scrapper && ./build/bin/devp2p-node-scrapper --devp2p-bootnodes ./services/bootnodes-devp2p
```

you may want to get yourself the go dependencies f you don't have them. Quick and dirty is

```
go get ./...
```

from the root directory.

### Useful debugging options

**More** Tracing with `debug`

```
./build/bin/devp2p-node-scrapper --devp2p-bootnodes ./services/bootnodes-devp2p --debug
```

**EVEN MORE** Tracing. Add `--devp2p-lib-debug`. Will show you what the `go-ethereum/p2p` library is doing.

```
./build/bin/devp2p-node-scrapper --devp2p-bootnodes ./services/bootnodes-devp2p --debug --devp2p-lib-debug
```

### Database

The schema in the redis database is very simple

* `devp2p-scrapped-peers:all`: A set containing all the scrapped peers.
* `devp2p-byzantium-peers:all`: A set containing all peers who passed the byzantium fork test.
* `devp2p-non-byzantium-peers:all`: A set containing all peers who failed the byzantium fork test.
* `devp2p-peerstatus:<peerid>`: A set containing all the recorded statuses for peer `<peerid>`.

### Scripts

You can extract information from the redis database to _csv_ files,
using the following convenience scripts located at `/services/scripts`

#### get-scrapped-devp2p-nodes-csv.sh

Will give you all scrapped nodes and their last recorded status.

#### get-byzantium-devp2p-nodes-csv.sh

Will give you a list of the discovered byzantium fork peers.

#### get-non-byzantium-devp2p-nodes-csv.sh

Will give you a list of peers discovered that fail the byzantium fork test.

### Documentation

At this stage, this is a very experimental package.

Documentation is in code. If you want to contribute to this application,
don't be shy to be verbose: Reading another person's code is where we
spend the more time. Let's make that easier for everybody.