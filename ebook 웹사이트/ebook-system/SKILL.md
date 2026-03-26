# SKILL.md
# Antigravity Web eBook Project Skill Guide

## Project Overview
This project builds a web-based eBook storybook system.
The system should create, organize, and display storybooks with images and short text.
The design should feel warm, simple, child-friendly, and easy to read on mobile and desktop.

## Main Goal
Build a web eBook reader that supports:
- 10-page storybooks
- One image per page
- Short text per page
- Previous / Next page navigation
- Story list page
- Mobile responsive layout

## Core Style Rules
- Use a warm and gentle storybook feeling
- Keep layouts clean and simple
- Avoid cluttered UI
- Prioritize mobile readability
- Use soft colors and calm spacing
- Make the reading experience feel like a digital picture book

## Content Rules
Each storybook should:
- Have one title
- Have 10 pages by default
- Include one image per page
- Include short text per page
- Keep tone warm, emotional, and easy to understand
- Maintain character consistency across pages when needed

## Story Structure Rules
For each story:
1. Opening scene
2. Character introduction
3. Emotional development
4. Key event
5. Conflict or question
6. Reflection
7. Hope or guidance
8. Growth
9. Resolution
10. Closing message

## Image Rules
Images should:
- Match the story page text
- Keep consistent style across all pages
- Maintain the same character appearance when required
- Use soft cinematic composition
- Feel like a storybook illustration
- Be suitable for 16:9 or book-friendly formats depending on page design

## Web Structure
The app should include:

### 1. Story List Page
- Show all available storybooks
- Each book displays cover image, title, and short description
- Clicking a book opens the viewer page

### 2. eBook Viewer Page
- Show current page image
- Show current page text
- Include Previous and Next buttons
- Show current page number
- Support mobile responsive reading

## Data Structure
Each storybook should be stored in JSON format like this:

```json
{
  "id": "peter-book-01",
  "title": "Peter's Calling",
  "description": "A warm spiritual storybook about Peter.",
  "coverImage": "/images/peter-cover.jpg",
  "pages": [
    {
      "page": 1,
      "image": "/images/peter-01.jpg",
      "text": "Peter stood by the sea, not knowing his life would soon change."
    }
  ]
}
