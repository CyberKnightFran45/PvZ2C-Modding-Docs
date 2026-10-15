# PvZ2C Modding Guide: How to modify your pp.dat?

The pp.dat file contains the player's progress serialized as binary data.

> Keep in mind that the Chinese version of PvZ2 has an anti-hacking system that detects changes in the data and reverts them.
Modifying certain values in recent versions of the game risks getting your account permanently banned.

---

**NOTE: I AM NOT RESPONSIBLE FOR ACCOUNT BLOCKING OR DATA LOSS. EDIT AT YOUR OWN RISK.**

That said, follow these steps to the letter.

1️⃣   Extract the file

Extract the pp.dat file from: **_/>data>data>com.popcap.pvz2cthdxx>no_backup_** and then move it to a folder where you can easily locate it.

`xx = 360, 4399, or cdbk, this varies depending on the game version`

**NOTE: To access this directory, your device must be rooted.
Also, don't forget to back up your data in case something goes wrong.**

2️⃣   Decode the file

RTONs from Chinese version are encrypted, so you will need to decrypt the file first and then decode it.

I recommend using [Sen](https://senharuma.com/es) or [RIPE](https://github.com/CyberKnightFran45/RipeConsole) for this. Although there are other tools available, they come with limitations or are obsolete.

(A) Sen: drag the file into the program and select **option 39 (PopCap RTON Encrypted to JSON)**

(B) RIPE: drag the file into the program and select **option 16 (RTON Parser - Decode)**

3️⃣   Download the editing software

Next, download one of the following programs:

- To edit on Windows

```
JSON Editor
Notepad++
```

- To edit on Android

```
MT Manager
JSON Validator
```

These are text editors for handling JSON files on different platforms.

4️⃣   Modify your save

You can modify the values to whatever amount you want.

Just make sure not to exceed `2,147,483,647` or they will become negative due to an overflow.

---

# Save fields

The following table maps each `pp` RTON property to its actual member in the cpp instance.

Reference version: `3.5.7 (debug)`

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Random seed  | rs |      m_randomSeed    |    uint        |
| Username  | n |      m_name    |    string        |
| Coins  | c |      m_coins    |    LawnKeyField     |
| Last Game Version | ffc |      m_strLastProductVersion    |    string     |
| Persistent data for some events | luapd |      m_strLuaPersistentData    |    string     |
| Unlocked Recharge Prizes  | urn |      m_unlockedRechargeNodes    |    RechargeNode[]     |
| Recharged Yuan (New UI)  | newrcc |      m_rechargeCurrency    |    LawnKeyField     |
| New Top-ups Prizes  | ntrrs |      m_newTotalRechargeRewardStatus    |    int[]     |
| Today Recharged Yuan  | trc |      m_todayRechargeCurrency    |    LawnKeyField     |
| Someday Yuan Recharge  | vdrc |      m_somedayRechargeCurrency    |    DailyRechargeCurrency[]     |
| Someday Gems Consumption  | vdgcc |      m_somedayGemConsumeCurrency    |    DailyRechargeCurrency[]     |
| Today Recharge Products  | trcp |      m_todayRechargeProductId    |    string[]     |
| Today Max Recharged Yuan  | mtrc |      m_todayMaxRechargeCurrency    |    LawnKeyField     |
| Today Date | td |      m_todayDate    |    int     |
| Monthly Recharged Yuan  | mrc |      m_monthRechargeCurrency    |    LawnKeyField     |
| Month Date | md |     m_monthDate    |    int     |
| Activity Recharge Completed | bar |     m_bActivityRecharge    |    bool     |
| Activity Left Time | alt |     m_activityLeftTime    |    int     |
| Have Purchased Tactical Bundle | hpcp |    m_bHasPurchaseCukePkg     |    bool     |
| Has Obtained First Recharge Award | grcdb |     m_hasGotFirstRechargeReward    |    bool     |
| First Recharge Rewards | grcdl |    m_GetRechargeDoubleList     |    FirstRechargeAwardData[]     |
| Has Recharge Piece Reward | hrpr |    m_bHasRechargePieceReward     |    bool     |
| Single Recharge Completed  | slrc |    m_bSingleRecharge     |    bool     |
| Limited Bundles Display  | dsplbd |    m_displayingBundle     |    BundleDisplay[]     |
| Limited Bundles Queue Conditions | quebc |    m_queuedBundleCondition     |    BundleQueueCondition[]     |
| Queued Limited Bundles | quebds |    m_queuedBundles     |    int[]     |
| Gems  | g |      m_gems    |    LawnKeyField     |
| Gems Given  | gg |      m_giveGems    |    GemCurrency     |
| ZPS | zs |      m_zombossSignal    |    ZombossSignalCurrency     |
| Has Recharged | rcg |     m_bRecharge    |    bool     |
| First Plant Buy | fbp |     m_bFirstBuyPlant    |    bool     |
| First Plant Bag Buy | fbpb |     m_bFirstBuyPlantBag    |    bool     |
| Has Bought New Gift Pack | nwpt |     m_bNewerPresent    |    bool     |
| Has Bought Advanced Gift Pack | adnwpt |     m_bAdvanceNewerPresent    |    bool     |
| Stars  | s |      m_stars    |    LawnKeyField        |
| Last Level Played  | l |      m_level    |    string        |
| New WorldMap Data  | wmed |      m_worldMapEventData    |    WorldCompletionData[]        |
| Plants  | p |      m_unlockedPlants    |    int[]        |
| Profile Version  | v |      m_version    |    PlayerProfileVersion        |
| Red Envelopes  | rp |      m_redPacket    |    LawnKeyField        |
| OS Version > 7  | losvis |     m_lastOSVersonIsSeven    |    bool      |
| Sign UUID (created on installation)  | snuuid | m_sign_uuid   |    string      |
| Upgrades  | gf |      m_unlockedGameFeatures    |    GameFeature[]        |
| New Tutorial Progress  | tpn |      m_tutorialNewProgress    |    MapTutorialState        |
| Completed New Tutorials | etnpa |      m_exTutorialNewProgressArray    |    MapTutorialState[]        |
| Completed Narration Events (World Map) | ne |      m_completedNarrationEvents    |    int[]        |
| Killed Zombies | kz |      m_killedZombies    |    int[]        |
| Powerups | pr |      m_powerupRecords    |    PowerupRecord[]        |
| Return to Universe Map | um |      m_onUniverseMap    |    bool       |
| Last WorldMap Zoom | lmz |      m_lastWorldMapZoom    |    float       |
| Player ID (not set) | pri |      m_profileId    |    int32       |
| Profile Index (same as rs) | i |      m_index    |    PlayerProfileIndex       |
| Version Number | vn |      m_versionNumber    |    int32       |
| Profile Creation Time (not set) | pct |      m_profileCreatedTime    |     time_t      |
| Marked for Deletion | mfd |      m_markedForDelete    |     bool      |
| Lifetime Session Count | lsc |      m_lifetimeSessionCount    |     uint32      |
| Last Tutorial Event Time | ltfet |      m_lastTutorialFunnelEventTime    |     time_t      |
| Highest Tutorial Event Reached | hter |      m_highestTutorialEventReached    |     uint8      |
| Plant Pieces | ppr |      m_plantPieceRecords    |     PlantPieceRecord[]      |
| Pendant Pieces | asp |      m_accessoryPieces    |     AccessoryPiece[]      |
| Skycity Weapons | rcstl |      m_reconstructionLevel    |     ReconstructionLevel[]      |
| Plant Levels | psla |      m_plantStarLevelArray    |     PlantStarLevel[]      |
| Current Artifact equipped | catfc |      m_currentArtifact    |     int      |
| Artifacts Info | atfcla |      m_artifactListArray    |     ArtifactInfo[]      |
| Plant Genes | mpgl |      m_plantGeneList    |     PlantGeneInfo[]      |
| Gene Essence | mpgel |      m_plantGeneEssenceList    |     PlantGeneEssenceInfo[]      |
| Zombie Levels | zsla |      m_zombieStarLevelArray    |     ZombieStarLevel[]      |
| Plants Awaken (Plant Adventure) | pawf |      m_plantAwakenInfo    |    int[]        |
| Daily Challenge Info | ainfo |      m_curOnlineEventInfo    |    OnlineEventInfo        |
| Last Plant Piece Completion  | lppcs |     m_LastplantPieceCompletionShow    |    int        |
| Number of Killed Zombies | kzn |      m_killedZombiesNum    |    int32        |
| Gold Return Value | rgv |      m_returnGoldValue    |    int32        |
| World Keys Return Value | rwkv |     m_returnWorldKeyValue     |    int        |
| Hard World Order | hwo |    m_hardWorldOrder      |    uint8[]        |
| Lottery Plays | dlt |    m_doLotteryTimes      |    int        |
| Last Lottery Date | lld |    m_lastLotteryDate      |    int        |
| Last Lottery Year | lly |    m_lastLotteryYear      |    int        |
| Display Reward Dialog | nsrd |    m_needShowRewardDialog      |    bool        |
| Display Rate App Dialog | nsrad |    m_needShowRatingDialog      |    bool        |
| Daily Lottery Spin Limit | altpd |    m_activityLotteryTimesPerDay      |    int        |
| Total Login Days | tld |    m_totalLoginDays      |    int        |
| Has Claimed Daily Reward | hgdr |    m_bHasGotDailyReward      |    bool        |
| Last Login Time | llts |    m_lastLoginTimeStamp      |    time_t        |
| Last Gem Consumption Time | llt |    m_lastLoginTimeStamp      |    time_t        |
| Last Sign Request Time | lrsts |    m_lastRequestSignTimeStamp      |    time_t        |
| Daily Sign Rewards | dsrs |    m_dailySignRewardSheet      |    SignRewardContent[]        |
| Claimed Daily Rewards | hgrl |    m_hasGotRewardList      |    int[]        |
| Count of days with a purchase | dpc |    dayPayCount_      |    int        |
| Last Purchase Order | lodid |    lastOrderId_      |    string        |
| Unlocked Plant Costumes | ulokpa |    m_listPlantAvatarsAvatarInfo     |      PlantAvatarInfo[]      |
| Costume Pieces | lpapi |    m_listPlantAvatarPiecesInfo     |     PlantAvatarPiecesInfo[]       |
| Daily Challenge Plant Indexes | lfprii |    m_listFestivalPlantRandomIndexInfo     |     FestivalPlantRandomIndex[]       |
| Secondary Plant Costumes | lpnai |    m_listPlantNewAvatarInfo     |     PlantNewAvatarInfo[]       |
| Secondary Costume Pieces | pnapi |    m_listPlantNewAvatarPiecesInfo     |     PlantNewAvatarPiecesInfo[]       |
| Costumes weared by plants | lpaei |    m_listPlantAvatarEquipInfo     |     PlantEquipAvatarInfo[]       |
| Collection Info | lcli |    m_listCollectionInfo     |     CollectionInfo[]       |
| Restored Purchases | rpi |    m_restorePurchaseInfo     |     PurchaseInfo       |
| Fake Count of what? | fc |    m_fakeCount     |     int32      |
| Uses Aug05 Currency Key | alkf |    m_hasUseAug05LawnKeyField     |     bool      |
| Game Rank Record | grr |    m_gameRankRecords     |     GameRankItem[]      |
| Has New Player Package | gnpp |     m_hasGotNewPlayerPackage     |    bool        |
| Synced Data with Server | sdws |    m_hasSyncDataWithServer     |     bool      |
| Delta Info Summary Level | disl |    m_deltaInfoSummaryLevelString     |     string      |
| Recharged in Daily Events | brxs |    m_bRechargeInActivityDays     |     bool      |
| Recharged Yuan (Daily Events) | adrc |    m_iActitiyDaysRechargeCurrency     |     int      |
| Bundle Purchase Info | bdpci |   m_bundlePurchaseInfo     |     PurchasedBundleInfo[]      |
| Purchased Plant Trails | pcpt |    m_purchasedPlantTrial    |     string[]      |
| Purchased World Packs | pcwp |   m_purchasedWorldPack     |     WorldPackInfo[]      |
| Display Yin-yang tiles dialog | caeg |    canAdviceEnergyGrid     |     bool      |
| Last World Visited | ltwname |    m_last_world_name     |     string      |
| Show Notice Once | sno |    m_bShowNoticeOnce     |     bool      |
| Rated App | hr |    m_hasRated     |     bool      |
| Login Count | mlgic |    m_loginCount    |    int      |
| Profile upload token | upk |    m_uploadKey     |     int      |
| Last-synced config version | cfv |    m_configVersion     |     int      |
| Stone Store Refresh Time  | mlgicstone |    m_iStoneStoreRefreshTime    |    time_t      |
| Purchased Kongfu World | pku |    m_purchasedKongfuUnlock     |     bool      |
| Last free gacha pull | lfgt |    m_lastFreeGachaTime     |     time_t      |
| Paid first gacha pull | fdga |    m_firstDiamondGacha     |     bool      |
| New gacha last free pull (Normal) | lfgtn |    m_lastFreeGachaTimeNormal     |     time_t      |
| New gacha last free pull (Rare) | lfgtr |    m_lastFreeGachaTimeRare     |    time_t      |
| New gacha last free pull (Costume Chest) | lfgta |    m_lastFreeGachaTimeAvatar     |     time_t      |
| Paid first new gacha pull (Normal) | fdgan |    m_firstDiamondGachaNormal     |     bool      |
| Paid first new gacha pull (Rare) | fdgar |    m_firstDiamondGachaRare     |     bool      |
| Paid first new gacha pull (Costume Chest) | fdgaa |   m_firstDiamondGachaAvatar     |     bool      |
| Has Avatar Compensation Gift | avcb |    m_avatarCompen     |     bool      |
| Zombie Warning (unused) | mzw |    m_zombieStoredMarks     |     ZombieStoredMarks      |
| New WorldMap Conversion Status | mcs |      m_mapConversionState    |     PlayerProfileMapConversionState      |
| Challenge Count | clgc |    m_challengeCount     |     int[]      |
| Has Gacha Compensation | gccb |    m_gachaCompen     |     bool      |
| Has Daily Reward Compensation | drcb |    m_dailyRewardCompen     |     bool      |
| Has iOS Bug Compensation | iobc |    m_iOSBugCompen     |     bool      |
| Daily Offers | vdfpf |    m_vDayFirstPayFlag     |     string[]      |
| Offers Seen (Stone Store) | vtlpstone |    m_vecStoneStoreRec     |     string[]      |
| Offers Bought (Stone Store) | vtlpstonebuyed |    m_vecStoneStoreRecBuyed     |     string[]      |
| Has GameCenter Profile | gmmp |    m_gmMadeProfile     |     bool      |
| Has Qihoo Reward | qhlr |    m_qihooLoginReward     |     bool      |
| New Endless Zone Data | drd |    m_dangerRoomEventData     |     StoredDangerRoomEventData      |
| Riddles Answered (Lantern Event) | rha |    m_riddlesHasAnswered    |    int[]      |
| Today Riddles Rewards | rgt |    m_riddlesGotToday    |    int[]      |
| Riddles Answered Today | rant |    m_riddlesAnsweredToday    |    int      |
| Riddles Correct Answered | rcn |    m_riddlesCorrectNum    |    int      |
| Riddles Answered Days | rad |    m_riddlesAnsweredDays    |    int      |
| Riddles Total Correct Answered | rct |    m_riddlesCorrectTotal    |    int      |
| Riddles Prize Index | rpgi |    m_riddlesPrizeGotIndex    |    int      |
| Riddles Last Time Accessed | lrts |    m_lastRiddleTimeStamp    |    time_t      |
| Red Envelopes Opened | rrot |    m_redPackOpenTotal    |    int      |
| Has New Year Leaderboard Reward | rprdg |    m_bRedPackRewardRankGet    |    bool      |
| Last Login Time | cigss |   m_iLoginDayTimeRec     |    time_t      |
| Monthly Card Refresh Time | mcrt |   m_monthlyCardRefreshTime     |    time_t      |
| Monthly Card Refresh Time (Super) | mcsrt |   m_monthlyCardSuperRefreshTime     |    time_t      |
| Monthly Card Refresh Time (Make-up) | mcmurt |   m_monthlyCardMakeUpRefreshTime     |    time_t      |
| Daily Event Flags | issggs |    m_iDayRecEventFlag    |    int      |
| Ranking (New Year Leaderboard) | rpr |    m_redPackRank    |    int      |
| Plant Pendants | pasi |   m_plantAccessoryInfos     |     PlantAccessoryInfo[]     |
| Plant Family Info | pfi |    m_plantFamilyInfos   |    PlantFamilyInfo[]      |
| Riddles Topic | rltn |    m_strRiddlesTopicName   |    string      |
| Vasebreaker Activity ID | vbai |    m_vaseBreakerActId    |    int      |
| Current Training Room World | ctwn |  m_currentTrainingWorldName     |    string      |
| Training Room Record | tird |   m_trainingRecords    |    DangerRoomTrainingRecord[]      |
| Recharge Gift Times | rgts |    m_rechargeGiftTimes    |    uint8      |
| Cached Recharge Gift | rgtc |   m_rechargeGiftCached     |    uint8      |
| Last Boss Rush Level | bflbl |   m_lastBossLevel     |    int      |
| Boss Rush Levels Set | bfbfl |   m_bossFightLevels     |    ProbabilitySet<int>      |
| Boss Rush Played Today  | bfbft |    m_bossFightToday    |    bool      |
| Is In Boss Rush  | bfplg |    m_playingBossFightLevels    |    bool      |
| Consumption Topic | cpttn |    m_strConsumptionTopicName   |    string      |
| Consumption Reward Count | icptrc |    m_iConsumptionRewardCount   |    int      |
| Gems Consumed | icptgs |    m_iConsumptionGems   |    int      |
| Gems Consumed (Lottery) | ncptgss |    m_nLotteryConsumptionGems   |    int      |
| Gems Consumed (Activity) | cags |    m_ConsumptionActivityGems   |    int      |
| Special Avatar Bonus | sab |    m_specialAvatarBonuns   |    string      |
| Endless Zone Unrewarded Levels | druls |    m_dangerRoomUnrewardLevels   |    int[]     |
| Plant Adventure: Dungeon States | pads |    m_plantAdventureStates    |    PlantAdventureStates[]    |
| Plant Adventure Info | paif |    m_plantAdventureInfos    |    PlantAdventureInfo[]    |
| Plant Adventure: Plants Exploring | piad |    m_plantsInAdventure    |    AdventurePlants[]    |
| Plant Adventure: Dungeons Opened | paoi |    m_plantAdventureOpenInfo    |    string[]    |
| World Trophies | wcif |   m_worldCupInfo   |    WorldCupInfo[]      |
| Current User Avatar | hsid |   m_headshotId   |    int32      |
| Unlocked User Avatars | unlockhs |   m_unlockHeadShotIds   |    int[]      |
| Unlocked User Banners | unlockrai |   m_unlockRankAvatarIds   |    int[]      |
| Current User Banner | cravr |   m_currentRankAvatar   |    int      |
| TW Login Days | twld |   m_twLoginDays   |    int      |
| Last TW Reward Time | twlrt |   m_twLastRewardTime   |    int32      |
| Event Version: TW Daily Sign | twdsv |   m_twDailySignVersion   |    string      |
| Materials / Items | mtrl |   m_materialList   |    MaterialInfo[]      |
| Monthly VIP Status | monvipst |   m_monthVIPState  |    int      |
| Monthly VIP: Last Gems Claim Time | lgvgemt |   m_lastGetVIPGemTime  |    time_t      |
| Monthly VIP: Last Coins Claim Time | lgvgoldt |   m_lastGetVIPGoldTime  |    time_t      |
| Current Ads Rate | crar |   m_currentAdsRate  |   int      |
| Current Ads Rate (Dave's Shop) | cdsr |   m_currentDaveShopAdsRate  |   int      |
| Has New WeChat Reward | mwcs |   m_bModernWeChatShare   |    bool      |
| Plant Bundle Purchase Time | pbbt |   m_plantBundleBuyTime   |    time_t      |
| Plant Bundle Purchases Left | pblb |   m_plantBundleLeftBuy   |    int      |
| User Authenticated (Chinese National Auth) | biai |   m_bIsAuthIDCard   |    bool      |
| Last Z-shop Refresh Time | lzsr |   m_lastZmatchShopRefrashTime   |    time_t      |
| New Profile Create Time (not set) | npct |   m_newProfileCreatedTime   |    time_t      |
| Bundles Offered | ofbd |   m_offeredBundles   |    string[]      |
| Last OPPO Login Time | odlg |   m_oppoDailyLoginGotTime   |    time_t      |
| OPPO Login Streak Days | odrd |   m_oppoDailyRewardDays   |    int      |
| ACLog Flags (now is serverside) | acl |   m_aclog   |    string      |
| ACLog Key | aclk |   m_aclk   |    string      |
| ACLog Info | acli |   m_aclInfo   |    uint32      |
| Group Buy Record | gbr |  m_groupBuyRecord   |    SynInfo[]      |
| Played World Cup event | hpwc |   m_hasPlayedWorldCup   |    bool      |
| Monthly Card Type | mct |  m_monthlyCardType   |    uint32      |
| Monthly Card Reminder First Time | mcrft |  m_monthlyCardRemindFirstTime   |    time_t      |
| Monthly Card Reminder Second Time | mcrst |  m_monthlyCardRemindSecondTime   |    time_t      |
| Arcade Progress | ap |  m_arcadeProgress   |    ArcadePackProgress[]      |
| PowerUp Collection (Arcade Mode) | puc |  m_powerUpCollections   |    PowerUpCollectionProgress[]      |
| Next Events Start Dates | mnpgs |  m_nextdayPopGameStart   |    NextPopData[]      |
| Flags for some game modes | mpfi |  m_playerFlagInfos   |    PlayerFlagInfo[]      |
| Player Storage (Boss Rush) | mpsi |  m_playerStorageInfos   |    PlayerStorageData[]      |
| Tasks Info: Travel Log | mtlti |  m_travelLogTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Dave's Treasure | mdti |  m_daveTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Penny's Guide | mpti |  m_pennyTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Golden Vases Event | mhvbti |  m_happyVaseBreakerTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Novice 7-Days | mnsdti |  m_noviceSevenDaysTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Call of Wish | mcowti |  m_callofWishTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Memory Lane: Achievements Info | mpvzai |  m_pvz1AchievementInfos   |    TravelLogTaskSaveInfo[]      |
| Memory Lane Completion (Hard Mode) | mphlci |  m_pvz1HardLevelCompleteInfos   |    PvZ1LevelCompleteInfo[]      |
| Memory Lane Completion | mpnlci |  m_pvz1NormalLevelCompleteInfos   |    PvZ1LevelCompleteInfo[]      |
| Tasks Info: Golden Eggs Event | mgeti |  m_goldenEggTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Arbor Day Event | madti |  m_arborDayTaskInfos  |    TravelLogTaskSaveInfo[]      |
| Tasks Info: Seasonal Pass | mboti |  m_battleOrderTaskInfos  |    TravelLogTaskSaveInfo[]      |
| Tasks Info: New PvP Battle Pass | mnpti |  m_newPVPTaskInfos  |    TravelLogTaskSaveInfo[]      |
| Secret Realms Tasks (Birthdayz Event) | ubtsi |  m_unchartedBirthdayTaskInfos  |    TravelLogTaskSaveInfo[]      |
| Secret Realms Tasks | ucti |  m_unchartedTaskInfos  |   std::map&lt;string, TravelLogTaskSaveInfo[]&gt;      |
| Tasks Info: Cornucopia Event | mcrcpti |  m_cornucopiaTaskInfos  |   TravelLogTaskSaveInfo[]      |
| Tasks Info: New Plant Trial | mpcti |  m_plantCultivateTaskInfo  |   TravelLogTaskSaveInfo[]      |
| Tasks Info: NFS Linkage Event | mbob |  m_nfsLinkageTaskInfos  |   TravelLogTaskSaveInfo[]      |
| Tasks Info: Lucky Chests | mlct |  m_luckyChestTaskInfos  |   TravelLogTaskSaveInfo[]      |
| Tasks Info: Gift for Return | mgfrti |  m_giftFoReturnTaskInfos  |   TravelLogTaskSaveInfo[]      |
| Tasks Info: Dave's Kitchen | mdkti |  m_daveKitchenTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Tasks Info: October Co-op | mtoti |  m_tourismOctoberTaskInfos   |    TravelLogTaskSaveInfo[]      |
| Event Record | mer |  m_eventRecord  |    EventTimesRecord[]      |
| Memory Lane: Defeated Elite Zombies | mpbez |  m_pvz1BeatEliteZombieList  |    string[]      |
| Event Version: Dave's Treasure | mcdtv |  m_currentDaveTreasureVersion  |    int      |
| Event Version: Penny Guide  | mcpgv |  m_currentPennyGuideVersion  |    int      |
| Event Version: Golden Vases | mchvbv |  m_currentHappyVaseBreakerVersion  |    int      |
| Event Version: Consume & Receive | mcarv |  m_consumeAndReceiveVersion  |    int      |
| Event Version: Seasonal Pass | mcbov |  m_currentBattleOrderVersion  |    int      |
| Event Version: New PvP Battle Pass | mcnobp |  m_currentNewPVPBattlePassVersion  |    int      |
| Secret Realms Tasks Version (Birthdayz) | cubve |  m_currentUnchartedBirthdayVersion  |    int      |
| Event Version: Gift for Return | cgrv |  m_currentGiftFoReturnVersion  |    int      |
| Secret Realms Tasks Version | cutv |  m_currentUnchartedTaskVersions  |    map&lt;string, int&gt;      |
| Limited gacha free pull time (x1) | mlgdto |  m_limitGachaDrawTimesOne  |    int      |
| Limited gacha free pull time (x10) | mlgdtt |  m_limitGachaDrawTimesTen  |    int      |
| Ads Watch Cooldowns | awti |  m_advertisementWatchTimeInfo  |    AdvertisementWatchTimeInfo     |
| Remaining ads to view  | awci |  m_advertisementWatchCountInfo  |    AdvertisementWatchCountInfo     |
| Penny Chronicles: Auction Start Dates  | wlpst |  m_worldLevelPackageStartTimeMap  |    map&lt;string, time_t&gt;     |
| Penny Chronicles: First Purchase  | wlpfp |  m_worldLevelPackageFirstPlay  |    bool     |
| Secret Realms: Claimed Anniversary Reward  | uar |  m_unchartedAnniversaryReward  |    bool     |
| Secret Realms Version (Anniversary) | uarv |  m_unchartedAnniversaryRewardVersion |    int      |
| Secret Realms Anniversary Bonus | uwabi |  m_unchartedWorldAnniversaryBonusInfos |    map&lt;string, UnchartedWorldAnniversaryBonusInfo&gt;      |
| Theater Hall Event Data | rbed |  m_richmanBattleEventData |    RichmanBattleEventSaveData      |
| Theater Hall Battle Data | rsd |  m_richmanGameSaveData |    RichmanGameSaveData     |
| Endless Bundles Purchased | drsosd |  m_dangerRoomSpecialOfferSaveData |    DangerRoomSpecialOfferSaveData     |
| Has Auth Verification Reward | avr |  m_authVerifyRewarded |   bool    |
| Penny Pursuit: Current Event ID | rid |  m_riftCurrentID |   int    |
| PP: Sub-Event ID | rsid |  m_riftCurrentSubID |   int    |
| PP: Bitfield of zomboss wins | rzw |  m_riftZombossWinField |   uint32    |
| PP: \# of times Zomboss played in current attempt | rza |  m_riftZombossAttemptCount |   uint32    |
| PP: \# of times Zomboss event reached | rzc |  m_riftZombossClearedCounter |   uint32    |
| PP: Difficulty selection for each Zomboss win | rzd | m_riftZombossAttemptDifficulty   |   int[]    |
| PP: Difficulty Bitfield (Easy) | rpd0 | m_riftProgressBitfieldDifficulty0   |   uint64    |
| PP: Difficulty Bitfield (Hard) | rpd1 | m_riftProgressBitfieldDifficulty1   |   uint64    |
| PP: Difficulty Bitfield (Impossible) | rpd2 | m_riftProgressBitfieldDifficulty2   |   uint64    |
| PP: Zomboss Next Available Time | rznt | m_zombossNextAvailableTime   |   time_t    |
| PP: Zomboss Fights this Cycle | rzfc | m_zombossFightsThisCycle   |   int    |
| PP: First Time Visiting Shop | rsfe | m_riftStoreFirstEntered   |   bool    |
| New PvP: First Time Training Zombies | tfed | m_newPVPTrainingFirstEntered   |   bool    |
| High FPS | hfps | m_isHighFPS   |   bool    |
| New PvP: Selected Plants | npsp | m_newPVPSelectedPlants   |   int[]    |
| Finished Secret Realms Tutorial | pmtf | m_pvz1ModeTutorialFinished   |   bool    |
| Tutorial First Checked | tffi | m_tutorialFirstChecked   |   bool    |
| Memory Lane: Difficulty Bitfield  | ppd0 | m_pvz1ProgressBitfieldDifficulty0   |   uint64    |
| Memory Lane: Difficulty Bitfield (Hard)  | ppd1 | m_pvz1ProgressBitfieldDifficulty1   |   uint64    |
| Secret Realms: Difficulty Bitfield  | upbd0 | m_UnchartedProgressBitfieldDifficulty0  |   uint64    |
| Secret Realms: Difficulty Bitfield (Hard)  | upbd1 | m_UnchartedProgressBitfieldDifficulty1   |   uint64    |
| Card Warfare: Difficulty Bitfield  | cgbpd0 | m_CardGameProgressBitfieldDifficulty0  |   uint64    |
| Card Warfare: Difficulty Bitfield (Hard)  | cgbpd1 | m_CardGameProgressBitfieldDifficulty1   |   uint64    |
| Memory Lane: First Time Played | pfp |  m_pvz1modeFirstPlay   |   bool    |
| Creative Courtyard: First Time Played | cfp |  m_customLevelFirstPlay   |   bool    |
| Creative Courtyard: Tutorial Completed | hgclt |  m_hasGotCustomLevelTutorialLevel   |   bool    |
| Penny Classroom Quiz Index (from `0` ~ `9`) | pcti |  m_pennyClassroomTestIndex   |   int    |
| Secret Realms: Worlds Completed | umwc |  m_pvz2UnchartedModeWorldCount   |   int    |
| Creative Courtyard: Suggest Levels | clgle |  m_customLevelGuessLikeEnable   |   bool    |

</br>

## Unknown fields

<br>

|  Node   | Type     | 
|---------|:--------:|
|  zgb    |   int    |
|  uuen   |   int    |
|  npfsp  |   Array  |
|  tbsp   |   Array  |
|  tbfsp  |   Array  |
|  ptte   |   map&lt;string, int[]&gt;  |
|  ptten  |   Object  |
|  pmmv   |   int  |

</br>

## Sign nodes

Used by the old anticheat system.

Although they are still seeded, game does Integrity Checks with Server signs (not local).

See: [Anticheat info](https://github.com/CyberKnightFran45/PvZ2C-Modding-Docs/blob/06d38f60208f7c6489e7d4c5370f089aac461ffd/Anticheat%20info/English.md)

## Sub-types


### ▶ time_t

Represents a date encoded as a Unix timestamp.

This [script](https://github.com/CyberKnightFran45/UnixTime-Convert) converts between Unix timestamps and UTC dates.

### ▶ LawnKeyField

Currency Value obfuscated with bits rotation.

This [script](https://github.com/CyberKnightFran45/LawnKeyFieldCrypt) can decrypt it to its plain form, and encrypt it back.

### ▶ RechargeNode

<br>

| Const | Value |
|---|---:|
| `RECHARGE_DOUBLE_COIN` | `2` |
| `RECHARGE_DOUBLE_LOTTERY` | `6` |
| `RECHARGE_PLANT_PACKAGE` | `10` |
| `RECHARGE_DOUBLE_SPEED` | `20` |
| `RECHARGE_BOMB` | `30` |

</br>

### ▶ DailyRechargeCurrency

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Recharge Date  | drcd |      date    |    int        |
| Recharge Amount  | drcl |      rechargeCurrency    |    LawnKeyField        |

</br>

### ▶ FirstRechargeAwardData

<br>

| Description | Node | Type     | 
|------------|:---------:|:----------:|
| Reward SKU | sSku   |  string        |
| Claimed  | bHas |      bool       |

</br>

### ▶ BundleDisplay

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Bundle Type  | bundbti |      bundleTypeId   |    int        |
| Object ID  | bundoi |      objectId    |    int       |
| Times Purchased  | bundbt |      buyTimes    |    int       |
| Expire Time  | bundet |      expireTime    |    time_t       |

</br>

### ▶ BundleQueueCondition

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Trigger Levels  | bdqcll |      levelList   |    string[]        |
| Trigger Condition  | bdqcc |      objectId    |    string       |
| Bundle Type  | bdtid |      bundleTypeId   |    int        |

</br>

### ▶ GemCurrency

Gem Currency. Integer value is clamped from `0` to `10000`

**NOTE: try not to exceed this or your Gems will be reset to 0 and your plants will be downgraded to Level 1.
This was done in some versions of the game as a measure to prevent the use of hacks.**

### ▶ ZombossSignalCurrency

ZPS Currency. Integer value is clamped from `0` to `100`

### ▶ WorldCompletionData

New WorldMap Completion Data

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World ID | w |      WorldId   |    uint8        |
| Events Completion | e |      Events    |    WorldEventCompletionData[]       |
| Received World Key  | r |      ReceivedWorldKey    |    bool       |

</br>

#### ◼️ World IDs

See: [Worlds](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/WorldMap/World%20IDs.md)

#### ◼️  WorldEventCompletionData

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Event ID | i |      EventId   |    uint16       |
| Hard Mode Completed  | h |      PassHard    |    uint8      |

</br>

- PassHard values: `0` for uncomplete; `1` for complete

---

### ▶ Plant IDs

Unlocked Plant IDs.

See: [Plants](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Plant/Plants.md)

### ▶ Player Profile Version

See: [PlayerProfileVer](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/PlayerProfileVer.md)

### ▶ Upgrade IDs

IDs for Upgrades the player unlocked.

See: [GameFeatures](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Features/GameFeatures.md)

### ▶ Zombie IDs

IDs of defeated zombies that will show up in the almanac.

See: [Zombies](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Zombies/Zombies.md)

### ▶ PowerupRecord

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Powerup Name | n |     Name   |    string       |
| Uses  | i |      Inventory    |    int      |

</br>

### ▶ PlayerProfileIndex

Index used when there are multiple profiles linked to a player.

### ▶ New Tutorial Events

Used in the `hter` node. States how far along the tutorial funnel are we.

See: [FunnelEvent](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Tutorial/FunnelEvent.md)

### ▶ PlantPieceRecord

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | pi |     PlantId   |    int       |
| Piece Count  | pc |     PieceCount    |    int     |

</br>

### ▶ AccessoryPiece

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Accessory Type | acpt |     Type   |    string       |
| Piece Count  | acpc |     PieceCount    |    int     |

</br>

### ▶ ReconstructionLevel

Sky City weapons.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World Name | rslwn |     ReconstructionWorldName   |    string       |
| Cannon  | rslcl |     CannonLevel    |    int     |
| Shield  | rslbl |     BoardLevel    |    int     |

</br>

#### ◼️ CannonLevel values

<br>

| Type | Value |
|---|---:|
| `Basic` | `1` |
| `Laser` | `2` |
| `Rocket Launcher` | `3` |

</br>

#### ◼️ BoardLevel values

<br>

| Type | Value |
|---|---:|
| `Basic` | `1` |
| `Metal` | `2` |
| `Gold` | `3` |

</br>

---

### ▶ PlantStarLevel

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | icpi |     iCurrentPlantId   |    int       |
| Current Level  | icl |     iCurrentLevel    |    int     |

</br>

### ▶ Artifact IDs

Unlocked Artifact IDs.

See: [Artifacts](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Features/Artifacts.md) 

### ▶ ArtifactInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Artifact ID | id |     ArtifactID   |    int       |
| Rank  | rank |     Rank    |    int     |
| Level  | level |     Level    |    int     |
| Artifact Bless Boosts  | boostinfos |     BoostInfos    |    ArtifactBoostInfo[]     |
| Unsaved Artifact Bless Boosts  | uboostinfos |     UnsavedBoostInfos    |    ArtifactBoostInfo[]     |

</br>

- Max Rank: `4`

- Max Level: `30`

#### ◼️ ArtifactBoostInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Boost ID | boostid  |     BoostId   |    int       |
| Value  | value |     Value    |    float     |

</br>

- Value: `0.0` ~ `1.0`

---

### ▶ PlantGeneInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Gene ID | geneid |     GeneID   |    int       |
| Boost Level  | level |     Level    |    int     |
| Unlocked  | lockState |     LockState    |    int     |

</br>

- Max Level: `10`

- LockState: `0` is unlocked; `1` is locked

#### ◼️ Plant Gene IDs

See: [PlantGenes](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Plant/Genes.md) 

---

### ▶ PlantGeneEssenceInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Essence ID | id |     GeneEssenceID   |    int       |
| Count  | num |     Number    |    int     |

</br>

### ▶ ZombieStarLevel

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Zombie ID | icpi |     iZombieId   |    int       |
| Current Level  | icl |     iCurrentLevel    |    int     |

</br>

### ▶ OnlineEventInfo

Daily Challenge Info

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Event Refresh Time | rAt |     RefreshOnlineEventTime   |    time_t       |
| How many times Yeti spawns today  | ytl |     TodayYetiLeftCount    |    LawnKeyField     |
| Tickets for Gargantuar Crisis event  | tcylc |     TodayGargantuarCrisisLeftCount    |    LawnKeyField     |
| Tickets for Yeti Madness event  | tgclc |     TodayCrazyYetiLeftCount    |    LawnKeyField     |
| Tickets for Devil Invasion event  | tdilc |     TodayCrazyYetiLeftCount    |    LawnKeyField     |
| Yeti Count per day  | yetiCountPerDay |         |    LawnKeyField     |
| Event Version | yetiCountPerDayVersion |         |    LawnKeyField     |
| Tickets for Minigame event | acl |     TodayMiniGameLeftCount    |    LawnKeyField     |
| Yeti Tutorial Played  | tyeti |    ToturialPlayered     |    bool     |
| Tickets for God of Wealth event | sptlc |     SpringbossLeftCount    |    LawnKeyField     |

</br>

### ▶ SignRewardContent

Daily Sign Reward

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | itemId |     ItemId   |    int       |
| Amount  | amount |     Amount    |    int     |

</br>

### ▶ PlantAvatarInfo

Main Plant Costume.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | paipid |    iPlantID    |    int       |
| Costume Type  | avt |     eAvatar    |    PlantAvatarType     |
| Unlocked  | vaulok |     vecAvatarUnlocked    |    uint8[]     |

</br>

#### ◼️ PlantAvatarType

<br>

| Const | Value |
|---|---:|
| `none` | `-1` |
| `normal` | `0` |

</br>

#### ◼️ vecAvatarUnlocked

Single element array; flag `1` is for unlocked, `0` for locked

---

### ▶ PlantAvatarPiecesInfo

Main Costume Pieces.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | papipid |    iPlantID    |    int       |
| Piece Count  | vapc |     vecAvatarPiecesCount    |    int[]     |

</br>

### ▶ FestivalPlantRandomIndex

Random index table for Daily Challenge.

Indexes represent which plant pieces appear in the event menu.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Game Mode | gm |    eGameMode    |    FestivalGameMode       |
| Level  | gl |     eGameLevel    |    FestivalGameLevel     |
| Random Index (Common Plants) | npri |     NormalPlantRandomIndex    |    time_t     |
| Random Index (Special Plants)  | fpri |     FewPlantRandomIndex    |    time_t     |
| Random Index (Rare Plants)  | rpri |     RarePlantRandomIndex    |    time_t     |

</br>

#### ◼️ FestivalGameMode

*NOTE: short name is how the enum gets serialized to RTON*

<br>

| Const | Shortname | Value |
|------|:----------:|:-----:|
| `CrazyYeti` | `yeti` | `0` |
| `GargantuarCrisis` | `gargantuar` | `1` |
| `DevilInvade` | `devil` | `2` |
| `WealthGod` | `wealth` | `3` |
| `MiniGame` | `` | `4` |

</br>

#### ◼️ FestivalGameLevel

*NOTE: short name is how the enum gets serialized to RTON*

<br>

| Const | Shortname | Value |
|------|:----------:|:-----:|
| `Medium` | `Normal` | `0` |
| `Hard` | `Hard` | `1` |
| `Legend` | `Legend` | `2` |

</br>

---

### ▶ PlantNewAvatarInfo

Secondary Plant Costume.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | pnaid |    iPlantID    |    int       |
| Costume ID  | vnaid |     vecNewAvatarUnlockedID    |    int[]     |

</br>

### ▶ PlantNewAvatarPiecesInfo

Secondary Costume Pieces.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | pnapid |    iPlantNewPiecesID    |    int       |
| Piece Count  | pnapc |     iPiecesCount    |    int     |

</br>

### ▶ PlantEquipAvatarInfo

Current costume weared by plant.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | peapid |    iPlantID    |    int       |
| Costume ID  | peaaid |     iAvatarID    |    int     |

</br>

### ▶ Plant Costume IDs

See: [PlantCostumes](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/Plant/Costumes.md) 

### ▶ PurchasedBundleInfo

Bundles purchasen in the Limitted Bundles event.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Bundle SKU | pbisku |    sku    |    string       |
| Items  | pbiil |   itemList      |    bundleItemInfo[]     |

</br>

#### ◼️ bundleItemInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | i |    itemId    |    int32       |
| Quantity  | q |   quantity      |    int32     |

</br>

---

### ▶ WorldPackInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Pack SKU | pwpsku |    sku    |    string       |
| World Name  | pwpwd |   world      |    string     |

</br>

### ▶ CollectionInfo

Items unlocked in Secret Realms, like the Red Queen Card.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | i |    CollectionID    |    int       |
| Rarity  | r |     Rare    |    int     |
| State  | s |     State    |    int     |

</br>

#### ◼️ Rarity values

<br>

| Const | Value |
|---|---:|
| `common` | `0` |
| `rare` | `1` |
| `epic` | `2` |

</br>

#### ◼️ State values

<br>

| Const | Value |
|---|---:|
| `unequipped` | `0` |
| `equipped` | `1` |

</br>

---

### ▶ PurchaseInfo

Restored purchase info.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Receipt ID | rcpi |    receiptId    |    string       |
| Receipt | rcp |    receipt    |    string       |
| Product ID | pdi |    productId    |    string       |
| Object ID  | oipi |     objectId    |    int     |

</br>

### ▶ PlayerProfileMapConversionState

Enum suffix: `MAPCONVERSION_`

<br>

| Const | Value |
|---|---:|
| `None` | `0` |
| `ProgressConverted` | `1` |
| `RewardsPresented` | `2` |
| `NotNeeded` | `3` |

</br>

### ▶ PlantAccessoryInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | paci |    PlantID    |    int32       |
| Accesory Type | pact |    Type    |    string       |
| Accesory ID | pacid |    AccessoryId    |    int64       |
| Pendant Level  | l |     Level    |    int     |

</br>

- Max Level: `5` (Super-Pendants only)

### ▶ PlantFamilyInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Family ID | pfi |    PlantID    |    int32       |
| Boosts | pfbv |    BoostsValue    |    PlantFamilyBoostValue[]       |

</br>

#### ◼️ PlantFamilyBoostValue

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Boost Type | pfbvt |    Type    |    string       |
| Boost Value  | pfbv |   Value      |    float     |
| Boost Type (Slot 2)  | pfbvrt |   ReplaceType      |    string     |
| Boost Value (Slot 2)  | pfbrv |   ReplaceValue      |    float     |
| MD5 Sign  | pfbm |   MD5      |    string     |
| Is Locked  | pfbl |   Lock      |    bool     |

</br>

---

### ▶ DangerRoomTrainingRecord

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World Name | wn |      WorldName   |    string       |
| Highest Level  | hl |      HighestLevel    |    int      |

</br>

### ▶ StoredDangerRoomEventData

New Endless Zone Event data that is stored locally.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Current Period | cp |      CurrentPeriod   |    int32       |
| Reward Start Date  | psd |      RewardStartDate    |    int32     |
| Reward End Date  | ped |      RewardEndDate    |    int32     |
| Claimed Rewards  | ipr |      IsPickedReward    |    bool     |
| Restarted Endless Zone  | hrd |      HasResetDangerRoom    |    bool     |
| Reset Rewards  | hrp |      HasResetPickedReward    |    bool     |
| Previous Highest Score  | phs |      PreHighestScore    |    int32     |
| Last Period  | lpi |      LastPeriod    |    time_t     |

</br>

### ▶ PlantAdventureStates

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Dungeon ID | dnid |      dungeonId   |    int       |
| State  | dnst |      state    |    int     |
| Times explored  | dntm |      times    |    int     |

</br>

### ▶ PlantAdventureInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Inited | padi |      inited   |    bool       |
| Has Surprise Bonus | hssp |      hasSurprise    |    bool     |
| Dungeon ID | dgid |      dungeonId    |    int     |
| Coin Bonus | cnbs |      coinBonus    |    int     |
| Plant Chip ID | pcid |      plantChipId    |    int     |
| Plant Chip Quantity | pcqt |      plantChipQuantity    |    int     |
| Surprise Item ID | spoi |      surpriseObjectId    |    int     |
| Bonus Price | sppc |      surprisePrice    |    int     |
| Surprise Item Quantity | spqt |      surpriseQuantity    |    int     |
| Bonus Display Time | sstm |      surpriseShowTime    |    uint32     |
| End Time  | endt |      endTime    |    uint32     |
| Plants sent to adventure  | pidl |      plantIdList    |    int[]     |

</br>

### ▶ AdventurePlants

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant ID | adpi |      plantId   |    int       |
| End Time  | adpt |      endTime    |    uint32     |

</br>

### ▶ WorldCupInfo

Unlocked World Trophies (present starting from `2.0.0`)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World Name | wcwn |      worldName   |    string       |
| Star Trophy Unlocked  | wcscu |      starCupUnlocked    |    bool    |
| Boss Trophy Unlocked  | wcbcu |      bossCupUnlocked    |    bool    |
| Plant Trophy Unlocked  | wcpcu |      plantCupUnlocked    |    bool    |

</br>

### ▶ User Avatar IDs

See: [UserAvatars](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/User/Avatars.md) 

### ▶ User Banner IDs

See: [UserBanners](https://github.com/CyberKnightFran45/PvZ2C-TypesMap/blob/0f06554664076deb9a280ed22ffbaabfcd85ce32/IDS/User/Banners.md) 

### ▶ MaterialInfo

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Material ID | id  |  int       |
| Item Count | count |  LawnKeyField       |

</br>

### ▶ SynInfo

Info for the Group Buy Event.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Purchase Date | t |      timestamp   |    time_t       |
| Item ID | i |     id   |    int      |

</br>

### ▶ eMonthlyCardType

<br>

| Const | Value |
|---|---:|
| `None` | `0` |
| `E_MC_MAKE_UP` | `1` |
| `E_MC_CLASSICAL` | `2` |
| `E_MC_SUPER` | `4` |
| `E_MC_CHINA_MOBILE` | `8` |

</br>

### ▶ ArcadePackProgress

Progress for Vasebreaker (only available in some limited events)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Level ID | i |      IDHash   |      NameHash     |
| Record | lp |     LevelProgress   |    ArcadeLevelProgress[]      |

</br>

#### ◼️ NameHash

Represents a string hash used for fast lookups.

#### ◼️ ArcadeLevelProgress

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Level ID | i |      IDHash   |      NameHash     |
| Progress | p |     Progress   |    uint32      |
| State | s |     State   |    uint32      |

</br>

---

### ▶ PowerUpCollectionProgress

Powerup Collections in Vasebreaker.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| ID | i |      IDHash   |      NameHash     |
| Record | up |     UnlockedPowerups   |    PowerUpProgress[]      |

</br>

#### ◼️ PowerUpProgress

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | i |      IDHash   |      NameHash     |
| Progress | p |     Progress   |    uint32      |

</br>

---

### ▶ NextPopData

Data for the Next events to Pop-Up? (not sure)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Next Time | ntm |      nextTime   |      time_t     |
| Type Index | tix |     typeIndex   |    string     |

</br>

### ▶ PlayerFlagInfo

Flags for some game modes that state if they're available or not? (not sure)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Available | flg |      flag   |     bool     |
| Mode | flgt |     flagType   |    string     |

</br>

### ▶ PlayerStorageData

Storage Data for Boss Rush event.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Event Name | name |      DataName   |     string     |
| Item Count | number |     DataNumber   |    int     |

</br>

### ▶ TravelLogTaskSaveInfo

General Tasks Info.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Task ID | id |      ID   |     int     |
| Progress | pro |     Progress   |    int     |
| Group ID | gid |     GroupID   |    int     |
| Completion State | sta |     State   |    int32     |
| Creation Time | cre |     Creation   |    time_t     |

</br>

### ▶ PvZ1LevelCompleteInfo

Memory Lane Level Completion.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Level Index | li |     LevelIndex   |    int     |
| Completed with Classic Plants | opp |     OnlyPvZ1Plant   |    bool     |
| Beated Elite Zombies | bez |     BeatEliteZombie   |    bool    |
| Current Stage | cs |     CurrentStage   |    int    |
| Themes | tl |     ThemeList   |    int[]    |

</br>

### ▶ EventTimesRecord

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Time | tt |     theTime   |    time_t     |
| Record | r |     record   |    int     |
| Sign | sn |     signName   |    string     |

</br>

### ▶ AdvertisementWatchTimeInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Free Chest (Normal) | fcn |     FreeChestNormal  |    time_t     |
| Free Chest (Rare) | fcr |     FreeChestRare   |    time_t     |
| Skip Plant Adventure | pas |     PlantAdventureSkip   |    time_t     |
| Challenge Doubler (GargantuarCrisis) | cgone |     Challenge1   |    time_t     |
| Challenge Doubler (DevilInvade) | cgtwo |     Challenge2   |    time_t     |
| Challenge Doubler (CrazyYeti) | cgthree |     Challenge3   |    time_t     |
| Daily Sign: Get Extra Reward | dsr |     DailySign   |    time_t     |
| Ruby Doubler | el |     Endlevel   |    time_t     |
| Endless Zone: Reset Shop | drsr |     DangerRoomShopRefresh   |    time_t     |
| Endless Zone: Reset Challenge | drcr |     DangerRoomChallengeReset   |    time_t     |
| Free Random Piece | wmadl |     WorldMapADLottery   |    time_t     |

</br>

### ▶ AdvertisementWatchCountInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Endless Zone: Watch Times | elc |  EndlessCount |   int     |

</br>

### ▶ UnchartedWorldAnniversaryBonusInfo

<br>

| Description | Node | Type     | 
|------------|:---------:|:----------:|
| Has Anniversary Bonus | HasAnniversaryBonus |   bool     |
| Event Version         | AnniversaryVersion  |   int      |

</br>

### ▶ RichmanBattleEventSaveData

Event Data for the Theater Hall Mode.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| First Pop-Up | np |  _needPopup |   bool     |
| Won Battle | bw |  _battleWin |   bool     |
| Battle Type | bet | _battleEventType |   int     |
| Level Name | ln |  _levelName |   string     |
| Reward ID | ri |  _rewardID |   int    |
| Reward Count | rc |  _rewardCount |   int    |
| Items Rewarded | ril |  _rewardItemList |   RichmanItemInfo[]    |
| Chests Rewarded | rcl |  _rewardChestList |   RichmanItemInfo[]    |
| TimeStamp | ts |  _timeStamp |   time_t    |

</br>


#### ◼️ RichmanItemInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | i |  _id |  int     |
| Quantity | q |  _count |   int     |

</br>

---

### ▶ RichmanGameSaveData

Local Data for the Theater Hall Mode.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Win Ratio | wr |  _winRatio |  float     |
| Lose Ratio | lr |  _loseRatio |   float     |
| Electro-beans | bc |  _beansCount |   int     |

</br>

### ▶ DangerRoomSpecialOfferSaveData

Data for purchased Offers in the New Endless Zone event.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Purchased Offer | hb |  _hasBought |  bool     |
| Expire Time | et |  _expiredTime |   time_t     |
| Times displayed | pc |  _popUpUICount |   int     |
| Server check? | c |  _bCheck |  bool     |

</br>

---

# Old Save fields

The following values are exclusive to older versions `(v1.0.1 - v1.7.7)`

Some of them might be still present in Current saves, but no longer used.

_NOTE: removed nodes are highlighted in **bold**_

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World Keys | wks |      m_worldkeys    |    LawnKeyField     |
| **Recharged Yuan**  | **rcc** |      **m_rechargeCurrency**    |    **LawnKeyField**     |
| Total Recharged Yuan  | ttrc |      m_totalRechargeCurrency    |    LawnKeyField     |
| Golden Beans  | ptss |     m_leafs     |    LawnKeyField        |
| WorldMap Data  | wm |      m_worldMapEventList    |    MapEventList        |
| Stone Currency  | sc |      m_stones    |    LawnKeyField        |
| Yeti Event Data | tyi |      m_treasureYetiInfo    |    TreasureYetiInfo        |
| Endless Zone Data | dri |      m_dangerRoomInfo    |    DangerRoomInfo        |
| Star Keys | wsk |      m_worldSpecificKeys    |    WorldSpecificKeys[]        |
| Tutorial Progress  | tp |      m_tutorialProgress    |    MapTutorialState        |
| Completed Tutorials  | etpa |      m_exTutorialProgressArray    |    MapTutorialState[]        |
| Delta Info Summary Level | disl |    m_deltaInfoSummaryLevelString     |     string      |
| PvP Info | ari |      m_arenaInfo    |    ArenaInfo        |
| Reconstruction Components | rcstc |      m_reconstructionComponents    |     ReconstructionComponent[]      |
| **Daily Sign Status** | **hds** |  **m_hasDailySigned**    |    **bool**        |
| Festival Event Milestones | mlescs |    m_LevelScores     |     LevelScoreItem[]      |
| Plants Claimed (Star Rewards) | psrr |    m_plantStarRewardsRecord     |     int[]      |
| Festival Endless Zone Level | cdl |    m_currentDangerRoomLevel     |     DangerRoomLevelType      |
| Endless Zone Life Data | cle |    m_currentLifeData     |     DangerRoomLifeData      |
| Gem Return Claimed List | grlt |    m_gemsReturnList    |    int[]      |
| Gem Return Daily Hint | grdh |    m_gemReturnDailyHint    |    bool      |
| Paid Gem Return | grpd |    m_gemReturnPaid    |    bool      |
| **Summer Event Data** | **vlli** |  **m_vacationLevelInfo**    |    **DangerRoomInfo**        |
| Last Life Reset Time | llrt |   m_lastLifeResetTimeStamp     |    time_t      |
| Last Level Reset Time | llrs |    m_lastLevelResetTimeStamp    |    time_t      |
| Gem Return Days | igggs |    m_iGemReturnDays    |    int      |
| Current Sprint Gift Index | fcsgs |   m_currentSpringGiftIndex     |    int      |
| Last Update Reward Version | lurv |    m_lastUpdateRewardVersion    |    int      |
| Is New Update | inu |    m_isNewUpdate    |    bool      |
| Last Gate Unlocked | lgu |    m_lastGateUnlocked    |    int      |
| World Anims Played | wmp |    m_worldAnimPlayed    |    string[]      |
| Plant Trial Cooldowns | vptcd |    m_vPlantTrialCD    |    PlantTrialCD[]      |
| Plant Trials Record | vptrrd |    m_vPlantTrialRecord    |    string[]      |
| Activity Topic | actop |  m_strActivityTopic   |    string      |
| Battle Array Record | bars |    m_battleArrayRecords   |    BattleArrayComponent[]      |
| Daily Achievement Record | dars |    m_dailyAchievementRecords   |    DailyAchievementRecord[]      |
| Daily Achievement Last Time | dart |    m_dailyAchiRecordTime   |    time_t      |
| National Day Record | ndtr |    m_vNationalDayDate   |    string[]      |
| Has 2nd Anniversary Reward | tybrg |    m_bTwoYearBirthdayRewardGet   |    bool      |
| Display Spring Gift | nssg |    m_bNeedShowSpringGift      |    bool        |
| Has Pop-Up Once Day | hppod |    m_hasPopupOnceDay    |    bool    |
| Display Plant Trail Pop-Up | hppt |    m_hasPopupPlantTrial    |    bool    |
| Has 2nd Anniversary WeChat Reward | tywcs |   m_bTwoYearWeChatShare   |    bool      |
| Birthdayz Record | bzrv |    m_vBirthZRecord   |    BirthZRecord[]      |
| Houses Occupied (PvP mode) | hhous |    m_hasHouse   |    int[]      |
| PvP Mode Unlocked | ulpvp |    m_unlockPVP   |    bool      |
| PvP Tutorial State | pvpts |    m_pvpTutorialState   |    int      |
| Today Ingots (Christmas Protect Event) | tcmpc |    m_todayChristmasProtectCurrency   |    int      |
| Christmas Lottery Plant Index | cmlpi |    m_nChristmasLotteryPlantIndex   |    int      |
| Christmas Lottery Index | cmli |    m_nChristmasLotteryIndex   |    int      |
| Christmas Pendant Event Info | caif |    m_christmasAccessoryInfo    |    ChristmasAccessoryInfo    |
| Golden Eggs Event Info | cgif |    m_goldenEggInfo    |    GoldenEggInfo    |
| Has a PvP account | hpa |    m_hasPvpAccount   |    bool      |
| Show Evil Dave Intro | sedi |    m_bShowEvilDavidIntro   |    bool      |
| Rebate Streak Activated | bhrr |    m_iHasRebateReward   |    bool      |
| Rebate Login Streak | vbhrr |    m_vRebateRewardState   |    int[]      |
| Rebate Charge | irc |    m_iRebateCharge   |    int      |
| Rebate Single Record | vrsr |    m_vRebateSingleRecord   |    RebateSingleRecord[]      |
| PvP Shop Info | psif |    m_pvpShopInfo   |    PvpShopInfo      |
| Current Sales Info | csif |    m_currentSalesInfo   |    CurrentSalesInfo      |
| Started Children Day Challenge | cds |    m_childrenDayStart   |    int32      |
| Children's Day Tries Bought | cdbc |   m_childrenDayBuyCount   |    int32      |
| Children's Day Max Tries | cdbl |   m_childrenDayBuyLimit   |    int32      |
| Event Version: Children's Day | cdv |   m_childrenDayVersion   |    string      |
| Treasure Lottery Info | glli |   m_geilivableLotteryInfo   |    GeilivableLotteryInfo      |
| LostNet Event: Token Dates | lnatd |   m_lostNetTokenDate   |    time_t[]      |
| LostNet Event: Last Bonus | llnab |   m_lastLostNetBonus   |    int      |
| LostNet Event: Last Token Date | llntd |   m_lastLostNetTokenDate   |    time_t      |
| National Shop Items | sits |   m_shopItems   |    NationalShopItem[]      |
| Festival Shop Items | fsit |   m_festivalShopItems   |    FestivalShopItem[]      |
| Anniversary Shop Items | asit |   m_anniversaryShopItem   |    FestivalShopItem[]      |

</br>

## Sub-types


### ▶ MapEventList

Alias of `std::vector<SavedWorldMapEventData>`

---

#### ◼️ SavedWorldMapEventData

Old WorldMap Completion Data

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World ID | W |      WorldId   |    uint8        |
| Event ID  | E |      EventId    |    uin16       |
| Event Status  | S |      Status    |    WorldMapEventStatus       |
| Stars  | C |      StarCompletion    |    int       |
| Times Completed  | N |      CompletionCount    |    int       |
| Times Played  | P |      PlayCount    |    int       |

</br>

#### - WorldMapEventStatus

<br>

| Const | Value |
|---|---:|
| `unexplored` | `0` |
| `locked` | `1` |
| `unlocked` | `2` |
| `completed` | `3` |

</br>

#### - StarCompletion values

<br>

| Const | Value |
|---|---:|
| `0` | `none` |
| `1` | ⭐ |
| `3` | ⭐⭐ |
| `7` | ⭐⭐⭐ |

</br>

### ▶ MapTutorialState

IDs for Completed Tutorials. See:

### ▶ WorldSpecificKeys

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World Name | wn |      WorldName   |    string       |
| Keys Count  | kc |      KeyCount    |    KeyCurrency      |

</br>

#### ◼️ KeyCurrency

Amount of Star Keys user has.

---

### ▶ TreasureYetiInfo

Used in early versions of the game.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Level where event triggers | wml |     WorldMapLocation   |    string       |
| Last time yeti was sighted  | lst |      LastSpawnTime    |    time_t      |
| Next date of the event  | nst |      NextSpawnTime    |    time_t      |

</br>

### ▶ DangerRoomInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| World/Event name | wn |     WorldName   |    string       |
| Current Level  | cl |     CurrentLevel    |    int32     |
| Highest Level  | hl |      HighestLevel    |    int32      |
| Remaining PlantFood  | pfco |      PlantfoodCarryOver    |    uint8      |
| Lawnmowers  | l |      Lives    |    uint16      |
| Seed bank  | sb |      SeedBank    |    int[]      |
| Last time accessed | ts |      TimeStamp    |    time_t      |
| Previous Level | pl |      PrevLevel   |    int32      |
| Has Reward | hr |      HasReward   |    bool      |
| Milestone Reached | hm |      HasMilestone   |    bool      |
| Plants placement | drp |      DangerRoomPlantList   |   DangerRoomPlantInfos      |
| Completed | hc |      HasCompleted   |   bool     |
| **Lives (Old System)** | **sss** |   **Lives**     |   **int[]**      |
| Current Score | cse |      CurrentScore   |   int      |
| Total Score | tse |      TotalScore   |   int      |
| Historic Score | hts |      HistoryScore   |   int      |
| Historic Score | hhs |      HistoryHighestScore   |   int      |
| Current Sun Money | csm |      CurrentSunMoney   |   int      |
| Game In Progress | dips |      IsInProgress   |   bool      |
| Reset Gem Cost | rg |      ResetGemCost   |   int      |
| Plants Placement (New Endless Zone) | drnp |      DangerRoomNewPlantList   |   DangerRoomNewPlantInfos      |

</br>

#### ◼️ DangerRoomPlantInfos

Alias of `std::vector<DangerRoomPlantInfo>`

#### - DangerRoomPlantInfo

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Plant Type | Type  |  PlantTypePtr       |
| Row in Grid | Row  |  int       |
| Column in Grid | Column  |  int       |
| Plant Level | Level  |  int       |

</br>

---

#### ◼️ DangerRoomNewPlantInfos

Alias of `std::vector<DangerRoomNewPlantInfo>`

#### - DangerRoomNewPlantInfo

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Column in Grid | Column  |  int       |
| Row in Grid | Row  |  int       |
| Plant Level | Level  |  int       |
| Plant ID | PlantId  |  int       |

</br>

---

### ▶ ArenaInfo

Info for old PvP mode.

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant List A | arp |     ArenaPlantList1   |    ArenaPlantInfos       |
| Plant List B  | arpp |     ArenaPlantList2    |    ArenaPlantInfos     |
| Plant List C  | arppp |     ArenaPlantList3    |    ArenaPlantInfos     |

</br>

#### ◼️ ArenaPlantInfos

Alias of `std::vector<ArenaPlantInfo>`

#### - ArenaPlantInfo

Plant Placement in PvP Mode

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Plant Type | Type  |  PlantTypePtr       |
| Row in Grid | Row  |  int       |
| Column in Grid | Column  |  int       |

</br>

---

### ▶ ReconstructionComponent

Amount of screws for the Reconstruction event (2017)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Component Type | rsct |     ComponentType   |    string       |
| Component Count  | rscc |     ComponentCount    |    int     |

</br>

### ▶ GameRankItem

Record for the old Rank system (deprecated)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Level Index | lix |     levelIndex   |    int       |
| Stars  | sr |     star    |    int     |
| Formation  | fmt |     formation    |    string     |
| Time  | tm |     time    |    int     |

</br>

### ▶ LevelScoreItem

Score in Festival Endless Zones.

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Milestone | mark  |  int      |
| Level Name | level_name |  string       |

</br>

### ▶ ZombieStoredMarks

Alias of `std::vector<ZombieWarning>`

#### ◼️ ZombieWarning

Marks for Zombie Warning System.

This is no longer used. The game now takes the sighted zombies stored on `kz` and their marks in `zsla`

<br>

| Description | Node |  Type     | 
|------------|:---------:|:----------:|
| Zombie Type | Type  |  ZombieTypePtr       |
| Level | Level |  int       |

</br>

---

### ▶ DangerRoomLevelType

<br>

| Const | Value |
|---|---:|
| `DR_LEVEL_ONE` | `0` |
| `DR_LEVEL_TWO` | `1` |
| `DR_LEVEL_THREE` | `2` |
| `DR_LEVEL_FOUR` | `3` |
| `DR_LEVEL_ENDLESS` | `4` |

</br>

### ▶ DangerRoomLifeData

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Lives | cte |     CurrentLife   |    int32       |
| Times Purchased  | bte |     BoughtTime    |    int32     |

</br>

### ▶ PlantTrialCD

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Plant Name | ptcdpn |      PlantName   |    string       |
| Cooldown  | ptcdt |      CDTime    |    time_t      |

</br> 

### ▶ BattleArrayComponent

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Battle Type | bacbt |      BattleType   |    int32       |
| Battle Log | bacbl |     BattleList   |    int[]      |

</br> 

### ▶ DailyAchievementRecord

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| ID of Target finished | darai |      targetFinished   |    int       |
| Target Count | dartc |     targetCount   |    int     |
| Achievement IDs | dartf |     actId   |    int[]     |
| Specific SKU | darss |     specificSku   |    string      |

</br> 

### ▶ BirthZRecord

Record for Rewards claimed in the Birthdayz event (2015)

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Day | dy |      strDay   |    string       |
| Count | gc |     iGetCount   |    int      |

</br>

### ▶ ChristmasAccessoryInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Inited | caii |      inited   |    bool       |
| Free Chances | cafc |      freeChances   |    int       |
| Coin Chances | cacc |      coinChances   |    int       |
| Gem Chances | cagc |      gemChances   |    int       |
| Last Refresh Time | calr |      lastRefreshTime   |    uint32       |
| Free Rewards Index | cafi |      freeIndex   |    int[]       |
| Coin Rewards Index | caci |      coinIndex   |    int[]       |
| Gem Rewards Index | cagi |      gemIndex   |    int[]       |

</br>

### ▶ GoldenEggInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Inited | cgei |      inited   |    bool       |
| Object ID | cgeoi |      ObjectId   |    int       |
| Hammers | cgeh |      hammers   |    int       |
| Hammers Left | cgegl |      hammersLeft   |    int       |
| Daily Reward ID | cgedr |      dailyReward   |    int       |
| Daily Hammers | cgeha |      dailyHammerAmount   |    int       |
| Daily Charge Amount | cgel |    dailyChargeAmount   |    uint32       |
| Last Refresh Time (in seconds) | cgeca |      lastRefreshTime   |    float       |
| Egg States | cges |      eggsStat   |    int[]       |
| Eggs Opened | cgeop |      openedInfo   |    int[]       |

</br>

### ▶ GeilivableLotteryInfo

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Total Chances | totalChances |      gltc   |    int       |
| Remaining Chances | glrc |     remainChances   |    int      |
| Config Name | configName |      glcn   |    string       |

</br>

### ▶ NationalShopItem

<br>

| Description | Node | Member      | Type     | 
|------------|:---------:|:--------:|:----------:|
| Item ID | objectId |      nsid   |    int       |
| Times Purchased | nsbt |     buyTimes   |    int      |

</br>

### ▶ FestivalShopItem

Same fields as `NationalShopItem`

---

## Author

Made by FranZ (CyberKnightFran)

## Special thanks to

Evil (evilhack28)