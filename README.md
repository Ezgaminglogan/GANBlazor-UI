# 🎨 GANBlazor.UI

A modern, minimal Blazor UI component library inspired by **shadcn/ui**. Build beautiful, accessible web applications with pre-styled components that integrate seamlessly with **Tailwind CSS**.

[![NuGet](https://img.shields.io/nuget/v/GANBlazor.UI.svg)](https://www.nuget.org/packages/GANBlazor.UI/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**📦 Current Version:** 0.2.0  
**📋 [View Changelog](CHANGELOG.md)** | **📚 [Component Documentation](COMPONENTS.md)**

---

## ✨ Features

- 🎯 **15+ Components** - Button, Form, Card, Alert, Badge, Modal, and more
- 🎨 **Tailwind CSS** - Built with Tailwind utility classes for easy customization
- ♿ **Accessible** - ARIA-compliant components with keyboard navigation support
- 🔧 **Flexible** - Customizable variants, sizes, and classes
- 🎭 **Icons** - Blazor.Heroicons integration for beautiful icons
- 📦 **Lightweight** - Zero JavaScript dependencies (except Tailwind)
- 🚀 **Ready to Use** - Drop in and start building immediately

---

## 🎨 Component Overview

### ✅ Available Components (v0.2.0)

**Form & Input:**
- **Button** - Versatile button with 5 variants (Default, Outline, Ghost, Danger, Unstyled)
- **Form** - Form wrapper with EditContext support
- **FormField** - Field grouping with label and validation
- **FormInput** - Styled input with validation
- **FormMessage** - Validation messages

**Layout & Structure:**
- **Card** - Container with shadow and border
- **CardHeader** - Card header section
- **CardContent** - Main card content
- **CardFooter** - Card footer section

**Feedback & Status:**
- **Alert** - Contextual alerts (Success, Warning, Error, Info)
- **Badge** - Status indicators and labels (7 variants, 3 sizes)

**Overlays:**
- **Modal** - Dialog component with backdrop
- **ModalHeader** - Modal header section
- **ModalContent** - Modal content area
- **ModalFooter** - Modal footer with actions

**📚 [View Complete Component Documentation →](COMPONENTS.md)**

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

GANBlazor.UI requires Tailwind CSS v4+ in your project.

1. Install Tailwind CSS via npm:

```bash
npm install tailwindcss @tailwindcss/cli
```

2. Create your input CSS file (e.g., `wwwroot/css/input.css`):

```css
@import "tailwindcss";
```

3. Build your CSS:

```bash
npx @tailwindcss/cli -i ./wwwroot/css/input.css -o ./wwwroot/css/output.css --watch
```

4. Add both stylesheets to your `App.razor`:

```razor
<head>
    <!-- Your Tailwind CSS -->
    <link rel="stylesheet" href="css/output.css" />
    
    <!-- GANBlazor.UI Component Styles -->
    <link rel="stylesheet" href="_content/GANBlazor.UI/ganblazor-ui.min.css" />
</head>
```

**Important:** Both stylesheets are required.

### Step 3: Add Imports

Add to your `_Imports.razor`:

```razor
@using GANBlazor.UI.Components
@using GANBlazor.UI.Components.UI
@using GANBlazor.UI.Classes.UI
@using static GANBlazor.UI.Classes.UI.ButtonTypes
@using Blazor.Heroicons
```

---

## 🚀 Quick Start Examples

### Button Component

```razor
@page "/example"

<!-- Default variants -->
<Button Variant="ButtonVariant.Default">Default</Button>
<Button Variant="ButtonVariant.Outline">Outline</Button>
<Button Variant="ButtonVariant.Ghost">Ghost</Button>
<Button Variant="ButtonVariant.Danger">Delete</Button>

<!-- Custom styling with Unstyled variant -->
<Button Variant="ButtonVariant.Unstyled"
        Class="bg-purple-600 hover:bg-purple-700 text-white">
    Custom
</Button>

<!-- With icons -->
<Button Icon="check" IconType="outline">
    Save Changes
</Button>

<!-- Loading state -->
<Button Loading="@isLoading" OnClick="HandleSubmit">
    Submit
</Button>

@code {
    bool isLoading = false;
    
    async Task HandleSubmit()
    {
        isLoading = true;
        await Task.Delay(2000);
        isLoading = false;
    }
}
```

### Card Component

```razor
<Card>
    <CardHeader>
        <h3 class="text-lg font-semibold">Card Title</h3>
    </CardHeader>
    <CardContent>
        <p>This is the card content.</p>
    </CardContent>
    <CardFooter>
        <Button>Action</Button>
    </CardFooter>
</Card>
```

### Alert Component

```razor
<Alert Variant="AlertVariant.Success"
       Icon="check-circle"
       Title="Success!"
       Dismissible="true">
    Your changes have been saved.
</Alert>

<Alert Variant="AlertVariant.Error"
       Icon="exclamation-triangle"
       Title="Error">
    Something went wrong.
</Alert>
```

### Modal Component

```razor
<Button OnClick="() => showModal = true">Open Modal</Button>

<Modal @bind-IsOpen="showModal" Size="ModalSize.Large">
    <ModalHeader>
        <h3 class="text-lg font-semibold">Confirm Action</h3>
    </ModalHeader>
    <ModalContent>
        <p>Are you sure you want to proceed?</p>
    </ModalContent>
    <ModalFooter>
        <Button Variant="ButtonVariant.Ghost" OnClick="() => showModal = false">
            Cancel
        </Button>
        <Button Variant="ButtonVariant.Danger" OnClick="HandleConfirm">
            Confirm
        </Button>
    </ModalFooter>
</Modal>

@code {
    bool showModal = false;
    
    void HandleConfirm()
    {
        showModal = false;
        // Handle action
    }
}
```

### Form Component

```razor
<Form Model="@model" OnSubmit="HandleSubmit">
    <FormField Label="Email" Required="true">
        <FormInput @bind-Value="model.Email" Type="email" />
        <MessageSlot>
            <ValidationMessage For="@(() => model.Email)" />
        </MessageSlot>
    </FormField>

    <FormField Label="Password" Required="true">
        <FormInput @bind-Value="model.Password" Type="password" />
        <MessageSlot>
            <ValidationMessage For="@(() => model.Password)" />
        </MessageSlot>
    </FormField>

    <Button Type="submit">Login</Button>
</Form>

@code {
    LoginModel model = new();

    void HandleSubmit(EditContext context)
    {
        if (context.Validate())
        {
            // Process form
        }
    }

    public class LoginModel
    {
        [Required]
        [EmailAddress]
        public string Email { get; set; }

        [Required]
        public string Password { get; set; }
    }
}
```

---

## 📚 Documentation

- **[Component Documentation](COMPONENTS.md)** - Complete API reference with examples
- **[Changelog](CHANGELOG.md)** - Version history and release notes

---

## 🎨 Customization

### Using the Unstyled Variant

For complete style control, use the `Unstyled` variant:

```razor
<Button Variant="ButtonVariant.Unstyled"
        Class="bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600 text-white px-4 py-2 rounded-lg">
    Gradient Button
</Button>
```

### Overriding Component Styles

Use the `Class` parameter with Tailwind's important modifier:

```razor
<Card Class="!bg-gradient-to-br from-blue-50 to-indigo-50">
    <CardContent>Custom background</CardContent>
</Card>

<Alert Variant="AlertVariant.Info" Class="!border-2 !border-blue-500">
    Custom border
</Alert>
```

---

## 🎯 What's New in v0.2.0

**Major Component Library Expansion!**

- ✅ **4 New Component Families** - Card, Alert, Badge, Modal
- ✅ **10 New Components Total** - CardHeader, CardContent, CardFooter, ModalHeader, ModalContent, ModalFooter, and more
- ✅ **New Documentation Structure** - Separate files for changelog and component docs
- ✅ **Enhanced Customization** - More variants, sizes, and options

**[View Full Changelog →](CHANGELOG.md)**

---

## 🌟 Example: Complete Dashboard Page

```razor
@page "/dashboard"

<div class="container mx-auto p-6 space-y-6">
    <!-- Welcome Alert -->
    <Alert Variant="AlertVariant.Success"
           Icon="check-circle"
           Title="Welcome back!"
           Dismissible="true">
        You have 3 new notifications.
    </Alert>

    <!-- Stats Cards -->
    <div class="grid md:grid-cols-3 gap-4">
        <Card>
            <CardHeader>
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold">Total Users</h3>
                    <Badge Variant="BadgeVariant.Success">+12%</Badge>
                </div>
            </CardHeader>
            <CardContent>
                <p class="text-3xl font-bold">1,234</p>
            </CardContent>
        </Card>

        <Card>
            <CardHeader>
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold">Revenue</h3>
                    <Badge Variant="BadgeVariant.Primary">+8%</Badge>
                </div>
            </CardHeader>
            <CardContent>
                <p class="text-3xl font-bold">$45,231</p>
            </CardContent>
        </Card>

        <Card>
            <CardHeader>
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold">Active Projects</h3>
                    <Badge Variant="BadgeVariant.Warning">3</Badge>
                </div>
            </CardHeader>
            <CardContent>
                <p class="text-3xl font-bold">12</p>
            </CardContent>
        </Card>
    </div>

    <!-- Action Card -->
    <Card>
        <CardHeader>
            <h3 class="text-lg font-semibold">Recent Activity</h3>
        </CardHeader>
        <CardContent>
            <div class="space-y-2">
                <div class="flex justify-between items-center">
                    <span>New user registration</span>
                    <Badge Variant="BadgeVariant.Info" Size="BadgeSize.Small">2m ago</Badge>
                </div>
                <div class="flex justify-between items-center">
                    <span>Payment received</span>
                    <Badge Variant="BadgeVariant.Success" Size="BadgeSize.Small">1h ago</Badge>
                </div>
            </div>
        </CardContent>
        <CardFooter>
            <Button OnClick="() => showDetailsModal = true">
                View All Activity
            </Button>
        </CardFooter>
    </Card>
</div>

<!-- Details Modal -->
<Modal @bind-IsOpen="showDetailsModal" Size="ModalSize.Large">
    <ModalHeader>
        <h3 class="text-lg font-semibold">Activity Details</h3>
    </ModalHeader>
    <ModalContent>
        <p>Detailed activity information goes here...</p>
    </ModalContent>
    <ModalFooter>
        <Button Variant="ButtonVariant.Ghost" OnClick="() => showDetailsModal = false">
            Close
        </Button>
    </ModalFooter>
</Modal>

@code {
    bool showDetailsModal = false;
}
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📄 License

This project is licensed under the MIT License.

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
- 📚 [Component Docs](COMPONENTS.md)
- 📋 [Changelog](CHANGELOG.md)

---

Made with ❤️ by GAN
