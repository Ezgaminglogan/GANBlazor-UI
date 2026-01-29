# 📋 Changelog

All notable changes to GANBlazor.UI will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.3.0] - 2026-01-28

### ✨ Added - New Interactive Components

**New Components:**

- **Switch Component:**
  - Toggle switch for boolean values
  - Two-way binding support (`@bind-Value`)
  - Disabled state
  - Smooth transition animations
  - Full accessibility with `role="switch"` and `aria-checked`

- **Spinner Component:**
  - Loading indicator with SVG animation
  - 4 size variants (Sm, Md, Lg, Xl)
  - Optional text label
  - Customizable via Class parameter

- **Tabs Components:**
  - `Tabs` - Container with state management
  - `TabList` - Tab button container
  - `Tab` - Individual tab buttons
  - `TabPanel` - Tab content panels
  - 3 variants (Underline, Pills, Boxed)
  - Keyboard accessibility with proper ARIA roles

- **Toast Components:**
  - `Toast` - Individual notification message
  - `ToastContainer` - Position manager for multiple toasts
  - 4 variants (Success, Warning, Error, Info)
  - 6 position options
  - Icon support with Heroicons

- **Tooltip Component:**
  - Hover tooltips with configurable delay
  - 4 positions (Top, Bottom, Left, Right)
  - Auto-positioning with arrows
  - Keyboard accessible (focus/blur events)

- **Avatar Component:**
  - User profile image display
  - Initials fallback (auto-generated from name)
  - Placeholder icon fallback
  - 5 size variants (Xs, Sm, Md, Lg, Xl)
  - Status indicators (Online, Offline, Away, Busy)
  - Rounded or square shape option
  - Image error handling

### 🔧 Enhanced

- **FormInput:** Added left and right icon support with Heroicons
- **Modal:** Added close button (top-right X icon)
- **Modal:** Added Escape key to close functionality

### 🗑️ Removed

- Cleaned up unused temporary files

### 📝 Documentation

- Added documentation for all new components
- Updated Table of Contents in COMPONENTS.md

---

## [0.2.1] - 2026-01-28

### 🐛 Fixed

- Fixed component packaging issue where .razor files were not included in NuGet package
- Removed `EnableDefaultContentItems` setting that was preventing components from being packaged
- Added proper static usage imports to all component files

---

## [0.2.0] - 2026-01-28

### ✨ Added - Major Component Library Expansion

**New Components:**

- **Card Components:**
  - `Card` - Container component with shadow, border, and hover effects
  - `CardHeader` - Card header section with bottom border
  - `CardContent` - Main card content area
  - `CardFooter` - Card footer section with gray background

- **Alert Component:**
  - Full-featured alert with 4 variants (Success, Warning, Error, Info)
  - Icon support with Heroicons integration
  - Optional title
  - Dismissible with close button
  - Event callback support

- **Badge Component:**
  - Inline status indicators
  - 7 variants (Default, Primary, Success, Warning, Error, Info, Outline)
  - 3 sizes (Small, Medium, Large)

- **Modal Components:**
  - `Modal` - Full-screen dialog with backdrop
  - `ModalHeader` - Modal header section
  - `ModalContent` - Modal body content
  - `ModalFooter` - Modal footer with action buttons
  - 5 size options (Small, Medium, Large, ExtraLarge, Full)
  - Backdrop blur effect
  - Close on backdrop click option
  - Smooth animations

**New Enums:**

- `AlertVariant` - Success, Warning, Error, Info
- `BadgeVariant` - Default, Primary, Success, Warning, Error, Info, Outline
- `BadgeSize` - Small, Medium, Large
- `ModalSize` - Small, Medium, Large, ExtraLarge, Full

**Documentation:**

- 📝 Created `COMPONENTS.md` - Detailed component API reference
- 📋 Created `CHANGELOG.md` - Version history (this file)
- ✨ Simplified `README.md` - Overview and quick start only

---

## [0.1.8] - 2026-01-28

### ✨ Added - Unstyled Variant & Better Class Override

**New Features:**

- `ButtonVariant.Unstyled` - New variant with no color styling for full customization
- Better `Class` parameter control - Override button styles easily
- Documentation for custom button styling patterns

**Usage Example:**

```razor
<!-- Unstyled variant with custom colors -->
<Button Variant="ButtonVariant.Unstyled"
        Class="bg-blue-900 hover:bg-blue-800 text-white">
    Custom Button
</Button>

<!-- Or use Tailwind important modifier -->
<Button Class="!bg-blue-900">Override Default</Button>
```

**Why This Change:**

Previously, the `Class` parameter couldn't override variant colors due to CSS specificity. Now you can use `Unstyled` variant for complete control, or use Tailwind's `!` modifier to override specific properties.

---

## [0.1.7] - 2026-01-27

### 🎯 Fixed - Package Cleanup (Final Fix)

**Changes:**

