---
title: Boot Node - Anubis Develop
---

Boot Nodes were introduced on the Anubis mainnet. Anubis Boot Nodes are similar to Ethereum Boot Nodes, refer [here](https://ethereum.org/en/developers/docs/nodes-and-clients/bootnodes/) for more details. The main benefit of Boot Nodes is that it would be easier for user to connect to the Anubis network. Users would no longer need to setup the `StaticNodes` in `config.toml`, just leave it empty and make sure delete the `BootstrapNodes` field in `config.toml`. 

## config.toml

```
[Eth]
NetworkId = 6714
SyncMode = "full"
DisablePeerTxBroadcast = false
EVNNodeIDsToAdd = []
EVNNodeIDsToRemove = []
HistoryMode = "all"
EthDiscoveryURLs = []
SnapDiscoveryURLs = []
BscDiscoveryURLs = []
NoPruning = false
NoPrefetch = false
EnableBAL = false
DirectBroadcast = false
DisableSnapProtocol = false
RangeLimit = false
TxLookupLimit = 2350000
TransactionHistory = 2350000
LogExportCheckpoints = ""
StateHistory = 600000
JournalFileEnabled = true
DatabaseCache = 512
DatabaseFreezer = ""
DatabaseEra = ""
PruneAncientData = false
TrieCleanCache = 154
TrieDirtyCache = 256
TrieTimeout = 600000000000
SnapshotCache = 102
TriesInMemory = 128
TriesVerifyMode = "local"
Preimages = false
FilterLogCacheSize = 32
EnablePreimageRecording = false
VMTrace = ""
VMTraceJsonConfig = ""
RPCGasCap = 50000000
RPCEVMTimeout = 5000000000
RPCTxFeeCap = 1e+00
BlobExtraReserve = 192000
EnableOpcodeOptimizing = false
EnableIncrSnapshots = false
IncrSnapshotPath = ""
IncrSnapshotBlockInterval = 0
IncrSnapshotStateBuffer = 0
IncrSnapshotKeptBlocks = 0
UseRemoteIncrSnapshot = false
RemoteIncrSnapshotURL = ""

[Eth.Miner]
DelayLeftOver = 25000000
GasFloor = 0
GasCeil = 100000000
GasPrice = 12000000000
Recommit = 10000000000
VoteEnable = false
MaxWaitProposalInSecs = 45
DisableVoteAttestation = false
TxGasLimit = 0

[Eth.Miner.Mev]
Enabled = false
GreedyMergeTx = true
BuilderFeeCeil = "0"
SentryURL = ""
Builders = []
ValidatorCommission = 100
BidSimulationLeftOver = 30000000
NoInterruptLeftOver = 235000000
MaxBidsPerBuilder = 2

[Eth.TxPool]
Locals = []
NoLocals = false
Journal = "transactions.rlp"
Rejournal = 3600000000000
PriceLimit = 1
PriceBump = 10
AccountSlots = 200
GlobalSlots = 8000
AccountQueue = 200
GlobalQueue = 4000
OverflowPoolSlots = 0
Lifetime = 10800000000000
ReannounceTime = 315360000000000000

[Eth.BlobPool]
Datadir = "blobpool"
Datacap = 2684354560
PriceBump = 100

[Eth.GPO]
Blocks = 20
Percentile = 60
MaxHeaderHistory = 0
MaxBlockHistory = 0
MaxPrice = 1000000000000
IgnorePrice = 4
OracleThreshold = 1000

[Node.P2P]
MaxPeers = 50
MaxPeersPerIP = 50
NoDiscovery = false
DiscoveryV4 = true
BootstrapNodes = ["enode://600c72f0bc452b135822faa4b683a53819e550a1d1785d12d5ddc7dcc5132ee8342a71933cfe3117c73ac32ebd89665621e46f98c64c90f4676dda5b4dae082b@13.212.58.194:30303", "enode://cebf0f851d6d2e092c0c5ba90b223fedcffbcffe8e9eee7c422cbcc8026eb905a2e1a2a8a4466940a30036412b7b74b0a400c2822c635cc7f780fd8cfc9b88f0@54.255.129.107:30303", "enode://a334282639318fa68481576eb3d72697b49889249d2f4940cb012044b9d99720426f25af433b12b56f6acc6b2d65e45e7dd036cbbd5a8380864a9a81adcacdeb@13.212.173.206:30303"]
StaticNodes = []
TrustedNodes = []
ListenAddr = ":30303"
DiscAddr = ""
NAT = "any"
EnableMsgEvents = false
PeerFilterPatterns = []

[Node.HTTPTimeouts]
ReadTimeout = 30000000000
ReadHeaderTimeout = 30000000000
WriteTimeout = 30000000000
IdleTimeout = 120000000000

[Node.LogConfig]
TimeFormat = "01-02|15:04:05.000"

[Metrics]
HTTP = "127.0.0.1"
Port = 6060
InfluxDBEndpoint = "http://localhost:8086"
InfluxDBDatabase = "geth"
InfluxDBUsername = "test"
InfluxDBPassword = "test"
InfluxDBTags = "host=localhost"
InfluxDBToken = "test"
InfluxDBBucket = "geth"
InfluxDBOrganization = "geth"

[FakeBeacon]
Enable = false
Addr = ""
Port = 0
```

## Impact To Users

### To Run A Boot Node

Boot nodes are super-lightweight nodes, they can be ran by a very cheap device, like: `2 cores, 2GB memory, 20GB disk`. \
If you want to support the Anubis ecosystem by providing new boot nodes, you can follow [this](https://github.com/anubis-chain/anubis#running-a-bootnode) guide to do it.

 If you want to support the Anubis ecosystem by providing new boot nodes, you can follow [this](https://github.com/anubis-chain/anubis#running-a-bootnode) guide to do it.

## Help

Since boot nodes have been introduced recently, if you get any problem in using it, please let us know. You may just create new issue in [Anubis GitHub repo](https://github.com/anubis-chain/anubis/issues).
