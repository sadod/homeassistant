# Technical Context: Technologies & Development Setup

## Technologies Used

### Home Assistant Stack
- **Home Assistant Core**: YAML-based configuration system
- **Database**: SQLite (home-assistant_v3.db)
- **Frontend**: Lovelace UI with theme support
- **Integrations**: default_config bundle + custom components
- **Automation Engine**: Built-in automation/script/scene system
- **TTS**: Google Translate platform
- **Media**: Sonos integration with discovery

### Development Environment Stack
- **Operating System**: Windows 10 Pro x64 (Build 19045)
- **Package Manager**: Windows Package Manager (winget) v1.11.430
- **Version Control**: Git v2.51.0
- **JavaScript Runtime**: Node.js v22.19.0 LTS
- **Package Manager**: npm v10.9.3
- **Python**: v3.13.0 with pip
- **Code Editor**: Visual Studio Code v1.104.1
- **Shell**: PowerShell 7 v7.5.3
- **Terminal**: Windows Terminal
- **Containerization**: Docker Desktop
- **API Testing**: Postman

## Development Setup

### System Configuration
```
Windows 10 Pro x64
├── PowerShell Execution Policy: RemoteSigned (CurrentUser)
├── Environment Variables: Auto-refreshed after installations
├── PATH: Includes all development tools
└── User Profile: Standard user with development permissions
```

### Installation Method
- **Primary**: winget (Windows Package Manager)
- **Verification**: Version checks for each tool
- **Documentation**: Comprehensive setup guide created
- **Recovery**: Error handling for common installation issues

### File Structure
```
E:\HomeAssistant\
├── configuration.yaml (main HA config)
├── configuration_improvements_summary.md
├── development_setup_summary.md
├── memory-bank\
│   ├── projectbrief.md
│   ├── productContext.md
│   ├── systemPatterns.md
│   ├── techContext.md
│   ├── activeContext.md
│   └── progress.md
├── automations.yaml (referenced)
├── scripts.yaml (referenced)
├── scenes.yaml (referenced)
├── themes\ (referenced directory)
└── .clinerules\ (coding standards)
```

## Technical Constraints

### Home Assistant Limitations
- **YAML Validation**: Strict syntax requirements
- **Secret Dependencies**: Configuration depends on secrets.yaml entries
- **Integration Dependencies**: Some components require additional setup
- **Restart Required**: Configuration changes need Home Assistant restart
- **File Includes**: External files must exist for successful validation

### Windows Development Constraints
- **PowerShell Execution Policy**: Default restrictions on script execution
- **PATH Length Limits**: Windows PATH variable length restrictions
- **Permission Requirements**: Some installations require administrator privileges
- **Environment Variables**: Changes require session refresh or restart
- **WSL2 Dependency**: Docker Desktop requires WSL2 for optimal performance

### Tool Version Constraints
- **Node.js**: LTS version for stability (v22.19.0)
- **Python**: Latest stable (v3.13.0)
- **Git**: Latest stable (v2.51.0)
- **PowerShell**: Modern version (v7.5.3) over Windows PowerShell
- **VS Code**: Regular updates recommended

## Dependencies

### Home Assistant Dependencies
```yaml
# Core dependencies (via default_config)
- automation
- backup
- config
- frontend
- history
- logbook
- map
- mobile_app
- person
- script
- sun
- system_health
- zone

# Additional dependencies
- recorder (SQLite database)
- logger (custom configuration)
- tts (Google Translate)
- sonos (media player)
- device_tracker (mobile_app platform)
```

### Development Tool Dependencies
```
Git
├── SSH client (for key-based authentication)
└── Credential manager (Windows integration)

Node.js
├── npm (package manager)
├── npx (package runner)
└── Node.js runtime

Python
├── pip (package installer)
├── venv (virtual environment)
└── Python interpreter

Docker Desktop
├── WSL2 (Windows Subsystem for Linux)
├── Hyper-V (virtualization)
└── Container runtime

VS Code
├── Extensions marketplace
├── Language servers
└── Integrated terminal
```

## Tool Usage Patterns

### Home Assistant Configuration
```yaml
# Pattern: Security-first configuration
homeassistant:
  country: GB  # Enable region-specific features
  allowlist_external_dirs:  # Restrict access
    - /config
    - /share
    - /media

# Pattern: Performance optimization
recorder:
  exclude:  # Remove noise from database
    entities: [sun.sun, sensor.date, sensor.time]
    entity_globs: [sensor.*_linkquality, sensor.*_battery]
    domains: [updater, weather]

# Pattern: Modular organization
automation: !include automations.yaml
script: !include scripts.yaml
scene: !include scenes.yaml
```

### Development Workflow
```powershell
# Pattern: Environment verification
git --version
node --version
npm --version
py --version

# Pattern: Project initialization
git init
npm init
py -m venv venv

# Pattern: Package management
npm install <package>
py -m pip install <package>
winget install <app>
```

## Integration Points

### Home Assistant Integrations
- **Mobile App**: Device tracking and notifications
- **Sonos**: Media player discovery and control
- **Frontend**: Theme integration via directory inclusion
- **Template Sensors**: Dynamic entity creation based on state
- **Input Helpers**: User interface controls for automations

### Development Tool Integrations
- **Git + VS Code**: Source control integration
- **Node.js + VS Code**: JavaScript/TypeScript development
- **Python + VS Code**: Python development with IntelliSense
- **Docker + VS Code**: Container development and debugging
- **PowerShell + Windows Terminal**: Enhanced command-line experience

## Performance Considerations

### Home Assistant Performance
- **Database Size**: Controlled via recorder exclusions
- **Memory Usage**: Optimized through component selection
- **Startup Time**: Reduced by excluding unnecessary integrations
- **Log Volume**: Controlled via logger configuration
- **Network Traffic**: Minimized through local discovery

### Development Environment Performance
- **Disk Space**: Tools installed to standard locations
- **Memory Usage**: Modern versions optimized for performance
- **Startup Time**: Tools configured for quick access
- **Network Usage**: Package managers cache downloads
- **CPU Usage**: Background processes minimized

## Security Considerations

### Home Assistant Security
- **HTTP Security**: IP banning, login attempt limits
- **CORS Protection**: Restricted origins for Cast integration
- **Directory Access**: Limited to essential directories
- **Proxy Trust**: Configured for reverse proxy scenarios
- **Secret Management**: Sensitive data in separate secrets.yaml

### Development Environment Security
- **Execution Policy**: Balanced security (RemoteSigned)
- **Package Sources**: Official repositories only
- **Tool Updates**: Regular updates recommended
- **SSH Keys**: Secure Git authentication
- **Container Security**: Docker best practices
