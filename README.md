# CBDC (Central Bank Digital Currency) Token using Corda


**Wholesale CBDC** :
    The wholesale CBDCs are suitable for financial institutions holding reserve deposits in a central bank. 
    The wholesale central bank digital currency can help in improving efficiency of payments and security settlement. 
    Additionally, it also resolves the concerns of liquidity and counterparty credit.

**Two-tier system with direct ledger access**
--------------------------------------------
We can demonstrate a CBDC as a sequence of state changes:
1. Collateralization of fiat currency against the issued CBDC as a bearer asset
2. Wholesale transfer moves the CBDC from the central bank to participant 1
3. Withdraw, representing the movement of the CBDC from the wholesale ecosystem to the retail
   ecosystem
4. CBDC transfers to from one retail holder to another
5. Retail user deposited the CBDC back into the wholesale system
6. Wholesale transfers back the CBDC to the central bank
7. The central banks redeems the CBDC against the original fiat funds

----------------------------------------------------------------------------------------
**How to build** 

` 1. cd ../Corda-CBDC/CBDC/`

` 2. ./gradlew deployNodes`

 `3. cd build/nodes/`

 `4. ./runnodes`

------------------------------------------------------------------------------------------
**Nodes in Network:**
1. Central Bank (UK Mint): O=UK Mint, L=London, C=GB
2. Wholesale Bank/Commercial Bank (client Bank): O=client, L=London, C=GB
3. Retail Bank (HSBC Bank) :O=HSBC, L=London, C=GB

----------------------------------------------------------------------------------------
Run the following steps in given order.

Note : you can check the balance of token on any node by running

        `flow start GetCBDCBalance`

 1.Goto node : O=UK Mint, L=London, C=GB : 
  Central bank issue e-GBP (CBDC)  worth of 100 GBP
  
  `flow start IssueEGBPFlow centralBank: "O=UK Mint, L=London, C=GB",amount: 100`

2. Goto node O=UK Mint, L=London, C=GB :
    Wholesale transfer moves the CBDC from the central bank to Commercial Bank (client Bank)

`flow start TransferEGBPFlow party: "O=client, L=London, C=GB", amount: 100`

 3. Goto node : O=client, L=London, C=GB
  client Bank transfer the CBDC to Retail Bank(HSBC Bank)
  
  `flow start TransferEGBPFlow party: "O=HSBC, L=London, C=GB", amount: 100`

 4. Goto node : O=HSBC, L=London, C=GB
  Retail(HSBC) user deposited the CBDC back into the wholesale system(client)
  
`flow start TransferEGBPFlow party: "O=client, L=London, C=GB", amount: 100`

 5. GOTO Node :O=client, L=London, C=GB 
    Wholesale transfers(client) back the CBDC to the central bank(UK mint)
    
    `flow start TransferEGBPFlow party: "O=UK Mint, L=London, C=GB", amount: 100`
    
 6. GOTO node:O=UK Mint, L=London, C=GB : The central banks redeems the CBDC against the original fiat funds
 
    `flow start RedeemEGbpFlow amount: 100`
    
    you will find that all the tokens are destroyed after it has been through the wholesale payment
    system using this flow
    
    `flow start GetCBDCBalance` should show 0
    
    
 
-----------------------------------------------------------------------------------------






