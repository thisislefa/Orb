# Orb — Testimonial Grid Component

## Overview
Orb is a sophisticated testimonial presentation component featuring a responsive 3-column grid layout with glassmorphism effects and integrated statistics. Designed for showcasing client success stories with visual impact and data-driven credibility.

<img width="1606" height="876" alt="lefajmofokeng github io_Orb_" src="https://github.com/user-attachments/assets/1975fafe-ba91-4dda-836b-0a5c114fd0df" />

# Live Deployment

[View Live Demo](https://lefajmofokeng.github.io/Orb)

## Technical Architecture

### Core Features
- **CSS Grid Layout**: Responsive 3-column desktop, 2-column tablet, 1-column mobile
- **Glassmorphism Effects**: CSS backdrop-filter for modern translucent overlays
- **Performance Optimized**: No JavaScript dependencies, pure CSS animations
- **Accessibility First**: Semantic HTML with proper ARIA labels

### CSS Structure
```css
:root {
    /* Design System Tokens */
    --color-text-primary: #1a1a1a;
    --color-text-secondary: #555555;
    --color-background-white: #f7f7f7;
    --color-card-background: #ffffff;
    --color-accent-gold: #ffc700;
    --font-family-inter: 'Inter', sans-serif;
    
    /* Responsive Breakpoints */
    --breakpoint-tablet: 1024px;
    --breakpoint-mobile: 768px;
}
```

### Grid Implementation
```css
.story-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    
    @media (max-width: 1024px) {
        grid-template-columns: 1fr 1fr;
    }
    
    @media (max-width: 768px) {
        grid-template-columns: 1fr;
    }
}
```

## Framework Integration

### React Component
```jsx
import React from 'react';
import './Orb.css';

const OrbTestimonial = ({ 
    brand = "Bloomberg", 
    title = "Success Stories",
    summary = "We’ve delivered 50+ projects...",
    testimonial = {},
    stats = [],
    review = {}
}) => {
    return (
        <section className="story-section">
            <div className="story-grid">
                {/* Header Card */}
                <div className="grid-card card-heading">
                    <span className="brand-logo">{brand}</span>
                    <h2 className="main-title">{title}</h2>
                    <p className="summary-text">{summary}</p>
                </div>
                
                {/* Featured Testimonial */}
                <div className="card-featured-testimonial">
                    <div className="featured-image-container">
                        <img className="featured-image" src={testimonial.image} alt={testimonial.alt} />
                        <div className="glass-overlay">
                            <p className="overlay-quote">{testimonial.quote}</p>
                            <span className="overlay-person-name">{testimonial.name}</span>
                            <span className="overlay-person-role">{testimonial.role}</span>
                        </div>
                    </div>
                </div>
                
                {/* Review & Stats Card */}
                <div className="grid-card card-review-stats">
                    {/* Content implementation */}
                </div>
            </div>
        </section>
    );
};

export default OrbTestimonial;
```

### Vue.js Implementation
```vue
<template>
    <section class="story-section">
        <div class="story-grid">
            <div class="grid-card card-heading">
                <span class="brand-logo">{{ brand }}</span>
                <h2 class="main-title">{{ title }}</h2>
                <p class="summary-text">{{ summary }}</p>
            </div>
            
            <div class="card-featured-testimonial">
                <div class="featured-image-container">
                    <img class="featured-image" :src="testimonial.image" :alt="testimonial.alt" />
                    <div class="glass-overlay">
                        <p class="overlay-quote">{{ testimonial.quote }}</p>
                        <span class="overlay-person-name">{{ testimonial.name }}</span>
                        <span class="overlay-person-role">{{ testimonial.role }}</span>
                    </div>
                </div>
            </div>
            
            <div class="grid-card card-review-stats">
                <!-- Review content -->
            </div>
        </div>
    </section>
</template>

<script>
export default {
    props: {
        brand: String,
        title: String,
        summary: String,
        testimonial: Object,
        stats: Array,
        review: Object
    }
};
</script>
```

## Content Management Integration

### Headless CMS Structure (Sanity.io)
```javascript
// Schema definition
export default {
    name: 'testimonialGrid',
    title: 'Testimonial Grid',
    type: 'document',
    fields: [
        {
            name: 'brand',
            title: 'Brand Name',
            type: 'string'
        },
        {
            name: 'title',
            title: 'Main Title',
            type: 'string'
        },
        {
            name: 'summary',
            title: 'Summary Text',
            type: 'text'
        },
        {
            name: 'featuredTestimonial',
            title: 'Featured Testimonial',
            type: 'object',
            fields: [
                { name: 'image', type: 'image' },
                { name: 'quote', type: 'text' },
                { name: 'name', type: 'string' },
                { name: 'role', type: 'string' }
            ]
        }
    ]
};
```

### GraphQL Query
```graphql
query GetTestimonialGrid {
    testimonialGrid(id: "main-grid") {
        brand
        title
        summary
        featuredTestimonial {
            image {
                asset {
                    url
                }
            }
            quote
            name
            role
        }
        stats {
            value
            label
        }
    }
}
```

## Performance Optimization

### Image Optimization Strategy
```html
<!-- Modern image attributes -->
<img 
    src="image.jpg" 
    alt="Description" 
    loading="lazy" 
    decoding="async" 
    class="featured-image"
    sizes="(max-width: 768px) 100vw, (max-width: 1024px) 50vw, 33vw"
/>
```

### Critical CSS Extraction
```css
/* Inline critical styles */
.story-grid {
    display: grid;
    gap: 20px;
}

.main-title {
    font-size: 56px;
    line-height: 1.1;
}

/* Async load remaining styles */
<link rel="stylesheet" href="orb.css" media="print" onload="this.media='all'">
```

## Accessibility Implementation

### ARIA Enhancements
```html
<div class="star-rating" 
     role="img" 
     aria-label="5 out of 5 stars"
     data-rating="5">
    ★★★★★
</div>

<div class="glass-overlay" 
     role="region" 
     aria-label="Client testimonial">
    <!-- Content -->
</div>
```

### Screen Reader Support
```css
/* Hide decorative images from screen readers */
.featured-image[alt=""] {
    aria-hidden="true";
}

/* Ensure proper focus order */
.grid-card:focus {
    outline: 2px solid var(--color-accent-gold);
    outline-offset: 2px;
}
```

## Build and Deployment

### CSS Processing Pipeline
```javascript
// PostCSS configuration
module.exports = {
    plugins: [
        require('postcss-preset-env')({
            stage: 3,
            features: {
                'nesting-rules': true,
                'custom-media-queries': true,
                'media-query-ranges': true
            }
        }),
        require('cssnano')({
            preset: 'default'
        })
    ]
};
```

### Module Bundling
```javascript
// Webpack configuration for component export
module.exports = {
    output: {
        library: 'OrbTestimonial',
        libraryTarget: 'umd',
        filename: 'orb-testimonial.js'
    },
    externals: {
        'react': 'React',
        'react-dom': 'ReactDOM'
    }
};
```

## Testing Strategy

### Visual Regression Tests
```javascript
// Playwright visual tests
test.describe('Orb Testimonial Grid', () => {
    test('renders correctly on desktop', async ({ page }) => {
        await page.goto('/testimonials');
        await expect(page.locator('.story-grid')).toHaveScreenshot({
            threshold: 0.1
        });
    });
});
```

### Accessibility Tests
```javascript
// axe-core integration
import axe from 'axe-core';

test('meets accessibility standards', async () => {
    const results = await axe.run(document);
    expect(results.violations).toHaveLength(0);
});
```

## Browser Support

### Compatibility Matrix
- **Chrome 90+**: Full support
- **Firefox 88+**: Full support (backdrop-filter with prefix)
- **Safari 14+**: Full support
- **Edge 90+**: Full support

### Fallback Strategies
```css
/* Progressive enhancement for backdrop-filter */
.glass-overlay {
    background: rgba(255, 255, 255, 0.95); /* Fallback */
}

@supports (backdrop-filter: blur(10px)) {
    .glass-overlay {
        background: rgba(255, 255, 255, 0.2);
        backdrop-filter: blur(10px);
    }
}
```

## Usage Examples

### Static Implementation
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="orb.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap" rel="stylesheet">
</head>
<body>
    <!-- Component markup -->
    <script src="orb.js" type="module"></script>
</body>
</html>
```

### Dynamic Content Loading
```javascript
// Fetch and render component dynamically
async function loadTestimonialGrid() {
    const response = await fetch('/api/testimonials');
    const data = await response.json();
    
    const grid = document.createElement('div');
    grid.className = 'story-section';
    grid.innerHTML = `
        <div class="story-grid">
            <!-- Dynamic content -->
        </div>
    `;
    
    document.body.appendChild(grid);
}
```

## License and Distribution
Orb is released under MIT License. The component can be integrated into commercial projects without attribution, though credit is appreciated. For enterprise support or custom implementations, contact the maintainer.

---

**Maintainer**: [Lefa](https://github.com/lefajmofokeng)  
**Technology**: CSS Grid with Glassmorphism Effects  
**Status**: Production Ready with Comprehensive Browser Support




