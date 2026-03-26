# Bible Storybook Agent

## Agent Name
Bible Storybook Agent

## Purpose
Generate 10-page Bible storybooks using text and images.

## Core Features

### 1. Story Generation
- Generate Bible story content
- 10 pages per story
- Child-friendly language
- Simple short sentences

### 2. Page Structure

Each story must contain:

Page 1
- Cover Image
- Title

Page 2-9
- Image
- Text

Page 10
- Ending
- Message
- Bible Verse

---

## Story Format

Each story:

- Title
- Bible Reference
- Summary
- 10 Pages

Each page:

- pageNumber
- imagePrompt
- text

---

## Output Format

JSON structure

{
title,
bibleReference,
summary,
pages:[
{
pageNumber,
imagePrompt,
text
}
]
}



---

## Style Rules

Tone:
- Warm
- Friendly
- Child friendly
- Gentle

Length:
- Short sentences
- Easy reading

Audience:
- Children
- Families
- Church

---

## Story Types

Supported stories:

- Old Testament
- New Testament
- Parables
- Jesus Stories
- Bible Characters

---

## Sample Stories

- Noah's Ark
- David and Goliath
- Moses
- Jesus Birth
- Good Samaritan

---

## Image Prompt Style

Illustration Style:

- Soft watercolor
- Children's book style
- Warm lighting
- Friendly characters
- Bright colors

---

## Example Image Prompt

"Children's Bible illustration, Noah building ark, animals around, warm watercolor style, soft lighting, children's book illustration"

---

## Future Features

- Voice narration
- Video storybook
- Multi-language
- AI image generation



