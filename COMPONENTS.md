# 📚 Component Documentation

Complete API reference for all GANBlazor.UI components.

---

## Table of Contents

- [Button](#button)
- [Form Components](#form-components)
  - [Form](#form)
  - [FormField](#formfield)
  - [FormInput](#forminput)
  - [FormMessage](#formmessage)
- [Card Components](#card-components)
  - [Card](#card)
  - [CardHeader](#cardheader)
  - [CardContent](#cardcontent)
  - [CardFooter](#cardfooter)
- [Alert](#alert)
- [Badge](#badge)
- [Modal Components](#modal-components)
  - [Modal](#modal)
  - [ModalHeader](#modalheader)
  - [ModalContent](#modalcontent)
  - [ModalFooter](#modalfooter)

---

## Button

A versatile button component with multiple variants, icon support, and loading states.

### Import

```razor
@using GANBlazor.UI.Components.UI
```

### Basic Usage

```razor
<Button>Click me</Button>
```

### Parameters

| Parameter      | Type                            | Default     | Description                               |
| -------------- | ------------------------------- | ----------- | ----------------------------------------- |
| `ChildContent` | `RenderFragment?`               | `null`      | Button content (text or HTML)             |
| `Variant`      | `ButtonVariant`                 | `Default`   | Visual style variant                      |
| `Type`         | `string?`                       | `"button"`  | HTML button type attribute                |
| `OnClick`      | `EventCallback<MouseEventArgs>` | -           | Click event handler                       |
| `Disabled`     | `bool`                          | `false`     | Whether button is disabled                |
| `Loading`      | `bool`                          | `false`     | Shows loading spinner and disables button |
| `Icon`         | `string?`                       | `null`      | Heroicon name to display                  |
| `IconType`     | `string?`                       | `"outline"` | Icon style (`outline` or `solid`)         |
| `IconPosition` | `string?`                       | `"left"`    | Icon position (`left` or `right`)         |
| `Class`        | `string?`                       | `null`      | Additional CSS classes                    |

### Variants

```csharp
public enum ButtonVariant
{
    Default,  // Solid blue background
    Outline,  // Border with transparent background
    Ghost,    // Subtle hover effect
    Danger,   // Red for destructive actions
    Unstyled  // No default styling (v0.1.8+)
}
```

### Examples

#### Variant Examples

```razor
<Button Variant="ButtonVariant.Default">Default</Button>
<Button Variant="ButtonVariant.Outline">Outline</Button>
<Button Variant="ButtonVariant.Ghost">Ghost</Button>
<Button Variant="ButtonVariant.Danger">Delete</Button>
<Button Variant="ButtonVariant.Unstyled" Class="bg-purple-600 hover:bg-purple-700 text-white">
    Custom
</Button>
```

#### With Icons

```razor
<Button Icon="check" IconType="outline">
    Save Changes
</Button>

<Button Icon="trash" IconType="solid" IconPosition="right" Variant="ButtonVariant.Danger">
    Delete
</Button>
```

#### Loading State

```razor
<Button Loading="@isSubmitting" OnClick="HandleSubmit">
    Submit Form
</Button>

@code {
    bool isSubmitting = false;

    async Task HandleSubmit()
    {
        isSubmitting = true;
        await Task.Delay(2000); // Simulate API call
        isSubmitting = false;
    }
}
```

#### Custom Styling

```razor
<!-- Using Unstyled variant (recommended) -->
<Button Variant="ButtonVariant.Unstyled"
        Class="bg-gradient-to-r from-purple-600 to-blue-600 hover:from-purple-700 hover:to-blue-700 text-white px-6 py-3 rounded-lg">
    Custom Gradient
</Button>

<!-- Using important modifier -->
<Button Class="!bg-green-600 !hover:bg-green-700">
    Override Variant
</Button>
```

---

## Form Components

### Form

A wrapper component for form elements with EditContext support.

#### Import

```razor
@using GANBlazor.UI.Components.UI
```

#### Parameters

| Parameter      | Type                         | Default | Description             |
| -------------- | ---------------------------- | ------- | ----------------------- |
| `ChildContent` | `RenderFragment?`            | `null`  | Form content            |
| `OnSubmit`     | `EventCallback<EditContext>` | -       | Form submission handler |
| `Model`        | `object?`                    | `null`  | Form model object       |
| `Class`        | `string?`                    | `null`  | Additional CSS classes  |

#### Example

```razor
<Form Model="@loginModel" OnSubmit="HandleLogin" Class="space-y-4">
    <FormField Label="Email">
        <FormInput @bind-Value="loginModel.Email" Type="email" />
        <MessageSlot>
            <ValidationMessage For="@(() => loginModel.Email)" />
        </MessageSlot>
    </FormField>

    <Button Type="submit">Login</Button>
</Form>

@code {
    LoginModel loginModel = new();

    void HandleLogin(EditContext context)
    {
        if (context.Validate())
        {
            // Process login
        }
    }
}
```

---

### FormField

Groups a label, input, and validation message together.

#### Parameters

| Parameter      | Type              | Default | Description                   |
| -------------- | ----------------- | ------- | ----------------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Field content (input)         |
| `MessageSlot`  | `RenderFragment?` | `null`  | Validation message content    |
| `Label`        | `string?`         | `null`  | Field label text              |
| `Required`     | `bool`            | `false` | Shows required indicator (\*) |
| `Class`        | `string?`         | `null`  | Additional CSS classes        |

#### Example

```razor
<FormField Label="Username" Required="true">
    <FormInput @bind-Value="model.Username" />
    <MessageSlot>
        <ValidationMessage For="@(() => model.Username)" />
    </MessageSlot>
</FormField>
```

---

### FormInput

A styled input component with validation support.

#### Parameters

| Parameter         | Type                        | Default  | Description               |
| ----------------- | --------------------------- | -------- | ------------------------- |
| `Value`           | `string?`                   | `null`   | Input value               |
| `ValueChanged`    | `EventCallback<string>`     | -        | Value change event        |
| `Type`            | `string?`                   | `"text"` | HTML input type           |
| `Placeholder`     | `string?`                   | `null`   | Placeholder text          |
| `Disabled`        | `bool`                      | `false`  | Whether input is disabled |
| `ValueExpression` | `Expression<Func<string>>?` | `null`   | Expression for validation |
| `Class`           | `string?`                   | `null`   | Additional CSS classes    |

#### Example

```razor
<FormInput @bind-Value="model.Email"
           Type="email"
           Placeholder="Enter your email"
           Class="w-full" />
```

---

### FormMessage

Displays validation or informational messages.

#### Parameters

| Parameter      | Type              | Default   | Description                                          |
| -------------- | ----------------- | --------- | ---------------------------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`    | Message content                                      |
| `Type`         | `string?`         | `"error"` | Message type (`error`, `info`, `success`, `warning`) |
| `Class`        | `string?`         | `null`    | Additional CSS classes                               |

#### Example

```razor
<FormMessage Type="error">
    This field is required
</FormMessage>

<FormMessage Type="info">
    Password must be at least 8 characters
</FormMessage>
```

---

## Card Components

### Card

A container component for grouping related content.

#### Import

```razor
@using GANBlazor.UI.Components.UI
```

#### Parameters

| Parameter      | Type              | Default | Description                |
| -------------- | ----------------- | ------- | -------------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Card content               |
| `Class`        | `string?`         | `null`  | Additional CSS classes     |
| `Hover`        | `bool`            | `true`  | Enable hover shadow effect |

#### Example

```razor
<Card>
    <CardHeader>
        <h3 class="text-lg font-semibold">Card Title</h3>
    </CardHeader>
    <CardContent>
        <p>This is the card content. You can put any content here.</p>
    </CardContent>
    <CardFooter>
        <Button>Action</Button>
    </CardFooter>
</Card>
```

---

### CardHeader

Header section of a card with bottom border.

#### Parameters

| Parameter      | Type              | Default   | Description                       |
| -------------- | ----------------- | --------- | --------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`    | Header content                    |
| `Icon`         | `string?`         | `null`    | Heroicon name to display          |
| `IconType`     | `HeroiconType`    | `Outline` | Icon style (`Outline` or `Solid`) |
| `Class`        | `string?`         | `null`    | Additional CSS classes            |

#### Examples

**Basic Header:**

```razor
<CardHeader>
    <h3 class="text-lg font-semibold">Product Details</h3>
    <p class="text-sm text-gray-600">View and manage product information</p>
</CardHeader>
```

**With Icon:**

```razor
<CardHeader Icon="user" IconType="HeroiconType.Solid">
    <h3 class="text-lg font-semibold">User Profile</h3>
</CardHeader>

<CardHeader Icon="shopping-cart">
    <h3 class="text-lg font-semibold">Shopping Cart</h3>
</CardHeader>
```

---

### CardContent

Main content area of a card.

#### Parameters

| Parameter      | Type              | Default | Description            |
| -------------- | ----------------- | ------- | ---------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Content                |
| `Class`        | `string?`         | `null`  | Additional CSS classes |

#### Example

```razor
<CardContent>
    <div class="space-y-4">
        <div>
            <label class="font-medium">Name:</label>
            <p>Product Name</p>
        </div>
        <div>
            <label class="font-medium">Price:</label>
            <p>$99.99</p>
        </div>
    </div>
</CardContent>
```

---

### CardFooter

Footer section of a card with gray background.

#### Parameters

| Parameter      | Type              | Default | Description            |
| -------------- | ----------------- | ------- | ---------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Footer content         |
| `Class`        | `string?`         | `null`  | Additional CSS classes |

#### Example

```razor
<CardFooter>
    <div class="flex justify-end space-x-2">
        <Button Variant="ButtonVariant.Ghost">Cancel</Button>
        <Button>Save Changes</Button>
    </div>
</CardFooter>
```

---

## Alert

Displays important messages with context-appropriate styling.

### Import

```razor
@using GANBlazor.UI.Components.UI
```

### Parameters

| Parameter      | Type              | Default     | Description                       |
| -------------- | ----------------- | ----------- | --------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`      | Alert content                     |
| `Title`        | `string?`         | `null`      | Alert title                       |
| `Variant`      | `AlertVariant`    | `Success`   | Alert style variant               |
| `Icon`         | `string?`         | `null`      | Heroicon name to display          |
| `IconType`     | `string?`         | `"outline"` | Icon style (`outline` or `solid`) |
| `Dismissible`  | `bool`            | `false`     | Show close button                 |
| `OnDismiss`    | `EventCallback`   | -           | Dismiss event handler             |
| `Class`        | `string?`         | `null`      | Additional CSS classes            |

### Variants

```csharp
public enum AlertVariant
{
    Success,  // Green - successful operations
    Warning,  // Yellow - warnings
    Error,    // Red - errors
    Info      // Blue - informational messages
}
```

### Examples

#### Basic Alerts

```razor
<Alert Variant="AlertVariant.Success" Title="Success!">
    Your changes have been saved successfully.
</Alert>

<Alert Variant="AlertVariant.Warning" Title="Warning">
    This action cannot be undone.
</Alert>

<Alert Variant="AlertVariant.Error" Title="Error">
    Failed to save changes. Please try again.
</Alert>

<Alert Variant="AlertVariant.Info" Title="Information">
    Your account will be upgraded in 24 hours.
</Alert>
```

#### With Icons

```razor
<Alert Variant="AlertVariant.Success"
       Icon="check-circle"
       IconType="solid"
       Title="Payment Successful">
    Your payment has been processed.
</Alert>

<Alert Variant="AlertVariant.Error"
       Icon="exclamation-triangle"
       IconType="solid"
       Title="Validation Error">
    Please correct the errors in the form.
</Alert>
```

#### Dismissible

```razor
<Alert Variant="AlertVariant.Info"
       Title="New Feature Available"
       Dismissible="true"
       OnDismiss="HandleAlertDismiss">
    Check out our new dashboard feature!
</Alert>

@code {
    void HandleAlertDismiss()
    {
        // Handle alert dismissal
        Console.WriteLine("Alert dismissed");
    }
}
```

#### Without Title

```razor
<Alert Variant="AlertVariant.Success" Icon="check">
    Operation completed successfully!
</Alert>
```

---

## Badge

Small status indicators and labels.

### Import

```razor
@using GANBlazor.UI.Components.UI
```

### Parameters

| Parameter      | Type              | Default   | Description                       |
| -------------- | ----------------- | --------- | --------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`    | Badge content                     |
| `Variant`      | `BadgeVariant`    | `Default` | Badge style variant               |
| `Size`         | `BadgeSize`       | `Medium`  | Badge size                        |
| `Icon`         | `string?`         | `null`    | Heroicon name to display          |
| `IconType`     | `HeroiconType`    | `Solid`   | Icon style (`Outline` or `Solid`) |
| `Class`        | `string?`         | `null`    | Additional CSS classes            |

### Variants

```csharp
public enum BadgeVariant
{
    Default,  // Gray
    Primary,  // Blue
    Success,  // Green
    Warning,  // Yellow
    Error,    // Red
    Info,     // Light blue
    Outline   // Border only
}

public enum BadgeSize
{
    Small,   // Compact
    Medium,  // Default
    Large    // Prominent
}
```

### Examples

#### Variant Examples

```razor
<Badge Variant="BadgeVariant.Default">Default</Badge>
<Badge Variant="BadgeVariant.Primary">Primary</Badge>
<Badge Variant="BadgeVariant.Success">Active</Badge>
<Badge Variant="BadgeVariant.Warning">Pending</Badge>
<Badge Variant="BadgeVariant.Error">Error</Badge>
<Badge Variant="BadgeVariant.Info">Info</Badge>
<Badge Variant="BadgeVariant.Outline">Outline</Badge>
```

#### Size Examples

```razor
<Badge Size="BadgeSize.Small">Small</Badge>
<Badge Size="BadgeSize.Medium">Medium</Badge>
<Badge Size="BadgeSize.Large">Large</Badge>
```

#### With Icons

```razor
<!-- Badge with icon -->
<Badge Icon="check" Variant="BadgeVariant.Success">Active</Badge>
<Badge Icon="clock" Variant="BadgeVariant.Warning">Pending</Badge>
<Badge Icon="x-mark" Variant="BadgeVariant.Error">Failed</Badge>

<!-- Different icon types -->
<Badge Icon="star" IconType="HeroiconType.Solid" Variant="BadgeVariant.Primary">
    Featured
</Badge>

<!-- Icon scales with size -->
<Badge Icon="bell" Size="BadgeSize.Small">3</Badge>
<Badge Icon="envelope" Size="BadgeSize.Large">New</Badge>
```

#### Status Indicators

```razor
<div class="flex items-center space-x-2">
    <span>Order Status:</span>
    <Badge Variant="BadgeVariant.Success">Delivered</Badge>
</div>

<div class="flex items-center space-x-2">
    <span>User Role:</span>
    <Badge Variant="BadgeVariant.Primary" Size="BadgeSize.Small">Admin</Badge>
</div>
```

#### In Lists

```razor
<div class="space-y-2">
    <div class="flex justify-between items-center">
        <span>Feature Request #123</span>
        <Badge Variant="BadgeVariant.Warning">Pending</Badge>
    </div>
    <div class="flex justify-between items-center">
        <span>Bug Report #456</span>
        <Badge Variant="BadgeVariant.Error">Critical</Badge>
    </div>
    <div class="flex justify-between items-center">
        <span>Enhancement #789</span>
        <Badge Variant="BadgeVariant.Success">Completed</Badge>
    </div>
</div>
```

---

## Modal Components

### Modal

A dialog overlay for important interactions.

#### Import

```razor
@using GANBlazor.UI.Components.UI
```

#### Parameters

| Parameter              | Type                  | Default  | Description                  |
| ---------------------- | --------------------- | -------- | ---------------------------- |
| `ChildContent`         | `RenderFragment?`     | `null`   | Modal content                |
| `IsOpen`               | `bool`                | `false`  | Whether modal is visible     |
| `IsOpenChanged`        | `EventCallback<bool>` | -        | IsOpen change event          |
| `OnClose`              | `EventCallback`       | -        | Close event handler          |
| `Size`                 | `ModalSize`           | `Medium` | Modal size                   |
| `CloseOnBackdropClick` | `bool`                | `true`   | Close when clicking backdrop |
| `Class`                | `string?`             | `null`   | Additional CSS classes       |

#### Sizes

```csharp
public enum ModalSize
{
    Small,       // max-w-sm
    Medium,      // max-w-lg (default)
    Large,       // max-w-2xl
    ExtraLarge,  // max-w-4xl
    Full         // max-w-7xl
}
```

#### Example

```razor
<Button OnClick="() => showModal = true">Open Modal</Button>

<Modal @bind-IsOpen="showModal" Size="ModalSize.Large">
    <ModalHeader>
        <h3 class="text-lg font-semibold">Confirm Action</h3>
    </ModalHeader>
    <ModalContent>
        <p>Are you sure you want to proceed with this action?</p>
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
        // Process action
        showModal = false;
    }
}
```

---

### ModalHeader

Header section of a modal.

#### Parameters

| Parameter      | Type              | Default   | Description                       |
| -------------- | ----------------- | --------- | --------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`    | Header content                    |
| `Icon`         | `string?`         | `null`    | Heroicon name to display          |
| `IconType`     | `HeroiconType`    | `Outline` | Icon style (`Outline` or `Solid`) |
| `Class`        | `string?`         | `null`    | Additional CSS classes            |

#### Examples

**Basic Header:**

```razor
<ModalHeader>
    <h3 class="text-lg font-semibold">Confirm Action</h3>
</ModalHeader>
```

**With Icon:**

```razor
<ModalHeader Icon="exclamation-triangle" IconType="HeroiconType.Solid">
    Warning
</ModalHeader>

<ModalHeader Icon="information-circle">
    Important Information
</ModalHeader>

<ModalHeader Icon="trash" IconType="HeroiconType.Solid">
    Delete Confirmation
</ModalHeader>
```

---

### ModalContent

Main content area of a modal.

#### Parameters

| Parameter      | Type              | Default | Description            |
| -------------- | ----------------- | ------- | ---------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Content                |
| `Class`        | `string?`         | `null`  | Additional CSS classes |

#### Example

```razor
<ModalContent>
    <div class="space-y-4">
        <p>This action will permanently delete your account.</p>
        <p class="text-sm text-gray-600">
            This cannot be undone. All your data will be lost.
        </p>
    </div>
</ModalContent>
```

---

### ModalFooter

Footer section of a modal, typically for action buttons.

#### Parameters

| Parameter      | Type              | Default | Description            |
| -------------- | ----------------- | ------- | ---------------------- |
| `ChildContent` | `RenderFragment?` | `null`  | Footer content         |
| `Class`        | `string?`         | `null`  | Additional CSS classes |

#### Example

```razor
<ModalFooter>
    <div class="flex justify-end space-x-2">
        <Button Variant="ButtonVariant.Ghost" OnClick="Cancel">
            Cancel
        </Button>
        <Button Variant="ButtonVariant.Danger" OnClick="Delete" Loading="@isDeleting">
            Delete Account
        </Button>
    </div>
</ModalFooter>
```

---

## Complete Example

Here's a complete example using multiple components together:

```razor
@page "/dashboard"
@using GANBlazor.UI.Components.UI

<div class="container mx-auto p-6 space-y-6">
    <!-- Alert -->
    <Alert Variant="AlertVariant.Success"
           Icon="check-circle"
           Title="Welcome back!"
           Dismissible="true">
        You have 3 new notifications.
    </Alert>

    <!-- Cards with Badges -->
    <div class="grid md:grid-cols-2 gap-4">
        <Card>
            <CardHeader>
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold">Project Status</h3>
                    <Badge Variant="BadgeVariant.Success">Active</Badge>
                </div>
            </CardHeader>
            <CardContent>
                <p>Your project is running smoothly.</p>
            </CardContent>
            <CardFooter>
                <Button OnClick="() => showDetailsModal = true">
                    View Details
                </Button>
            </CardFooter>
        </Card>

        <Card>
            <CardHeader>
                <div class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold">Team Members</h3>
                    <Badge Variant="BadgeVariant.Primary" Size="BadgeSize.Small">5</Badge>
                </div>
            </CardHeader>
            <CardContent>
                <p>Manage your team members and permissions.</p>
            </CardContent>
            <CardFooter>
                <Button Variant="ButtonVariant.Outline">
                    Manage Team
                </Button>
            </CardFooter>
        </Card>
    </div>

    <!-- Modal -->
    <Modal @bind-IsOpen="showDetailsModal" Size="ModalSize.Large">
        <ModalHeader>
            <h3 class="text-lg font-semibold">Project Details</h3>
        </ModalHeader>
        <ModalContent>
            <div class="space-y-4">
                <div>
                    <label class="font-medium">Status:</label>
                    <Badge Variant="BadgeVariant.Success">Active</Badge>
                </div>
                <div>
                    <label class="font-medium">Created:</label>
                    <p>January 28, 2026</p>
                </div>
            </div>
        </ModalContent>
        <ModalFooter>
            <Button Variant="ButtonVariant.Ghost" OnClick="() => showDetailsModal = false">
                Close
            </Button>
        </ModalFooter>
    </Modal>
</div>

@code {
    bool showDetailsModal = false;
}
```

---

## Styling Tips

### Custom Colors with Unstyled Variant

```razor
<Button Variant="ButtonVariant.Unstyled"
        Class="bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600 text-white px-4 py-2 rounded-lg">
    Gradient Button
</Button>
```

### Overriding Default Styles

```razor
<!-- Card with custom background -->
<Card Class="bg-gradient-to-br from-blue-50 to-indigo-50">
    <CardContent>Custom gradient background</CardContent>
</Card>

<!-- Alert with custom border -->
<Alert Variant="AlertVariant.Info" Class="!border-2 !border-blue-500">
    Custom border alert
</Alert>
```

### Responsive Design

```razor
<!-- Responsive grid of cards -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <Card><!-- Card 1 --></Card>
    <Card><!-- Card 2 --></Card>
    <Card><!-- Card 3 --></Card>
</div>

<!-- Responsive modal -->
<Modal Size="ModalSize.Large" Class="sm:max-w-full lg:max-w-4xl">
    <!-- Content -->
</Modal>
```

---

## Accessibility

All components are built with accessibility in mind:

- **Semantic HTML**: Proper use of `<button>`, `<form>`, `<label>`, etc.
- **ARIA Attributes**: Appropriate `aria-*` attributes for screen readers
- **Keyboard Navigation**: Full keyboard support with Tab, Enter, and Escape keys
- **Focus Management**: Visible focus indicators and logical focus order
- **Color Contrast**: WCAG AA compliant color combinations

---

## Browser Support

GANBlazor.UI supports all modern browsers:

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

---

## Need Help?

- 🐛 [Report Issues](https://github.com/Ezgaminglogan/GANBlazor-UI/issues)
- 💡 [Request Features](https://github.com/Ezgaminglogan/GANBlazor-UI/issues/new)
- 📦 [View on NuGet](https://www.nuget.org/packages/GANBlazor.UI)
- 📖 [Back to README](README.md)
- 📋 [View Changelog](CHANGELOG.md)

---

Made with ❤️ by GAN
