
# Symmetrical Update contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Arbitrum One, Arbitrum Nova, Fantom, Optimism, BNB chain,  Polygon, Avalanche, Base
___

### Q: Which ERC20 tokens do you expect will interact with the smart contracts? 
USDT and USDC 
___

### Q: Which ERC721 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Which ERC777 tokens do you expect will interact with the smart contracts? 
none
___

### Q: Are there any FEE-ON-TRANSFER tokens interacting with the smart contracts?

none
___

### Q: Are there any REBASING tokens interacting with the smart contracts?

none
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED?
TRUSTED
___

### Q: Is the admin/owner of the protocol/contracts TRUSTED or RESTRICTED?
TRUSTED
___

### Q: Are there any additional protocol roles? If yes, please explain in detail:
MUON_SETTER_ROLE: Can change settings of the Muon Oracle.
SYMBOL_MANAGER_ROLE: Can add, edit, and remove markets, as well as change market settings like fees and minimum acceptable position size.
PAUSER_ROLE: Can pause all system operations.
UNPAUSER_ROLE: Can unpause all system operations.
PARTY_B_MANAGER_ROLE: Can add new partyBs to the system.
LIQUIDATOR_ROLE: Can liquidate users.
SETTER_ROLE: Can change main system settings.
Note: All roles are trusted except for LIQUIDATOR_ROLE.
___

### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
ERC-2535: Diamonds, Multi-Facet Proxy  
Create modular smart contract systems that can be extended after deployment.
___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
There are some already found issues here in the previous contest

https://github.com/sherlock-audit/2023-06-symmetrical-judging
___

### Q: Please provide links to previous audits (if any).
https://github.com/sherlock-audit/2023-06-symmetrical-judging
___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)?
Liquidator Bots, Force close Bots, Force cancel Bots, Anomaly detector Bots
___

### Q: In case of external protocol integrations, are the risks of external contracts pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality.
1- Collateral tokens, which are stablecoins, we accept the risks.

2- The potential for the Muon app to be down or give inaccurate data is also considered acceptable.
___

### Q: Do you expect to use any of the following tokens with non-standard behaviour with the smart contracts?
Yes... USDC and USDT can be used as collateral
___

### Q: Add links to relevant protocol resources
https://docs.symm.io/protocol-overview/general-information

https://docs.symm.io/building-on-symm-io/technical-documentation
___



# Audit scope


