# System Patterns: Architecture & Technical Decisions

## Home Assistant Configuration Architecture

### Configuration Structure
```
configuration.yaml (main config)
├── Core Settings (homeassistant block)
├── Component Configurations
├── File Inclusions (!include directives)
├── Input Helpers (input_boolean, input_number, input_select)
├── Template Sensors
└── Optional Components (commented for future use)
```

### Key Design Patterns

#### Security-First Approach
- **Directory Allowlisting**: Restrict external directory access to `/config`, `/share`, `/media`
- **HTTP Security**: CORS settings, trusted proxies, IP ban protection
- **Country Code**: Added for better integration support

#### Performance Optimization Pattern
- **Database Exclusions**: Remove frequently changing entities (sun, date, time, battery levels)
- **History Filtering**: Match recorder exclusions for consistency
- **Logger Configuration**: Reduce verbosity for core components
- **Commit Intervals**: Optimize database write frequency

#### Modular Configuration Pattern
- **File Separation**: automations.yaml, scripts.yaml, scenes.yaml
- **Theme Integration**: !include_dir_merge_named themes
- **Optional Components**: Commented sections ready to enable
- **Secrets Management**: !secret tags for sensitive data

#### Input Helper Hierarchy
```
input_boolean (simple on/off states)
├── lighting_automation
├── guest_mode
├── vacation_mode
└── sleep_mode

input_number (numeric values)
└── brightness_level (1-100%)

input_select (multiple choice)
└── house_mode (Home/Away/Sleep/Guest/Vacation)
```

## Development Environment Architecture

### Tool Installation Strategy
- **Package Manager First**: Use winget for consistent, repeatable installations
- **Version Management**: Install latest LTS versions for stability
- **Environment Integration**: Ensure proper PATH and environment variable setup
- **Documentation Driven**: Every installation documented with verification steps

### Core Tool Stack
```
Development Foundation
├── Git (version control)
├── Node.js + npm (JavaScript ecosystem)
├── Python (general programming)
├── VS Code (primary editor)
└── PowerShell 7 (modern shell)

Workflow Enhancement
├── Windows Terminal (modern terminal)
├── Docker Desktop (containerization)
└── Postman (API testing)
```

### Configuration Patterns

#### PowerShell Configuration
- **Execution Policy**: RemoteSigned for current user (security + functionality balance)
- **Environment Variables**: Automatic PATH refresh after installations
- **Version Verification**: Systematic checking of all installed tools

#### PATH Management Pattern
```powershell
$env:PATH = [System.Environment]::GetEnvironmentVariable("PATH","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("PATH","User")
```

## Critical Implementation Paths

### Home Assistant Configuration Flow
1. **Base Configuration**: Core homeassistant settings with secrets
2. **Component Setup**: Add integrations with proper configuration
3. **Performance Tuning**: Apply recorder/history exclusions
4. **Security Hardening**: HTTP settings and access controls
5. **Input Helpers**: Create automation control interfaces
6. **Optional Components**: Comment out components requiring additional setup
7. **Validation**: Ensure configuration passes Home Assistant checks

### Development Environment Flow
1. **System Assessment**: Check existing installations and OS version
2. **Core Tools**: Install Git, Node.js, Python via winget
3. **Environment Tools**: Add Windows Terminal, PowerShell 7, Docker
4. **Configuration**: Set execution policies, refresh environment variables
5. **Verification**: Test all tools with version checks
6. **Documentation**: Create comprehensive setup guide

## Component Relationships

### Home Assistant Dependencies
```
default_config → Multiple built-in integrations
recorder → history (shared exclusion patterns)
frontend → themes (directory inclusion)
template sensors → person entities (occupancy detection)
input_helpers → automations (control interfaces)
```

### Development Tool Dependencies
```
Git → SSH keys → GitHub/GitLab integration
Node.js → npm → global packages → project tools
Python → pip → virtual environments → project packages
VS Code → extensions → language support → debugging
Docker → WSL2 → container development → deployment
```

## Design Decisions

### Home Assistant Choices
- **SQLite over PostgreSQL**: Simpler setup, adequate for most use cases
- **Exclusion over Inclusion**: Recorder includes specific domains rather than excluding everything
- **Commented Optionals**: Better than removing - shows possibilities without breaking validation
- **Template Sensors**: House occupancy as foundation for automation logic

### Development Environment Choices
- **winget over Chocolatey**: Native Windows package manager, better integration
- **PowerShell 7 over Windows PowerShell**: Cross-platform, modern features
- **LTS Versions**: Stability over cutting-edge features
- **Comprehensive Documentation**: Self-service approach for user independence

## Error Handling Patterns

### Configuration Validation
- **Incremental Fixes**: Address one validation error at a time
- **Optional Components**: Comment out rather than remove problematic sections
- **Environment Refresh**: Reload PATH after installations
- **Verification Commands**: Systematic testing of each component

### Installation Recovery
- **Version Checks**: Verify successful installation before proceeding
- **PATH Refresh**: Handle environment variable updates
- **Execution Policy**: Address PowerShell script restrictions
- **Documentation**: Provide troubleshooting steps for common issues
