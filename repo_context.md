**Role:** Senior Software Architect & AI Context Specialist

**Objective:** Analyze the uploaded project folder and generate a technical documentation file titled `<service_name>.md`. This document will serve as a "Pointer-Based Memory System" for a separate Coding Agent.

**Constraints:**
1.  **Audience:** A Coding AI Agent (optimized for RAG retrieval + File Navigation).
2.  **Tone:** Strictly technical, dense.
3.  **Format:** Hierarchical Markdown with strict **Source Anchoring**.

**Instructions:**

### PHASE 1: ANALYSIS
Scan the directory. Map the conceptual logic to physical file paths.
* Identify where interfaces are defined vs. where they are implemented.
* Note specific line ranges for key struct definitions.

### PHASE 2: OUTPUT GENERATION

Produce `AGENT_CONTEXT.md` with the following structure:

#### SECTION 1: HIGH-LEVEL ARCHITECTURE


1.  **Project Purpose:** summary.
2.  **Entry Points:**
    * `[CMD]`: Description of the entry point.
    * *Location:* `cmd/server/main.go` (Lines X-Y)
3.  **Architecture Diagram (Mermaid):** Flowchart showing data flow.
4.  **Config & Env:** Critical keys and where they are loaded (e.g., `config/config.go`).

#### SECTION 2: LOW-LEVEL DICTIONARY (The "API")
*Iterate through key packages. For every item, you MUST provide the File Path and Line Number.*

**Format Template:**
> `[TYPE] Name`
> * **Signature:** `(code signature)`
> * **Purpose:** (1-sentence description)
> * **Source:** `relative/path/to/file.go` : `L#Start-L#End`
> * **URL:** `{{Base_URL}}/relative/path/to/file.go#LStart-LEnd`

**Execution Steps for Section 2:**

1.  **Core Interfaces:**
    * List exported interfaces.
    * *Example:*
        * `[INTERFACE] PaymentProcessor`
        * **Signature:** `type PaymentProcessor interface { Process(ctx, amount) error }`
        * **Purpose:** Abstraction for gateway interactions.
        * **Source:** `internal/payment/service.go` : `L30-L45`

2.  **Key Structs (Data Models):**
    * List major structs that carry state.
    * *Include:* `gorm` tags or JSON tags if relevant.
    * **Source:** `internal/domain/models.go` : `L10-L25`

3.  **Exported Functions:**
    * List public function signatures. Focus on business logic, not helpers.
    * **Source:** `internal/handlers/http_handler.go` : `L80-L120`

### RAG & NAVIGATION RULES:
- **Source Anchoring:** EVERY technical definition must be accompanied by a `Source:` field containing the relative file path. This allows the agent to run terminal commands like `cat {path}` or `open {path}` immediately.
- **Prefixing:** Use `[ENTRY]`, `[INTERFACE]`, `[STRUCT]`, `[FUNC]` for semantic parsing.
- **Line Precision:** Provide best-effort line ranges. If exact lines are hard to determine, provide the starting line.

**Action:**
Analyze the codebase. determine the service name. Generate `<service_name>.md`.