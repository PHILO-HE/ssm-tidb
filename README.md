# modification

1. For PD, modify Makefile and cmd/pd-server/main.go.
2. For Tikv, add mod src/kvserver which is modified based on src/bin and add callkv as an entry.
3. For TiDB, modify Makefile and tidb-server/main.go.

# build prerequisite

1. build rocksdb.
   https://github.com/pingcap/docs/blob/3e186ac6d49e30659531a6864fc78f1519282556/scripts/build_rocksdb.sh
2. install golang in /usr/local/.
3. install rust. Only nightly version is valid.
   https://www.rust-lang.org/en-US/other-installers.html


# deployment tips

1. unset http_proxy and https_proxy. This is necessary.
2. The client-urls option for pd must be a http address and hostname is not valid.
   The addr option for tikv should be a ip address without starting with http.
   The pd option for tikv and the path option for tidb can be a hostname or an ip address.
   In the cluster situation, the client-url option for pd and the addr option for tikv should not be 127.0.0.1.

   For pd server, --name=pd --data-dir=pd --client-urls="http://192.168.150.104:2379" --peer-urls="http://192.168.150.104:2380" --log-file=pd.log

   For tikv server, --pd="192.168.150.104:2379" --addr="192.168.150.109:20160"  --data-dir=tikv --log-file=tikv.log

   For tidb server, --store=tikv --path="192.168.150.104:2379" --log-file=tidb.log
