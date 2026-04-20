# HR Workflow Designer (Tredence Case Study)

A modern, full-featured **React + TypeScript workflow builder** for HR processes. This project demonstrates a scalable, modular architecture for creating and managing complex business workflows with real-time validation, simulation, and analytics.

Built as a **Full Stack Engineering Intern case study**, showcasing best practices in component design, state management, and workflow orchestration.

---

## 🎯 Core Features

### ✅ What is Implemented

### 1) Workflow Canvas (React Flow)
- Drag-and-drop node creation from a left sidebar
- Custom node types with visual color coding:
  - Start Node (Green)
  - Task Node (Blue)
  - Approval Node (Amber)
  - Automated Step Node (Purple)
  - End Node (Red)
- Connect nodes with edges
- Select node to edit configuration
- Delete nodes with panel action and delete key for canvas selections
- **Node-level metrics badges** showing field count
- **Premium UI** with gradients, shadows, hover effects, and smooth transitions
- Basic validation:
  - Exactly one Start node
  - At least one End node
  - Start cannot have incoming edges
  - Non-End nodes must have outgoing edges
  - Non-Start nodes must have incoming edges
  - Cycle detection

### 2) Node Editing / Configuration Forms
Right panel updates based on selected node type using controlled form state.

- **Start Node**
  - Title
  - Metadata key-value pairs

- **Task Node**
  - Title (required by UX intent)
  - Description
  - Assignee
  - Due date
  - Custom fields (key-value)

- **Approval Node**
  - Title
  - Approver role
  - Auto-approve threshold (number)

- **Automated Step Node**
  - Title
  - Action selector from mock API (`GET /automations` behavior)
  - Dynamic parameters generated from action definition

- **End Node**
  - End message
  - Summary flag toggle

### 3) Mock API Layer
Implemented in `src/api/mockApi.ts` as async local mocks:
- `getAutomations()` simulates `GET /automations`
- `simulate(graph)` simulates `POST /simulate`

Mock automations include:
- `send_email`
- `generate_doc`
- `create_ticket`

### 4) Workflow Test / Sandbox Panel
- Serializes complete graph (`nodes + edges`) and displays JSON
- Runs simulation against mock API
- Shows validation issues when invalid
- Shows step-by-step execution log when valid

### 5) Performance Analytics & Insights Dashboard
Real-time workflow metrics:
- **Total Nodes & Connections** count
- **Average Outgoing Connections** per node
- **Workflow Complexity** calculation (Simple → Very Complex)
- **Node Breakdown** by type with color-coded badges
- **Workflow Features** detection (Approval Steps, Automation)
- **Execution Time Estimate** based on workflow composition

### 6) Example Workflow

The following shows a **medium-complexity HR onboarding workflow** with 7 nodes demonstrating parallel processing, approvals, and automations:

- **Start** → Employee Onboarding Started
- **Task 1** → Submit Pre-Onboarding Documents (with metadata: department, priority)
- **Approval** → Manager Review (with auto-approve threshold)
- **Automation** → Send Welcome Email & Generate Credentials
- **Task 2a** → IT Equipment Setup (parallel)
- **Task 2b** → HR Compliance Training (parallel)
- **End** → Onboarding Complete

This example demonstrates:
✅ Multi-step workflow progression  
✅ Parallel task execution  
✅ Approval gates with validation  
✅ Automated actions with external integrations  
✅ Complex node metadata and custom fields  

---

## 🏗️ System Architecture

### Component Structure

```text
src/
  api/
    mockApi.ts                  # Mock data layer (automations, simulations)
  components/
    canvas/
      WorkflowCanvas.tsx        # React Flow canvas + node rendering
    forms/
      NodeFormPanel.tsx         # Dynamic form panel for node editing
    insights/
      PerformanceInsights.tsx   # Real-time metrics & analytics dashboard
    nodes/
      StartNode.tsx, TaskNode.tsx, ApprovalNode.tsx, AutomatedNode.tsx, EndNode.tsx
      BaseNode.tsx              # Shared node logic & styling
    palette/
      NodePalette.tsx           # Drag-and-drop node palette
    sandbox/
      SandboxPanel.tsx          # Workflow simulation & test panel
  types/
    workflow.ts                 # TypeScript interfaces & types
  utils/
    graphValidation.ts          # Validation engine (cycles, rules, edges)
  App.tsx, main.tsx, index.css
```

### Architecture Diagram

The following diagram shows the system layers, component interactions, and data flow:

![Architecture Diagram](./docs/architecture-diagram.png)

**Key interactions:**
- **UI Layer** → State Management (nodes, edges, form state)
- **Node Palette** → Creates nodes via drag-and-drop
- **Workflow Canvas** → Renders and manages node/edge interactions
- **Form Panel** → Updates selected node configuration
- **Validation Engine** → Validates graph rules (cycles, start/end constraints)
- **Mock API** → Provides automation definitions and simulation results
- **Performance Insights** → Reads state for real-time metrics

