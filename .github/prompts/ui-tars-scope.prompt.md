------
mode: 'agent'
description: 'Scope and requirements for UI-TARS Azure OpenAI desktop automation project.'
------



# Project Scope: UI-TARS Azure OpenAI Desktop Automation# UI-TARS Azure OpenAI Computer Use Integration



## Goal## Project Scope

Set up UI-TARS to use Azure OpenAI keys for vision-language inference and enable computer use automation on your desktop via an AI agent.Integrate Azure OpenAI vision-language models with UI-TARS for automated computer control. This project adds Azure OpenAI API support and computer automation capabilities to the existing UI-TARS action parsing framework.



## Requirements## Objectives

- Use Azure OpenAI API keys (provided by user)- ✅ Azure OpenAI API integration for vision-language inference

- Authenticate and interact with Azure OpenAI endpoints- ✅ Screenshot capture and processing for model input

- Parse model outputs to structured actions using UI-TARS- ✅ End-to-end automation loop (screenshot → AI → action → execute)

- Execute actions on the local desktop (mouse, keyboard, screenshots)- ✅ Configuration management for API credentials

- All automation should be performed by the AI agent- 🔄 Example scripts and documentation

- 🔄 Dependency management and testing

## Success Criteria

- Desktop can be controlled by the AI agent using Azure OpenAI## Architecture Overview

- Actions are parsed and executed safely on the user's machine```

- Configuration is environment-variable driven (no hardcoded secrets)UI-TARS Core (existing)

├── action_parser.py          # Existing: Parse responses to actions

## Out of Scope├── prompt.py                 # Existing: System prompts

- No support for non-Azure AI providers└── __init__.py              # Existing: Package initialization

- No web or mobile automation

- No training or fine-tuning modelsAzure Integration (new)

├── azure_config.py          # Azure OpenAI API configuration

## Usage Pattern├── azure_inference.py       # Vision-language model wrapper  

- Authenticate with Azure OpenAI using your keys├── screenshot.py            # Screen capture and processing

- Run the agent to automate desktop tasks via UI-TARS├── automation_agent.py      # Main orchestration class

- All actions and automation are performed locally└── config.py               # Configuration management



---Examples & Documentation

This prompt defines the boundaries and requirements for the project. Use it to guide all development and AI assistance for this repository.├── examples/               # Usage examples and demos
├── docs/                  # Additional documentation
└── README_azure.md       # Azure-specific setup guide
```

## Key Design Principles
1. **Leverage Existing UI-TARS**: Use `parse_action_to_structure_output()` and `parsing_response_to_pyautogui_code()` rather than reimplementing
2. **Azure-First**: Focus on Azure OpenAI integration, not general AI provider support
3. **Environment-Driven Config**: Use environment variables for API credentials
4. **macOS Optimized**: Primary development and testing on macOS
5. **Safety First**: Include failsafes and safe mode for computer automation

## Core Components

### AzureOpenAIConfig
- Manages API keys, endpoints, deployment names
- Validates configuration and creates Azure OpenAI clients
- Environment variable integration

### AzureOpenAIInference  
- Wraps Azure OpenAI vision API calls
- Handles image encoding and message formatting
- Supports conversation history for multi-turn interactions

### ScreenshotCapture
- Cross-platform screen capture (macOS focus)
- Image resizing for model compatibility
- Region-based and full-screen capture

### UITARSAutomationAgent
- Main orchestration class combining all components
- Automation loop: screenshot → inference → parse → execute
- Progress tracking and error handling

## Required Environment Variables
```bash
AZURE_OPENAI_API_KEY=your_api_key_here
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
AZURE_OPENAI_DEPLOYMENT_NAME=your_deployment_name
```

## Dependencies to Add
- `openai` - Azure OpenAI API client
- `pyautogui` - Computer automation  
- `pyperclip` - Clipboard operations
- `pillow` - Image processing (already included)

## Usage Pattern
```python
from ui_tars.automation_agent import UITARSAutomationAgent
from ui_tars.azure_config import AzureOpenAIConfig

# Configure Azure OpenAI
config = AzureOpenAIConfig()  # Uses environment variables

# Create automation agent
agent = UITARSAutomationAgent(config)

# Run automation task
result = agent.run_automation("Click the search button and type 'hello world'")
```

## Success Criteria
- [ ] Can authenticate with Azure OpenAI using environment variables
- [ ] Can capture and process screenshots for model input
- [ ] Can perform end-to-end automation: screenshot → AI response → computer actions
- [ ] Includes working examples for common automation tasks
- [ ] Has comprehensive documentation for setup and usage

## Out of Scope
- Support for non-Azure AI providers (OpenAI, Anthropic, etc.)
- Training or fine-tuning models
- Web automation (browser-specific)
- Mobile device automation
- GUI for configuration or monitoring

## File Structure
```
codes/ui_tars/
├── __init__.py
├── action_parser.py         # [EXISTING] 
├── prompt.py               # [EXISTING]
├── azure_config.py         # [NEW] Azure API configuration
├── azure_inference.py      # [NEW] Azure OpenAI wrapper
├── screenshot.py           # [NEW] Screen capture utilities  
├── automation_agent.py     # [NEW] Main automation orchestrator
└── config.py              # [NEW] Configuration management

examples/
├── basic_automation.py     # Simple automation example
├── multi_step_task.py      # Complex multi-step example
└── screenshot_demo.py      # Screenshot capture demo

docs/
├── azure_setup.md         # Azure OpenAI setup guide
├── automation_guide.md    # Computer use automation guide
└── troubleshooting.md     # Common issues and solutions
```

## Development Guidelines
- Use existing UI-TARS functions wherever possible
- Prioritize simplicity over feature completeness  
- Include comprehensive error handling and logging
- Test all functionality on macOS primarily
- Document environment variable requirements clearly
- Implement safety checks for computer automation