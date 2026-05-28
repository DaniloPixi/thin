
# Yu's Cottage Website Blueprint

## Overview

This document outlines the design, features, and development plan for the Yu's Cottage website. The site is a single-page portfolio designed to showcase the restaurant's unique ambiance, menu, and contact information in an elegant and modern layout.

### Key Features & Design

*   **Hero Section:** A section with an image and a "Book a Table" button.
*   **Menu:** A section that displays the restaurant's menu. The main navigation bar has a "Menu" button that opens the menu PDF in a new tab.
*   **Contact Section:** A section with contact information and a map.
*   **Image Slider:** A dynamic image slider to showcase the restaurant's ambiance and dishes.
*   **Floating Buttons:** Floating buttons for quick access to social media and other important links.
*   **Map Modal:** A modal window that displays a map of the restaurant's location.

### Current Task: Replace Hero with About Section

*   **Task:** Replace the original hero section with the about section, including the image and a "Book a Table" button.
*   **Implementation:**
    *   The `Hero.vue` component has been deleted.
    *   The `About.vue` component has been updated to include the image and the "Book a Table" button.
    *   The `App.vue` file has been updated to remove the `Hero` component.

## Project Structure

*   **`src/`**
    *   **`components/`**: Contains all Vue components.
        *   `About.vue`: The hero and about section.
        *   `Menu.vue`: The menu section.
        *   `Contact.vue`: The contact section.
        *   `ImageSlider.vue`: The image slider.
        *   `FloatingButtons.vue`: Floating action buttons.
        *   `MapModal.vue`: The map modal.
        *   `Header.vue`: The main navigation header.
        *   `Footer.vue`: The main footer.
    *   **`assets/`**: Contains static assets like images and styles.
