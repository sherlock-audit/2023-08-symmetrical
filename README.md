
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

### Additional context into the update contest:

In the ever-evolving landscape of software development, continuous improvement is key. Our team has recently completed
the first part of the Sherlock Audit contest for our project, and several important changes have been made to enhance
functionality, improve security, and fix bugs. Below is a comprehensive list of commits, each accompanied by a brief
explanation to provide context for the updates.

### Commit List and Explanations

1. **Allowing PartyBs to Deregister**
    - This update allows partyBs to deregister from the system, offering greater flexibility in user participation.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/696836fd00cf5392ef95f78129fdb50c4008fcf4)

2. **Check for Zero Address in PartyB Registering**
    - This change adds a validation check to prevent registration of a zero address as partyB.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/d866948523c18354199c44f9c509f1dcbc27ac63)

3. **Fix the Pending Locked Balance of PartyB When Position is Opened Partially**
    - This update corrects the pending locked balance of partyB when a position is opened partially. Specifically, all
      pending locked amounts of the quote should have been released.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/439206d72ec9ca96b7b7c13ef14d4b3eb5d5c7f3)

4. **Fix the Bug that the PartyA Nonce Was Incremented Before Setting the PartyB Field on Quote**
    - This change addresses a bug where the nonce for partyA was incremented before setting the partyB field on the
      quote.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/e9708a882b610397145b84343e6ba9df40ed63e7)

5. **Check Symbol's Validness Before Opening the Position**
    - This update adds a check to validate the trading symbol before opening a position.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/104dbdfd9b1db81d1b0edb222a36010230e36cca)

6. **Bug in Liquidation Process Allowing Reuse of Old Signatures**
    - This change fixes a bug in the liquidation process that allowed users to use old signatures, possibly from
      previous liquidations, more than once.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/98eb13e005e3d8eafeaae207ce779ae8ab47a5a2)

7. **Change in Trading Fee Process**
    - This update modifies the process of collecting trading fees. Specifically, it prevents the fee collector from
      withdrawing collected fees when the respective positions are not yet opened. The trading fee is now subtracted
      from the allocated balance of the user and handed over to the fee collector when the position opens.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/96d23fedd4a13a40a17a7e36d40a9111e120f25a)

8. **Fix the Bug that Expired Signatures Can Be Used in Liquidating PartyB**
    - This change corrects a bug that allowed expired signatures to be used in the liquidation process for partyB.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/a2410a85eab2429ed3a5145b86ed141dc36a4c2d)

9. **Trading Fee Could Have Changed While the Quote is Pending**
    - This update addresses an issue where the trading fee could change while a quote is pending but not yet opened.
      This could result in a loss or profit for the user. Now, the trading fee that the quote is sent with is stored in
      the quote structure itself. Additionally, trading fees of pending quotes are returned to the user when the quote
      gets liquidated.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/bf447ecbb1d00ce71735898606ed92bdeaee1114)

10. **Bug with Decimals in depositAndAllocateForPartyB Method**
    - This change resolves a bug related to decimal handling in the `depositAndAllocateForPartyB` method. It also
      removes the redundant `depositForPartyB` method.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/93af25a9b67db81da2190bc890240ff82b4c803f)

11. **PartyB Should Not Deallocate or Transfer During Unfinished Liquidation**
    - This update prevents partyB from deallocating or transferring its allocated collateral when the user is liquidated
      but their liquidation process is not yet complete. This is because partyB may still owe money to the user.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/d1e00f179a4b98329fda4528ca74fc66d7235598)

12. **Muon Signatures Share the Same Set of Fields**
    - To address the issue of muon signatures sharing the same set of fields, this change adds the name itself to the
      hash to make each signature unique.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/4270112464239b77deb276bbbcb280025d467c8b)

13. **Problem with PartyB Postponing Force Close**
    - This update fixes a problem where partyB could delay a force close by closing a small part of the request and
      updating the `modifyTimestamp` field. The field name is now changed to `statusModifyTimestamp` and, as the name
      suggests, it only changes when the quote status changes.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/9afb4ef041f09d09e8264f02718cecfd93029462)

14. **Post-Solvency Check Issue in Open Position Function**
    - This commit addresses an issue with the post-solvency check in the `openPosition` function. The problem was that
      after the check we were updating its corresponding locked values so the checking wasn't valid (The provided
      solution in this commit has some problems that the locked values of quote were considered twice... It got fixed in
      another commit later: 33rd item)
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/decf86f0b9eb678003736e148fbbb1b91861c137)

15. **Upnl Signature Reusability in Liquidation**
    - This update fixes a problem where the Upnl signature of liquidation could be reused in other functions. To prevent
      this, the partyA nonce, which is a part of the signature in liquidation, is incremented.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/68eae953c77e183925fc8ccf4eb9d2958f674d24)

16. **Review of Nonce Increases in Code**
    - This change involves a comprehensive review of all places in the code where nonces are increased. Unnecessary
      nonce increments were removed, and missing ones were added.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/b8315f4dd82a01554fe6fa7517101469e40fd5ed)

17. **Emergency Close Functionality for ClosePending Positions**
    - This update fixes an issue where `ClosePending` positions were not allowed in the `emergencyClose` function. The
      absence of this feature could be abused by partyA to prevent their positions from being emergency closed by
      partyB.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/76cd78c66a8f31289fd59004285d9f7170855d5c)

18. **Mistake in ForceClose Method**
    - This commit corrects a mistake in the `ForceClose` method where the quote was being closed by
      its `requestedClosePrice` instead of the actual price that comes from the signature.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/7cf25b050873981ef44aa54fbcc0387f81e821c8)

