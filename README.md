# HR Workflow Designer

A modern **React + TypeScript workflow builder** for HR processes with read-time validation, simulation and analytics.

# Live Demo
[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Now-brightgreen?style=for-the-badge)](https://hr-workflow-designer-module-hivq.vercel.app/)

## Core Features

### What is Implemented

- Drag-and-drop node creation from a left sidebar
- Custom node types with visual color coding:
  - Start Node (Green)
  - Task Node (Blue)
  - Approval Node (Yellow)
  - Automated Step Node (Purple)
  - End Node (Red)
- Real-time validation
- Workflow Automation (Mock API)

## Architecture
<p align="center">
  <img src="./Tredence/docs/image.png" width="600" height="400" />
</p>

## Workflow
<p aligh="center">
  <img src="./Tredence/docs/workflow.jpeg" width="600" height="400" />
</p>

## Preview
<p aligh="center">
  <img src="./Tredence/docs/preview.png" width="600" />
</p>

## What you see here
- **Drag & Drop Builder (Left)**  
  Create workflows using Start, Task, Approval, Automated, and End nodes  

- **Visual Workflow Canvas (Center)**  
  Connect nodes to design complex flows with parallel execution  

- **Node Configuration Panel (Right)**  
  Edit selected node properties dynamically  

- **Real-time Insights Dashboard**  
  View node count, connections, and workflow complexity  

- **Simulation Lab (Bottom)**  
  Run workflows and view execution logs step-by-step  

## Run Locally
- Clone Repo: git clone https://github.com/yourusername/hr-workflow-designer.git
- Go To Project: cd hr-workflow-designer 
- Install Dependencies: npm install 
- Start App: npm run dev

## Tech Stack
- React + TypeScript
- Vite
- React Flow
- Mock API

## Design Decisions
- **Mock API Layer** - Simulates backend without requiring actual server
- **TypeScript** - Ensures type safety across all components
- **Component-Based Architecture** - Easy to extend with new node types
- **Controlled Form State** - Direct manipulation of workflow state for real-time updates

## What's Completed
- 5 customizable node types (Start, Task, Approval, Automated, End)
- Real-time graph validation with cycle detection
- Workflow simulation & execution testing
- Drag-and-drop canvas interface
- Dynamic node configuration forms
- Mock API integration for automations

## Future Enhancements
- Auto-layout algorithm for workflow canvas
- Authentication & multi-user collaboration
- Pre-built workflow templates library

## Deployed On
This project is live at: https://hr-workflow-designer-module-hivq.vercel.app/
Built with Vite for lightning-fast builds and deployment.
