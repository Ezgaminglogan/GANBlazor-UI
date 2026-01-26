# 🎨 GANBlazor.UI

A modern, minimal Blazor UI component library inspired by **shadcn/ui**. Build beautiful, accessible web applications with pre-styled components that integrate seamlessly with **Tailwind CSS**.

[![NuGet](https://img.shields.io/nuget/v/GANBlazor.UI.svg)](https://www.nuget.org/packages/GANBlazor.UI/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## ✨ Features

- 🎯 **Modern Design** - Clean, minimal UI components with smooth animations
- 🎨 **Tailwind CSS** - Built with Tailwind utility classes for easy customization
- ♿ **Accessible** - ARIA-compliant components with keyboard navigation support
- 🔧 **Flexible** - Customizable variants, sizes, and classes
- 📦 **Lightweight** - Zero JavaScript dependencies (except Tailwind)
- 🚀 **Ready to Use** - Drop in and start building immediately

---

## 📦 Installation

### Step 1: Install the NuGet Package

```bash
dotnet add package GANBlazor.UI
```

Or via Package Manager Console:

```powershell
Install-Package GANBlazor.UI
```

### Step 2: Install Tailwind CSS

GANBlazor.UI requires Tailwind CSS in your project. Follow the [Tailwind CLI installation guide](https://tailwindcss.com/docs/installation/tailwind-cli):

1. Install Tailwind CSS and CLI via npm:

```bash
npm install tailwindcss @tailwindcss/cli
```

2. Create your input CSS file (e.g., `css/input.css`):

```css
@import "tailwindcss";
```

3. Start the Tailwind CLI build process to scan your files and build CSS:

```bash
npx @tailwindcss/cli -i ./wwwroot/css/input.css -o ./wwwroot/css/output.css --watch
```

4. Add the compiled CSS to your `App.razor`:

```razor
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="/" />
    <link rel="stylesheet" href="css/output.css" />
    <!-- Or if using static assets: -->
    <link rel="stylesheet" href="@Assets["output.css"]" />
    <HeadOutlet @rendermode="InteractiveServer" />
</head>
<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
</body>
</html>
```

### Step 3: Add Imports

Add the following to your `_Imports.razor`:

```razor
@using GANBlazor.UI.Components
@using GANBlazor.UI.Components.UI
@using GANBlazor.UI.Classes.UI
@using static GANBlazor.UI.Classes.UI.ButtonTypes
@using Blazor.Heroicons
```

---

## 🚀 Quick Start

Here's a simple example to get you started:

```razor
@page "/example"

<h1>Welcome to GANBlazor.UI</h1>

<Button Variant="ButtonVariant.Default" OnClick="HandleClick">
    Click Me
</Button>

@code {
    private void HandleClick()
    {
        // Handle button click
    }
}
```

---

## 📚 Components

### 🔘 Button

A versatile button component with multiple variants, sizes, and icon support.

#### Basic Usage

```razor
<Button>Default Button</Button>

<Button Variant="ButtonVariant.Outline">Outline Button</Button>

<Button Variant="ButtonVariant.Ghost">Ghost Button</Button>

<Button Variant="ButtonVariant.Danger">Danger Button</Button>
```

#### With Icons (Heroicons)

GANBlazor.UI integrates with [Blazor.Heroicons](https://github.com/tmcknight/blazor-heroicons). You can specify icons using the `HeroiconName` enum:

```razor
<Button LeftHeroicon="@HeroiconName.ArrowLeft">Back</Button>

<Button RightHeroicon="@HeroiconName.ArrowRight">Next</Button>

<Button LeftHeroicon="@HeroiconName.Trash" Variant="ButtonVariant.Danger">Delete</Button>
```

**Available Icon Types:**

- `HeroiconType.Outline` (default) - Outlined stroke icons
- `HeroiconType.Solid` - Filled solid icons
- `HeroiconType.Mini` - 20x20 solid icons
- `HeroiconType.Micro` - 16x16 solid icons

```razor
<Button LeftHeroicon="@HeroiconName.Star"
        LeftHeroiconType="HeroiconType.Solid">
    Favorite
</Button>
```

#### Icon-Only Button

```razor
<Button IconOnly="true" LeftHeroicon="@HeroiconName.Cog" />
```

#### Sizes

```razor
<Button Size="ButtonSize.Sm">Small</Button>

<Button Size="ButtonSize.Md">Medium</Button>

<Button Size="ButtonSize.Lg">Large</Button>
```

#### Loading State

```razor
<Button IsLoading="true" LoadingText="Saving...">Save</Button>

<Button IsLoading="@isProcessing" OnClick="ProcessData">
    Process
</Button>

@code {
    private bool isProcessing = false;

    private async Task ProcessData()
    {
        isProcessing = true;
        await Task.Delay(2000); // Simulate processing
        isProcessing = false;
    }
}
```

#### Full Width & Alignment

```razor
<Button FullWidth="true">Full Width Button</Button>

<Button FullWidth="true" Align="ButtonAlign.Center">Centered</Button>

<Button FullWidth="true" Align="ButtonAlign.End">Right Aligned</Button>
```

#### Form Submit Button

```razor
<Button Type="ButtonType.Submit" Variant="ButtonVariant.Default">
    Submit Form
</Button>
```

#### Custom Styling

```razor
<Button Class="bg-blue-600 hover:bg-blue-700 text-white">
    Custom Blue Button
</Button>
```

#### API Reference

| Parameter           | Type            | Default        | Description                                           |
| ------------------- | --------------- | -------------- | ----------------------------------------------------- |
| `Variant`           | `ButtonVariant` | `Default`      | Visual style: `Default`, `Outline`, `Ghost`, `Danger` |
| `Size`              | `ButtonSize`    | `Md`           | Button size: `Sm`, `Md`, `Lg`                         |
| `Type`              | `ButtonType`    | `Button`       | HTML type: `Button`, `Submit`, `Reset`                |
| `Disabled`          | `bool`          | `false`        | Disables the button                                   |
| `IsLoading`         | `bool`          | `false`        | Shows loading spinner                                 |
| `LoadingText`       | `string?`       | `"Loading..."` | Text shown during loading                             |
| `LeftHeroicon`      | `string?`       | `null`         | Heroicon name for left icon (use `HeroiconName`)      |
| `LeftHeroiconType`  | `HeroiconType`  | `Outline`      | Icon style: `Outline`, `Solid`, `Mini`, `Micro`       |
| `RightHeroicon`     | `string?`       | `null`         | Heroicon name for right icon (use `HeroiconName`)     |
| `RightHeroiconType` | `HeroiconType`  | `Outline`      | Icon style: `Outline`, `Solid`, `Mini`, `Micro`       |
| `IconOnly`          | `bool`          | `false`        | Makes button square for icon-only display             |
| `FullWidth`         | `bool`          | `false`        | Makes button full width                               |
| `Align`             | `ButtonAlign`   | `Start`        | Alignment: `Start`, `Center`, `End`                   |
| `Class`             | `string?`       | `null`         | Additional CSS classes                                |
| `OnClick`           | `EventCallback` | -              | Click event handler                                   |

---

### 📝 Form

A wrapper component for Blazor's `EditForm` with consistent styling and spacing.

#### Basic Usage

```razor
<Form Model="@formModel" OnValidSubmit="HandleSubmit">
    <DataAnnotationsValidator />

    <!-- Form fields go here -->

    <Button Type="ButtonType.Submit">Submit</Button>
</Form>

@code {
    private MyFormModel formModel = new();

    private void HandleSubmit()
    {
        // Handle form submission
    }

    public class MyFormModel
    {
        [Required]
        public string? Name { get; set; }
    }
}
```

#### API Reference

| Parameter         | Type                         | Default | Description                 |
| ----------------- | ---------------------------- | ------- | --------------------------- |
| `Model`           | `object?`                    | `null`  | The form model              |
| `EditContext`     | `EditContext?`               | `null`  | Optional EditContext        |
| `OnValidSubmit`   | `EventCallback`              | -       | Called when form is valid   |
| `OnInvalidSubmit` | `EventCallback<EditContext>` | -       | Called when form is invalid |
| `Class`           | `string?`                    | `null`  | Additional CSS classes      |

---

### 🏷️ FormField

A container component for form inputs with label and message support.

#### Basic Usage

```razor
<FormField Label="Email Address">
    <FormInput @bind-Value="formModel.Email" placeholder="Enter your email" />
</FormField>
```

#### With Error Message

```razor
<FormField Label="Password">
    <FormInput @bind-Value="formModel.Password"
               type="password"
               placeholder="Enter password" />
    <Message>
        <ValidationMessage For="@(() => formModel.Password)" />
    </Message>
</FormField>
```

#### API Reference

| Parameter      | Type              | Default | Description                |
| -------------- | ----------------- | ------- | -------------------------- |
| `Label`        | `string?`         | `null`  | Field label text           |
| `ChildContent` | `RenderFragment?` | `null`  | Input component content    |
| `Message`      | `RenderFragment?` | `null`  | Message/validation content |
| `Class`        | `string?`         | `null`  | Additional CSS classes     |

---

### 📥 FormInput

A styled text input component with validation support.

#### Basic Usage

```razor
<FormInput @bind-Value="username" placeholder="Enter username" />
```

#### With Attributes

```razor
<FormInput @bind-Value="email"
           type="email"
           placeholder="you@example.com"
           autocomplete="email" />
```

#### API Reference

| Parameter         | Type                         | Default | Description            |
| ----------------- | ---------------------------- | ------- | ---------------------- |
| `Value`           | `string?`                    | `null`  | Input value            |
| `ValueChanged`    | `EventCallback<string?>`     | -       | Value change callback  |
| `ValueExpression` | `Expression<Func<string?>>?` | `null`  | For validation         |
| `Class`           | `string?`                    | `null`  | Additional CSS classes |

**Note:** Supports all standard HTML input attributes via `AdditionalAttributes` (type, placeholder, disabled, etc.)

---

### 💬 FormMessage

A component for displaying error/validation messages.

#### Basic Usage

```razor
<FormMessage>This field is required</FormMessage>
```

#### With Blazor Validation

```razor
<FormMessage>
    <ValidationMessage For="@(() => formModel.Email)" />
</FormMessage>
```

#### API Reference

| Parameter      | Type              | Default | Description            |
| -------------- | ----------------- | ------- | ---------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Message content        |
| `Class`        | `string?`         | `null`  | Additional CSS classes |

---

## 📋 Complete Form Example

Here's a complete registration form demonstrating all components working together:

```razor
@page "/register"
@using System.ComponentModel.DataAnnotations

<div class="max-w-md mx-auto p-6">
    <h1 class="text-2xl font-bold mb-6">Create Account</h1>

    <Form Model="@model" OnValidSubmit="HandleRegistration">
        <DataAnnotationsValidator />

        <FormField Label="Full Name">
            <FormInput @bind-Value="model.FullName"
                       placeholder="John Doe"
                       autocomplete="name" />
            <Message>
                <ValidationMessage For="@(() => model.FullName)" />
            </Message>
        </FormField>

        <FormField Label="Email Address">
            <FormInput @bind-Value="model.Email"
                       type="email"
                       placeholder="you@example.com"
                       autocomplete="email" />
            <Message>
                <ValidationMessage For="@(() => model.Email)" />
            </Message>
        </FormField>

        <FormField Label="Password">
            <FormInput @bind-Value="model.Password"
                       type="password"
                       placeholder="••••••••"
                       autocomplete="new-password" />
            <Message>
                <ValidationMessage For="@(() => model.Password)" />
            </Message>
        </FormField>

        <FormField Label="Confirm Password">
            <FormInput @bind-Value="model.ConfirmPassword"
                       type="password"
                       placeholder="••••••••"
                       autocomplete="new-password" />
            <Message>
                <ValidationMessage For="@(() => model.ConfirmPassword)" />
            </Message>
        </FormField>

        <div class="flex gap-3 mt-8">
            <Button Type="ButtonType.Submit"
                    FullWidth="true"
                    IsLoading="@isSubmitting">
                Create Account
            </Button>

            <Button Variant="ButtonVariant.Outline"
                    FullWidth="true"
                    OnClick="Cancel">
                Cancel
            </Button>
        </div>
    </Form>
</div>

@code {
    private RegistrationModel model = new();
    private bool isSubmitting = false;

    private async Task HandleRegistration()
    {
        isSubmitting = true;

        // Simulate API call
        await Task.Delay(2000);

        // Handle registration logic here
        Console.WriteLine($"Registering: {model.Email}");

        isSubmitting = false;
    }

    private void Cancel()
    {
        // Navigate away or clear form
    }

    public class RegistrationModel
    {
        [Required(ErrorMessage = "Full name is required")]
        [StringLength(100, ErrorMessage = "Name must be less than 100 characters")]
        public string? FullName { get; set; }

        [Required(ErrorMessage = "Email is required")]
        [EmailAddress(ErrorMessage = "Invalid email address")]
        public string? Email { get; set; }

        [Required(ErrorMessage = "Password is required")]
        [StringLength(100, MinimumLength = 8, ErrorMessage = "Password must be at least 8 characters")]
        public string? Password { get; set; }

        [Required(ErrorMessage = "Please confirm your password")]
        [Compare(nameof(Password), ErrorMessage = "Passwords do not match")]
        public string? ConfirmPassword { get; set; }
    }
}
```

---

## 🎨 Customization

All components support custom CSS classes via the `Class` parameter, allowing you to override or extend default styles:

```razor
<!-- Override background color -->
<Button Class="bg-purple-600 hover:bg-purple-700">
    Custom Purple
</Button>

<!-- Add custom spacing -->
<Form Class="space-y-8 p-6 bg-gray-50 rounded-lg">
    <!-- Form content -->
</Form>

<!-- Custom input styling -->
<FormInput Class="border-blue-300 focus:ring-blue-500" />
```

---

## 🛠️ Advanced Examples

### Multi-Step Form with Progress

```razor
<div class="max-w-2xl mx-auto p-6">
    <div class="mb-8">
        <div class="flex justify-between mb-2">
            @for (int i = 1; i <= 3; i++)
            {
                <div class="@(currentStep >= i ? "text-zinc-900 font-medium" : "text-zinc-400")">
                    Step @i
                </div>
            }
        </div>
        <div class="h-2 bg-zinc-200 rounded-full">
            <div class="h-full bg-zinc-900 rounded-full transition-all duration-300"
                 style="width: @((currentStep / 3.0 * 100))%"></div>
        </div>
    </div>

    @if (currentStep == 1)
    {
        <Form Model="@model" OnValidSubmit="NextStep">
            <FormField Label="Personal Information">
                <FormInput @bind-Value="model.Name" placeholder="Full Name" />
            </FormField>

            <Button Type="ButtonType.Submit" RightHeroicon="arrow-right">
                Continue
            </Button>
        </Form>
    }
    else if (currentStep == 2)
    {
        <Form Model="@model" OnValidSubmit="NextStep">
            <FormField Label="Contact Details">
                <FormInput @bind-Value="model.Email" type="email" placeholder="Email" />
            </FormField>

            <div class="flex gap-3">
                <Button Variant="ButtonVariant.Outline"
                        LeftHeroicon="@HeroiconName.ArrowLeft"
                        OnClick="PreviousStep">
                    Back
                </Button>
                <Button Type="ButtonType.Submit" RightHeroicon="@HeroiconName.ArrowRight">
                    Continue
                </Button>
            </div>
        </Form>
    }
    else
    {
        <div class="text-center">
            <h2 class="text-xl font-bold mb-4">Review & Submit</h2>
            <p class="mb-6">Name: @model.Name</p>
            <p class="mb-6">Email: @model.Email</p>

            <div class="flex gap-3">
                <Button Variant="ButtonVariant.Outline" OnClick="PreviousStep">
                    Back
                </Button>
                <Button OnClick="Submit" IsLoading="@isSubmitting">
                    Submit
                </Button>
            </div>
        </div>
    }
</div>

@code {
    private int currentStep = 1;
    private bool isSubmitting = false;
    private FormModel model = new();

    private void NextStep() => currentStep++;
    private void PreviousStep() => currentStep--;

    private async Task Submit()
    {
        isSubmitting = true;
        await Task.Delay(2000);
        isSubmitting = false;
    }

    private class FormModel
    {
        public string? Name { get; set; }
        public string? Email { get; set; }
    }
}
```

### Action Bar with Mixed Buttons

```razor
<div class="flex items-center justify-between p-4 bg-white border-t">
    <div class="flex gap-2">
        <Button Variant="ButtonVariant.Ghost"
                LeftHeroicon="@HeroiconName.DocumentDuplicate">
            Duplicate
        </Button>
        <Button Variant="ButtonVariant.Ghost"
                LeftHeroicon="@HeroiconName.ArchiveBox">
            Archive
        </Button>
    </div>

    <div class="flex gap-2">
        <Button Variant="ButtonVariant.Danger"
                LeftHeroicon="@HeroiconName.Trash">
            Delete
        </Button>
        <Button LeftHeroicon="@HeroiconName.Check">
            Save Changes
        </Button>
    </div>
</div>
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🙏 Acknowledgments

- Inspired by [shadcn/ui](https://ui.shadcn.com/)
- Built with [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
- Styled with [Tailwind CSS](https://tailwindcss.com/)
- Icons by [Heroicons](https://heroicons.com/)

---

## 📞 Support

- 🐛 [Report Issues](https://github.com/Ezgaminglogan/GANBlazor-UI/issues)
- 💡 [Request Features](https://github.com/Ezgaminglogan/GANBlazor-UI/issues/new)
- 📦 [View on NuGet](https://www.nuget.org/packages/GANBlazor.UI)

---

Made with ❤️ by GAN
