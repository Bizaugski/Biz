# Biz
# DFB API

## Introduction

The DFB API provides a multi-chain monitoring solution for blockchain data. It offers various endpoints to retrieve blockchain-related information such as swap quotes, contract ABIs, source codes, token prices, and more.

You can perform the same queries through our interface:

[DFB-API-DOC](https://docs-api.dfb.network/)

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
  - [Get Swap Quote](#get-swap-quote)
  - [Get Contract ABI](#get-contract-abi)
  - [Get Contract Source Code](#get-contract-source-code)
  - [Get Token Price](#get-token-price)
  - [Get Transaction Data](#get-transaction-data)
  - [Get Contract Event](#get-contract-event)
  - [Add Wallet](#add-wallet)
  - [Add Contract](#add-contract)
- [Dependencies](#dependencies)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Examples](#examples)
- [Troubleshooting](#troubleshooting)

## Installation

To use the DFB API, ensure your environment is set up to make HTTPS requests to external services. This might involve installing HTTP client libraries in your preferred programming language.

## Usage

### Get Swap Quote

This endpoint allows you to retrieve a swap quote by `POST`  request. Below are example queries in different programming languages.

`https://heimdall-5lo5blc2.uc.gateway.dev/api/v1/swap/quote`

#### **Java**
```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/api/v1/swap/quote"))
    .header("Content-Type", "application/json")
    .POST(HttpRequest.BodyPublishers.ofString("{\"fromAddress\":\"0x...\",\"fromAmount\":\"1000\",\"fromChain\":\"ETH\",\"fromToken\":\"0x...\",\"toAddress\":\"0x...\",\"toChain\":\"BSC\",\"toToken\":\"0x...\"}"))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### C#

```C#

HttpClient client = new HttpClient();
HttpContent content = new StringContent("{\"fromAddress\":\"0x...\",\"fromAmount\":\"1000\",\"fromChain\":\"ETH\",\"fromToken\":\"0x...\",\"toAddress\":\"0x...\",\"toChain\":\"BSC\",\"toToken\":\"0x...\"}", Encoding.UTF8, "application/json");
HttpResponseMessage response = await client.PostAsync("https://heimdall-5lo5blc2.uc.gateway.dev/api/v1/swap/quote", content);
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);
```

#### JavaScript

```JavaScript
fetch('https://heimdall-5lo5blc2.uc.gateway.dev/api/v1/swap/quote', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ fromAddress: "0x...", fromAmount: "1000", fromChain: "ETH", fromToken: "0x...", toAddress: "0x...", toChain: "BSC", toToken: "0x..." })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

```

#### Python

```python

import requests

data = {
    "fromAddress": "0x...",
    "fromAmount": "1000",
    "fromChain": "ETH",
    "fromToken": "0x...",
    "toAddress": "0x...",
    "toChain": "BSC",
    "toToken": "0x..."
}
response = requests.post("https://heimdall-5lo5blc2.uc.gateway.dev/api/v1/swap/quote", json=data)
print(response.text)
```

### Get Contract ABI

This endpoint allows you to retrieve the ABI from ethereum smartcontract through `GET`requests

`https://heimdall-5lo5blc2.uc.gateway.dev/contract/abi/{contractAddress}`

#### JAVA

```java
String contractAddress = "0x...";
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/contract/abi/" + contractAddress))
    .GET()
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### C#

```C#

string contractAddress = "0x...";
HttpResponseMessage response = await client.GetAsync($"https://heimdall-5lo5blc2.uc.gateway.dev/contract/abi/{contractAddress}");
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);
```

#### JavaScript

```JavaScript
let contractAddress = "0x...";
fetch(`https://heimdall-5lo5blc2.uc.gateway.dev/contract/abi/${contractAddress}`)
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
#### Python

```python
contract_address = "0x..."
response = requests.get(f"https://heimdall-5lo5blc2.uc.gateway.dev/contract/abi/{contract_address}")
print(response.text)
```

### Get Contract Source Code

This endpoint allows you to retrieve the source code of a ethereum smartcontract through a `GET` request

`https://heimdall-5lo5blc2.uc.gateway.dev/contract/source/{contractAddress}`

#### JAVA

```java
String contractAddress = "0x...";
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/contract/source/" + contractAddress))
    .GET()
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### C#

```C#
string contractAddress = "0x...";
HttpResponseMessage response = await client.GetAsync($"https://heimdall-5lo5blc2.uc.gateway.dev/contract/source/{contractAddress}");
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);
```

#### JavaScript

```JavaScript
let contractAddress = "0x...";
fetch(`https://heimdall-5lo5blc2.uc.gateway.dev/contract/source/${contractAddress}`)
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
#### Python

```python
contract_address = "0x..."
response = requests.get(f"https://heimdall-5lo5blc2.uc.gateway.dev/contract/source/{contract_address}")
print(response.text)
```

### Get Token Price

This endpoint allows you to retrieve the source code of a ethereum smartcontract through a `GET` request

`https://heimdall-5lo5blc2.uc.gateway.dev/uniswap/token-price/{chainid}/{amount}/{tokenInAddress}/{tokenOutAddress}`

#### JAVA

```java
String chainId = '1'
String amount = '100' 
String tokenIn = "0x...";
String tokenOut = "0x...";
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/uniswap/token-price/" + 
    chainId + amount + tokenIn + tokenOut))
    .GET()
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### C#

```C#
string chainId = "1";
string amount = "100";
string tokenIn = "0x...";
string tokenOut = "0x...";
HttpResponseMessage response = await client.GetAsync($"https://heimdall-5lo5blc2.uc.gateway.dev/uniswap/token-price/{chainId}/{amount}/{tokenIn}/{tokenOut}");
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);
```

#### JavaScript

```JavaScript
let chainId = "1";
let amount = "100";
let tokenIn = "0x...";
let tokenOut = "0x...";
fetch(`https://heimdall-5lo5blc2.uc.gateway.dev/uniswap/token-price/${chainId}/${amount}/${tokenIn}/${tokenOut}`)
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
#### Python

```python
chain_id = "1"
amount = "100"
token_in = "0x..."
token_out = "0x..."
response = requests.get(f"https://heimdall-5lo5blc2.uc.gateway.dev/uniswap/token-price/{chain_id}/{amount}/{token_in}/{token_out}")
print(response.text)
```

### Get Transaction Data

This endpoint provides data for a specific transaction identified by its hash and the blockchain chain ID through a `GET`.

`https://heimdall-5lo5blc2.uc.gateway.dev/evm/transaction/{txHash}`

#### JAVA

```java
HttpClient client = HttpClient.newHttpClient();
String chainId = "1";  // Example for Ethereum Mainnet
String txHash = "0x123abc...";  // Replace with actual transaction hash
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/evm/transaction/" + chainId + "/" + txHash))
    .GET()
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());

```

#### C#

```C#
HttpClient client = new HttpClient();
string chainId = "1";  // Example for Ethereum Mainnet
string txHash = "0x123abc...";  // Replace with actual transaction hash
HttpResponseMessage response = await client.GetAsync($"https://heimdall-5lo5blc2.uc.gateway.dev/evm/transaction/{chainId}/{txHash}");
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);

```

#### JavaScript

```JavaScript
const chainId = "1";  // Example for Ethereum Mainnet
const txHash = "0x123abc...";  // Replace with actual transaction hash
fetch(`https://heimdall-5lo5blc2.uc.gateway.dev/evm/transaction/${chainId}/${txHash}`)
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

```
#### Python

```python
import requests

chain_id = "1"  # Example for Ethereum Mainnet
tx_hash = "0x123abc..."  # Replace with actual transaction hash
url = f"https://heimdall-5lo5blc2.uc.gateway.dev/evm/transaction/{chain_id}/{tx_hash}"
response = requests.get(url)
print(response.text)
```

### Add Wallet

This endpoint is used to register a new wallet for monitoring. The wallet address is sent in the body of the `POST` request.

`https://heimdall-5lo5blc2.uc.gateway.dev/wallets/addWallet`

#### JAVA

```java
HttpClient client = HttpClient.newHttpClient();
String walletAddress = "0xabcdef...";  // Replace with actual wallet address
String requestBody = "{\"address\":\"" + walletAddress + "\"}";
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/wallets/addWallet"))
    .header("Content-Type", "application/json")
    .POST(HttpRequest.BodyPublishers.ofString(requestBody))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### C#

```C#
HttpClient client = new HttpClient();
string walletAddress = "0xabcdef...";  // Replace with actual wallet address
HttpContent content = new StringContent("{\"address\":\"" + walletAddress + "\"}", Encoding.UTF8, "application/json");
HttpResponseMessage response = await client.PostAsync("https://heimdall-5lo5blc2.uc.gateway.dev/wallets/addWallet", content);
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);
```

#### JavaScript

```JavaScript
const walletAddress = "0xabcdef...";  // Replace with actual wallet address
fetch('https://heimdall-5lo5blc2.uc.gateway.dev/wallets/addWallet', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({ address: walletAddress })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
#### Python

```python
import requests

wallet_address = "0xabcdef..."  # Replace with actual wallet address
data = {"address": wallet_address}
response = requests.post("https://heimdall-5lo5blc2.uc.gateway.dev/wallets/addWallet", json=data)
print(response.text)
```
### Add Contract

This endpoint is used to add a contract to the monitoring system by providing the chain ID and contract address in `POST`the request body.

`https://heimdall-5lo5blc2.uc.gateway.dev/contracts/addContract`

#### JAVA

```java
HttpClient client = HttpClient.newHttpClient();
String requestBody = "{\"chainId\":\"1\", \"address\":\"0x123456...\"}"; // Replace with actual chain ID and contract address
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://heimdall-5lo5blc2.uc.gateway.dev/contracts/addContract"))
    .header("Content-Type", "application/json")
    .POST(HttpRequest.BodyPublishers.ofString(requestBody))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());

```

#### C#

```C#
HttpClient client = new HttpClient();
string requestBody = "{\"chainId\":\"1\", \"address\":\"0x123456...\"}"; // Replace with actual chain ID and contract address
HttpContent content = new StringContent(requestBody, Encoding.UTF8, "application/json");
HttpResponseMessage response = await client.PostAsync("https://heimdall-5lo5blc2.uc.gateway.dev/contracts/addContract", content);
string result = await response.Content.ReadAsStringAsync();
Console.WriteLine(result);

```

#### JavaScript

```JavaScript
const requestBody = {
    chainId: "1",  // Example for Ethereum Mainnet
    address: "0x123456..."  // Replace with actual contract address
};
fetch('https://heimdall-5lo5blc2.uc.gateway.dev/contracts/addContract', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(requestBody)
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

```
#### Python

```python
import requests

data = {
    "chainId": "1",  // Example for Ethereum Mainnet
    "address": "0x123456..."  // Replace with actual contract address
}
response = requests.post("https://heimdall-5lo5blc2.uc.gateway.dev/contracts/addContract", json=data)
print(response.text)

```


 
