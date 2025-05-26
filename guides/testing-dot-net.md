## 🧪 Testing .NET Class Libraries

This document outlines testing standards and setup instructions for .NET class libraries, particularly those in the Application and Core layers.

---

## 📝 Instructions

Use this document when creating or maintaining test coverage for .NET libraries. The `✅ Tasks` section should be parsed by AI to scaffold and verify testing efforts.

---

## ## ✅ Tasks

-  [ ] Create a test project         
-  [ ]  Add reference to the project under test
-  [ ] Install `xUnit` for unit testing   
-  [ ] Install `Moq` for mocking dependencies
-  [ ] Install Shouldly for expressive assertions

---

## 📁 Recommended Folder Layout

```
/MyApp.Tests.Unit
  /Services       ← Application services
  /Validation     ← Validators and rules
  /Helpers        ← Extension methods and utils
```

---

## 🧪 Example Patterns

### Pure Function Test

```
[Fact]
public void Add_ReturnsCorrectSum()
{
    var result = MathService.Add(2, 3);
    result.Should().Be(5);
}
```

### Service with Dependency

```
[Fact]
public void GetUser_ReturnsUser_WhenExists()
{
    var userRepo = new Mock<IUserRepository>();
    userRepo.Setup(r => r.GetById(1)).Returns(new User { Id = 1 });

    var service = new UserService(userRepo.Object);
    var result = service.GetUser(1);

    result.Should().NotBeNull();
    result.Id.Should().Be(1);
}
```

### Validation

```
[Fact]
public void Validator_FailsWhenNameMissing()
{
    var validator = new UserValidator();
    var result = validator.Validate(new User());

    result.IsValid.Should().BeFalse();
    result.Errors.Should().Contain(e => e.PropertyName == "Name");
}
```

---

## 💡 Best Practices

- Follow AAA (Arrange, Act, Assert) pattern
- Keep each test focused on a single behavior
- Use test builders or factories for complex object creation
- Mock only what you must—favor real dependencies if simple
- Aim for high coverage but prioritize meaningful tests

---

## 🧭 Summary

Testing .NET libraries ensures the reliability of your application's business logic and core services. A well-structured test suite improves confidence, supports refactoring, and enables safe iteration.