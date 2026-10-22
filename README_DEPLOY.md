# NOCTIS TECHNOLOGIES — DEPLOYMENT & VERIFICATION GUIDE

Complete step-by-step guide to deploy the site to InfinityFree hosting
and verify everything works correctly.

═══════════════════════════════════════════════════════════════════
PART 1 — FILES YOU SHOULD HAVE
═══════════════════════════════════════════════════════════════════

FRONTEND (14 files)
  ✓ style.css
  ✓ index.html
  ✓ about.html
  ✓ services.html
  ✓ portfolio.html
  ✓ pricing.html
  ✓ team.html
  ✓ contact.html
  ✓ privacy.html
  ✓ terms.html
  ✓ team/sam-immanuel-j.html
  ✓ team/esther-jebarani-j.html
  ✓ team/milton-prabhu-j.html
  ✓ team/pradeep-kumar-n.html

INFINITY HOST / SEO LAYER (6 files)
  ✓ .htaccess
  ✓ seo-engine.php
  ✓ locations.php         (141 locations, with helper functions added)
  ✓ seo-master.js
  ✓ robots.txt
  ✓ sitemap.xml           (static fallback)
  ✓ indexnow.php

IMAGES (must be in /htdocs/ root)
  ✓ sam.jpg
  ✓ esther.jpg
  ✓ milton.jpg
  ✓ pradeep.jpg
  ✓ central-and-stores.webp
  ✓ justin-scholarship-portal.webp
  ✓ logo-512.png
  ✓ og-home.jpg
  ✓ og-about.jpg
  ✓ og-portfolio.jpg
  ✓ og-services.jpg
  ✓ og-team.jpg

OPTIONAL
  ✓ 404.html             (custom error page)
  ✓ <INDEXNOW_KEY>.txt   (IndexNow verification key file)

═══════════════════════════════════════════════════════════════════
PART 2 — UPLOAD STEPS (InfinityFree / FTP)
═══════════════════════════════════════════════════════════════════

