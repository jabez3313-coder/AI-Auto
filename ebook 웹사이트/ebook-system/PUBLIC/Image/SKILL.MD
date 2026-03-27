# Image Skill - eBook System

This folder stores all images used in eBook storybooks.

Images should be generated using Stitch MCP and follow book-style layout rules.

---

# Image Generation System

Images are generated using:

- Stitch MCP
- AI Image Generation
- Consistent Storybook Style

Images must match:

- Story tone
- Character consistency
- Book layout

---

# eBook Image Ratio (Important)

Use book-friendly ratio instead of 16:9

Recommended Ratios:

4:5 (Best for eBook)
2:3 (Book style)

Recommended Sizes:

1600 x 2000 (Best)
1200 x 1500
1024 x 1536

Avoid:

16:9
Video format

Reason:

- Better reading experience
- Mobile friendly
- Book-like layout

---

# Stitch MCP Rules

Image generation must:

- Connect to Stitch MCP
- Generate images per page
- Maintain consistent style
- Maintain consistent characters

Workflow:

Story JSON
↓
Image Agent
↓
Stitch MCP
↓
Generate Image
↓
Save to public/images/

---

# Folder Structure

Each story has its own folder:

public/images/

Example:

public/images/
 └── story-01/
     ├── story-01-01.jpg
     ├── story-01-02.jpg
     ├── story-01-03.jpg

---

# Naming Rules

Image naming format:

story-id-page.jpg

Example:

story-01-01.jpg
story-01-02.jpg

---

# Character Consistency

Characters must remain consistent:

- Face
- Age
- Clothing
- Style
- Background tone

Across all pages

---

# Text Layout for eBook

Images must allow space for text

Recommended Layout:

Image Top Layout (Best)

[ Image ]

Story Text

Reason:

- Most readable
- Book-like structure
- Mobile friendly

---

# Text Alignment Rules

Use book-style alignment

Title Alignment:

Center

Example:

제 1 장  
베드로의 부르심

---

Story Text Alignment:

Left aligned

Example:

베드로는 갈릴리 바닷가에서  
예수님을 만났습니다.  
그의 삶은 바뀌기 시작했습니다.

---

# Text Position

Recommended:

Bottom Text Layout

[ Image ]

Text below image

Avoid:

Text on busy background

---

# Text Spacing

Use:

- 2 ~ 4 lines per page
- Comfortable spacing
- Large readable text

Example:

베드로는  
갈릴리 바닷가에서  
예수님을 만났습니다.

---

# Margin Rules

Use safe margins:

Top margin  
Bottom margin  
Side margin  

Avoid:

Text touching edges

---

# Font Style Recommendation

Recommended:

- Simple fonts
- Readable fonts
- Calm tone fonts

Example:

- Noto Sans
- Noto Serif
- Pretendard
- Nanum Myeongjo

---

# Reading Experience Goal

Images must feel like:

- Storybook
- Picture book
- Devotional book
- Calm reading experience

---

# Supported Formats

Images:

JPG (Recommended)  
PNG

---

# Future Expansion

Support:

- animation
- audio narration
- video storybook

---

# Final Goal

This folder stores all eBook images generated using Stitch MCP, optimized for book-style reading and layout.
