
# Nova Standards

These are the official standards and philosophies for all Nova Modules - Both current and future.
They define how every Nova system should be written, named, structured, and designed to ensure consistency, maintainability and professionalism across the entire engine ecosystem.

---
## Philosophy
Nova follows a design philosophy centered around **clarity**, **determinism** and foremost **performance**.
Every system must be explicit, modular, and easily understandable in isolation.

**Core principles**
- Minimal abstracton - prefer direct control and transparency.
- Deterministic behaviour - no hidden states or race conditions.
- Consistant naming and structure across all modules.
- Independence - every module should compile and function standalone.
- Explicit ownership and resource managment (no raw `new`/`delete`).
- Prioritize performance, control and precision - even if it means sacrificing simplicity or ease of use.

---

## Module Naming

Every Nova Module **must** include the `Nova` prefix to ensure clear identification and avoid conflicts with external libraries.

**Examples:**
- `NovaCore`
- `NovaGraphics`
- `NovaPhyiscs`
- `NovaAudio`
- `NovaAI`
- `NovaInput`
- `NovaNetwork`

**Guidelines:**
- Use **PascalCase** for all module names.
- The name should clearly describe it's purpose (avoid abbreviations).
- Each module must live in it's own namespace (e.g. `namespace Nova::Graphics`)
- Modules should define an **alias** for convenience, where `Nova` is aliased with `N` (e.g. `namespace N = Nova`)
- Always use the **full module name** when defining or referencing symbols.
    - `Nova::VulkanLayer` - yes
    - `Nova::VL` - only as alias

---

## Code Rules

### File Conventions
- Always start headers with `#pragma once`.
- File names must match class names (`Renderer.hpp` -> `Renderer.cpp`).
- Only one class per file (exceptions allowed for small utility headers).
- In header files dont use `using namespace std;`, only in source files
### Naming
| Element | Style | Example |
|---------------|------------|--------------|
| Namespace | `PascalCase` | `Nova::Core` |
| Classes | `PascalCase` | `Renderer`, `SceneManager` |
| Functions | `camelCase` | `updateFrame()`, `createPipeline()` |
| Variables | `camelCase` | `frameTime`, `windowHandle` |
| Constants | `ALL_CAPS` | `MAX_LIGHTS` |
| Enums | `PascalCase` + preifx | `enum class RenderMode {Forward, Deferred};` |
| Class Variables | `mPascalCase` | `mFrame`, `mTick` |
| Files | `PascalCase` | `Core.hpp`, `Renderer.hpp` |

---

## C++ Standards

- C++20 minimum.
- Use `std::unique_ptr` by default, `std::shared_ptr` only when necessary.
- use `const` and `constexpr` wherever possible.
- Avoid macros - prefer inline functions or templates.
- Avoid implicit conversions and magic numbers.

---
## Module Independence
Each Nova Module:
- Must have it's own CMake target.
- Cannot depend on other high-level modules
- Can depend on **NovaCore** for fundamental types and utilities.
- Should define a clean public interface and internal implemention.
- Usage of `template-cmake` is recommended
---
## Build System
- CMake is the only supported build system.
- All modules must use `target_include_directories()` and `target_link_libraries()` properly.
- No global include directories or compiler flags.
- Optional dependencies (e.g. Jolt, Vulkan, Taskflow) must be isolated inside their modules.

---

## Libraries and Dependencies
Each module may depend on specific libraries, defined clearly in it's documentation:
| Module | Dependencies |
| -----------|----------------------|
| **NovaPhyiscs** | Jolt Physics |
| **NovaGraphics** | NovaVulkanLayer |
| **NovaCore** | fmt, spdlog |
| **NovaAI** | - |
| **NovaNetwork** | SLikeNet |

Each library should be wrapped in clean abstraction layer - no direct usage in unrelated modules.


---

## Licensing
All Nova standards and documentation are licensed under the **MIT License**.
This allows full reuse in both open-source and commercial projects.

`MIT License @ 2025 rhacker`

---
## Future Goals
- Unify all older Nova Modules under this standard.
- Maintain a Consistant coding identity across the Nova ecosystem.
