# CareerGraph Product Architecture

**Source:** careerhub/Docs/Graph_Memory_Architecture_Decision.md  
**Date:** 2026-08-20  
**Owner:** careerhub  
**Phase:** 4B.1

## Purpose

Document CareerGraph product layer extracted from Graph Memory Architecture Decision.

## Product Layer

### CareerGraph
Open source:
- desktop app;
- MCP integration;
- professional graph model;
- career workflows;
- vacancy tracking;
- matching;
- exports.

## Product Features

CareerGraph provides:
- Professional graph model for career management
- Career workflows
- Vacancy tracking
- Matching capabilities
- Export functionality

## Open Source Client Model

CareerGraph operates as open source client:
```
Open source client
+
Private intelligence engine
```

Not selling "another CV generator".

## Ownership Note

This document contains CareerGraph product layer concepts extracted from careerhub/Docs/Graph_Memory_Architecture_Decision.md. Core architecture concepts remain in graph-memory-core.

**Original source preserved:** careerhub/Docs/Graph_Memory_Architecture_Decision.md
