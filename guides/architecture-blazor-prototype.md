This document provides architectural guidance for rapid Blazor prototyping. The goal is fast iteration while maintaining enough structure to evolve into a more robust architecture later if needed.

---

## 📝 Instructions

Use this structure when building proof-of-concept or early-stage Blazor applications. Favor simplicity, but respect separation of concerns to allow a smoother path to scale later. Tasks marked below will be included in a unified project task list.

---

## ✅ Tasks
*  [ ] Create the Blazor Web App with the folder structure listed below

---

## 🔍 Simplified Architecture

```
Blazor UI (Pages & Components)
   ↓
Services (Business Logic, API Calls)
   ↓
Models (DTOs, Domain Types)
```

All logic resides in a single project, but concerns are separated via folder boundaries.

---

## 📁 Recommended Folder Layout

```
/MyPrototypeApp
  /Pages           ← Razor components for routing
  /Components      ← Reusable UI elements
  /Services
    /Api           ← HttpClient-based API services
    /Core          ← Business logic and utility services
  /Models          ← DTOs and domain models
  /wwwroot         ← Static assets (CSS, images, etc.)
  Program.cs
  App.razor
```

---

## 💡 Practices

- Use partial classes or `.razor.cs` for separation of logic and markup
- Avoid deep nesting and over-engineering
- Create `IService` interfaces only where mocking/testing is necessary
- Consider MediatR only if you expect to grow the app later

---

## 🔥 When to Graduate to Enterprise Architecture

Upgrade when:

- Business rules grow beyond trivial logic
- More than one UI client is planned (e.g., mobile, web)
- You need unit testing for use cases
- External systems (APIs, messaging, DBs) multiply

---

## 🧭 Summary

This prototype architecture balances speed and structure. It lets you get results quickly while keeping your project easy to grow into an enterprise solution when needed.