- Disabled automatic content file inclusion (`IncludeContentInPack`)
- Explicitly controlled package contents
- Removed ALL development files from package (npm, node_modules, build artifacts)
- Package now contains ONLY essential runtime files

**What's Included:**

- Compiled component library (`.dll`)
- Pre-built CSS (`ganblazor-ui.min.css`)
- Documentation (`README.md`)
- Package icon (`icon.png`)
- Build targets for setup instructions

**What's Excluded:**

- `package.json` and `package-lock.json`
- `node_modules/` directory
- Source CSS files
- Build artifacts (`bin/`, `obj/`)

**Impact:**

- Clean installation with no unwanted files
- No more npm dependency warnings
- Smaller package size

---

## [0.1.6] - 2026-01-27

### 🐛 Fixed - Critical Package Issue

**Changes:**

- Removed `package.json` and `package-lock.json` from NuGet package
- These npm files were incorrectly being copied to consuming projects

**Impact:**

- Projects installing GANBlazor.UI will no longer get unwanted npm files
- Cleaner project structure in consuming applications

---

## [0.1.5] - 2026-01-27

### 🐛 Fixed - Bug Fix Release

**Changes:**

- Removed `node_modules` from NuGet package (caused CS2015 binary file errors)
- Excluded build artifacts (`bin/`, `obj/`)
- Package now only contains essential files

**What's Included:**

- Compiled component library (`.dll`)
- Pre-built CSS (`ganblazor-ui.min.css`)
- Documentation (`README.md`)
- Package icon
- Build targets for setup instructions

---

## [0.1.4] - 2026-01-27

### ⚠️ Breaking Change - Simplified FormField Syntax

**Changes:**

- `Message` parameter renamed to `MessageSlot` in FormField component
- **No more `<ChildContent>` wrappers required!**
- Much cleaner, more intuitive syntax

**Migration Guide:**

```razor
<!-- ❌ OLD (0.1.3 and earlier) - Required ChildContent wrapper -->
<FormField Label="Email">
    <ChildContent>
        <FormInput @bind-Value="model.Email" />
    </ChildContent>
    <Message>
        <ValidationMessage For="@(() => model.Email)" />
    </Message>
</FormField>

<!-- ✅ NEW (0.1.4) - Clean and simple! -->
<FormField Label="Email">
    <FormInput @bind-Value="model.Email" />
    <MessageSlot>
        <ValidationMessage For="@(() => model.Email)" />
    </MessageSlot>
</FormField>
```

**Why This Change:**

Blazor requires explicit `<ChildContent>` wrappers when a component has a parameter named `Message`. By renaming to `MessageSlot`, we keep `ChildContent` as the only implicit parameter, making the syntax much cleaner!

---

## [0.1.3] - 2026-01-27

### ✨ Improved - Better Developer Experience

**Changes:**

- Added automatic setup instructions on first build
- Build message displays all required `@using` statements
- Shows CSS link setup for `App.razor`
- Improved developer onboarding experience

**What You'll See:**

After installing the package, the first build will show helpful setup instructions with all required imports and CSS links.

---

## [0.1.2] - 2026-01-27

### ✨ Added - Pre-built CSS Bundle

**Changes:**

- Added pre-built CSS bundle (`ganblazor-ui.min.css`) for component styles
- Fixed Tailwind CSS styling issues with compiled components
- Improved package distribution with bundled styles
- Updated documentation with proper CSS setup instructions

**Migration from 0.1.1:**

Add the component stylesheet to your `App.razor`:

```razor
<link rel="stylesheet" href="_content/GANBlazor.UI/ganblazor-ui.min.css" />
```

---

## [0.1.1] - 2026-01-27

### ✨ Improved - Package Presentation

**Changes:**

- Added package icon (GANBlazor logo)
- Improved NuGet package presentation

---

## [0.1.0] - 2026-01-26

### 🎉 Initial Release

**Components:**

- Button component with 4 variants (Default, Outline, Ghost, Danger)
- Form wrapper component
- FormField component with label and message support
- FormInput component with validation
- FormMessage component for error display

**Features:**

- Full Tailwind CSS integration
- Heroicons support for button icons
- Loading states and animations
- ARIA-compliant and accessible components

---

## Legend

- ✨ **Added** - New features
- 🔄 **Changed** - Changes in existing functionality
- 🐛 **Fixed** - Bug fixes
- ⚠️ **Breaking** - Breaking changes
- 🗑️ **Deprecated** - Soon-to-be removed features
- ❌ **Removed** - Removed features
- 🔒 **Security** - Security fixes

---

[0.2.0]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.2.0
[0.1.8]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.8
[0.1.7]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.7
[0.1.6]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.6
[0.1.5]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.5
[0.1.4]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.4
[0.1.3]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.3
[0.1.2]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.2
[0.1.1]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.1
[0.1.0]: https://github.com/Ezgaminglogan/GANBlazor-UI/releases/tag/v0.1.0
