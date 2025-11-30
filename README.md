Digital Garden \& Productivity OS



A "Headless" CMS and Personal Operating System built with Vanilla JS, Firebase, and Cloudflare R2.



It combines a public-facing "Digital Garden" (blog/portfolio) with a private, secured productivity dashboard.



Live Preview: \[Link to your site]



🌟 Features



🏡 Public Garden (Frontend)



Masthead Layout: Merged hero and featured article for high information density.



Dynamic Sections: \* Featured Essay: Highlight your best work with a visual cover.



The Stream: Chronological feed of public notes.



Pillars: Curated collections of content.



Markdown Rendering: Full markdown support for articles.



Smart Attachments: Displays images inline or provides download cards for files.



🔐 Gardener's OS (Admin)



Content Management:



Markdown Editor: Distraction-free writing environment.



Visibility Control: Set posts to Public, Draft, or Private.



Smart Uploads: Automatically saves small files (<500KB) to the database and uploads large files to Cloudflare R2 (via Worker).



Preview Mode: See how your article looks before publishing.



Productivity Tools:



Shared Tasks: A Todo list that can be shared with specific email addresses.



Full Calendar: Monthly view agenda with event tracking.



🏗 Tech Stack



Frontend: HTML5, CSS3 (Swiss Style), Vanilla JavaScript (ES6 Modules).



Backend: Firebase (Firestore Database, Authentication).



Storage: Hybrid (Firestore for small blobs, Cloudflare R2 for large assets).



Hosting: Agnostic (Vercel, Netlify, GitHub Pages).



🚀 Quick Start



Clone the Repo



git clone \[https://github.com/yourusername/digital-garden.git](https://github.com/yourusername/digital-garden.git)

cd digital-garden





Configure Backend



See FIREBASE\_SETUP.md for database rules.



See CLOUDFLARE\_SETUP.md for large file storage.



Update Config



Open admin.html, index.html, and article.html.



Replace the const firebaseConfig = { ... } block with your own keys.



Deploy



Push to GitHub and connect to Vercel/Netlify.



Note: No build step required. It's just static files.



🛠 Customization



Design System:

Colors and fonts are controlled by CSS variables in the <style> block of each file:



:root { 

&nbsp;   --paper: #F4F4F0; 

&nbsp;   --ink: #1A1A1A; 

&nbsp;   --font-serif: 'Playfair Display', serif; 

}





📝 License



MIT.

