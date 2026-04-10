Here's a complete README for your Knowledge Hub project:

```markdown
# 📚 Knowledge Hub

A free, open digital library where anyone can access and share educational resources - videos and documents. No paywalls, no premium tiers, just knowledge freely shared.

## 🌟 Live Demo

[View Live Site](https://knowledge-hub-nine.vercel.app/)

## ✨ Features

### For Everyone (No Account Needed)
- 🔍 **Search** - Find resources by title, tags, or institution
- 📂 **Browse** - Explore content by category
- 🎬 **Watch Videos** - Embedded YouTube player
- 📄 **View Documents** - PDF preview and EPUB support
- 📥 **Download** - Save documents for offline reading

### For Contributors (Free Account)
- 📤 **Upload Videos** - Share YouTube educational videos
- 📑 **Upload Documents** - Share PDF and EPUB files
- ✏️ **Edit** - Update your resource metadata
- 🗑️ **Delete** - Remove your contributions
- 📋 **My Uploads** - Manage all your resources in one place

### Content Organization
- 🏷️ **Categories** - Computer Science, Mathematics, Physics, Biology, Engineering, History, Literature, and more
- 🏫 **Institution Tags** - Optional attribution (MIT, Stanford, Khan Academy, or leave blank)
- 🔖 **User Tags** - Custom keywords for better discovery

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **HTML/CSS/JS** | Frontend - no frameworks, no build steps |
| **Vercel** | Hosting (free tier) |
| **Supabase** | Database + Authentication + Storage (free tier) |
| **YouTube oEmbed** | Video metadata fetching |

### Why This Stack?
- **Zero Cost** - All services have generous free tiers
- **Simple** - No complex frameworks to learn or maintain
- **Fast** - Static pages load instantly
- **Portable** - Easy to migrate if needed

## 🚀 Quick Start

### Prerequisites
- GitHub account (free)
- Vercel account (free)
- Supabase account (free)

### Setup Steps

1. **Clone or Fork this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/knowledge-hub.git
   ```

