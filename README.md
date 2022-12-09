# Cosmos-SDK Tutorial

## Cosmos SDK Cloning

Cosmos SDK를 클론 받아서 빠르게 진행할 수 있다. 

```
git clone https://github.com/cosmos/cosmos-sdk 
cd cosmos-sdk
make build
```

다음과 같이 특정 버전으로 이동할 수도 있다. 대신 deprecated된 패키지가 있을 수 있으니 main 브랜치에서 그대로 작업하는 것을 추천

```
git clone https://github.com/cosmos/cosmos-sdk 
cd cosmos-sdk
git checkout tags/v0.44.3
make build
```

## Local에서 키링을 만드는 법

```shell

# build 디렉토리로 이동
cd build

# simd 데모 실행
./simd init demo 
>> {"app_message":{"auth":{"accounts":[],"params":{"max_memo_characters":"256",
>> "sig_verify_cost_ed25519":"590","sig_verify_cost_secp256k1":"1000","tx_sig_limit"
>> :"7","tx_size_cost_per_byte":"10"}},"authz":{"authorization":[]},"bank":{"balances":[],
>> "denom_metadata":[],"params":{"default_send_enabled":true,"send_enabled":[]},"send_enabled":[],
>> "supply":[]},"capability":{"index":"1","owners":[]},"consensus":null,"crisis":{"constant_fee":
>> {"amount":"1000","denom":"stake"}},"distribution":{"delegator_starting_infos":[],
>> "delegator_withdraw_infos":[],"fee_pool":{"community_pool":[]},"outstanding_rewards":[],
>> "params":{"base_proposer_reward":"0.010000000000000000","bonus_proposer_reward":"0.040000000000000000",
>> "community_tax":"0.020000000000000000","withdraw_addr_enabled":true},"previous_proposer":"",
>> "validator_accumulated_commissions":[],"validator_current_rewards":[],"validator_historical_rewards":[],
>> "validator_slash_events":[]},"evidence":{"evidence":[]},"feegrant":{"allowances":[]},"genutil":
>> {"gen_txs":[]},"gov":{"deposit_params":{"max_deposit_period":"172800s","min_deposit":[{"amount":
>> "10000000","denom":"stake"}]},"deposits":[],"params":{"max_deposit_period":"172800s","min_deposit":
>> [{"amount":"10000000","denom":"stake"}],"min_initial_deposit_ratio":"0.000000000000000000","quorum":
>> "0.334000000000000000","threshold":"0.500000000000000000","veto_threshold":"0.334000000000000000",
>> "voting_period":"172800s"},"proposals":[],"starting_proposal_id":"1","tally_params":{"quorum":
>> "0.334000000000000000","threshold":"0.500000000000000000","veto_threshold":"0.334000000000000000"},
>> "votes":[],"voting_params":{"voting_period":"172800s"}},"group":{"group_members":[],"group_policies":[],
>> "group_policy_seq":"0","group_seq":"0","groups":[],"proposal_seq":"0","proposals":[],"votes":[]},"mint":
>> {"minter":{"annual_provisions":"0.000000000000000000","inflation":"0.130000000000000000"},"params":
>> {"blocks_per_year":"6311520","goal_bonded":"0.670000000000000000","inflation_max":"0.200000000000000000",
>> "inflation_min":"0.070000000000000000","inflation_rate_change":"0.130000000000000000",
>> "mint_denom":"stake"}},"nft":{"classes":[],"entries":[]},"params":null,"slashing":{"missed_blocks":[],
>> "params":{"downtime_jail_duration":"600s","min_signed_per_window":"0.500000000000000000",
>> "signed_blocks_window":"100","slash_fraction_double_sign":"0.050000000000000000","slash_fraction_downtime"
>> :"0.010000000000000000"},"signing_infos":[]},"staking":{"delegations":[],"exported":false,
>> "last_total_power":"0","last_validator_powers":[],"params":{"bond_denom":"stake","historical_entries"
>> :10000,"max_entries":7,"max_validators":100,"min_commission_rate":"0.000000000000000000","unbonding_time"
>> :"1814400s"},"redelegations":[],"unbonding_delegations":[],"validators":[]},"upgrade":{},"vesting":{}},
>> "chain_id":"test-chain-Uz49eB","gentxs_dir":"","moniker":"demo","node_id":"9ccf1e51b395d37907f557d8720a8
>> 1c805e45456"}

# 현재 키는 아무것도 없음 
./simd keys list 
>> No records were found in keyring

# b9lab 이라는 키를 추가
./simd keys add b9lab

./simd keys list                                                                                                                                                                                                            ✔  base   00:01:56  
- address: cosmos1sj9gz3w8rfpezk4kscg658xaxdzvzzmfxsehy4
  name: b9lab
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"Ajx9Z846MpK/d0/7Caat+Rb4DToijk9iIo+GBQEH3zmR"}'
  type: local


# add-genesis-account 
./simd add-genesis-account b9lab 100000000stake

./simd gentx b9lab 70000000stake --chain-id test-chain-Uz49eB 
>> Genesis transaction written to "/Users/gimmingyu/.simapp/config/gentx/gentx-9ccf1e51b395d37907f557d8720a81c805e45456.json"
    
./simd collect-gentxs
>> {"app_message":{"auth":{"accounts":[{"@type":"/c..."


# Start Blcokchain
./simd start
```