19. **Check for Token Decimals in SetCollateral Method**
    - This update adds a check to ensure that token decimals in the `SetCollateral` method are not greater than 18, as
      the rest of the code expects them to be that way.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/735386aeb20694ad4c08f979c51bb5ebc554cf5a)

20. **Update Locked Values for Market Orders When Position Opens**
    - This commit ensures that locked values for market orders are also updated when a position is opened, maintaining
      the integrity of the trading system.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/2e786f1740fc074ed307e0ebd0042ee9bb57f04e)

21. **Remove Solvency Check During Position Close Request**
    - This update removes the solvency check for users when they request to close their positions. The rationale is that
      the user's solvency state may change by the time partyB wants to fill the close request.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/d83c3afe71af299ca431ca124c019e5bf81dcbe8)

22. **Revision of PartyA Liquidation Process**
    - This change addresses several issues in the liquidation process for partyA. One problem was that if a user becomes
      solvent after the first liquidation step, there would be leftover money that didn't belong to anyone. To fix this,
      the process now requires the same signatures in both the first and second steps. Another issue was that pending
      positions were changed to 'LIQUIDATED' status during liquidation, which was unclear for third-party services. This
      has been changed to 'CANCELLED' status for better clarity.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/8b27d99f312f17a857f75ed245eecdad6d17b17d)

23. **Introduction of Funding Rate Feature**
    - This update introduces the funding rate feature to the system. Detailed information about the funding rate and its
      implementation can be found in the documentation.
      [GitHub Commit 1](https://github.com/SYMM-IO/symmio-core/pull/30/commits/4b81f6ec891c32448f05fad2d4315e8aaeb91b2e)
      [GitHub Commit 2](https://github.com/SYMM-IO/symmio-core/pull/30/commits/c52f251b25cda580b963dcc2d85c9ff733835876)
      [GitHub Commit 3](https://github.com/SYMM-IO/symmio-core/pull/30/commits/e892e8907ecfe44ccbd09761a54192851d1a9e61)

24. **Prevent Suspended PartyAs from Opening Positions**
    - This update prevents partyAs that are suspended from opening new positions.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/53453970e0f82b2703b3d09c3f8d9c6364faae0f)

25. **Handling Insufficient Funds for PartyB**
    - This commit addresses a scenario where partyB may not have enough money to fully pay partyA. This could happen
      when partyB is also liquidatable but has not yet been liquidated by the liquidator. In such cases, partyA might
      not receive their full profits.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/f052a6c1b9f39aa034f3417582a9f34ff1d2412b)

26. **Additional Checks for Small Calculation Errors in Closing Quote**
    - This update adds some extra checks to account for possible but very small calculation errors that could occur when
      closing a quote.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/0b41dafa619ae1a10877c5327dffc71a81017550)

27. **Ensure No Old Collateral Is Left When Changing Collateral Token**
    - This change adds an additional check to ensure that no old collateral is left on the contract when changing the
      collateral token.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/7c8ed469fcea25abfda322f28f53d588f8587c76)

28. **Check for Minimum Quote Value in OpenPosition Method**
    - This update adds checks in the `openPosition` method to ensure that the quote value doesn't fall below the minimum
      acceptable amount due to price changes.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/d9a6eda876ec785b99f0b7ca75fd1b89f01a76eb)

29. **Setting Max Leverage for Symbols on the Contract**
    - This commit allows for the setting of maximum leverage for trading symbols directly on the contract.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/f0787e37644a8f310e3b00b27a0f54ff8d8c3bb7)

30. **Restrictions on PartyB in Emergency Mode**
    - This update prevents a partyB that is in emergency mode from opening a new position. This is because they could
      abuse this state to close positions at will and take profits. As the name suggests, emergency mode is extremely
      rare and only intended for genuine emergencies.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/pull/30/commits/8d2034fe5a06a503e66facbeea7cdb9ebb9bddcd)

31. **Multi-Account and Proxy Contract Features**
    - This commit adds a multi-account feature, allowing users to have multiple accounts linked to the same wallet. This
      enables users to simulate isolated trading modes. Additionally, partyB can now use multiple wallets but still
      appear in the system under a single address, thanks to a proxy contract known as the SymmioPartyB contract.
      [GitHub Commit 1](https://github.com/SYMM-IO/symmio-core/pull/30/commits/e532a027a6929e87e43caf297be8c5976e6547ad)
      [GitHub Commit 2](https://github.com/SYMM-IO/symmio-core/pull/30/commits/1f27baab6071be9a4691b9c823cbf94810565f6c)

32. **Check for Expired Signatures in LiquidatePartyA Method**
    - This update adds a check to prevent the use of expired signatures in the `LiquidatePartyA` method.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/commit/55b6b4202b75a318ee81b21e5e057c7b5d3a912f)

33. **Issue with Double-Counting Locked Values in Post-Solvency Check**
    - This commit resolves an issue in the post-solvency check performed when opening a position. Specifically, the
      locked values of the opening position were being double-counted in the calculations.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/commit/9c4fe32b3f28179799f79a23b191b8b9ddd13642)

34. **Optimization of PartyB Contract Size for Deployment**
    - This change addresses a problem where the PartyB contract was too large for deployment. One of its methods has
      been extracted to another library to resolve this issue.
      [GitHub Commit](https://github.com/SYMM-IO/symmio-core/commit/5165b7419d67cc410048c28f8c6f9d2616c069fa)

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