2. **Create Supabase Project**
   - Go to [supabase.com](https://supabase.com)
   - Create new project
   - Run the SQL schema (see below)

3. **Run the Database Schema**
   ```sql
   -- Videos table
   CREATE TABLE videos (
       id BIGSERIAL PRIMARY KEY,
       created_at TIMESTAMPTZ DEFAULT NOW(),
       youtube_url TEXT NOT NULL,
       youtube_id TEXT NOT NULL UNIQUE,
       title TEXT NOT NULL,
       category TEXT NOT NULL,
       institution TEXT,
       tags TEXT NOT NULL,
       description TEXT,
       user_id UUID REFERENCES auth.users(id),
       submitter_email TEXT
   );

   -- Documents table
   CREATE TABLE documents (
       id BIGSERIAL PRIMARY KEY,
       created_at TIMESTAMPTZ DEFAULT NOW(),
       title TEXT NOT NULL,
       category TEXT NOT NULL,
       institution TEXT,
       tags TEXT NOT NULL,
       description TEXT,
       file_name TEXT NOT NULL,
       file_url TEXT NOT NULL,
       file_size INTEGER NOT NULL,
       file_type TEXT NOT NULL,
       user_id UUID REFERENCES auth.users(id),
       submitter_email TEXT
   );

   -- Enable RLS and create policies
   ALTER TABLE videos ENABLE ROW LEVEL SECURITY;
   ALTER TABLE documents ENABLE ROW LEVEL SECURITY;

   -- Anyone can view
   CREATE POLICY "Anyone can view videos" ON videos FOR SELECT USING (true);
   CREATE POLICY "Anyone can view documents" ON documents FOR SELECT USING (true);

   -- Authenticated users can insert
   CREATE POLICY "Users can insert videos" ON videos FOR INSERT WITH CHECK (auth.uid() = user_id);
   CREATE POLICY "Users can insert documents" ON documents FOR INSERT WITH CHECK (auth.uid() = user_id);

   -- Users can update/delete their own
   CREATE POLICY "Users can update own videos" ON videos FOR UPDATE USING (auth.uid() = user_id);
   CREATE POLICY "Users can delete own videos" ON videos FOR DELETE USING (auth.uid() = user_id);
   CREATE POLICY "Users can update own documents" ON documents FOR UPDATE USING (auth.uid() = user_id);
   CREATE POLICY "Users can delete own documents" ON documents FOR DELETE USING (auth.uid() = user_id);
   ```

4. **Create Storage Bucket**
   - In Supabase dashboard → Storage
   - Create bucket named `documents`
   - Make it public
   - Add policy for authenticated uploads

5. **Configure Environment Variables**
   Replace `YOUR_SUPABASE_URL` and `YOUR_ANON_KEY` in all HTML files with your Supabase project values

6. **Deploy to Vercel**
   - Push code to GitHub
   - Import repository in Vercel
   - Deploy (no configuration needed)

## 📁 Project Structure

```
knowledge-hub/
├── index.html          # Homepage with search and recent items
├── browse.html         # Browse all resources with filters
├── video.html          # Video player page
├── document.html       # Document viewer page
├── upload.html         # Upload form (videos & documents)
├── my-uploads.html     # User's uploaded resources
├── login.html          # Authentication page
├── about.html          # Project information
├── style.css           # Global styles
└── README.md           # This file
```

## 🎯 Categories

| Category | Icon |
|----------|------|
| Computer Science | 💻 |
| Mathematics | 📐 |
| Physics | ⚡ |
| Chemistry | 🧪 |
| Biology | 🧬 |
| Engineering | 🔧 |
| Medicine | 💊 |
| History | 📜 |
| Literature | 📖 |
| Philosophy | 💭 |
| Art & Design | 🎨 |
| Music | 🎵 |
| Business | 💼 |
| Economics | 📊 |
| Language Learning | 🗣️ |
| Research Paper | 📑 |
| Thesis | 🎓 |
| Project Report | 📋 |

## 🤝 Contributing

### How to Contribute Content
1. Create a free account
2. Click "Upload"
3. Choose video or document
4. Fill in metadata (title, category, tags)
5. Submit

### How to Contribute Code
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📝 License

This project is open source. Content uploaded by users is owned by their respective creators. Please respect copyright and only upload content you have permission to share.

## 🛡️ Security

- Row Level Security (RLS) policies protect all database operations
- Users can only edit/delete their own content
- Email verification available for account creation
- File uploads are scanned for type and size limits

## 📧 Contact

- **Issues**: [GitHub Issues](https://github.com/YOUR_USERNAME/knowledge-hub/issues)
- **Email**: knowledgehub@example.com
- **DMCA/Copyright**: knowledgehub@example.com (subject: DMCA)

## 🚧 Future Plans

- [ ] User ratings/reviews
- [ ] Playlists/collections
- [ ] Comments section
- [ ] More document formats
- [ ] Mobile app
- [ ] API access

## 🙏 Acknowledgments

- Built with [Supabase](https://supabase.com) - Open source Firebase alternative
- Hosted on [Vercel](https://vercel.com) - Static hosting
- Icons via Unicode emojis
- YouTube embedding via YouTube API

## 📊 Status

![Vercel](https://img.shields.io/badge/deployed-vercel-blue)
![Supabase](https://img.shields.io/badge/database-supabase-green)
![License](https://img.shields.io/badge/license-MIT-yellow)

---

**Knowledge Hub** - Because knowledge should be free for everyone. 📚
```

## What to Do Now

1. **Create a new file** called `README.md` in your project folder
2. **Copy and paste** the content above
3. **Replace** `YOUR_USERNAME` with your actual GitHub username
4. **Replace** `knowledgehub@example.com` with your actual contact email if desired
5. **Save** the file
6. **Upload** to GitHub

The README will automatically display on your GitHub repository page. It includes:
- Project overview
- Feature list
- Tech stack explanation
- Setup instructions
- Database schema
- Contributing guidelines
- License information

Let me know if you want me to add or modify any sections!
