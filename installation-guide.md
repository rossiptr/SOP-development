<h1 align="center">Installation Guideline - Project Name</h1>
<hr>

## Project description

**Project Name:** [Replace with actual project name]

**Description:** A comprehensive solution for [specific use case]. This project provides [key functionality] and enables users to [main benefits].

**Key Features:**

- Feature 1: [Brief description]
- Feature 2: [Brief description]
- Feature 3: [Brief description]

**Target Users:** [Developers/Researchers/System Administrators/etc.]

> [!CAUTION]
> Make this document private by default. Only make it public after publishing the project.
>
> Request access with the GitHub admin in our group.

> [!NOTE]
> **Purpose of Installation Guide:**
> This guide focuses on setup, configuration, and getting the system running on your local environment or target deployment system.

## Table of Contents

to allow other people to quickly navigate especially long or detailed READMEs.

- [Project description](#project-description)
- [Table of Contents](#table-of-contents)
- [Remote Access Methods](#remote-access-methods)
  - [SSH](#ssh)
  - [Anydesk](#anydesk)
- [Action Items](#action-items)
- [System Architecture](#system-architecture)
- [Repository Structure](#repository-structure)
- [Minimum Specification Requirements](#minimum-specification-requirements)
- [Table of Paramaters](#table-of-paramaters)
  - [Inputs Parameters](#inputs-parameters)
- [Message Sequence Chart (MSC)](#message-sequence-chart-msc)
  - [User Authentication Flow (O-RAN O1 Interface)](#user-authentication-flow-o-ran-o1-interface)
  - [Cell Configuration Flow (O-RAN F1 Interface)](#cell-configuration-flow-o-ran-f1-interface)
  - [Configuration](#configuration)
  - [Installation Steps](#installation-steps)
- [Post-Installation Verification](#post-installation-verification)
- [Troubleshooting](#troubleshooting)
  - [Common Issues and Solutions](#common-issues-and-solutions)
- [Additional Resources](#additional-resources)

## Remote Access Methods

### SSH

```shell
ssh user@<IP address>
```

### Anydesk

```markdown
ID: # Anydesk ID / Public IP / private IP with on VPN access
Pass: <password>
```

## Action Items

Write your installation/integration plan & status in here:

| Step                         | Command/Action                                               | Description                                        | Status |
| ---------------------------- | ------------------------------------------------------------ | -------------------------------------------------- | ------ |
| Clone the repository         | `git clone https://github.com/your-username/your-repo.git` | Clone the project repository to your local machine | ✅     |
| Install dependencies         | `npm install`                                              | Install all necessary dependencies                 | ✅     |
| Set up environment variables | Create a `.env` file and refer to `.env.example`         | Configure environment variables                    | ⌛️   |
| Run the application          | `npm start`                                                | Start the application                              | ❌     |
| Open in browser              | Navigate to `http://localhost:3000`                        | Open the application in your web browser           |        |

## System Architecture

**Important Components to Include in System Architecture (O-RAN O-DU Architecture Pattern):**

1. **O-RAN Interfaces** - F1, E2, O1, FAPI interfaces with specific protocols
2. **Functional Blocks** - L2/L3 protocol stack components (RLC, MAC, PDCP, RRC)
3. **Thread Architecture** - Multiple processing threads for different functional blocks
4. **Message Exchanges** - SCTP, EGTP, ASN.1 codecs for inter-module communication
5. **Management Interfaces** - O1 for configuration, alarms, and performance management
6. **IP Addressing** - Clear network topology following O-RAN deployment patterns

### O-DU System Architecture
```mermaid
graph TD
    subgraph O-DU["O-DU"]
        subgraph DU_APP["DU APP"]
            direction TB
            subgraph O1_MODULE["O1 Interface"]
                O1_CLIENT["O1 Client<br/>o1_client/"]
                VES["VES Agent<br/>ves/"]
                ALARM["Alarm Mgmt<br/>alarm/"]
                O1_CONFIG["Config Mgmt<br/>config/"]
            end
            
            CONFIG["Config Handler<br/>du_cfg.c"]
            
            subgraph MANAGERS["Management Layer"]
                DU_MGR["DU Manager<br/>du_mgr.c"]
                UE_MGR["UE Manager<br/>du_ue_mgr.c"]
            end
            
            subgraph INTERFACES["Interface Handlers"]
                SCTP_MGR["SCTP Manager<br/>du_sctp.c"]
                F1AP["F1AP Handler<br/>du_f1ap_msg_hdl.c"]
                E2AP["E2AP Handler<br/>du_e2ap_msg_hdl.c"]
            end
            
            subgraph CODECS["ASN.1 Codecs"]
                F1AP_CODEC["F1AP/<br/>codecs"]
                E2AP_CODEC["E2AP/<br/>codecs"]
                RRC_CODEC["RRC/<br/>codecs"]
                COMMON_CODEC["Common/<br/>utilities"]
            end
        end

        subgraph L2_STACK["L2 Stack"]
            direction TB
            subgraph RLC_LAYER["5G NR RLC Layer"]
                RLC_UL["RLC UL<br/>kw_ul_ex_ms.c<br/>kw_amm_ul.c"]
                RLC_DL["RLC DL<br/>kw_dl_ex_ms.c<br/>kw_amm_dl.c"]
                RLC_UIM["Upper Interface<br/>kw_uim.c"]
            end
            
            subgraph MAC_LAYER["5G NR MAC Layer"]
                direction TB
                MAC_UPR["Upper MAC<br/>mac_upr_inf_api.c<br/>mac_ue_mgr.c"]
                MAC_SLOT["Slot Processing<br/>mac_slot_ind.c"]
                LOWER_MAC["Lower MAC<br/>lwr_mac_fsm.c<br/>lwr_mac_handle_phy.c"]
                
                subgraph SCH_BLOCK["5G NR Scheduler"]
                    SCH_MAIN["Main Scheduler<br/>sch.c<br/>sch_common.c"]
                    SCH_SLOT["Slot Handler<br/>sch_slot_ind.c"]
                    SCH_UE["UE Manager<br/>sch_ue_mgr.c"]
                    SCH_UTILS["Utilities<br/>sch_utils.c"]
                end
            end
        end

        subgraph COMMON["Common Modules"]
            direction LR
            CM_DEF["Common Definitions<br/>common_def.c"]
            LRG["Layer Management<br/>lrg.c"]
            DU_RLC_INF["DU-RLC Interface<br/>du_app_rlc_inf.c"]
            DU_MAC_INF["DU-MAC Interface<br/>du_app_mac_inf.c"]
        end

        subgraph MT_UTILS["Multi-Threading"]
            direction LR
            MT_SS["System Services<br/>mt_ss.c"]
            MT_ID["Thread ID<br/>mt_id.c"]
        end
    end

    %% Define main connections
    DU_APP <--> L2_STACK
    DU_APP --> COMMON
    L2_STACK --> COMMON
    DU_APP --> MT_UTILS
    L2_STACK --> MT_UTILS
    
    %% Internal L2 connections
    RLC_LAYER <--> MAC_LAYER
    MAC_LAYER <--> SCH_BLOCK
    
    %% Internal RLC connections
    RLC_UL <--> RLC_UIM
    RLC_DL <--> RLC_UIM
    
    %% Internal MAC connections
    MAC_UPR <--> MAC_SLOT
    MAC_SLOT <--> LOWER_MAC
    LOWER_MAC <--> SCH_BLOCK
    
    %% Internal Scheduler connections
    SCH_MAIN <--> SCH_SLOT
    SCH_MAIN <--> SCH_UE
    SCH_SLOT <--> SCH_UTILS
    
    %% O1 internal connections
    O1_CLIENT <--> VES
    O1_CLIENT <--> ALARM
    O1_CLIENT <--> O1_CONFIG

    %% Styling to match the architecture image
    style O-DU fill:#f0e6ff,stroke:#b39ddb,stroke-width:3px
    style DU_APP fill:#cceeff,stroke:#0077c2,stroke-width:2px
    style L2_STACK fill:#e8f5e9,stroke:#66bb6a,stroke-width:2px
    style COMMON fill:#fff3e0,stroke:#ff8f00,stroke-width:2px
    style MT_UTILS fill:#f3e5f5,stroke:#8e24aa,stroke-width:2px
    
    %% DU APP components
    style O1_MODULE fill:#ffcdd2,stroke:#c62828,stroke-width:2px
    style CONFIG fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    style MANAGERS fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    style INTERFACES fill:#fff9c4,stroke:#f9a825,stroke-width:2px
    style CODECS fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    
    %% L2 Stack components
    style RLC_LAYER fill:#ffe0b2,stroke:#ef6c00,stroke-width:2px
    style MAC_LAYER fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style SCH_BLOCK fill:#d1c4e9,stroke:#4527a0,stroke-width:2px,stroke-dasharray: 5 5
    
    %% Individual components
    style RLC_UL fill:#ffcc80,stroke:#e65100,stroke-width:1px
    style RLC_DL fill:#a5d6a7,stroke:#1b5e20,stroke-width:1px
    style RLC_UIM fill:#90caf9,stroke:#0d47a1,stroke-width:1px
    style LOWER_MAC fill:#ce93d8,stroke:#4a148c,stroke-width:1px
    style O1_CLIENT fill:#ef9a9a,stroke:#b71c1c,stroke-width:1px
    style VES fill:#f8bbd9,stroke:#880e4f,stroke-width:1px
    style ALARM fill:#ffab91,stroke:#bf360c,stroke-width:1px
    style O1_CONFIG fill:#80cbc4,stroke:#004d40,stroke-width:1px
```


## Repository Structure

> [!NOTE]
>
> 1. Add `.gitignore` file with C/C++ and O-RAN specific patterns.
> 2. Add Apache 2.0 LICENSE (standard for O-RAN projects).
> 3. Create O-RAN compliant source structure following O-DU High architecture.
> 4. Structure code following the [System Architecture](#system-architecture) with thread-based organization.

```
o-ran-o-du-l2/
├── src/                           # Main source code directory
│   ├── du_app/                    # DU Application Layer
│   │   ├── du_mgr.c              # DU Manager implementation
│   │   ├── du_ue_mgr.c           # UE Manager implementation
│   │   ├── du_cfg.c              # Configuration Handler
│   │   ├── du_f1ap_msg_hdl.c     # F1AP message handling
│   │   ├── du_e2ap_msg_hdl.c     # E2AP message handling
│   │   └── du_sctp.c             # SCTP interface handling
│   ├── 5gnrmac/                   # 5G NR MAC Layer
│   │   ├── lwr_mac_fsm.c         # Lower MAC FSM
│   │   ├── lwr_mac_handle_phy.c  # PHY interface handling
│   │   ├── mac_slot_ind.c        # Slot indication processing
│   │   ├── mac_upr_inf_api.c     # Upper interface APIs
│   │   └── mac_ue_mgr.c          # MAC UE management
│   ├── 5gnrrlc/                   # 5G NR RLC Layer
│   │   ├── kw_ul_ex_ms.c         # RLC UL main functions
│   │   ├── kw_dl_ex_ms.c         # RLC DL main functions
│   │   ├── kw_amm_ul.c           # AM mode UL processing
│   │   ├── kw_amm_dl.c           # AM mode DL processing
│   │   └── kw_uim.c              # Upper interface management
│   ├── 5gnrsch/                   # 5G NR Scheduler
│   │   ├── sch.c                 # Main scheduler functions
│   │   ├── sch_slot_ind.c        # Slot indication handling
│   │   ├── sch_ue_mgr.c          # UE management in scheduler
│   │   ├── sch_common.c          # Common scheduler functions
│   │   └── sch_utils.c           # Scheduler utilities
│   ├── cm/                        # Common modules
│   │   ├── common_def.c          # Common definitions
│   │   ├── lrg.c                 # Layer management
│   │   ├── du_app_rlc_inf.c      # DU-RLC interface
│   │   └── du_app_mac_inf.c      # DU-MAC interface
│   ├── codec_utils/               # ASN.1 Codecs
│   │   ├── F1AP/                 # F1AP ASN.1 codecs
│   │   ├── E2AP/                 # E2AP ASN.1 codecs
│   │   ├── RRC/                  # RRC ASN.1 codecs
│   │   └── common/               # Common codec utilities
│   ├── o1/                        # O1 Interface Module
│   │   ├── o1_client/            # O1 client implementation
│   │   ├── ves/                  # VES agent
│   │   ├── alarm/                # Alarm management
│   │   └── config/               # Configuration management
│   └── mt/                        # Multi-threading utilities
│       ├── mt_ss.c               # System services
│       └── mt_id.c               # Thread identification
├── build/                         # Build system
│   ├── scripts/                  # Build scripts
│   │   ├── build_odu.sh         # Main build script
│   │   └── cleanup.sh           # Cleanup script
│   ├── odu/                      # ODU build artifacts
│   └── makefile                  # Main makefile
├── config/                        # Configuration files
│   ├── startup_config.xml        # Initial configuration
│   ├── fapi_config.json         # FAPI configuration
│   └── odu_config.xml           # ODU configuration
├── docs/                          # Documentation
│   ├── overview.md               # Architecture overview
│   ├── user-guide.md            # User guide
│   ├── developer-guide.md       # Developer guide
│   └── api-docs/                # API documentation
├── tests/                         # Test framework
│   ├── scripts/                  # Test scripts
│   ├── stub/                     # Stub implementations
│   │   ├── cu_stub/             # CU stub
│   │   ├── ric_stub/            # RIC stub
│   │   └── phy_stub/            # PHY stub
│   └── integration/              # Integration tests
├── tools/                         # Development tools
│   ├── fapi_decoder/            # FAPI message decoder
│   ├── memory_analyzer/         # Memory leak detection
│   └── log_analyzer/            # Log analysis tools
├── bin/                           # Binary executables
│   ├── odu                      # Main ODU executable
│   ├── cu_stub                  # CU stub executable
│   └── ric_stub                 # RIC stub executable
├── .gitignore                     # Git ignore patterns
├── LICENSE                        # Apache 2.0 License
├── README.md                      # Project overview
├── CONTRIBUTING.md                # Contribution guidelines
└── CHANGELOG.md                   # Change log
```

## Minimum Specification Requirements

| Component        | Requirement               |
| ---------------- | ------------------------- |
| Operating System | Ubuntu 22.04 or higher    |
| CPU              | 2 GHz dual-core processor |
| Memory           | 4 GB RAM                  |
| GCC Version      | 7.5 or higher             |
| Python Version   | 3.6 or higher             |
| Kubernetes       | 1.18 or higher            |

## Table of Paramaters

> [!NOTE]
> **Parameter Comparison Guidelines:**
>
> 1. **Standards Compliance** - All vendor implementations must maintain backward compatibility with 3GPP standards
> 2. **Performance Enhancement** - Vendor-specific features often provide performance improvements beyond standard requirements
> 3. **Interoperability** - Ensure vendor-specific parameters don't compromise network interoperability
> 4. **Documentation** - Always refer to the latest version of specifications as standards evolve
> 5. **Testing** - Validate vendor-specific implementations against 3GPP test cases

### Inputs Parameters

| Parameter Name                  | Description                                    | 3GPP Reference                                                                      | 3GPP Standard     | Ericsson                                                                                   | Nokia                                                                              | Huawei                                                                           | Samsung                                                         |
| ------------------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Cell ID**               | Unique identifier for each cell in the network | [TS 36.211 Section 6.11](https://www.3gpp.org/ftp/Specs/archive/36_series/36.211/)     | nrCellIdentity    | [Cell Identity (CI)](https://www.ericsson.com/en/ran)                                         | Cell_ID                                                                            | Cell_Identifier                                                                  | CellId                                                          |
| **Tracking Area Code**    | Area identifier for location management        | [TS 23.003 Section 19.4.2.3](https://www.3gpp.org/ftp/Specs/archive/23_series/23.003/) | trackingAreaCode  | TAC_Enhanced                                                                               | [TAC_Extended](https://www.nokia.com/networks/mobile-networks/airscale-radio-access/) | TAC_Advanced                                                                     | TAC_Optimized                                                   |
| **PLMN ID**               | Public Land Mobile Network identifier          | [TS 23.003 Section 2.2](https://www.3gpp.org/ftp/Specs/archive/23_series/23.003/)      | plmnIdentity      | PLMN_ID                                                                                    | PLMN_Identifier                                                                    | [PLMN_Enhanced](https://carrier.huawei.com/en/products/wireless-network/small-cell) | PLMN_Code                                                       |
| **Bandwidth**             | Radio channel bandwidth allocation             | [TS 36.104 Section 5.6](https://www.3gpp.org/ftp/Specs/archive/36_series/36.104/)      | dlBandwidth       | BW_Config                                                                                  | Bandwidth_Setting                                                                  | BW_Parameter                                                                     | [Extended_BW](https://www.samsung.com/us/business/networks/)       |
| **Transmission Power**    | Maximum transmission power per antenna         | [TS 36.101 Section 6.2.5](https://www.3gpp.org/ftp/Specs/archive/36_series/36.101/)    | maxTxPower        | TxPower_Max                                                                                | Power_Config                                                                       | PowerControl_Enhanced                                                            | [TxPwr_Adaptive](https://www.zte.com.cn/global/products/wireless/) |
| **Antenna Configuration** | Number of transmit/receive antenna elements    | [TS 36.213 Section 7.1](https://www.3gpp.org/ftp/Specs/archive/36_series/36.213/)      | antennaPortsCount | [Massive_MIMO](https://www.ericsson.com/en/portfolio/networks/ericsson-radio-system/antennas) | MIMO_Config                                                                        | Antenna_Array                                                                    | MIMO_Setup                                                      |

Output Parameters

| Parameter Name                  | Description                                   | 3GPP Reference                                                                   | 3GPP Standard       | Ericsson                                     | Nokia                                                                              | Huawei                                                                            | Samsung                                                                |
| ------------------------------- | --------------------------------------------- | -------------------------------------------------------------------------------- | ------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **RSRP**                  | Reference Signal Received Power measurement   | [TS 36.214 Section 5.1.1](https://www.3gpp.org/ftp/Specs/archive/36_series/36.214/) | rsrpResult          | RSRP_Enhanced                                | [RSRP_Precise](https://www.nokia.com/networks/technologies/self-organizing-networks/) | RSRP_Advanced                                                                     | RSRP_Optimized                                                         |
| **RSRQ**                  | Reference Signal Received Quality measurement | [TS 36.214 Section 5.1.3](https://www.3gpp.org/ftp/Specs/archive/36_series/36.214/) | rsrqResult          | RSRQ_Adaptive                                | RSRQ_Extended                                                                      | [RSRQ_Intelligent](https://carrier.huawei.com/en/solutions/ran-solutions/son)        | RSRQ_Smart                                                             |
| **SINR**                  | Signal to Interference plus Noise Ratio       | [TS 36.214 Section 4](https://www.3gpp.org/ftp/Specs/archive/36_series/36.214/)     | sinrResult          | SINR_Optimized                               | SINR_Advanced                                                                      | SINR_Enhanced                                                                     | [AI_SINR](https://www.samsung.com/us/business/networks/private-networks/) |
| **Throughput**            | Maximum data transmission rate                | [TS 36.306 Table 4.1A](https://www.3gpp.org/ftp/Specs/archive/36_series/36.306/)    | dlThroughput        | DL_Throughput                                | UL_DL_Rate                                                                         | Throughput_Max                                                                    | [CA_Throughput](https://www.zte.com.cn/global/about/news/20200520-2)      |
| **Latency**               | End-to-end packet transmission delay          | [TS 22.261 Section 6.1](https://www.3gpp.org/ftp/Specs/archive/22_series/22.261/)   | packetDelayBudget   | [Ultra_Latency](https://www.ericsson.com/en/5g) | Latency_Optimized                                                                  | Delay_Minimized                                                                   | Latency_Reduced                                                        |
| **Handover Success Rate** | Percentage of successful handover procedures  | [TS 36.331 Section 5.5](https://www.3gpp.org/ftp/Specs/archive/36_series/36.331/)   | handoverSuccessRate | HO_Success_Rate                              | [ML_Handover_Rate](https://www.nokia.com/networks/solutions/network-automation/)      | Smart_HO_Rate                                                                     | Adaptive_HO_Rate                                                       |
| **Cell Load**             | Physical Resource Block usage percentage      | [TS 36.213 Section 6](https://www.3gpp.org/ftp/Specs/archive/36_series/36.213/)     | prbUtilizationDL    | Cell_Load_PRB                                | PRB_Usage                                                                          | [Dynamic_Load](https://carrier.huawei.com/en/solutions/ran-solutions/load-balancing) | Load_Balance                                                           |

## Message Sequence Chart (MSC)

> [!NOTE]
> **MSC Should Include:**
>
> 1. **Actors/Components** - All participating systems and users
> 2. **Message Flow** - Sequential communication between components
> 3. **Timing** - Order of operations and dependencies
> 4. **Error Handling** - Alternative flows and error scenarios
> 5. **Data Validation** - Authentication and authorization steps

### User Authentication Flow (O-RAN O1 Interface)
```mermaid
sequenceDiagram
    participant USER as Network Operator
    participant SMO as SMO/OAM System
    participant NETCONF as NETCONF Server
    participant O1_CLIENT as O1 Client Module
    participant DU_MGR as DU Manager
    participant AUTH_DB as Authentication DB
    participant ALARM as Alarm Manager
    participant VES as VES Agent
    participant LOG as Audit Logger

    title O-DU User Authentication Flow (O-RAN O1 Interface)

    Note over USER,LOG: Initial Authentication Request
    USER->>SMO: Login Request (username/password)
    SMO->>AUTH_DB: Validate Credentials
    AUTH_DB->>SMO: User Profile & Permissions
    
    alt Authentication Success
        SMO->>NETCONF: Establish NETCONF Session
        Note right of NETCONF: TCP:830 (NETCONF over SSH)
        NETCONF->>O1_CLIENT: NETCONF Hello Exchange
        O1_CLIENT->>NETCONF: Capability Advertisement
        NETCONF->>SMO: Session Established
        
        SMO->>O1_CLIENT: Authentication Token Validation
        O1_CLIENT->>DU_MGR: Validate O-DU Access Rights
        DU_MGR->>AUTH_DB: Check Role-Based Permissions
        AUTH_DB->>DU_MGR: Permission Matrix
        
        alt Authorized Access
            DU_MGR->>O1_CLIENT: Access Granted
            O1_CLIENT->>SMO: Authentication Success
            
            Note over O1_CLIENT,LOG: Security Event Logging
            O1_CLIENT->>ALARM: Generate Security Event
            ALARM->>VES: Security Alarm (Authentication Success)
            VES->>LOG: Audit Log Entry
            LOG->>VES: Log Confirmed
            VES->>ALARM: VES Event Sent
            ALARM->>O1_CLIENT: Security Event Logged
            
            SMO->>USER: Login Successful
            
            Note over USER,LOG: Authenticated Session Management
            loop Session Management
                USER->>SMO: O-DU Management Operations
                SMO->>NETCONF: NETCONF RPC Request
                NETCONF->>O1_CLIENT: Validate Session Token
                O1_CLIENT->>DU_MGR: Check Operation Permissions
                
                alt Permission Granted
                    DU_MGR->>O1_CLIENT: Operation Authorized
                    O1_CLIENT->>NETCONF: Execute Operation
                    NETCONF->>SMO: Operation Response
                    SMO->>USER: Operation Result
                    
                    Note right of O1_CLIENT: Log successful operation
                    O1_CLIENT->>LOG: Operation Audit Log
                    
                else Permission Denied
                    DU_MGR->>O1_CLIENT: Access Denied
                    O1_CLIENT->>ALARM: Generate Security Violation
                    ALARM->>VES: Security Alarm (Unauthorized Access)
                    VES->>LOG: Security Violation Log
                    LOG->>VES: Violation Logged
                    VES->>ALARM: Security Alert Sent
                    ALARM->>O1_CLIENT: Violation Processed
                    
                    O1_CLIENT->>NETCONF: Operation Rejected
                    NETCONF->>SMO: Access Denied Response
                    SMO->>USER: Operation Unauthorized
                end
            end
            
        else Unauthorized Access
            DU_MGR->>O1_CLIENT: Access Denied
            O1_CLIENT->>ALARM: Security Violation Alert
            ALARM->>VES: Failed Authentication Alarm
            VES->>LOG: Failed Auth Audit Log
            LOG->>VES: Security Log Created
            VES->>ALARM: Alert Dispatched
            ALARM->>O1_CLIENT: Security Alert Processed
            
            O1_CLIENT->>SMO: Authentication Failed
            SMO->>USER: Access Denied
        end
        
    else Authentication Failure
        AUTH_DB->>ALARM: Authentication Failure Event
        ALARM->>VES: Failed Login Alarm
        VES->>LOG: Failed Login Audit
        LOG->>VES: Failure Logged
        VES->>ALARM: Failure Alert Sent
        ALARM->>AUTH_DB: Security Event Processed
        
        SMO->>USER: Invalid Credentials
    end
    
    Note over USER,LOG: Session Termination
    USER->>SMO: Logout Request
    SMO->>NETCONF: Close NETCONF Session
    NETCONF->>O1_CLIENT: Session Termination
    O1_CLIENT->>DU_MGR: Invalidate Session Tokens
    DU_MGR->>O1_CLIENT: Session Cleared
    O1_CLIENT->>LOG: Session Termination Log
    LOG->>O1_CLIENT: Logout Recorded
    O1_CLIENT->>NETCONF: Session Closed
    NETCONF->>SMO: Session Terminated
    SMO->>USER: Logout Successful
```

### Cell Configuration Flow (O-RAN F1 Interface)
**O-DU Message Sequence Chart**
```mermaid
sequenceDiagram
    participant SMO
    participant OCU
    participant DU APP
    participant RLC
    participant SCH
    participant MAC
    participant ODU_LOW
    participant UE

    title O-DU High Cell Up and Broadcast Procedure

    SMO->>OCU: [O1_ENABLE]
    OCU->>OCU: edit-config [Cell Configuration]
    note right of OCU: Store Cell Configuration in local DB
    
    note over DU APP, ODU_LOW: Platform and layer initialization

    OCU->>DU APP: F1 SETUP REQUEST
    DU APP->>OCU: F1 SETUP RESPONSE

    DU APP->>RLC: Cell Configuration Request
    RLC->>SCH: Cell Configuration Request
    SCH->>MAC: Cell Configuration Request
    MAC->>ODU_LOW: CONFIG.Request
    ODU_LOW-->>MAC: CONFIG.Response
    MAC-->>SCH: Cell Configuration Response
    SCH-->>RLC: Cell Configuration Response
    RLC-->>DU APP: Cell Configuration Response

    DU APP->>OCU: GNB-DU CONFIGURATION UPDATE
    OCU-->>DU APP: GNB-DU CONFIGURATION UPDATE ACKNOWLEDGE

    DU APP->>RLC: CELL START REQ
    RLC->>SCH: CELL START REQ
    SCH->>MAC: START.request
    MAC->>ODU_LOW: SLOT Indication
    ODU_LOW-->>MAC: SLOT Indication
    MAC-->>SCH: SLOT INDICATION #1
    SCH-->>RLC: SLOT INDICATION #1

    RLC->>DU APP: CELL UP

    alt O1_ENABLE
        DU APP->>OCU: CELL UP Alarm Notification
    end

    MAC-->>SCH: SLOT INDICATION #2
    MAC-->>SCH: SLOT INDICATION #n

    SCH->>SCH: SSB OCCASION DETECTED
    SCH->>MAC: DL SCHEDULING INFO
    MAC->>ODU_LOW: DL TTI Req[SSB]
    ODU_LOW->>UE: SSB(MIB)

    SCH->>SCH: SIB1 OCCASION DETECTED
    SCH->>MAC: DL SCHEDULING INFO
    MAC->>ODU_LOW: DL TTI Req[PDCCH]
    MAC->>ODU_LOW: TX TTI Req[PDSCH]
    ODU_LOW->>UE: SIB
```

### Configuration

**Environment Variables:**
Create a `.env` file in the root directory with the following variables:

```bash
# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=your_database_name
DB_USER=your_username
DB_PASSWORD=your_password

# Application Settings
APP_PORT=3000
APP_DEBUG=false
```

**Configuration Files:**

- `config/settings.json`: Contains application-specific settings
- Refer to `config/.env.example` for all available environment variables

### Installation Steps

Installation is the next section in an effective README. Tell other users how to install your project locally. Optionally, include a gif to make the process even more clear for other people.

1. **Clone the repository:**

   ```sh
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```
2. **Install dependencies:**

   ```sh
   pip install -r requirements.txt 
   ```
3. **Set up environment variables:**

   Create a `.env` file in the root directory and add the necessary environment variables. Refer to `.env.example` for guidance.
4. **Run the application:**

   ```sh
   python3 app.py
   ```

## Post-Installation Verification

Follow these steps to verify your installation was successful:

1. **Check Application Status:**

   ```bash
   # Check if the application is running
   ps aux | grep app.py
   ```

   **Expected Result:** You should see the process running with PID and resource usage information.
2. **Test Basic Functionality:**

   ```bash
   # Test API endpoint (if applicable)
   curl http://localhost:3000/health
   ```

   **Expected Result:** Response should return `{"status": "OK", "timestamp": "..."}` or similar.
3. **Verify Database Connection:**

   ```bash
   # Run database connectivity test
   python3 -c "from src.main import test_db_connection; test_db_connection()"
   ```

   **Expected Result:** Output should confirm successful database connection.

## Troubleshooting

### Common Issues and Solutions

1. **Issue: Port already in use**

   **Error Message:** `Address already in use: 3000`

   **Solution:**

   ```bash
   # Find process using the port
   sudo lsof -i :3000
   # Kill the process (replace PID with actual process ID)
   kill -9 <PID>
   ```
2. **Issue: Python dependencies not found**

   **Error Message:** `ModuleNotFoundError: No module named 'module_name'`

   **Solution:**

   ```bash
   # Reinstall dependencies
   pip install -r requirements.txt
   # Or install specific package
   pip install module_name
   ```
3. **Issue: Permission denied errors**

   **Error Message:** `Permission denied: '/path/to/file'`

   **Solution:**

   ```bash
   # Fix file permissions
   chmod 755 /path/to/file
   # Or run with appropriate user permissions
   sudo python3 app.py
   ```

## Additional Resources

**Documentation:**

- [Official Project Documentation](https://your-project-docs.com)
- [API Reference Guide](https://your-project-api.com)
- [Configuration Reference](https://your-project-config.com)

**Community Support:**

- [GitHub Issues](https://github.com/your-username/your-repo/issues)
- [Stack Overflow Tag](https://stackoverflow.com/questions/tagged/your-project)
- [Discord Community](https://discord.gg/your-project)

**Contact:**

- **Maintainer:** Your Name (<your.email@example.com>)
- **Support Team:** <support@your-project.com>
- **Emergency Contact:** +1-xxx-xxx-xxxx (for critical issues only)

---

> [!NOTE]
> This installation guide is regularly updated. For the latest version, check the [GitHub repository](https://github.com/your-username/your-repo).
