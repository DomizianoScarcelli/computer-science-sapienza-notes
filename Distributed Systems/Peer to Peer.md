---
Exam:
  - Distributed Systems
---
P2P comes handy when we have a large file to share that some people want to download at the same time. A normal architecture would overload the single server that has the file.

The idea is to make a distributed system in which every person (peer) that downloads the file, also makes it available to other peers. The server has just the role of distributing the file initially, and then the system should work between the clients.

A file in BitTorrent is distributed in different blocks inside many clients, and those blocks can be downloaded in parallel.

The file that has to be downloaded is described in a file with the `.torrent` extension. Inside this file the hashes of all the blocks that make the file are described. The size of the block is usually 0.25MB.

The `.torrent` file also stores the url of the tracker, that is a peer that has the informations about all the peers that share the file. You can ask the trackers for a list of peers that have the file, and download it. The tracker also has the information about the blocks and the statistics about the peers. The tracker can be chosen by the peers or sometimes there are some other servers that are trackers for several files. 

The list that the tracker gives us is a partial list of peers, that is a subset of the entire list. Tipically this subset is chosen randomly.

When you start downloading, you should start from a certain block. One idea is to select the rarest block first, in order that rare blocks are shared a little bit more than the others in order to assure avaliability. 

Another policy is just by choosing it randomly. This because there is a problem with the rarest block: you can take a long time to start, since the rarest block can be anywhere in some computer with a low bandwitdth.

## Problems with P2P

### Last block (Endgame Mode)

The last blocks of the file could be rare, and so their download could be a lot slower. In order to solve this problem, the last blocks or the last one is split in other sub-blocks that are downloaded in parallel. This is called endgame mode.

### Choking

If a certain peer has to upload a file to too many peers, its bandwidth could be saturated.

A solution is to choke (interrupt) some of the connections to some particular peers. Usually only 4 peers are unchoked and selected for the upload. The problem here is how to select them:

- **This-for-that**: this method is about unchoking a peer only if they unchoke you back. The idea is to avoid free-riders, meaning the peers that download the file and then leave without uploading it, since they are bad for the entire system.
- **Optimistic unchoking**: when a new peer wants to download a file, it starts without any block. Using the previous strategy, the peer wouldn’t have any block to upload and so would be choked by all the other peers. With optimistic unchoking 1 out of 4 peers is randomly chosen, otherwise it couldn’t download the file.

## Vulnerabilities

The peer to peers system has some vulnerabilities, meaning it’s possible in some way to distrupt the system in these ways:

- Track the trackers and take them down;
- Inject some nodes in the system that don't do anything;
- Poisoning, meaning inserting fake blocks in order to corrupt the whole file. This is not easy since the .torrent file stores the hashes of the block, that allwos to discard a fake block by checking the hash.
- Poisoning the whole file, by inserting a file with the same name of the original but with different “garbage” content. For a peer to realize the content is different, it has to download it, but it will also upload it and the file would be distributed in the system. This is done mainly when you don’t want a certain content to be available.