# API reference

## API reference for [SilMaster.sol](https://github.com/sil-finance/sister-in-law/blob/main/contracts/SilMaster.sol)

SilMaster is the main entrance of SIL , Manage pool and distribute SIL Token to mining user

### Main Functions open to external users


| Name      		| Description 			|
| ----------- 	| ----------- 			|
| pendingSil    	| Query mined SIL      	|
| withdrawSil   	| Withdraw minted SIL in specific pool   |
| deposit 		| deposit token to pool	|
| depositEth 		| deposit ETH via payable function |
| withdrawToken 	| retrieve token			|

**pendingSil**

Query mined SIL Token in specific pool and side

```
function pendingSil(uint256 _pid, uint256 _index, address _user) external view   returns (uint256)

```

> Parameters

- _pid : Pool index
- _index : Token index in [Uniswap, SushiSwap] pair, (Token0 | Token1)
- _user : Address

> Return Values
 
  - RETURN : Mined SIL Token amount


**withdrawSil**

Withdraw SIL Token in secific pool

```
function withdrawSil(uint256 _pid) public
```

> Parameters

- _pid : Pool index

**deposit**

Deposit Token to specific pool

```
function deposit(uint256 _pid, uint256 _index,  uint256 _amount) public
```
> Parameters

- _pid : Pool index
- _index : Token index in [Uniswap, SushiSwap] pair, ( Token0 | Token1)
- _amount : Token amount which wants to deposit for mining

**depositEth**
Same with `depist`, add `payable` for accept ETH payment

```
function depositEth(uint256 _pid, uint256 _index ) public payable
```

> Parameters

- _pid : Pool index
- _index : Token index in [Uniswap, SushiSwap] pair, (Token0 | Token1)
- `_amount` : Pay ETH via `value` field

**withdrawToken**

Withdraw token in the pool

```
function withdrawToken(uint256 _pid, uint256 _index, uint256 _amount) public
```

> Paramenters


- _pid : Pool index
- _index : Token index in [Uniswap, SushiSwap] pair, (Token0 | Token1)
- _amount : Token amount which wants to withdraw form specific pool

## API reference for [MatchPair.sol](https://github.com/sil-finance/sister-in-law/blob/main/contracts/MatchPair.sol)

MatchPair is responsible for matching token0 to token1  for minting LP

### Main Functions open to external users

| Name      		| Description 			|
| ----------- 	| ----------- 			|
| queueTokenAmount    	| Amount in pending queue    |
| tokenAmount   	| Token amount in pending queue   |
| lPAmount 		| LP amount in LP queue |
| maxAcceptAmount 		| Max amount depositable |
| stakeGatling 	| stakeGatling address	|

**queueTokenAmount**

Amount in pending queue

```
function queueTokenAmount(uint256 _index) public view override  returns (uint256)
```

> Parameters

- _index : Token index in [Uniswap, SushiSwap] pair, ( Token0 | Token1)

> Return values

- RETURN : Token amount 


**tokenAmount**

Token amount in pending queue

```
function tokenAmount(uint256 _index, address _user) public view returns (uint256)
```

> Parameters

- _index : Token index in [Uniswap, SushiSwap] pair, ( Token0 | Token1)
- _user : user address

> Return values

- RETURN : token amount

**lPAmount**

LP amount in pending queue

```
function lPAmount(uint256 _index, address _user) public view returns (uint256)
```

> Parameters

- _index : Token index in [Uniswap, SushiSwap] pair, ( Token0 | Token1)
- _user : user address

> Return values

- RETURN : Paired LP token amount

**maxAcceptAmount**

If `SilMaster.whaleSpear == true`, the amount in queue cannot bigger than paired token amount multipy `SilMaster.maxAcceptMultiple`

```
function maxAcceptAmount(uint256 _index, uint256 _times, uint256 _inputAmount) public view override returns (uint256)
```

> Parameters

- _index : Token index in [Uniswap, SushiSwap] pair, ( Token0 | Token1)
- _times : `SilMaster.maxAcceptMultiple`
- _inputAmount : intent to deposit amount

> Return values

- RETURN : Acceptable amount

**stakeGatling**

StakeGatling contract address

```
function stakeGatling() returns (address)
```

- RETURN : StakeGatling address


## API reference for [StakeGatling.sol](https://github.com/sil-finance/sister-in-law/blob/main/contracts/StakeGatling.sol)

MatchPair is responsible for matching token0 to token1  for minting LP

### Main Functions open to external users

| Name      		| Description 			|
| ----------- 	| ----------- 			|
| totalAmount    	| Amount in mining current   |
| currentProfitRate   	| Reinvest  times   |
| reprofitCountAverage 		| Average reinvest  times |
| totalLp 		| LpPair.balanceOf(address(this)) |


**totalAmount**

Amount in mining current

```
function totalAmount() returns (uint256)
```

- RETURN : LP amount

**currentProfitRate**

Reinvest  times

```
function currentProfitRate() public view returns (uint256 _times, uint256 _interval) 
```

> Return values

- _times : Reinvest  times
- _interval : Days interval of late

**reprofitCountAverage**

Average reinvest  times per day

```
function reprofitCountAverage() public view returns (uint256)
```

- RETURNS : Reinvest  times per day from contract create

**totalLp**

Call `balanceOf` function of `stakeToken`

```
function totalLp() public view returns (uint256 balance)
```

- RETURNS : Balance of `address(this)`