
# Yu's Cottage Website Blueprint

## Overview

This document outlines the design, features, and development plan for the Yu's Cottage website. The site is a single-page portfolio designed to showcase the restaurant's unique ambiance, menu, and contact information in an elegant and modern layout.

### Key Features & Design

*   **Hero Section:** A full-screen hero section with a large, centered logo and a background image. The logo is slightly larger for better visibility.
*   **About Section:** A section with an image and text describing the restaurant.
*   **Menu:** A section that displays the restaurant's menu. The main navigation bar has a "Menu" button that opens the menu PDF in a new tab.
*   **Contact Section:** A section with contact information and a map.
*   **Image Slider:** A dynamic image slider to showcase the restaurant's ambiance and dishes.
*   **Floating Buttons:** Floating buttons for quick access to social media and other important links.
*   **Map Modal:** A modal window that displays a map of the restaurant's location.

### Current Task: Add PDF Menu

*   **Task:** Add a "Menu" button to the header that opens a PDF menu in a new tab.
*   **Implementation:**
    *   The menu PDF (`Yus_Speisekarte_08-25_ENG_HOME.pdf`) is located in the `public` directory.
    *   The `Header.vue` component is updated to include a link to the PDF.

## Project Structure

*   **`src/`**
    *   **`components/`**: Contains all Vue components.
        *   `Hero.vue`: The main hero section.
        *   `About.vue`: The about section.
        *   `Menu.vue`: The menu section.
        *   `Contact.vue`: The contact section.
        *   `ImageSlider.vue`: The image slider.
        *   `FloatingButtons.vue`: Floating action buttons.
        *   `MapModal.vue`: The map modal.
        *   `Header.vue`: The main navigation header.
        *   `Footer.vue`: The main footer.
    *   **`assets/`**: Contains static assets like images and styles.