### Execution Flow Diagram

The following sequence diagram shows the complete user interaction flow:

![Execution Flow](./docs/execution-flow.png)

**Key flows:**
1. User opens application → Initialize nodes, edges, state
2. Drag node → Add to canvas, update UI
3. Click node → Load configuration into form panel
4. Edit properties → Update node data, re-render
5. Validate graph → Check rules, show errors or allow execution
6. Execute automation → Fetch data from mock API, update node output
7. Display metrics → Calculate and show performance insights

---

## 🚀 Getting Started

### Tech Stack
- **React 18** - UI framework
- **TypeScript** - Type safety
- **Vite** - Build tool & dev server
- **React Flow** (`@xyflow/react`) - Workflow canvas library

### Installation & Setup
### Installation & Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/hr-workflow-designer.git
cd hr-workflow-designer

# Install dependencies
npm install

# Start development server
npm run dev
```

The application will be available at `http://localhost:5173`

### Build for Production

```bash
npm run build      # TypeScript compilation + Vite build
npm run preview    # Preview production build locally
```

---

## 💡 Design Principles

- **Separation of Concerns** - Canvas, forms, API, and validation are decoupled
- **Type Safety** - Reusable TypeScript interfaces across all components
- **Extensibility** - Easy to add new node types or validation rules
- **Premium UX** - Gradients, shadows, transitions for polished feel
- **Zero Backend** - Mock API preserves integration boundaries without server dependency

---

## 🔑 Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Async Mock API** | Allows realistic integration patterns without requiring a backend |
| **Centralized Validation** | `graphValidation.ts` is reused by canvas, forms, and simulation |
| **Typed Node Data** | `WorkflowNodeData` interface shared across all components |
| **Feature-First Architecture** | Components organized by feature (canvas, forms, insights) for scalability |
| **React Flow Library** | Industry-standard for workflow builders; handles complex graph interactions |

---

## 📋 Assumptions & Scope

- ✓ Prototype focuses on workflow design, not persistence
- ✓ Canvas layout is manual; auto-layout is out of scope
- ✓ Validation is practical for common workflows, not BPMN-grade
- ✓ No authentication or multi-user collaboration
- ✓ Mock API provides sufficient fidelity for demonstration

---

## 🛠️ Development

### Project Structure
```
Tredence/
├── src/
│   ├── components/          # React components by feature
│   ├── types/               # TypeScript interfaces
│   ├── utils/               # Utilities (validation)
│   ├── api/                 # Mock API layer
│   ├── App.tsx              # Root component
│   └── main.tsx             # Entry point
├── index.html               # HTML template
├── vite.config.ts           # Vite configuration
├── tsconfig.json            # TypeScript configuration
├── package.json             # Dependencies
└── README.md                # This file
```

### Adding New Node Types

To add a new node type:

1. Create `src/components/nodes/YourNode.tsx` extending `BaseNode`
2. Add type to `WorkflowNodeType` enum in `src/types/workflow.ts`
3. Add form fields in `src/components/forms/NodeFormPanel.tsx`
4. Export from `src/components/nodes/index.ts`
5. Add to palette in `src/components/palette/NodePalette.tsx`

---

## 📞 Support

For questions or issues, please open an issue on GitHub.

---

## 📝 License

This project is open source. Feel free to fork and extend!

---

## 📚 References

- [React Flow Documentation](https://reactflow.dev/)
- [React Documentation](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Vite Documentation](https://vitejs.dev/)

## What is completed vs. what can be added

### Completed
- Core canvas interactions with premium styling
- Custom node components with visual badges for field counts
- Dynamic node config forms
- Mock API integration
- Workflow simulation panel
- Basic validation and cycle detection
- Export workflow as JSON
- Import workflow from JSON
- Undo/Redo (history state with max 40 snapshots)
- **Performance analytics dashboard** with real-time metrics
- **Node complexity analysis** and workflow composition detection
- **Execution time estimation** based on workflow structure
- **Gradient-based premium UI** with smooth transitions and hover effects

### If more time is available
- Rich node-level validation badges (inline error indicators)
- Better simulation timeline UI with visual progress bar
- Persistent storage (local IndexedDB or backend)
- Unit tests (Jest/RTL) and E2E (Cypress/Playwright)
- Node templates and presets (common workflow patterns)
- Workflow versioning and comparison
- Collaborative editing with WebSocket

## Submission notes (for internship application)
When submitting, include:
1. GitHub repository URL
2. Other project links
3. One tricky frontend bug story
4. Resume / LinkedIn

---
This implementation is intentionally practical and interview-focused: clean architecture, working functionality, and clear extension paths.
