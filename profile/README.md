<center><img src="logo.jpg" alt="logo" width="200"/></center>

```ld-agent is a dynamic linker for AI capabilities - think `ld-so` but for agentic systems instead of shared libraries. Just as `ld-so` discovers, loads, and links shared objects at runtime to create executable programs, ld-agent discovers, loads, and links agentic capabilities at runtime to create composable AI systems.```


## What is ld-agent?

Like traditional dynamic linkers, ld-agent:
- **Discovers capabilities** at runtime from standardized locations
- **Resolves dependencies** and validates compatibility  
- **Loads modules** into the runtime namespace
- **Links symbols** (AI tools/functions) for execution
- **Manages the runtime environment** for loaded capabilities

This enables truly modular AI systems where capabilities can be mixed, matched, and composed dynamically - no recompilation required.

## Language Implementations

ld-agent is available in multiple languages, each leveraging language-specific strengths while maintaining the same conceptual model:

### 🐍 [Python](./ld-agent-python/)
- **Best for**: AI agent frameworks, MCP servers, rapid prototyping
- **Features**: Pydantic validation, automatic environment management, CLI tools
- **Install**: `pip install ld-agent`

### 🚀 [Go](./ld-agent-go/)
- **Best for**: High-performance servers, cloud-native deployments, system tools
- **Features**: Compile-time safety, reflection-based validation, shared library loading
- **Install**: `go get github.com/your-org/ld-agent-go`

### 📦 [TypeScript/JavaScript](./ld-agent-ts/)
- **Best for**: Web applications, Node.js services, browser-based AI
- **Features**: Type safety, async/await support, npm ecosystem integration
- **Install**: `npm install ld-agent`

## Quick Start

### Python
```python
from ldagent import load_plugins

# Load all capabilities
plugins = load_plugins()

# Use a tool
calculator = plugins.get_tool("calculator.add_numbers")
result = calculator(10, 20)  # Returns 30
```

### Go
```go
package main

import "github.com/your-org/ld-agent-go"

func main() {
    loader := ldagent.NewPluginLoader("plugins")
    loader.LoadAll()
    
    tool := loader.GetTool("calculator.add_numbers")
    result := tool.Call(10.0, 20.0)  // Returns 30.0
}
```

### TypeScript
```typescript
import { PluginLoader } from 'ld-agent';

const loader = new PluginLoader('plugins');
await loader.loadAll();

const tool = loader.getTool('calculator.add_numbers');
const result = await tool(10, 20);  // Returns 30
```

## Plugin Development

All ld-agent implementations follow the same plugin specification. Here's a simple calculator plugin:

### Python
```python
# plugins/calculator.py
_module_info = {
    "name": "Calculator",
    "description": "Basic arithmetic operations",
    "version": "1.0.0"
}

def add_numbers(a: float, b: float) -> float:
    """Add two numbers together."""
    return a + b

_module_exports = {
    "tools": [add_numbers]
}
```

### Go
```go
// plugins/calculator/main.go
package main

var ModuleInfo = map[string]interface{}{
    "name": "Calculator",
    "description": "Basic arithmetic operations",
    "version": "1.0.0",
}

func AddNumbers(a, b float64) float64 {
    return a + b
}

var ModuleExports = map[string]interface{}{
    "tools": []interface{}{
        map[string]interface{}{
            "name": "add_numbers",
            "function": AddNumbers,
            "description": "Add two numbers together",
        },
    },
}
```

### TypeScript
```typescript
// plugins/calculator.ts
export const moduleInfo = {
    name: "Calculator",
    description: "Basic arithmetic operations",
    version: "1.0.0"
};

export function addNumbers(a: number, b: number): number {
    return a + b;
}

export const moduleExports = {
    tools: [addNumbers]
};
```

## Architecture

ld-agent follows the same conceptual model as traditional dynamic linkers:

1. **Discovery** - Scans plugin directories for capabilities
2. **Loading** - Uses language-specific module loading mechanisms
3. **Symbol Resolution** - Finds exported functions and metadata
4. **Registration** - Builds registries of available capabilities
5. **Execution** - Calls functions with proper argument mapping

This creates a universal standard for composable AI systems - essentially **POSIX for agentic systems**.

## Documentation

- 📖 [Plugin Specification](./docs/PLUGIN_SPECIFICATION.md) - Standard interface for all plugins
- 🏗️ [Architecture Guide](./docs/ARCHITECTURE.md) - How ld-agent works internally
- 🐍 [Python Documentation](./ld-agent-python/README.md) - Python-specific guide
- 🚀 [Go Documentation](./ld-agent-go/README.md) - Go-specific guide  
- 📦 [TypeScript Documentation](./ld-agent-ts/README.md) - TypeScript-specific guide

## Use Cases

### AI Agent Frameworks
```python
# Pydantic AI, LangChain, etc.
from ldagent import load_plugins

plugins = load_plugins()
agent = Agent(tools=plugins.list_tools())
```

### MCP Servers
```python
# Model Context Protocol servers
from mcp.server import Server
from ldagent import load_plugins

server = Server("my-agent")
plugins = load_plugins()

for tool_name in plugins.list_tools():
    tool = plugins.get_tool(tool_name)
    server.register_tool(tool_name, tool)
```

### Microservices
```go
// High-performance Go services
loader := ldagent.NewPluginLoader("plugins")
loader.LoadAll()

http.HandleFunc("/tools", func(w http.ResponseWriter, r *http.Request) {
    tools := loader.ListTools()
    json.NewEncoder(w).Encode(tools)
})
```

### Web Applications
```typescript
// Browser-based AI applications
import { PluginLoader } from 'ld-agent';

const loader = new PluginLoader('/plugins');
await loader.loadAll();

// Use in React, Vue, etc.
const tools = loader.listTools();
```

## Features

- 🔌 **Universal Plugin System** - Same interface across all languages
- 🤖 **AI Agent Ready** - Perfect for agent frameworks and MCP servers
- 🌍 **Environment Management** - Automatic `.env` template generation
- 📦 **Dependency Handling** - Automatic dependency detection and validation
- 🛠️ **CLI Tools** - Command-line interface for plugin management
- 🔧 **Platform Aware** - Built-in platform compatibility checking
- 📋 **Rich Metadata** - Comprehensive plugin descriptions and requirements
- ⚡ **High Performance** - Optimized for production use
- 🔒 **Type Safe** - Strong typing in all implementations

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality
4. Run tests for all implementations
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Community

- 🐛 [Report Issues](https://github.com/your-org/ld-agent/issues)
- 💬 [Discussions](https://github.com/your-org/ld-agent/discussions)
- 📚 [Documentation](./docs/)
- 🔧 [Examples](./examples/)

---

**ld-agent**: Making AI systems as composable as Unix systems. 
