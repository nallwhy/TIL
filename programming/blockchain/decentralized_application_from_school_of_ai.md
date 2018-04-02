# Decentralized Application from School of AI

https://www.theschool.ai/courses/decentralized-applications

## Introduction

### Web 3.0

기회가 많다.

### Install Ethereum node (on Mac)

    brew tap ethereum/ethereum
    brew install ethereum

### Run

Create an account:

    geth account new

Run the node:

    geth

### Remix(web compiler)

http://remix.ethereum.org/

Electron version: https://github.com/horizon-games/remix-app/


### Livestream 내용

- video: https://www.youtube.com/watch?v=nkt-MBPNRCc&feature=youtu.be&t=36s
- source code: https://github.com/llSourcell/simple_auction/blob/master/simple-auction.html

bytecode, abi 를 이용해서 contract 에 접근한다. (왜 단지 address 주소로만은 안되는거지? 계약을 맺는게 안되는건가. 메타 데이터를 얻기 위함이라고 한다. 단지 정보를 보내고 받는 것이 다라면 필요 없다. smart contract 업데이트 같은)

코드가 많아지면 gas 가 많이 든다. 모든 코드가 contract 에 있을 필요는 없다. consensus 에 대한 부분은 contract 에 있어야한다.

#### Codes

```solidity
pragma solidity ^0.4.0;

contract SimpleAuction {

    // parameters
    address public beneficiary;
    uint public auctionStart;
    uint public biddingTime;

    // current state of the auction
    address public highestBidder;
    uint public highestBid;

    // withdrawals that are allowed
    mapping(address => uint) pendingReturns;

    // did the auction end
    bool ended;

    // event
    event HighestBidIncreased(address bidder, uint amount);
    event AuctionEnded(address winner, uint amount);

    function SimpleAuction(
        uint _biddingTime,
        address _beneficiary) {
            beneficiary = _beneficiary;
            auctionStart = now;
            biddingTime = _biddingTime;
        }

    function bid() payable {
        if (now > auctionStart + biddingTime) {
            throw;
        }

        if (msg.value <= highestBid) {
            throw;
        }

        if (highestBidder != -0) {
            pendingReturns[highestBidder] += highestBid;
        }

        highestBidder = msg.sender;
        highestBid = msg.value;
        HighestBidIncreased(msg.sender, msg.value);
    }

    function withdraw() returns (bool) {
        var amount = pendingReturns[msg.sender];
        if (amount > 0) {
            pendingReturns[msg.sender] = 0;

            if (!msg.sender.send(amount)) {
                pendingReturns[msg.sender] = amount;
                return false;
            }
        }

        return true;
    }

    function auctionEnd() {
        // 1. Checking condition
        if (now <= auctionStart + biddingTime) {
            throw;
        }

        if (ended) {
            throw;
        }

        // 2. Performing auctions
        ended = true;
        AuctionEnded(highestBidder, highestBid);

        // 3. Interaction with contracts
        if (!beneficiary.send(highestBid)) {
            throw;
        }
    }
}
```

#### Run test client

https://github.com/trufflesuite/ganache-cli

    yarn global add granache-cli
    granache-cli

#### Run codes on test client

On Remix, set `Run` -> `Environment` -> `Web3 Provider`.


## Decentralized Chat

### Consensus layer ( == Ethereum blockchain)

- EVM (consensus)
- Whisper (messaging)
- Swarm (Storage)

### Whisper

- Darkness
- High cost
- Off-chain
- Can be considered a Distributed Hash Table
- Every message delivered to every node for darkness
- Identity-based message
- To prevent DDOS, a POW is used
- Non-persistent with preset TTL (from 10 minutes to 2 days)
- Non-realtime

#### API

- Whisper API is only exposed to **contracts**
- Low-bandwidth: only for smaller data transfers
- Unpredictable latency: not for real-time communication
- All API for whisper is contained in the `web3.ssh` object

```javascript
var f = web3.ssh.filter({optics: ["qwerty"]})
f.get()
web3.ssh.getMessages("qwerty")
web.ssh.post({topics: ["qwerty"], payload: "0x847a786376", ttl: "0x1E", workToProve: "0x9"})
```

#### Messages

- A unique process of message sealing, compression and encryption
- Each message has a lifespan < 2days, a recipient(public key), topics

##### Sending a whisper message

1. Create a new whisper.Message
2. Seal it
3. Send it

```
topics := TopicsFromString("my", "message")
msg := whisper.NewMessage([]byte("hello world"))
envelope := msg.Seal(whisper.Opts{
    From: myPrivateKey,
    Topics: topics
})
whisper.Send(envelope)
```

##### Watching

```
topics := TopicsFromString("my", "message")
whisper.Watch(Filter{
    Topics: topics
    Fn: func(msg *Message) {
        fmt.Println(msg)
    }
})
```

#### Sealing (PoW)

- Hashing contents of the message **repeatedly** into the smallest possible number
- The cost of compution PoW can be regarded as the price you pay

PoW = (2^BestBit) / (size * TTL)

More computation, more priority




