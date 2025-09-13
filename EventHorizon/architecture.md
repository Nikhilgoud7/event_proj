# EventHorizon Architecture

```mermaid
graph TB
    subgraph Frontend[Frontend - React + TypeScript]
        Client[Client Entry - main.tsx]
        Router[Router]
        
        subgraph Pages
            Dashboard[Dashboard]
            Events[EventsPage]
            CreateEvent[CreateEventPage]
            Analytics[AnalyticsPage]
            Attendance[AttendancePage]
            Profile[ProfilePage]
        end
        
        subgraph Components
            UI[UI Components Library]
            Custom[Custom Components]
            
            subgraph CustomComponents[Key Components]
                EB[EventBuilder]
                AD[AnalyticsDashboard]
                AT[AttendanceTracker]
                EC[EventCard]
                AS[AppSidebar]
            end
        end
        
        subgraph State
            TQ[TanStack Query]
            Hooks[Custom Hooks]
        end
    end

    subgraph Backend[Backend - Express + TypeScript]
        Server[Server Entry - index.ts]
        Routes[API Routes]
        Vite[Vite Dev Server]
        Storage[File Storage]
    end

    subgraph Database[Database Layer]
        Drizzle[Drizzle ORM]
        PG[PostgreSQL]
        Schema[Database Schema]
    end

    subgraph SharedLayer[Shared Layer]
        Types[TypeScript Types]
        Validation[Zod Schemas]
    end

    %% Frontend Connections
    Client --> Router
    Router --> Pages
    Pages --> Components
    Components --> UI
    Components --> Custom
    Pages --> State
    State --> TQ

    %% Backend Connections
    Server --> Routes
    Server --> Vite
    Routes --> Storage
    Routes --> Drizzle

    %% Database Connections
    Drizzle --> PG
    Schema --> PG

    %% Shared Layer Connections
    SharedLayer --> Frontend
    SharedLayer --> Backend
    
    %% API Communication
    TQ --REST API--> Routes

    style Frontend fill:#f9f,stroke:#333,stroke-width:2px
    style Backend fill:#bbf,stroke:#333,stroke-width:2px
    style Database fill:#bfb,stroke:#333,stroke-width:2px
    style SharedLayer fill:#fdb,stroke:#333,stroke-width:2px

```

## Architecture Components

### Frontend Layer
- **Client**: React-based SPA using TypeScript
- **Routing**: Wouter for lightweight routing
- **State Management**: TanStack Query for server state
- **UI Components**: 
  - Shadcn UI components
  - Custom components for specific features
- **Key Features**:
  - Drag-and-drop event builder
  - Analytics dashboard with charts
  - Attendance tracking
  - Event management

### Backend Layer
- **Server**: Express.js with TypeScript
- **Development**: Vite for dev server and building
- **File Handling**: Storage utilities for file uploads
- **API Routes**: RESTful endpoints for:
  - User management
  - Event operations
  - Analytics
  - Attendance

### Database Layer
- **ORM**: Drizzle for type-safe database operations
- **Database**: PostgreSQL
- **Schema**: 
  - Users
  - Events
  - Attendance records
  - Analytics data

### Shared Layer
- **Types**: Shared TypeScript interfaces
- **Validation**: Zod schemas for data validation
- **Constants**: Shared configuration and constants

## Key Technologies
- TypeScript
- React
- Express.js
- PostgreSQL
- Drizzle ORM
- TanStack Query
- Shadcn UI
- Recharts
- Tailwind CSS

## Development Architecture
- **Development Server**: Vite
- **Build System**: 
  - Vite for frontend
  - esbuild for backend
- **Type Checking**: TypeScript
- **Package Management**: npm
- **Environment**: Node.js

## Security Layer
- User authentication
- Password hashing
- Session management
- Input validation using Zod

## Deployment Architecture
- **Production Build**:
  - Frontend: Static assets
  - Backend: Node.js server
  - Database: PostgreSQL instance
- **Environment Variables**:
  - Database configuration
  - Server settings
  - API keys