METHOD A — FTP (recommended, handles dotfiles correctly)
  1. Install FileZilla (filezilla-project.org) if you don't have it.
  2. Get FTP credentials from InfinityFree control panel → FTP Accounts.
  3. Connect: host / username / password / port 21.
  4. Navigate to /htdocs/ (that's the web root).
  5. Upload ALL files above, preserving folder structure.
  6. IMPORTANT: in FileZilla, enable "Force showing hidden files"
     (Server menu) so you can see and upload .htaccess.
  7. Verify .htaccess is present — some FTP clients skip dotfiles
     silently.

METHOD B — InfinityFree File Manager
  1. Login → Control Panel → File Manager.
  2. Navigate to /htdocs/.
  3. Upload files one folder at a time (root files first, then /team/).
  4. NOTE: File Manager sometimes strips or renames .htaccess —
     verify it's exactly ".htaccess" (no .txt appended).

═══════════════════════════════════════════════════════════════════
PART 3 — CONFIGURATION CHECK BEFORE TESTING
═══════════════════════════════════════════════════════════════════

Open seo-engine.php and confirm:
  Line ~21: define('DOMAIN', 'https://www.noctistechnologies.gt.tc');
  Line ~22: define('SITE_NAME', 'Noctis Technologies');
  Line ~23: define('SITE_EMAIL', 'mr.samimmanuel.j@gmail.com');
  Line ~24: define('SITE_PHONE', '+91-95431-28730');

Open indexnow.php and confirm:
  Line ~20: define('INDEXNOW_KEY', 'YOUR_KEY_HERE');
  Line ~21: define('DOMAIN', 'https://www.noctistechnologies.gt.tc');

Open each HTML file and confirm:
  window.NOCTIS_CONFIG.supabaseUrl = "REPLACE_SUPABASE_URL"
  (will be filled in Phase C once Supabase project is created)

═══════════════════════════════════════════════════════════════════
PART 4 — TEST SEQUENCE (open each URL, expect 200 OK)
═══════════════════════════════════════════════════════════════════

CORE PAGES
  □ https://www.noctistechnologies.gt.tc/
  □ https://www.noctistechnologies.gt.tc/about.html
  □ https://www.noctistechnologies.gt.tc/services.html
  □ https://www.noctistechnologies.gt.tc/portfolio.html
  □ https://www.noctistechnologies.gt.tc/pricing.html
  □ https://www.noctistechnologies.gt.tc/team.html
  □ https://www.noctistechnologies.gt.tc/contact.html
  □ https://www.noctistechnologies.gt.tc/privacy.html
  □ https://www.noctistechnologies.gt.tc/terms.html

TEAM ENTITY PAGES
  □ https://www.noctistechnologies.gt.tc/team/sam-immanuel-j.html
  □ https://www.noctistechnologies.gt.tc/team/esther-jebarani-j.html
  □ https://www.noctistechnologies.gt.tc/team/milton-prabhu-j.html
  □ https://www.noctistechnologies.gt.tc/team/pradeep-kumar-n.html

PROGRAMMATIC LOCATION PAGES
  □ https://www.noctistechnologies.gt.tc/tamil-nadu/tiruppur
  □ https://www.noctistechnologies.gt.tc/tamil-nadu/towns/pollachi
  □ https://www.noctistechnologies.gt.tc/india/states/andhra-pradesh
  □ https://www.noctistechnologies.gt.tc/india/cities/bengaluru
  □ https://www.noctistechnologies.gt.tc/international/united-states

SYSTEM FILES
  □ https://www.noctistechnologies.gt.tc/sitemap.xml
  □ https://www.noctistechnologies.gt.tc/robots.txt

═══════════════════════════════════════════════════════════════════
PART 5 — GOOGLE SEARCH CONSOLE (critical for indexing)
═══════════════════════════════════════════════════════════════════

1. Go to: https://search.google.com/search-console
2. Click "Add Property" → choose "URL prefix"
3. Enter: https://www.noctistechnologies.gt.tc
4. Verify ownership. Easiest method:
   → "HTML tag" option → copy the <meta name="google-site-verification" ...>
   → paste into <head> of index.html
   → re-upload index.html
   → click "Verify" in Search Console
5. Once verified, submit your sitemap:
   → Left menu → Sitemaps
   → Enter: sitemap.xml
   → Click Submit
6. Use URL Inspection on each major page:
   → Paste URL → "Request Indexing"
   → Do this for: /, /about.html, /services.html, /team.html, and 2-3 location pages.

═══════════════════════════════════════════════════════════════════
PART 6 — BING WEBMASTER TOOLS (for IndexNow tracking)
═══════════════════════════════════════════════════════════════════

1. Go to: https://www.bing.com/webmasters
2. Add site: https://www.noctistechnologies.gt.tc
3. Verify ownership (same method as Google — meta tag or file)
4. Submit sitemap: sitemap.xml
5. After IndexNow fires (Part 7), new pages appear in Bing within hours.

═══════════════════════════════════════════════════════════════════
PART 7 — INDEXNOW (instant Bing/Yandex pings)
═══════════════════════════════════════════════════════════════════

ONE-TIME SETUP:
  1. Pick your key (e.g. 8Ze8xP4vGZ).
  2. Create a plain text file: <your-key>.txt
     Content: exactly the key, nothing else (no newline at end).
  3. Upload to /htdocs/<your-key>.txt
  4. Update indexnow.php with the key in INDEXNOW_KEY constant.
  5. Verify: https://www.noctistechnologies.gt.tc/<your-key>.txt
     Should show the key as plain text.

FIRE THE PING:
  1. Visit: https://www.noctistechnologies.gt.tc/indexnow.php?run=1
  2. Expected output: "HTTP status: 200" or "202" (accepted).
  3. If 403: key file not found / wrong content. Recheck step 5.
  4. If 422: domain mismatch. Check DOMAIN constant in indexnow.php.

ONGOING (after each content update):
  → Visit indexnow.php?run=1 once. New pages pinged instantly.
  → Or add a daily cron in InfinityFree control panel (optional).

═══════════════════════════════════════════════════════════════════
PART 8 — CHECK YOUR SITEMAP IS COMPLETE
═══════════════════════════════════════════════════════════════════

Open: https://www.noctistechnologies.gt.tc/sitemap.xml

Expected: ~154 URLs total
  • 13 core pages
  • 141 location pages

If you see only ~13 URLs:
  → seo-engine.php routing is failing for sitemap
  → Check .htaccess has the sitemap rewrite rule
  → Check PHP is enabled on InfinityFree

If you see 0 URLs or blank:
  → locations.php may have a PHP syntax error
  → Run locally: php -l locations.php
  → Fix errors, re-upload.

═══════════════════════════════════════════════════════════════════
PART 9 — TROUBLESHOOTING MATRIX
═══════════════════════════════════════════════════════════════════

PROBLEM                          | LIKELY CAUSE          | FIX
─────────────────────────────────┼───────────────────────┼───────────────────────────
404 on all location pages        | .htaccess not found   | Re-upload .htaccess via FTP
404 on /sitemap.xml              | rewrite rule missing  | Check .htaccess Part 4
500 Internal Server Error        | PHP syntax error      | Check error log in InfinityFree
Blank white page on location     | display_errors=0 hides | Temporarily set display_errors=1
CSS not loading                  | wrong path            | Verify style.css in /htdocs/ root
Images broken                    | filename mismatch     | Compare case sensitivity
Canonical points to http (no s)  | HTTPS rewrite off    | Check .htaccess Part 2
Google Search Console fail       | wrong property type   | Use "URL prefix" not "Domain"
IndexNow returns 403             | key file wrong        | Recreate <key>.txt exactly
Sitemap shows only 13 URLs       | PHP fallback          | Debug .htaccess routing

═══════════════════════════════════════════════════════════════════
PART 10 — AFTER DEPLOYMENT IS VERIFIED
═══════════════════════════════════════════════════════════════════

IMMEDIATE (day 1):
  ✓ All Part 4 URLs return 200
  ✓ Sitemap lists 154 URLs
  ✓ Search Console property verified
  ✓ Sitemap submitted to Search Console
  ✓ Sitemap submitted to Bing Webmaster
  ✓ IndexNow fired successfully (HTTP 200/202)

SHORT-TERM (week 1-2):
  → Monitor Search Console → Coverage report
  → Fix any pages marked "Excluded" or "Error"
  → Check "Mobile Usability" report — all pass expected
  → Check "Page Experience" — Core Web Vitals
  → Request indexing for top 10 pages via URL Inspection

MEDIUM-TERM (month 1-3):
  → Track keyword impressions in Search Console → Performance
  → Identify top-performing location pages → enhance content
  → Build Google Business Profile (separate critical action)
  → Collect real reviews to strengthen local signals
  → Set up analytics (Plausible, Umami, or GA4 — free tier)

ONGOING:
  → Add a new location page every week (expand from 141)
  → Run IndexNow ping after each content update
  → Update sitemap.xml lastmod dates monthly
  → Monitor for 404s in Search Console, fix promptly

═══════════════════════════════════════════════════════════════════
PART 11 — PHASE C NEXT (ADMIN PANEL)
═══════════════════════════════════════════════════════════════════

Once Part 4 checklist is green, the site is deployed and indexable.
Next phase = Admin panel (Supabase backend):

  Files to be delivered:
    • supabase/schema.sql         (all tables + RLS + triggers)
    • supabase/seed.sql           (initial content)
    • supabase/storage-setup.md   (bucket config)
    • admin/index.html            (login + dashboard)
    • admin/app.js                (full admin logic)
    • admin/style.css             (admin theme)
    • admin/README.md             (setup guide)

  What admin unlocks:
    • Edit any page content from browser (no FTP)
    • Add/remove team members (auto-generates Person entity pages)
    • Moderate reviews (pending/published)
    • View + reply to enquiries (contact form inbox)
    • Change domain from admin (all canonical/schema/sitemap update)
    • Manage media (upload/optimize images)
    • Bulk SEO editor for all 141 location pages

  Prerequisite: Supabase project created (free tier).
  → If not created yet, admin README will walk through it.

═══════════════════════════════════════════════════════════════════
END OF DEPLOYMENT GUIDE
═══════════════════════════════════════════════════════════════════
