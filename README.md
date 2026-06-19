# 🚀 AI News-to-Video Social Media Automation

An end-to-end AI-powered content automation workflow built with **n8n**, **OpenAI**, **Leonardo AI**, **RunwayML**, and **Creatomate**.

The workflow automatically discovers trending AI and automation news, summarizes articles, generates images and videos, creates voiceovers, assembles a complete social media video, uploads assets to cloud storage, and publishes content across multiple platforms.

---

## 📌 Features

- Fetch trending articles from Hacker News
- Identify AI and Automation-related content
- Summarize articles using GPT-4o-mini
- Analyze article images using OpenAI Vision
- Generate newsletter-ready content
- Create AI image prompts
- Generate images using Leonardo AI
- Convert images into videos using RunwayML
- Generate voiceovers using OpenAI TTS
- Assemble final videos using Creatomate
- Upload generated assets to cloud storage
- Publish content automatically to social media

---

## 🏗 Workflow Architecture

```text
Manual Trigger
      │
      ▼
Hacker News
      │
      ▼
Limit Results
      │
      ▼
Loop Through Articles
      │
      ▼
Article Analysis (GPT)
      │
      ▼
AI/Automation Filter
      │
      ▼
Image Analysis
      │
      ▼
Article Preparation
      │
      ▼
Image Prompt Generation
      │
      ▼
Leonardo AI
(Image Generation)
      │
      ▼
RunwayML
(Image to Video)
      │
      ▼
Creatomate
(Video Assembly)
      │
      ▼
Cloud Upload
      │
      ▼
Social Media Publishing
```

---

# 🔄 Workflow Breakdown

## 1. Trigger Workflow

The workflow starts manually through the n8n trigger node.

### Node

```text
When clicking "Test Workflow"
```

---

## 2. Fetch Trending Articles

Retrieves the latest trending stories from Hacker News.

### Output

```json
{
  "title": "Latest AI Breakthrough",
  "url": "https://example.com/article"
}
```

---

## 3. Limit Processing

Limits processing to the latest 50 articles.

### Purpose

- Reduce API costs
- Improve execution speed

---

## 4. Process Articles

The workflow loops through each article individually.

### Node

```text
Loop Over Items
```

---

# 🧠 Article Analysis

## 5. Fetch Full Article

Uses HTTP Request to retrieve article content.

### Node

```text
HTTP Request
```

---

## 6. AI Article Analysis

GPT-4o-mini analyzes the article.

### Tasks

- Check if article relates to AI
- Check if article relates to Automation
- Generate summary
- Extract image URL

### Prompt

```text
Can you tell me if the article is related to automation or AI?

Create a 250-word summary.

List one relevant image URL.
```

### Output

```json
{
  "summary": "...",
  "related": "yes",
  "image_urls": "..."
}
```

---

## 7. Structured Output Parsing

Converts GPT output into JSON format.

### Output Schema

```json
{
  "summary": "string",
  "related": "string",
  "image_urls": "string"
}
```

---

## 8. Topic Filtering

Only articles marked as relevant continue.

### Condition

```text
related = yes
```

Non-relevant content is skipped.

---

# 🖼 Image Processing

## 9. Analyze Article Image

Uses GPT-4o-mini Vision to analyze the extracted image.

### Purpose

Improve context for media generation.

---

## 10. Download Image

Retrieves the selected image from the article.

---

# ✍ Content Generation

## 11. Prepare Newsletter Content

GPT creates:

- Article Title
- Article Blurb
- Summary Blurb 1
- Summary Blurb 2
- Image Prompt 1
- Image Prompt 2

### Example Output

```json
{
  "Article Title": "AI Agents Are Reshaping Work",
  "Article Blurb": "How AI agents automate tasks.",
  "Summary Blurb 1": "AI boosts productivity.",
  "Summary Blurb 2": "Automation adoption increases.",
  "Image Prompt 1": "...",
  "Image Prompt 2": "..."
}
```

---

## 12. Format Content

Stores generated content for later use.

### Variables

```json
{
  "property_name": "...",
  "property_text": "...",
  "property_image_url": "..."
}
```

---

# 🎨 Image Generation

## 13. Improve Prompts

Leonardo AI enhances image prompts.

### Endpoint

```http
POST /prompt/improve
```

---

## 14. Generate Images

Leonardo AI generates images using:

- 1024x768 resolution
- Alchemy mode
- High resolution
- Monochrome style

### Endpoint

```http
POST /generations
```

---

## 15. Wait For Completion

The workflow pauses while images are rendered.

### Wait Time

```text
30 seconds
```

---

## 16. Retrieve Images

Gets generated image URLs from Leonardo AI.

---

# 🎬 Video Generation

## 17. Create Video

RunwayML converts images into videos.

### Model

```text
Gen-3 Turbo
```

### Endpoint

```http
POST /image_to_video
```

---

## 18. Wait For Rendering

### Wait Time

```text
3 minutes
```

---

## 19. Retrieve Videos

Fetches completed video URLs.

---

# 🎤 Voice Generation

OpenAI TTS generates narration.

### Model

```text
tts-1
```

### Voice

```text
Onyx
```

Voiceovers are created for:

- Article title
- Summary section 1
- Summary section 2

---

# 🎞 Video Assembly

## 20. Create Final Video

Creatomate combines:

- AI-generated images
- Runway videos
- AI voiceovers
- Animated subtitles

### Video Structure

#### Intro

- Image
- Title
- Voiceover

#### Scene 1

- Video
- Summary narration
- Subtitles

#### Scene 2

- Video
- Summary narration
- Subtitles

---

## 21. Render Final Video

Creates the final social-media-ready video.

### Output

```json
{
  "video_url": "..."
}
```

---

# ☁ Storage Integrations

Generated assets can be uploaded to:

- Dropbox
- Google Drive
- Microsoft OneDrive
- MinIO

---

# 📢 Social Media Publishing

The workflow supports automatic publishing to:

- YouTube
- X (Twitter)
- LinkedIn
- Instagram

---

# 🛠 Tech Stack

## Workflow Automation

- n8n

## AI Models

- OpenAI GPT-4o-mini
- OpenAI Vision
- OpenAI TTS

## Image Generation

- Leonardo AI

## Video Generation

- RunwayML Gen-3 Turbo

## Video Editing

- Creatomate

## Cloud Storage

- Dropbox
- Google Drive
- OneDrive
- MinIO

## Social Media

- YouTube API
- LinkedIn API
- X API
- Instagram API

---

# 📂 Output Structure

```text
outputs/
│
├── article_summary.json
├── generated_image_1.png
├── generated_image_2.png
├── runway_video_1.mp4
├── runway_video_2.mp4
├── voiceover.mp3
├── final_video.mp4
└── social_post.txt
```

---

# 🚀 Use Cases

- AI News Channels
- LinkedIn Content Automation
- YouTube Shorts Automation
- Newsletter Creation
- Personal Branding
- Social Media Marketing
- AI Content Agencies

---

## Future Improvements

- TikTok Integration
- Multi-language Content
- Automated Scheduling
- SEO Optimization
- Trend Scoring
- Agent-Based Planning

---

## License

MIT License

---

Built with ❤️ using n8n, OpenAI, Leonardo AI, RunwayML, and Creatomate.