[symmio-core @ 0dec905617d3c6355ce4393de3e77274b90e2eb4](https://github.com/SYMM-IO/symmio-core/tree/0dec905617d3c6355ce4393de3e77274b90e2eb4)
- [symmio-core/contracts/Diamond.sol](symmio-core/contracts/Diamond.sol)
- [symmio-core/contracts/facets/Account/AccountFacet.sol](symmio-core/contracts/facets/Account/AccountFacet.sol)
- [symmio-core/contracts/facets/Account/AccountFacetImpl.sol](symmio-core/contracts/facets/Account/AccountFacetImpl.sol)
- [symmio-core/contracts/facets/Account/IAccountEvents.sol](symmio-core/contracts/facets/Account/IAccountEvents.sol)
- [symmio-core/contracts/facets/DiamondCutFacet.sol](symmio-core/contracts/facets/DiamondCutFacet.sol)
- [symmio-core/contracts/facets/DiamondLoupFacet.sol](symmio-core/contracts/facets/DiamondLoupFacet.sol)
- [symmio-core/contracts/facets/PartyA/IPartyAEvents.sol](symmio-core/contracts/facets/PartyA/IPartyAEvents.sol)
- [symmio-core/contracts/facets/PartyA/PartyAFacet.sol](symmio-core/contracts/facets/PartyA/PartyAFacet.sol)
- [symmio-core/contracts/facets/PartyA/PartyAFacetImpl.sol](symmio-core/contracts/facets/PartyA/PartyAFacetImpl.sol)
- [symmio-core/contracts/facets/PartyB/IPartyBEvents.sol](symmio-core/contracts/facets/PartyB/IPartyBEvents.sol)
- [symmio-core/contracts/facets/PartyB/PartyBFacet.sol](symmio-core/contracts/facets/PartyB/PartyBFacet.sol)
- [symmio-core/contracts/facets/PartyB/PartyBFacetImpl.sol](symmio-core/contracts/facets/PartyB/PartyBFacetImpl.sol)
- [symmio-core/contracts/facets/ViewFacet.sol](symmio-core/contracts/facets/ViewFacet.sol)
- [symmio-core/contracts/facets/control/ControlFacet.sol](symmio-core/contracts/facets/control/ControlFacet.sol)
- [symmio-core/contracts/facets/control/IControlEvents.sol](symmio-core/contracts/facets/control/IControlEvents.sol)
- [symmio-core/contracts/facets/liquidation/ILiquidationEvents.sol](symmio-core/contracts/facets/liquidation/ILiquidationEvents.sol)
- [symmio-core/contracts/facets/liquidation/LiquidationFacet.sol](symmio-core/contracts/facets/liquidation/LiquidationFacet.sol)
- [symmio-core/contracts/facets/liquidation/LiquidationFacetImpl.sol](symmio-core/contracts/facets/liquidation/LiquidationFacetImpl.sol)
- [symmio-core/contracts/interfaces/IDiamondCut.sol](symmio-core/contracts/interfaces/IDiamondCut.sol)
- [symmio-core/contracts/interfaces/IDiamondLoupe.sol](symmio-core/contracts/interfaces/IDiamondLoupe.sol)
- [symmio-core/contracts/interfaces/IERC165.sol](symmio-core/contracts/interfaces/IERC165.sol)
- [symmio-core/contracts/interfaces/IMultiAccount.sol](symmio-core/contracts/interfaces/IMultiAccount.sol)
- [symmio-core/contracts/interfaces/ISymmio.sol](symmio-core/contracts/interfaces/ISymmio.sol)
- [symmio-core/contracts/interfaces/ISymmioPartyA.sol](symmio-core/contracts/interfaces/ISymmioPartyA.sol)
- [symmio-core/contracts/libraries/LibAccessibility.sol](symmio-core/contracts/libraries/LibAccessibility.sol)
- [symmio-core/contracts/libraries/LibAccount.sol](symmio-core/contracts/libraries/LibAccount.sol)
- [symmio-core/contracts/libraries/LibDiamond.sol](symmio-core/contracts/libraries/LibDiamond.sol)
- [symmio-core/contracts/libraries/LibLockedValues.sol](symmio-core/contracts/libraries/LibLockedValues.sol)
- [symmio-core/contracts/libraries/LibMuon.sol](symmio-core/contracts/libraries/LibMuon.sol)
- [symmio-core/contracts/libraries/LibMuonV04ClientBase.sol](symmio-core/contracts/libraries/LibMuonV04ClientBase.sol)
- [symmio-core/contracts/libraries/LibPartyB.sol](symmio-core/contracts/libraries/LibPartyB.sol)
- [symmio-core/contracts/libraries/LibQuote.sol](symmio-core/contracts/libraries/LibQuote.sol)
- [symmio-core/contracts/libraries/LibSolvency.sol](symmio-core/contracts/libraries/LibSolvency.sol)
- [symmio-core/contracts/multiAccount/MultiAccount.sol](symmio-core/contracts/multiAccount/MultiAccount.sol)
- [symmio-core/contracts/multiAccount/SymmioPartyA.sol](symmio-core/contracts/multiAccount/SymmioPartyA.sol)
- [symmio-core/contracts/multiAccount/SymmioPartyB.sol](symmio-core/contracts/multiAccount/SymmioPartyB.sol)
- [symmio-core/contracts/storages/AccountStorage.sol](symmio-core/contracts/storages/AccountStorage.sol)
- [symmio-core/contracts/storages/GlobalAppStorage.sol](symmio-core/contracts/storages/GlobalAppStorage.sol)
- [symmio-core/contracts/storages/MAStorage.sol](symmio-core/contracts/storages/MAStorage.sol)
- [symmio-core/contracts/storages/MuonStorage.sol](symmio-core/contracts/storages/MuonStorage.sol)
- [symmio-core/contracts/storages/QuoteStorage.sol](symmio-core/contracts/storages/QuoteStorage.sol)
- [symmio-core/contracts/storages/SymbolStorage.sol](symmio-core/contracts/storages/SymbolStorage.sol)
- [symmio-core/contracts/upgradeInitializers/DiamondInit.sol](symmio-core/contracts/upgradeInitializers/DiamondInit.sol)
- [symmio-core/contracts/utils/Accessibility.sol](symmio-core/contracts/utils/Accessibility.sol)
- [symmio-core/contracts/utils/Ownable.sol](symmio-core/contracts/utils/Ownable.sol)
- [symmio-core/contracts/utils/Pausable.sol](symmio-core/contracts/utils/Pausable.sol)


