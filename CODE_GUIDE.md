# Website Code Guide

## Introduction

This guide provides an overview of the `index.html` file for this portfolio website. It explains how the content is structured and managed, enabling easier updates and maintenance. The entire website (HTML, CSS, and JavaScript) is contained within `index.html`.

## File Structure

-   **`index.html`**: The single source file for the website.
    -   **HTML**: Defines the basic page structure, navigation, content container, and footer.
    -   **CSS**: Embedded within `<style>` tags in the `<head>`. It controls the visual appearance and is organized by components/sections.
    -   **JavaScript**: Embedded within `<script>` tags at the end of the `<body>`. It handles dynamic content generation, interactivity, and feature implementation.

## Content Configuration (`CONFIG` object)

The primary way to update the website's content is by modifying the `CONFIG` JavaScript object found within the `<script>` tags in `index.html`.

```javascript
const CONFIG = {
    personal: { /* ... */ },
    about: { /* ... */ },
    skills: { /* ... */ },
    experience: [ /* ... */ ],
    projects: [ /* ... */ ]
};
```

### 1. `personal`
   - Contains your personal information.
   - **Fields:**
     - `name`: Your name (e.g., "Nilay").
     - `title`: Your professional title (e.g., "Senior Python Developer & Full-Stack Engineer").
     - `email`: Your contact email.
     - `phone`: Your phone number.
     - `location`: Your general location (e.g., "Chicago, Illinois").
     - `linkedin`: Full URL to your LinkedIn profile.
     - `github`: Full URL to your GitHub profile.
     - `description`: A short bio for the hero section.
   - **To Update:** Directly edit the string values for these fields.

### 2. `about`
   - Contains the paragraphs for the "About Me" section.
   - **Field:**
     - `text`: An array of strings. Each string is a paragraph.
   - **To Update:** Add, remove, or modify the strings in the `text` array.

### 3. `skills`
   - Organizes your skills into categories.
   - **Structure:** An object where each key is a skill category (e.g., "Programming Languages") and its value is an array of skill strings (e.g., `["Python", "JavaScript"]`).
   - **To Update:**
     - To add a new category: Add a new key-value pair.
     - To add a skill: Add the skill string to the appropriate category's array.
     - The icon next to the skill category is determined by the `getSkillIcon(category)` function. You might need to update this function if adding new categories that need specific icons.

### 4. `experience`
   - An array of objects, where each object represents a job experience.
   - **Fields per job object:**
     - `title`: Job title (e.g., "Senior Python Developer").
     - `company`: Company name (e.g., "Bank of America (GIS)").
     - `duration`: Employment duration (e.g., "February 2024 – May 2025").
     - `achievements`: An array of strings, each being a key achievement or responsibility.
   - **To Update:** Add new job objects to the array or modify existing ones. Ensure achievements are listed as strings in the `achievements` array.

### 5. `projects`
   - An array of objects, where each object represents a project.
   - **Fields per project object:**
     - `title`: Project title.
     - `subtitle`: A brief subtitle or context for the project.
     - `description`: Detailed project description.
     - `technologies`: An array of strings listing technologies used.
     - `github`: (This property was previously used for GitHub links but is currently not rendered on the site. You can still store the URL here for your reference if desired).
     - `demo`: URL to a live demo if available. Set to `null` or an empty string if no demo.
   - **To Update:** Add new project objects or modify existing ones.

## Rendering Functions

JavaScript functions like `renderHero()`, `renderAbout()`, `renderSkills()`, `renderExperience()`, and `renderProjects()` are responsible for taking the data from the `CONFIG` object and dynamically generating the HTML for each section. These functions are called by `initializeWebsite()` which injects the content into the `<div id="content-container"></div>`. You generally don't need to modify these functions unless you want to change the layout or structure of a section.

## Styling (CSS)

All CSS rules are located within the `<style>` tags in the `<head>` section of `index.html`. The styles are generally organized by section or component (e.g., `.navbar`, `.hero`, `.project-card`). You can modify these rules to change the visual appearance. The site also supports a dark/light theme, controlled by CSS variables and a theme toggle.

## Key Features

### Contact Form (EmailJS)
-   The contact form in the "Get In Touch" section uses EmailJS to send messages.
-   **Configuration (in `index.html`):**
    -   `serviceID`: `'service_wqqye6a'`
    -   `templateID`: `'template_krk8xst'`
    -   `publicKey`: `'0w-ctlVVYZ12OWHVZ'` (used in `emailjs.init()`)
-   **Important:** For the form to send details correctly to your email:
    1.  Ensure your form inputs in `index.html` have `name` attributes (e.g., `name="name"`, `name="email"`). This was recently updated.
    2.  You **must** configure your email template on the EmailJS dashboard (for `template_krk8xst`) to include variables like `{{name}}`, `{{email}}`, `{{subject}}`, and `{{message}}` in its body to capture the form data.
-   User feedback messages (success/failure) are displayed below the form.

### PDF Resume Generation
-   The "Download Resume" buttons trigger the `generatePDF()` JavaScript function.
-   This function dynamically creates HTML content for your resume using data from the `CONFIG` object.
-   It then uses the browser's print dialog (`window.print()`) to allow saving this generated content as a PDF.
-   The content and styling of the PDF are defined within this function's `pdfContent` variable.

### Theme Toggle
-   A theme toggle button (moon/sun icon) allows users to switch between light and dark modes.
-   The current theme preference is saved in the browser's local storage.

## Making Changes to Content

1.  **Open `index.html`** in a text editor.
2.  **Locate the `CONFIG` object** in the `<script>` section.
3.  **Modify the data** within the `CONFIG` object as needed (e.g., update your job title, add a new project, change skills).
4.  **Save the `index.html` file.**
5.  **View your changes** by opening the `index.html` file in a web browser.

## Deployment

After making changes to `index.html`, you need to redeploy the file to your web hosting provider (e.g., Netlify, Vercel, GitHub Pages, or your own server) for the changes to be live on the internet. The specific deployment steps depend on your hosting setup.

```
