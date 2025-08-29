# Instructions: Customizing Your PyCon GR Presentation Links Site

This repository contains a Jekyll-based GitHub Pages site for sharing links related to your PyCon GR talk. Follow these steps to customize and publish your site.

## Step 1: Replace TBD Placeholders

Edit `index.md` and replace all `TBD` values in the front matter:

- **title**: Your talk title
- **subtitle**: Optional subtitle or tagline for your talk
- **date**: Date of your talk (e.g., "March 15, 2024")
- **location**: Venue or city (e.g., "Athens, Greece")
- **speaker_name**: Your full name
- **bio_short**: 1–2 sentence bio (e.g., "Software engineer at Sentry working on error monitoring and performance.")
- **description**: Brief description for SEO

## Step 2: Update About the Talk Section

In `index.md`, replace "TBD short abstract (2–4 sentences)." with a brief description of your talk's content and key takeaways.

## Step 3: Add Your Links

Edit `_data/links.yml` and customize the links:

- Replace example URLs with your actual links
- Update titles and descriptions as needed
- Add or remove links as appropriate
- Order them as you prefer (they'll appear in the order listed)

Required links (per acceptance criteria):

- Slides
- Rust Book (or relevant technical resource)
- Your GitHub profile
- Your LinkedIn profile

## Step 4: Add Images (Optional)

If you want to include a headshot:

1. Add your image to `assets/images/` (recommended: `headshot.jpg`)
2. Update `headshot_src` in `index.md` front matter to match the filename

Note: The site uses a custom minimal layout without header/footer for a clean presentation-focused design.

## Step 5: Configure for GitHub Pages

1. If this is a project page (not your main username.github.io site):

   - Uncomment and update the `url` and `baseurl` lines in both `_config.yml` and `index.md`
   - Set `url` to "https://YOUR_USERNAME.github.io"
   - Set `baseurl` to "/presentation-links" (or your repo name)

2. Replace `YOUR_USERNAME` with your actual GitHub username in any URLs

## Step 6: Enable GitHub Pages

1. Go to your repository on GitHub
2. Navigate to Settings → Pages
3. Under "Source", select "Deploy from a branch"
4. Choose "main" branch and "/ (root)" folder
5. Click "Save"

## Step 7: Verify Your Site

Your site will be available at:

- User page: `https://YOUR_USERNAME.github.io/` (if this is your main site)
- Project page: `https://YOUR_USERNAME.github.io/presentation-links/` (if this is a project site)

GitHub Pages may take a few minutes to build and deploy your site after your first push.

## Optional Customization

### Custom Styling

If you want to customize the appearance, edit `assets/css/custom.css`. The theme will automatically include this file.

### Head Includes

If you need additional meta tags or CSS, create `_includes/head-custom.html` and add your custom HTML there.

## Local Development (Optional)

To preview your site locally:

1. Install Ruby and Bundler
2. Run:
   ```bash
   bundle init
   bundle add jekyll
   bundle exec jekyll serve
   ```
3. Visit `http://localhost:4000` in your browser

## Support

This site uses Jekyll with the Minima theme. For more customization options, refer to:

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Minima Theme Documentation](https://github.com/jekyll/minima)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
