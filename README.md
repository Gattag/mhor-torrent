# Mhor Torrent
A clustered BitTorrent client meant for multi homed traffic over various network types

### This is a complete (will be) BitTorrent client meant to solve a few issues
 - Simplify use of multiple VPNs (and other proxy types) simulateouly for increased BitTorrent perforamnce
 - Provide redundancy and rotation when a single proxy connection fails
 - Spread load over more threads and multiple systems
 - Provide a modern UI

Mhor Torrent is a clustered solution, utilizing Kubernetes for Docker container-orchestation. It is built on top of the [libtorrent](https://www.libtorrent.org/) BitTorrent implementation.

Mhor Torrent works by running serveral libtorrent instances simulaneously and each instance has their own set of network connections. A manager will orchestate piece selection for all of the instances, in total only recving each piece once across all of the systems. All of the pieces can then be seeded to a single collection node where the files can be exported. Currently this means that total space consumption is exactly 200% of the torrent files.

Mhor Torrent will support several proxy types (OpenVPN, Wireguard, and more), with an extention system to add custom solutions. These proxies will exist in pools where a fixed number of connections to servers in a pool can exist at any one time, which allows for a new unused server in a pool to be used when an active connection dies in that same pool.
