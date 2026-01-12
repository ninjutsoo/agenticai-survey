# Master Literature CSV Schema

## Purpose
This schema defines the columns for `master_literature.csv`, a systematic classification framework for papers on agentic AI in clinical medicine.

---

## Column Definitions

### 1. Identity (non-negotiable)

#### Paper_ID
- **Type**: String
- **Description**: Short identifier you define for quick reference
- **Format**: Typically `[NAME][YEAR]` (e.g., `BAYMAX25`, `TEAMMED25`)
- **Required**: Yes
- **Unique**: Yes

#### Title
- **Type**: String
- **Description**: Full title of the paper
- **Required**: Yes

#### Year
- **Type**: Integer
- **Description**: Year of publication
- **Format**: YYYY
- **Required**: Yes

#### Paper_Type
- **Type**: Categorical
- **Description**: The type of contribution
- **Values**: 
  - `Survey` - Literature review or survey paper
  - `Primary system` - Novel system or application
  - `Framework` - Conceptual or architectural framework
- **Required**: Yes

---

### 2. Clinical Intent (coarse but necessary)

#### Clinical_Context
- **Type**: Categorical (can be multiple, separated by `/`)
- **Description**: Primary clinical use case or domain
- **Values**:
  - `Diagnosis` - Disease diagnosis and differential diagnosis
  - `Dialogue` - Patient-clinician or clinical dialogue systems
  - `Coding` - Medical coding, billing, documentation
  - `Education` - Medical education and training
  - `Workflow` - Clinical workflow optimization
  - `Evidence` - Evidence synthesis, literature review
- **Required**: Yes

---

### 3. Agency Structure (core axis)

#### Agent_Presence
- **Type**: Categorical
- **Description**: Number of distinct agents in the system
- **Values**:
  - `Single-agent` - One autonomous agent
  - `Multi-agent` - Multiple collaborating agents
- **Required**: Yes

#### Primary_Topology
- **Type**: Categorical
- **Description**: Organizational structure of agent(s)
- **Values**:
  - `Solo` - Single agent acting independently
  - `Dyadic` - Two agents in partnership
  - `Hierarchical` - Layered authority structure
  - `Committee` - Peer agents with voting/consensus
  - `Society` - Complex, emergent multi-agent organization
- **Required**: Yes
- **Note**: This is a key differentiator that existing surveys lack

---

### 4. Control & Verification (medicine-critical)

#### Control_Structure
- **Type**: Categorical
- **Description**: How control is distributed across agents
- **Values**:
  - `Centralized` - Single point of control/orchestration
  - `Decentralized` - Distributed control among peers
  - `Mixed` - Hybrid of centralized and decentralized elements
- **Required**: Yes

#### Verification_Type
- **Type**: Categorical
- **Description**: Mechanism for validating agent outputs
- **Values**:
  - `None` - No explicit verification
  - `Peer` - Cross-agent verification
  - `Symbolic` - Rule-based or formal verification
  - `Hybrid` - Combination of peer and symbolic
- **Required**: Yes

#### Veto_Mechanism
- **Type**: Categorical
- **Description**: Ability to override or block agent decisions
- **Values**:
  - `None` - No veto capability
  - `Soft` - Advisory warnings, suggestions to reconsider
  - `Hard` - Blocking capability, must be addressed
- **Required**: Yes
- **Note**: Critical for safety and auditability in clinical settings

---

### 5. Temporal Reasoning (rarely covered, high value)

#### Temporal_Scope
- **Type**: Categorical
- **Description**: Time horizon over which the agent operates or adapts
- **Values**:
  - `Episodic` - Single interaction or task
  - `Session` - Within a single session or encounter
  - `Longitudinal` - Across multiple sessions over time
  - `Adaptive` - Dynamically adjusts temporal scope
- **Required**: Yes
- **Note**: Rarely addressed in existing surveys but crucial for clinical continuity

---

### 6. Learning & Correction (agentic maturity)

#### Learning_Mode
- **Type**: Categorical
- **Description**: How the agent learns or updates its behavior
- **Values**:
  - `Frozen` - No learning, static model
  - `Fine-tuned` - Pre-trained then specialized
  - `RL` - Reinforcement learning during deployment
  - `Online` - Continuous learning from interactions
- **Required**: Yes

#### Self_Correction
- **Type**: Categorical
- **Description**: Mechanism for the agent to correct its own errors
- **Values**:
  - `None` - No self-correction capability
  - `Prompt-level` - Correction via prompting strategies (e.g., reflection)
  - `Architectural` - Built-in correction mechanisms in architecture
- **Required**: Yes

---

### 7. Survey Logic (meta-analysis)

#### Covered_By_Existing_Surveys
- **Type**: Categorical
- **Description**: Whether this paper's contribution is already covered in existing surveys
- **Values**:
  - `Yes` - Fully covered by existing literature reviews
  - `Partial` - Partially addressed but gaps remain
  - `No` - Not covered, represents a novel gap
- **Required**: Yes
- **Note**: This column supports your argument for why this survey is needed

#### Primary_Survey_Section
- **Type**: String
- **Description**: Which section of your survey this paper primarily belongs to
- **Format**: Free text (e.g., "Multi-agent Diagnosis Systems", "Temporal Clinical Workflows")
- **Required**: Yes

#### Key_Insight
- **Type**: String
- **Description**: One-sentence summary of why this paper matters for your taxonomy
- **Format**: Single sentence, focus on taxonomic contribution
- **Required**: Yes

---

## Usage Notes

1. **Required vs. Optional**: All columns are required for completeness
2. **Multiple Values**: Some fields (like `Clinical_Context`) can contain multiple values separated by `/`
3. **Consistency**: Use exact categorical values as specified to enable filtering and analysis
4. **Key_Insight**: Keep concise; this is for quick reference, not abstract summarization

---

## Example Row

```csv
Paper_ID,Title,Year,Paper_Type,Clinical_Context,Agent_Presence,Primary_Topology,Control_Structure,Verification_Type,Veto_Mechanism,Temporal_Scope,Learning_Mode,Self_Correction,Covered_By_Existing_Surveys,Primary_Survey_Section,Key_Insight
MEDAGENT24,MedAgent: A Multi-Agent Framework for Clinical Decision Support,2024,Primary system,Diagnosis/Workflow,Multi-agent,Hierarchical,Centralized,Peer,Soft,Session,Fine-tuned,Prompt-level,Partial,Multi-Agent Clinical Systems,Demonstrates hierarchical peer review in diagnostic agents with soft veto for safety
```
