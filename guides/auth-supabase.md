# Supabase Authentication Integration

## 📝 Instructions

This document guides the setup and integration of Supabase Authentication within your .NET application’s infrastructure layer. Use the MCP server to securely manage environment variables related to authentication.

Supabase Auth supports multiple providers (email/password, OAuth, magic links, etc.). The guidance here focuses on best practices for integrating the Supabase Auth client SDK, handling tokens, and securing access.

---

## ✅ Tasks

-  [ ] Add Supabase NuGet package if not already added  (https://www.nuget.org/packages/supabase)
-  [ ] Retrieve Auth-related keys from the MCP server (e.g., `SUPABASE_URL`, `SUPABASE_ANON_KEY`)
-  [ ] Create an `AuthService` class to wrap Supabase Auth client calls
-  [ ] Implement token storage and refresh logic securely (e.g., in-memory or secure storage)
-  [ ] Set up event handlers for sign-in, sign-out, and session refresh
-  [ ] Implement sign-up, sign-in, and sign-out methods using Supabase Auth API
-  [ ] Add OAuth provider integration as needed (Google, GitHub, etc.)
-  [ ] Handle authentication state changes and propagate events to the UI
-  [ ] Secure API calls by attaching the access token in request headers

---

## 🗂 Recommended Folder Structure

/Infrastructure
  /Supabase
    AuthService.cs
    SupabaseAuthExtensions.cs

---

## 🔒 Environment Variables (via MCP Server)

- `SUPABASE_URL` — your Supabase project URL
- `SUPABASE_ANON_KEY` — public anon key for client SDK
- `SUPABASE_SERVICE_ROLE_KEY` — for admin-level operations (use cautiously)

---

## 💡 Best Practices

- Always use the latest version of the Supabase .NET SDK
- Keep sensitive keys secure; never expose service role keys to client apps
- Use secure token storage mechanisms on client and server sides
- Handle token expiration and refresh proactively to maintain sessions
- Subscribe to auth state events to keep UI and backend in sync
- Abstract Supabase Auth calls behind service interfaces for easier testing and future changes
