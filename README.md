# aki-chain QUICK START
A blockchain testnet based on graphene toolkit
AUTHOR:Akirasen AKA langta,TONI LAI,LAI FEI LIM ~

## 1.Enable a screen
```
screen -R ynode
```
## 2.Connect the seed node and start your node
```
./ynode --data-dir data --genesis-json my-genesis.json -s 45.76.239.253:9527 --rpc-endpoint=127.0.0.1:9090
```
Your node will synchronize the existing blocks from the seed node to the local, which may take a few minutes to hours. You will see:
```
root@akira:/www/wwwroot/test2# ./ynode --data-dir data --genesis-json my-genesis.json -s 45.76.239.253:9527 --rpc-endpoint=127.0.0.1:9090
698830ms th_a       main.cpp:126                  create_new_config_fi ] Writing new config file at /www/wwwroot/test2/data/config.ini
698833ms th_a       witness.cpp:86                plugin_initialize    ] witness plugin:  plugin_initialize() begin
698835ms th_a       witness.cpp:96                plugin_initialize    ] Public Key: YYW6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
698836ms th_a       witness.cpp:114               plugin_initialize    ] witness plugin:  plugin_initialize() end
698837ms th_a       db_management.cpp:185         open                 ] Wiping object_database due to missing or wrong version
698838ms th_a       object_database.cpp:100       wipe                 ] Wiping object database...
698839ms th_a       object_database.cpp:102       wipe                 ] Done wiping object databse.
698840ms th_a       object_database.cpp:115       open                 ] Opening object database from www/wwwroot/test2/data/blockchain ...
698842ms th_a       object_database.cpp:124       open                 ] Done opening object database.
698842ms th_a       application.cpp:360           operator()           ] Initializing database...
698849ms th_a       db_update.cpp:774             adjust_budgets       ] budgets adjusted on block 0, next scheduled adjust block is 10512000
698851ms th_a       db_update.cpp:750             update_committee     ] committee updated on block 0, next scheduled update block is 864000
698854ms th_a       application.cpp:152           reset_p2p_node       ] Adding seed node 45.76.239.253:9527
699051ms th_a       application.cpp:194           reset_p2p_node       ] Adding seed node 3.84.191.136:2018
699053ms th_a       application.cpp:194           reset_p2p_node       ] Adding seed node 212.64.59.19:2018
699054ms th_a       application.cpp:209           reset_p2p_node       ] Configured p2p node to listen on 0.0.0.0:43780
699055ms th_a       application.cpp:284           reset_websocket_serv ] Configured websocket rpc to listen on 127.0.0.1:9090
699056ms th_a       witness.cpp:119               plugin_startup       ] witness plugin:  plugin_startup() begin
699057ms th_a       witness.cpp:134               plugin_startup       ] No witnesses configured! Please add witness IDs and private keys to configuration.
699058ms th_a       witness.cpp:135               plugin_startup       ] witness plugin:  plugin_startup() end
699058ms th_a       main.cpp:250                  main                 ] Started yoyow node on a chain with 0 blocks.
699058ms th_a       main.cpp:251                  main                 ] Chain ID is 1d275ec1ac88627b12ce2c0b03bc219255d9bfd86b6528cda3977cf6892d0cb7
750105ms th_a       application.cpp:572           handle_block         ] Got block: #10000 000027109a3cc516ca2fe30da934adab3b38bd73 time: 2021-08-10T09:25:00 latency: 362850105 ms from: 27944/init9  irreversible: 9992 (-8)
```
When it is synchronized to the current block height, a block will be produced in 3 seconds, and the latency will be reduced to within 500ms，You will see:
```
1320385ms th_a       application.cpp:572           handle_block         ] Got block: #131121 000200310b41a9a27fb611fbd8ce433b71541ff6 time: 2021-08-14T14:22:00 latency: 385 ms from: 27027/init5  irreversible: 131113 (-8)
1323404ms th_a       application.cpp:572           handle_block         ] Got block: #131122 00020032473e78f91a55ccb7548880d441ddebf0 time: 2021-08-14T14:22:03 latency: 404 ms from: 28182/init10  irreversible: 131114 (-8)
1326351ms th_a       application.cpp:572           handle_block         ] Got block: #131123 00020033cff677b6acdd4ec27eab685008ba1b87 time: 2021-08-14T14:22:06 latency: 351 ms from: 27944/init9  irreversible: 131115 (-8)
1329351ms th_a       application.cpp:572           handle_block         ] Got block: #131124 00020034fb5aa193d1750179d0c39e5c92dc8ec7 time: 2021-08-14T14:22:09 latency: 351 ms from: 26861/init4  irreversible: 131116 (-8)
```
Great. That's it！
## 3.detach the current screen
Hold down key `Ctrl`(control) while pressing key `A` and key `D`
If successful, screen will run in the background.
You will see:
```
[detached from 23018.ynode]
root@akira:/www/wwwroot/test2# 
```
## 4.Use wscat connection node API
```
wscat -c ws://localhost:9090
```
If successful, You will see:
```
root@akira:/www/wwwroot/test2# wscat -c ws://localhost:9090

connected (press CTRL+C to quit)
> 
```
## 5.Send JSON format request to node
```
{"jsonrpc": "2.0", "method": "get_block", "params": [130428], "id": 1}

```
If successful, You will see:
```
root@akira:/www/wwwroot/test2# wscat -c ws://localhost:9090
connected (press CTRL+C to quit)
> {"jsonrpc": "2.0", "method": "get_block", "params": [130428], "id": 1}

< {"id":1,"jsonrpc":"2.0","result":{"previous":"0001fd7bebbaa8e4945c158cc5247d9275ba0efd","timestamp":"2021-08-14T13:47:21","witness":27447,"transaction_merkle_root":"1de9434d52846201cd48f94f8fc75d4e0d3d5cc7","witness_signature":"1f5daa44dc2348b4ceffdad8e6f9435f650156cfd1759b6e3ddda6f62ab0c2e5ee163f2a8a3bd0fce10a7505fcdde31f41222335d8bdf06f282867eb50de3da582","transactions":[{"ref_block_num":64891,"ref_block_prefix":3836263147,"expiration":"2021-08-14T13:49:18","operations":[[41,{"fee":{"total":{"amount":41443,"asset_id":0}},"license_lid":18,"platform":25997,"type":1,"hash_value":"8165478cb6554c78a00fd507662aba09","extra_data":"作品确权服务由市民通随手拍提供：https://suishoupai.bashe.cc","title":"作品确权","body":"imgurl:https://vkceyugu.cdn.bspapp.com/VKCEYUGU-db1045ed-d474-4ca0-ac76-a1567f786a5c/3e9c0096-053e-4cce-8ffd-4e857cfa3eb3.png,imghash:D620A93B7320AE5E6C929918E42D8A50443A5C9D18622744D82CC1383CBEA0F0"}]],"signatures":["1f04ea9e98f66914ad657745c862084f4a2c41549dff920abca4ed6b726c824cf86d5953171a3f0d275530fb5dba601c80a8f64bfa40b0d73177a961d0d874c043"],"operation_results":[[1,"2.17.187"]]}],"block_id":"0001fd7cdf3a90ff9f0716d3bdd49d0f54dffd76","signing_key":"YYW7jpaLdV1A8UsED5kV7H5JZkZUUtAS77moo94oU66FrwXK2peUK","transaction_ids":["ad5cccdb117466887eddfd055b0e0d56a282a4f8"]}}
> 

```
The above is the transaction data recorded in blocknum 130428. You can also modify the blocknum in params to the blocknum where your content certificate is located
