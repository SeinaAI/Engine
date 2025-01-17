<div align="left">

## Seina 🌗

<img src="https://cdn.discordapp.com/attachments/975464918939742268/1329922414108479498/360_F_640359075_73HXrNPNVxRjX6fFctQBbyeRGsIgEtXU.jpg?ex=678c1a44&is=678ac8c4&hm=6883f0c94cc0656fd28b0924bdc17d6c7c621451808a7d25144ff04f4c275418&" alt="gitBanner" />

&nbsp;

**Seina** is an open-source framework for adding blockchain tools such as wallets, being able to hold or trade tokens, or interacting with blockchain smart contracts, to your AI agent.

&nbsp;

**Problem**: 

Making agents perform onchain actions is tedious. The ecosystem is heavily fragmented, spanning 5+ popular agent development frameworks, multiple programming languages, and dozens of different blockchains and wallet architectures.
For developers without blockchain expertise, finding clear instructions to perform simple actions - like sending USDC payments or placing Polymarket bets - is nearly impossible.

&nbsp;

**Solution**: 

**Seina** solves this by providing an open-source, provider-agnostic framework that abstracts away all these combinations.

- **For agent developers**: **Seina** offers an always-growing catalog of ready made blockchain actions (sending tokens, using a DeFi protocol, ...) that can be imported as tools into your existing agent. It works with the most popular agent frameworks (Langchain, Vercel's AI SDK, Eliza, etc), Typescript and Python, 30+ blockchains (Solana, Base, Polygon, Mode, ...), and many wallet providers.

- **For dApp / smart contract developers**: develop a plug-in in **Seina**, and allow agents built with any of the most popular agent development frameworks to access your service.

&nbsp;

### Key features
1. **Works Everywhere**: Compatible with Langchain, Vercel’s AI SDK, Eliza, and more.
2. **Wallet Agnostic**: Supports all wallets, from your own key pairs to CEXs.
3. **Multi-Chain**: Supports EVM chains and Solana (more coming 👀).
4. **Customizable**: Use or build plugins for any onchain functionality (sending tokens, checking wallet balance, etc) and protocol (Polymarket, Uniswap, etc).

&nbsp;

### How it works
**Seina** plugs into your agents tool calling capabilities adding all the functions your agent needs to interact with the blockchain. 

High-level, here's how it works:

#### Configure the wallet you want to use
```typescript
// ... Code to connect your wallet (e.g createWalletClient from viem)
const wallet = ...

const tools = getOnChainTools({
  wallet: viem(wallet),
})
```

#### Add the plugins you need to interact with the protocols you want
```typescript
const wallet = ...

const tools = getOnChainTools({
  wallet: viem(wallet),
  plugins: [
    sendETH(),
    erc20({ tokens: [USDC, PEPE] }),
    faucet(),
    polymarket(),
    // ...
  ],
})
```

#### Connect it to your agent framework of choice
```typescript
// ... Code to connect your wallet (e.g createWalletClient from viem)
const wallet = ...

const tools = getOnChainTools({
  wallet: viem(wallet),
  plugins: [ 
    sendETH(),
    erc20({ tokens: [USDC, PEPE] }), 
    faucet(), 
    polymarket(), 
    // ...
  ],
})

// Vercel's AI SDK
const result = await generateText({
    model: openai("gpt-4o-mini"),
    tools: tools,
    maxSteps: 5,
    prompt: "Send 150 ETH to selene.eth",
});
```

&nbsp;

[More Examples](https://github.com/0xOyster/Selene/tree/main/typescript/examples)
