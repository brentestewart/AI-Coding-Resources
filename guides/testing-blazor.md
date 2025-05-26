## 🧪 Testing Blazor Components

This document provides specific guidelines and setup instructions for testing Blazor components using bUnit and related tools.

---

## 📝 Instructions

Use this document to set up and maintain component tests in Blazor projects. The `✅ Tasks` section should be parsed by AI to help scaffold and verify test coverage.

---

## ✅ Tasks
*  [ ] Create the test project for the Blazor App
*  [ ] Add bUnit
*  [ ] Add xUnit
*  [ ] Add Shouldly
*  [ ] Add Microsoft.AspNetCore.Components.Web

---

## 📁 Recommended Folder Layout

```
/MyApp.Tests.Components
  /Pages         ← Page-level component tests
  /Components    ← Core reusable component tests
  /Shared        ← Layouts, wrappers, and static UIs
```

---

## 🧪 Example Patterns

### Basic Rendering Test

```
[Fact]
public void RendersCorrectMarkup()
{
    var ctx = new TestContext();
    var cut = ctx.RenderComponent<MyComponent>(parameters => parameters
        .Add(p => p.Title, "Test Title"));

    cut.MarkupMatches("<h1>Test Title</h1>");
}
```

### Event Handling

```
[Fact]
public void TriggersCallbackOnClick()
{
    var triggered = false;
    var cut = new TestContext().RenderComponent<MyButton>(parameters => parameters
        .Add(p => p.OnClick, () => triggered = true));

    cut.Find("button").Click();
    Assert.True(triggered);
}
```

### Cascading Values & Services

```
[Fact]
public void RendersWithCascadingValue()
{
    var ctx = new TestContext();
    ctx.Services.AddSingleton<IMyService>(new MockMyService());

    var cut = ctx.RenderComponent<MyComponent>();
    // assertions here
}
```

---

## 💡 Best Practices

- Group tests by component type or folder hierarchy
- Use clear, descriptive test method names (e.g., `Should_DisplayError_WhenApiFails`)
- Keep setup logic reusable with test helpers or `Fixture` classes
- Prefer real rendering over mocking whenever feasible
- Validate both markup and behavior (events, callbacks, data changes)

---

## 🧭 Summary

Component testing in Blazor is essential for verifying UI correctness and behavior without relying on full browser automation. bUnit provides a powerful and fast way to achieve this with familiar .NET testing tools.