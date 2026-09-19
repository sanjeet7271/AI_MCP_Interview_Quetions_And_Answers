# Basic MCP clients and Server details

<img width="1536" height="1024" alt="ChatGPT Image Sep 20, 2026, 12_44_49 AM" src="https://github.com/user-attachments/assets/37ca4a09-4d5d-45ca-938d-d8a6fc807aac" />


## Types of MCP Server
                        MCP Servers
                        │
                        ├── 1. Local MCP Server
                        │   │
                        │   ├── Runs on local machine
                        │   ├── Same environment as MCP Client/Host
                        │   └── Examples:
                        │       ├── Local Files
                        │       ├── Local Database
                        │       └── Local Test Automation
                        │
                        ├── 2. Remote MCP Server
                        │   │
                        │   ├── Runs on remote server/cloud
                        │   ├── Accessed over network
                        │   └── Examples:
                        │       ├── Jenkins
                        │       ├── Cloud Services
                        │       ├── Remote Database
                        │       └── Enterprise Applications
                        │
                        └── 3. Custom MCP Server
                            │
                            ├── Developed for specific business requirements
                            ├── Can be Local or Remote
                            └── Example: QA Automation MCP Server
                                ├── run_test()
                                ├── rerun_test()
                                ├── get_test_logs()
                                ├── get_screenshot()
                                ├── trigger_jenkins()
                                └── create_jira_bug()
